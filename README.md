# Pulse SDK for Python

[![PyPI version](https://img.shields.io/pypi/v/pulse-ai.svg)](https://pypi.org/project/pulse-ai/)

The Pulse SDK for Python provides access to the [Pulse API](https://docs.runpulse.com/v2/introduction) from Python applications. It covers every route of API version 2, sends `Pulse-Version: 2` on every request, and returns typed results.

## Documentation

Full documentation is available at **[docs.runpulse.com/v2/sdks](https://docs.runpulse.com/v2/sdks)**. Every method and its parameters are listed in [reference.md](./reference.md).

## Installation

```sh
pip install pulse-ai
```

The package installs the `pulse` module. If you have the 1.x SDK, `pulse-python-sdk`, uninstall it first: it installs the same module.

## Getting started

Create an API key in the [Pulse dashboard](https://platform.runpulse.com) under **API Keys**, then:

```python
import os

from pulse import Pulse

client = Pulse(api_key=os.environ["PULSE_API_KEY"])

job = client.parse.run(
    file_url="https://platform.runpulse.com/api/examples/637e5678-30b1-45fa-acc4-877f2d636419/pdf",
    config={"model": "ultra-2"},
)

parse = client.parse.get_result(job.parse_id)
print(parse.markdown)
```

`api_key` is required. The client doesn't read it from the environment.

## Usage

### Endpoints

Each endpoint is a group on the client, and every group has the same four calls. For Parse:

| Call | HTTP |
| --- | --- |
| `client.parse.run(...)` | `POST /parse` |
| `client.parse.get(parse_id)` | `GET /parse/{parse_id}` |
| `client.parse.get_result(parse_id)` | `GET /parse/{parse_id}/result` |
| `client.parse.cancel(parse_id)` | `DELETE /parse/{parse_id}` |

`classify`, `extract`, `split`, `tables`, `charts`, `pipeline` and `parse.batch` work the same way. Saved configs are in `client.<endpoint>.configs`, such as `client.extract.configs`. Webhooks are in `client.webhook`, usage is `client.usage.get()`, and organization settings are in `client.settings.org`.

Extract, Split, Tables and Charts read a completed parse by its `parse_id`:

```python
job = client.extract.run(
    parse_id=parse_id,
    config={
        "input_schema": {
            "type": "object",
            "properties": {
                "account_holder": {"type": "string"},
                "closing_balance": {"type": "number"},
            },
        }
    },
)

result = client.extract.get_result(job.extract_id)
print(result.extraction.enriched)
```

### Async jobs

By default, `run` waits for its job to end. Send `async_=True` to get the job's id at once, then poll its status. Use it for long documents, and wherever a proxy or load balancer might time out first. Pipelines and batches always run async.

```python
import time

job = client.parse.run(
    file_url="https://example.com/report.pdf",
    config={"model": "ultra-2"},
    async_=True,
)

delay = 2.0
while (status := client.parse.get(job.parse_id)).status in ("queued", "processing"):
    time.sleep(delay)
    delay = min(delay * 1.5, 15)

if status.status == "completed":
    result = client.parse.get_result(job.parse_id)
```

Status reads are free. Instead of polling, a [webhook](https://docs.runpulse.com/v2/webhooks) can tell your server when a job ends. [Jobs and results](https://docs.runpulse.com/v2/jobs) covers statuses and how long results are kept.

### Async client

`AsyncPulse` takes the same arguments and has the same calls, which you `await`:

```python
import asyncio
import os

from pulse import AsyncPulse

client = AsyncPulse(api_key=os.environ["PULSE_API_KEY"])


async def main() -> None:
    job = await client.parse.run(
        file_url="https://example.com/report.pdf",
        config={"model": "ultra-2"},
    )
    status = await client.parse.get(job.parse_id)
    print(status.status)


asyncio.run(main())
```

`AsyncPulse` uses `httpx.AsyncClient`. To use aiohttp instead, install `pip install "pulse-ai[aiohttp]"`; the client picks it up.

### File uploads

Send a document as `file` or `file_url`, never both:

```python
with open("statement.pdf", "rb") as f:
    job = client.parse.run(file=f, config={"model": "ultra-2"})
```

`file` accepts an open binary file or `bytes`. To set the part's filename and content type, pass a tuple:

```python
with open("statement.pdf", "rb") as f:
    job = client.parse.run(
        file=("statement.pdf", f, "application/pdf"),
        config={"model": "ultra-2"},
    )
```

A `file` is limited to 100 MB. Send a larger PDF or TIFF by `file_url`. See [Files and limits](https://docs.runpulse.com/v2/files).

### Request and response types

Requests take plain dicts, typed as `TypedDict`s, as the [API reference](https://docs.runpulse.com/api-reference/v2/parse/run-parse) shows them. Responses are Pydantic models. Both are exported from `pulse`:

```python
from pulse import ParseConfigParams

config: ParseConfigParams = {"model": "ultra-2"}
```

Names are the API's own, in snake_case. Where a name clashes with Python, it has a trailing underscore: `async_`, `from_` on `usage.get`, and `json_` on a table's `content`.

### Handling errors

A failed request raises a subclass of `ApiError`, such as `GoneError` or `NotFoundError` from `pulse.errors`. For a status the API documents, `body` is the error's [problem details](https://docs.runpulse.com/v2/errors), typed as `pulse.Problem`:

```python
from pulse.core.api_error import ApiError
from pulse.errors import GoneError

try:
    client.parse.get_result(parse_id)
except GoneError as e:
    print(e.body.code)  # such as "RESULT_EXPIRED"
    print(e.body.request_id)  # quote it to support
except ApiError as e:
    print(e.status_code)
    print(e.headers)
    print(e.body)
```

Branch on the problem's `code`, never on `title` or `detail`. [Error codes](https://docs.runpulse.com/errors) lists every code and what to do about it.

A status the API doesn't document, such as a `502` from a proxy, raises a plain `ApiError` with the body as it arrived. A timeout or a dropped connection raises `httpx`'s own error, such as `httpx.TimeoutException`.

### Retries

The SDK never retries a request. The `max_retries` option has no effect.

Reads are safe to retry: a status or result read never starts a job or costs credits. A `run` is not. When a `run` fails with a `5xx` or times out, Pulse may already have started the job, and a second `run` starts a second, billed job. [Errors and retries](https://docs.runpulse.com/v2/errors#retry-without-starting-a-job-twice) shows how to retry each case safely.

### Timeouts

Calls have no timeout by default, so a call without `async_` waits until its job ends or the connection closes. To set one, in seconds:

```python
client = Pulse(api_key=os.environ["PULSE_API_KEY"], timeout=120.0)  # every call

client.parse.get(parse_id, request_options={"timeout": 10})  # one call
```

### Raw responses

`.with_raw_response` returns the same calls, answering with the parsed body as `.data` and the HTTP response's `.headers` and `.status_code`. Use it to read headers, such as the `Link` header on a page of a batch's manifest:

```python
response = client.parse.batch.with_raw_response.get_result(batch_id, limit=100)

print(response.headers.get("link"))
print(response.data)
```

### Additional headers and query parameters

```python
client = Pulse(
    api_key=os.environ["PULSE_API_KEY"],
    headers={"X-Custom-Header": "custom value"},  # every call
)

client.parse.get(
    parse_id,
    request_options={
        "additional_headers": {"X-Custom-Header": "custom value"},  # one call
        "additional_query_parameters": {"custom_query_param_key": "custom query param value"},
    },
)
```

### Logging

Logging is off by default. To turn it on:

```python
client = Pulse(
    api_key=os.environ["PULSE_API_KEY"],
    logging={
        "level": "debug",  # defaults to "info"
        "silent": False,  # defaults to True
    },
)
```

To use your own logger, pass it as `"logger"`. It needs `debug`, `info`, `warn` and `error` methods that take a message and keyword arguments.

### Custom HTTP client

To configure proxies, transports or other `httpx` settings, pass your own client. Use `httpx.AsyncClient` with `AsyncPulse`.

```python
import httpx

client = Pulse(
    api_key=os.environ["PULSE_API_KEY"],
    httpx_client=httpx.Client(
        proxy="http://my.test.proxy.example.com",
        transport=httpx.HTTPTransport(local_address="0.0.0.0"),
    ),
)
```

Without `timeout=`, calls use the `httpx` client's own timeout, which defaults to 5 seconds. Set `timeout=None` on the `httpx` client, or pass `timeout=` to `Pulse`, so a call without `async_` can wait for its job.

## Moving from 1.x

`pulse-ai` replaces `pulse-python-sdk`. Both install the `pulse` module, so uninstall the 1.x package first:

```sh
pip uninstall pulse-python-sdk
pip install pulse-ai
```

It calls API version 2, where two endpoints change names: version 1's `/extract` is version 2's `/parse`, and version 1's `/schema` is version 2's `/extract`.

| 1.x (`pulse-python-sdk`) | 2.x (`pulse-ai`) |
| --- | --- |
| `client.extract(...)` | `client.parse.run(...)`, then `client.parse.get_result(parse_id)` |
| `client.extract_async(...)` | `client.parse.run(..., async_=True)` |
| `client.jobs.get_job(...)` | `client.parse.get(parse_id)`, or the `get` of the job's own endpoint |
| `client.schema(...)` | `client.extract.run(parse_id=..., config=...)` |
| `client.split(...)`, `client.tables(...)` | `client.split.run(parse_id=..., config=...)`, and the same for `tables` |
| `client.batch.extract(...)` | `client.parse.batch.run(...)` |
| `client.batch.schema(...)`, `client.batch.split(...)`, `client.batch.tables(...)` | None: run the step on each document's parse |
| `client.pipeline.execute(...)` | `client.pipeline.run(...)` |
| `client.webhooks.create_webhook_link()` | `client.webhook.create(...)` |
| `client.form`, `client.results`, `client.large_results` | None: these stay on version 1 |

Version 2 also changes what a call returns: a `run` returns the job's id, and you read the result with `get_result`. [Moving from V1](https://docs.runpulse.com/v2/moving-from-v1) maps every option.

> [!WARNING]
> Keep your organization's default API version at 1 while any code still uses `pulse-python-sdk`. The 1.x SDK sends no `Pulse-Version` header, so with the default at 2, its calls reach version 2 and fail.

## Requirements

Python 3.10 or later.

## Contributing

This library is generated from the Pulse API's OpenAPI document. A change made directly to the code here is overwritten by the next release. Open an issue first, or a PR as a proof of concept, and we'll move the change into the generator.

Changes to this README are welcome: it's maintained by hand.

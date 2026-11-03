# Reference
## Parse
<details><summary><code>client.parse.<a href="src/pulse/parse/client.py">run</a>(...) -> ParseResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Parse a document into Markdown and elements, each with its page and position. Send a `file` or a `file_url`, with `config` or a saved `config_id`. A parse costs 1 credit per page. By default, the call waits for the job to end. With `async: true`, it returns `202` at once. Read the result at `GET /parse/{parse_id}/result`. Uploads are limited to 100 MB, so send a larger PDF or TIFF by `file_url`. The result's `failed_pages` lists any page that couldn't be parsed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.run(
    file="example_file",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**async:** `typing.Optional[bool]` — Set to `true` to return `202` at once instead of waiting.
    
</dd>
</dl>

<dl>
<dd>

**file:** `typing.Optional[core.File]` 
    
</dd>
</dl>

<dl>
<dd>

**file_url:** `typing.Optional[str]` — The document's URL: a public `http(s)` URL, a public `s3://` or `gs://` object, or an upload URL Pulse issued.
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[ParseConfig]` — This request's options.
    
</dd>
</dl>

<dl>
<dd>

**config_id:** `typing.Optional[str]` — A saved config's id, sent in place of `config`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.<a href="src/pulse/parse/client.py">get</a>(...) -> ParseStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a parse's status. Once it is `completed`, read its result at `GET /parse/{parse_id}/result`. Anyone in your organization can read the status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.get(
    parse_id="parse_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**parse_id:** `str` — The `parse_id` that `POST /parse` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.<a href="src/pulse/parse/client.py">cancel</a>(...) -> ParseStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel a parse that is still `queued` or `processing`. A canceled parse never completes and isn't charged, and anything it saved is deleted. Only the user who started it can cancel it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.cancel(
    parse_id="parse_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**parse_id:** `str` — The `parse_id` that `POST /parse` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.<a href="src/pulse/parse/client.py">get_result</a>(...) -> ParseResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a completed parse's Markdown, elements and requested outputs, with the pages and credits it used. Anyone in your organization can read it. If your organization's retention deletes a result the first time it's read, save the response, because a later read returns `410`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.get_result(
    parse_id="parse_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**parse_id:** `str` — The `parse_id` that `POST /parse` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Classify
<details><summary><code>client.classify.<a href="src/pulse/classify/client.py">run</a>(...) -> ClassifyResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sort a document into one of the categories you list in `config.classifications`. Send a `file` or a `file_url`, with `config` or a saved `config_id`. By default, the call waits for the job to end. With `async: true`, it returns `202` at once. Read the result at `GET /classify/{classify_id}/result`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.classify.run(
    file="example_file",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**file:** `typing.Optional[core.File]` 
    
</dd>
</dl>

<dl>
<dd>

**file_url:** `typing.Optional[str]` — The document's URL: a public `http(s)` URL, a public `s3://` or `gs://` object, or an upload URL Pulse issued.
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[ClassifyConfig]` — This request's options.
    
</dd>
</dl>

<dl>
<dd>

**config_id:** `typing.Optional[str]` — A saved config's id, sent in place of `config`.
    
</dd>
</dl>

<dl>
<dd>

**async:** `typing.Optional[bool]` — Set to `true` to return `202` at once instead of waiting.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.classify.<a href="src/pulse/classify/client.py">get</a>(...) -> ClassifyStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a classification's status. Once it is `completed`, read its result at `GET /classify/{classify_id}/result`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.classify.get(
    classify_id="classify_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**classify_id:** `str` — The `classify_id` that `POST /classify` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.classify.<a href="src/pulse/classify/client.py">cancel</a>(...) -> ClassifyStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel a classification that is still `queued` or `processing`. Only the user who started it can cancel it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.classify.cancel(
    classify_id="classify_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**classify_id:** `str` — The `classify_id` that `POST /classify` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.classify.<a href="src/pulse/classify/client.py">get_result</a>(...) -> ClassifyResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a completed classification's category and confidence, with the credits it used.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.classify.get_result(
    classify_id="classify_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**classify_id:** `str` — The `classify_id` that `POST /classify` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Extract
<details><summary><code>client.extract.<a href="src/pulse/extract/client.py">run</a>(...) -> ExtractResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fill in your JSON Schema with data from a completed parse. Send the parse's `parse_id` with `config` or a saved `config_id`. By default, the call waits for the job to end. With `async: true`, it returns `202` at once. Read the data at `GET /extract/{extract_id}/result`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.extract.run(
    parse_id="parse_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**parse_id:** `str` — The `parse_id` of a completed parse whose result hasn't expired.
    
</dd>
</dl>

<dl>
<dd>

**async:** `typing.Optional[bool]` — Set to `true` to return `202` at once instead of waiting.
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[ExtractConfig]` — This request's options.
    
</dd>
</dl>

<dl>
<dd>

**config_id:** `typing.Optional[str]` — A saved config's id, sent in place of `config`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.extract.<a href="src/pulse/extract/client.py">get</a>(...) -> ExtractStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get an extraction's status. Once it is `completed`, read its data at `GET /extract/{extract_id}/result`. Anyone in your organization can read the status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.extract.get(
    extract_id="extract_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**extract_id:** `str` — The `extract_id` that `POST /extract` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.extract.<a href="src/pulse/extract/client.py">cancel</a>(...) -> ExtractStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel an extraction that is still `queued` or `processing`. Only the user who started it can cancel it. For anyone else, the cancel returns `404`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.extract.cancel(
    extract_id="extract_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**extract_id:** `str` — The `extract_id` that `POST /extract` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.extract.<a href="src/pulse/extract/client.py">get_result</a>(...) -> ExtractResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a completed extraction's data in the formats `config.format` asked for, with the credits it used and the parse it read.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.extract.get_result(
    extract_id="extract_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**extract_id:** `str` — The `extract_id` that `POST /extract` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Split
<details><summary><code>client.split.<a href="src/pulse/split/client.py">run</a>(...) -> SplitResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Find the pages of a completed parse that belong to each topic you name. A split reads the whole parse and costs 1 credit per page (6 with `effort: high`), however many topics you send. By default, the call waits for the job to end. With `async: true`, it returns `202` at once. Read the pages at `GET /split/{split_id}/result`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.split.run(
    parse_id="parse_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**parse_id:** `str` — The `parse_id` of a completed parse whose result hasn't expired.
    
</dd>
</dl>

<dl>
<dd>

**async:** `typing.Optional[bool]` — Set to `true` to return `202` at once instead of waiting.
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[SplitConfig]` — This request's options.
    
</dd>
</dl>

<dl>
<dd>

**config_id:** `typing.Optional[str]` — A saved config's id, sent in place of `config`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.split.<a href="src/pulse/split/client.py">get</a>(...) -> SplitStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a split's status. Once it is `completed`, read its pages at `GET /split/{split_id}/result`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.split.get(
    split_id="split_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**split_id:** `str` — The `split_id` that `POST /split` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.split.<a href="src/pulse/split/client.py">cancel</a>(...) -> SplitStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel a split that is still `queued` or `processing`. A canceled split never completes and isn't charged. Only the user who started it can cancel it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.split.cancel(
    split_id="split_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**split_id:** `str` — The `split_id` that `POST /split` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.split.<a href="src/pulse/split/client.py">get_result</a>(...) -> SplitResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get the pages a completed split found for each topic, with the credits it used and the parse it read.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.split.get_result(
    split_id="split_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**split_id:** `str` — The `split_id` that `POST /split` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Tables
<details><summary><code>client.tables.<a href="src/pulse/tables/client.py">run</a>(...) -> TableResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Merge a completed parse's tables across pages and return each in the formats you ask for. Send the parse's `parse_id` with `config` or a saved `config_id`. It costs 0.5 credits per table returned. By default, the call waits for the job to end. With `async: true`, it returns `202` at once. Read the tables at `GET /tables/{tables_id}/result`. Tables must be enabled for your organization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.tables.run(
    parse_id="parse_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**parse_id:** `str` — The `parse_id` of a completed parse whose result hasn't expired.
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[TableConfig]` — This request's options.
    
</dd>
</dl>

<dl>
<dd>

**config_id:** `typing.Optional[str]` — A saved config's id, sent in place of `config`.
    
</dd>
</dl>

<dl>
<dd>

**async:** `typing.Optional[bool]` — Set to `true` to return `202` at once instead of waiting.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.tables.<a href="src/pulse/tables/client.py">get</a>(...) -> TableStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a tables job's status. Once it is `completed`, read its tables at `GET /tables/{tables_id}/result`. Anyone in your organization can read the status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.tables.get(
    tables_id="tables_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**tables_id:** `str` — The `tables_id` that `POST /tables` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.tables.<a href="src/pulse/tables/client.py">cancel</a>(...) -> TableStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel a tables job that is still `queued` or `processing`. A canceled job never completes and isn't charged, and anything it saved is deleted. Only the user who started it can cancel it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.tables.cancel(
    tables_id="tables_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**tables_id:** `str` — The `tables_id` that `POST /tables` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.tables.<a href="src/pulse/tables/client.py">get_result</a>(...) -> TableResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a completed job's tables in the formats `config.format` asked for, with the credits it used. Anyone in your organization can read it. A `TABLE_ANALYSIS_SKIPPED`, `MERGE_NOT_VERIFIED` or `MERGE_FALLBACK` warning means some cross-page merges may be wrong, so check those tables.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.tables.get_result(
    tables_id="tables_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**tables_id:** `str` — The `tables_id` that `POST /tables` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Charts
<details><summary><code>client.charts.<a href="src/pulse/charts/client.py">run</a>(...) -> ChartsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Read every chart on the selected pages of a completed parse as data (type, axes, series and points), and build the export files you ask for. It costs 1 credit per chart read. By default, the call waits for the job to end. With `async: true`, it returns `202` at once. Read the charts and exports at `GET /charts/{charts_id}/result`. Charts must be enabled for your organization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.charts.run(
    parse_id="parse_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**parse_id:** `str` — The `parse_id` of a completed parse whose result hasn't expired.
    
</dd>
</dl>

<dl>
<dd>

**async:** `typing.Optional[bool]` — Set to `true` to return `202` at once instead of waiting.
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[ChartsConfig]` — This request's options.
    
</dd>
</dl>

<dl>
<dd>

**config_id:** `typing.Optional[str]` — A saved config's id, sent in place of `config`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.charts.<a href="src/pulse/charts/client.py">get</a>(...) -> ChartsStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a charts job's status. Once it is `completed`, read its result at `GET /charts/{charts_id}/result`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.charts.get(
    charts_id="charts_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**charts_id:** `str` — The `charts_id` that `POST /charts` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.charts.<a href="src/pulse/charts/client.py">cancel</a>(...) -> ChartsStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel a charts job that is still `queued` or `processing`. A canceled job isn't charged. Only the user who started it can cancel it. A job that has already ended returns `409`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.charts.cancel(
    charts_id="charts_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**charts_id:** `str` — The `charts_id` that `POST /charts` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.charts.<a href="src/pulse/charts/client.py">get_result</a>(...) -> ChartsResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a completed job's charts, with each export file's full content in `exports`. To save a file, decode its `content_base64` and write it under its `filename`. If your organization's retention deletes a result the first time it's read, exports included, save the response, because a later read returns `410`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.charts.get_result(
    charts_id="charts_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**charts_id:** `str` — The `charts_id` that `POST /charts` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Pipeline
<details><summary><code>client.pipeline.<a href="src/pulse/pipeline/client.py">run</a>(...) -> PipelineResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Parse one document (`config.step`), then run up to 10 more steps on the parse once it completes (`config.children`). A pipeline always runs async. Read its status at `GET /pipeline/{pipeline_id}`, each step's status at `GET /pipeline/{pipeline_id}/result`, and a completed step's output at its own endpoint. Each step costs what its endpoint costs, and the pipeline adds nothing. The pipeline and its steps expire together, counted from the pipeline's end.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.pipeline.run(
    file="example_file",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**file:** `typing.Optional[core.File]` 
    
</dd>
</dl>

<dl>
<dd>

**file_url:** `typing.Optional[str]` — The document's URL: a public `http(s)` URL, a public `s3://` or `gs://` object, or an upload URL Pulse issued.
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[PipelineConfig]` — This request's options.
    
</dd>
</dl>

<dl>
<dd>

**config_id:** `typing.Optional[str]` — A saved config's id, sent in place of `config`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.pipeline.<a href="src/pulse/pipeline/client.py">get</a>(...) -> PipelineStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a pipeline's status. Each step's own status is at `GET /pipeline/{pipeline_id}/result`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.pipeline.get(
    pipeline_id="pipeline_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**pipeline_id:** `str` — The `pipeline_id` that `POST /pipeline` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.pipeline.<a href="src/pulse/pipeline/client.py">cancel</a>(...) -> PipelineStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel a pipeline that is still `queued` or `processing`, along with its unfinished steps. Those steps never complete and aren't charged. A step that already completed keeps its result. Only the user who started the pipeline can cancel it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.pipeline.cancel(
    pipeline_id="pipeline_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**pipeline_id:** `str` — The `pipeline_id` that `POST /pipeline` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.pipeline.<a href="src/pulse/pipeline/client.py">get_result</a>(...) -> PipelineResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get each step's current status. You can read it as soon as `POST /pipeline` returns, and after the pipeline ends or expires. It holds no step output, so read a completed step at its own endpoint, such as `GET /parse/{parse_id}/result`. `usage` totals the completed steps. Reading this doesn't count as reading a step's result. A step's result returns `410` once it has expired, or once it was read and your organization's retention deletes a result on its first read.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.pipeline.get_result(
    pipeline_id="pipeline_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**pipeline_id:** `str` — The `pipeline_id` that `POST /pipeline` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Usage
<details><summary><code>client.usage.<a href="src/pulse/usage/client.py">get</a>(...) -> UsageResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get the pages processed and credits used by your organization's jobs created in the window, with your plan's credit allowance. Calling this endpoint is free.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.usage.get()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**from:** `typing.Optional[str]` — The window's start, inclusive. Send an ISO 8601 time ending in `Z`, such as `2026-10-01T00:00:00Z`. Defaults to 30 days before `to`.
    
</dd>
</dl>

<dl>
<dd>

**to:** `typing.Optional[str]` — The window's end, exclusive. Send an ISO 8601 time ending in `Z`, such as `2026-10-01T00:00:00Z`. Defaults to now.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhook
<details><summary><code>client.webhook.<a href="src/pulse/webhook/client.py">list</a>() -> WebhookListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List your organization's webhooks, newest first, without their secrets or header values.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.webhook.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhook.<a href="src/pulse/webhook/client.py">create</a>(...) -> WebhookPostResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Add a webhook. Your organization can have up to 10. Pulse pings the new webhook at once, and the response says whether the ping got through. This is the only response that returns the signing `secret`. Jobs created 15 seconds or more after this call send each listed event, signed per Standard Webhooks and carrying only the job's id. A newer status replaces one not yet delivered. Failed deliveries are retried for about 35 hours, and a webhook that keeps failing is turned off.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.webhook.create(
    url="url",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**url:** `str` — The URL Pulse sends events to: a public `https` URL on port 443, at most 2,048 characters, with no credentials in it. You can't change it later.
    
</dd>
</dl>

<dl>
<dd>

**events:** `typing.Optional[typing.List[CreateWebhookRequestEventsItem]]` — The events to send, each named `<job type>.<status>`, such as `extract.completed`. Defaults to none.
    
</dd>
</dl>

<dl>
<dd>

**description:** `typing.Optional[str]` — A note for your own reference.
    
</dd>
</dl>

<dl>
<dd>

**headers:** `typing.Optional[typing.Dict[str, str]]` — Static headers to send with every delivery, such as a token your gateway checks. You can set up to 5, but not Pulse's own, such as `Content-Type` or `webhook-*`. Values are encrypted and never returned.
    
</dd>
</dl>

<dl>
<dd>

**secret:** `typing.Optional[str]` — The signing secret, as `whsec_` followed by the base64 of 24 to 64 random bytes. If omitted, Pulse generates one. Only the create response returns it.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhook.<a href="src/pulse/webhook/client.py">get</a>(...) -> WebhookResponseBase</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get one of your organization's webhooks, without its secret or header values.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.webhook.get(
    webhook_id="webhook_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**webhook_id:** `str` — The `webhook_id` that `POST /webhook` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhook.<a href="src/pulse/webhook/client.py">delete</a>(...) -> WebhookDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a webhook. Pulse sends it nothing more, including retries.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.webhook.delete(
    webhook_id="webhook_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**webhook_id:** `str` — The `webhook_id` that `POST /webhook` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhook.<a href="src/pulse/webhook/client.py">update</a>(...) -> WebhookResponseBase</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Change a webhook. Each field you send replaces its current value. You can't change the URL, so create another webhook instead. Turning the webhook back on with `enabled: true` clears `disabled_reason`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.webhook.update(
    webhook_id="webhook_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**webhook_id:** `str` — The `webhook_id` that `POST /webhook` returned.
    
</dd>
</dl>

<dl>
<dd>

**events:** `typing.Optional[typing.List[UpdateWebhookRequestEventsItem]]` — The events to send, replacing the current list. An event you add applies only to jobs created 15 seconds or more after this request.
    
</dd>
</dl>

<dl>
<dd>

**enabled:** `typing.Optional[bool]` — Set to `false` to turn the webhook off, or `true` to turn it back on and clear `disabled_reason`. After 30 days off, it covers only jobs created 15 seconds or more after this request.
    
</dd>
</dl>

<dl>
<dd>

**description:** `typing.Optional[str]` — A new note. An empty string clears the note.
    
</dd>
</dl>

<dl>
<dd>

**headers:** `typing.Optional[typing.Dict[str, str]]` — Static headers to replace the current ones, or `{}` to clear them. You can set up to 5, but not Pulse's own, such as `Content-Type` or `webhook-*`. Values are encrypted and never returned.
    
</dd>
</dl>

<dl>
<dd>

**secret:** `typing.Optional[str]` — A signing secret of your own, as `whsec_` followed by the base64 of 24 to 64 random bytes. The previous secret keeps signing alongside it for 24 hours.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhook.<a href="src/pulse/webhook/client.py">rotate</a>(...) -> WebhookRotateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Generate a new signing secret, which only this response returns. For 24 hours, deliveries are signed with both the new and the previous secret. Rotating again within that time retires the oldest secret at once.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.webhook.rotate(
    webhook_id="webhook_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**webhook_id:** `str` — The `webhook_id` that `POST /webhook` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhook.<a href="src/pulse/webhook/client.py">ping</a>(...) -> WebhookPingResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Send the webhook a signed `webhook.ping` and report whether it got through within 15 seconds. A ping doesn't count toward the webhook's failures. You can ping each URL 10 times per hour, and your organization's webhooks 30 times per hour in all.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.webhook.ping(
    webhook_id="webhook_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**webhook_id:** `str` — The `webhook_id` that `POST /webhook` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Charts Configs
<details><summary><code>client.charts.configs.<a href="src/pulse/charts/configs/client.py">list</a>() -> ChartsConfigListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List your organization's saved `/charts` configs, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.charts.configs.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.charts.configs.<a href="src/pulse/charts/configs/client.py">create</a>(...) -> ChartsConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Save a config under a name. Later, send its `config_id` to `POST /charts` in place of `config`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.charts.configs.create(
    name="name",
    config={},
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `ChartsConfig` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.charts.configs.<a href="src/pulse/charts/configs/client.py">delete_all</a>()</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete every `/charts` config your organization saved. Their ids are refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.charts.configs.delete_all()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.charts.configs.<a href="src/pulse/charts/configs/client.py">get</a>(...) -> ChartsConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get one of your organization's saved `/charts` configs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.charts.configs.get(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.charts.configs.<a href="src/pulse/charts/configs/client.py">delete</a>(...) -> ConfigDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a saved config. Its id is refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.charts.configs.delete(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.charts.configs.<a href="src/pulse/charts/configs/client.py">update</a>(...) -> ChartsConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Rename a saved config, replace its whole config, or both. An empty body changes nothing.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.charts.configs.update(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[ChartsConfig]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Classify Configs
<details><summary><code>client.classify.configs.<a href="src/pulse/classify/configs/client.py">list</a>() -> ClassifyConfigListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List your organization's saved `/classify` configs, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.classify.configs.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.classify.configs.<a href="src/pulse/classify/configs/client.py">create</a>(...) -> ClassifyConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Save a config under a name. Later, send its `config_id` to `POST /classify` in place of `config`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.classify.configs.create(
    name="name",
    config={
        "classifications": [
            {
                "name": "name"
            }
        ]
    },
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `ClassifyConfig` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.classify.configs.<a href="src/pulse/classify/configs/client.py">delete_all</a>()</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete every `/classify` config your organization saved. Their ids are refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.classify.configs.delete_all()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.classify.configs.<a href="src/pulse/classify/configs/client.py">get</a>(...) -> ClassifyConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get one of your organization's saved `/classify` configs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.classify.configs.get(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.classify.configs.<a href="src/pulse/classify/configs/client.py">delete</a>(...) -> ConfigDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a saved config. Its id is refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.classify.configs.delete(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.classify.configs.<a href="src/pulse/classify/configs/client.py">update</a>(...) -> ClassifyConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Rename a saved config, replace its whole config, or both. An empty body changes nothing.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.classify.configs.update(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[ClassifyConfig]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Extract Configs
<details><summary><code>client.extract.configs.<a href="src/pulse/extract/configs/client.py">list</a>() -> ExtractConfigListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List your organization's saved `/extract` configs, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.extract.configs.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.extract.configs.<a href="src/pulse/extract/configs/client.py">create</a>(...) -> ExtractConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Save a config under a name. Later, send its `config_id` to `POST /extract` in place of `config`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.extract.configs.create(
    name="name",
    config={
        "input_schema": {
            "key": "value"
        }
    },
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `ExtractConfig` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.extract.configs.<a href="src/pulse/extract/configs/client.py">delete_all</a>()</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete every `/extract` config your organization saved. Their ids are refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.extract.configs.delete_all()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.extract.configs.<a href="src/pulse/extract/configs/client.py">get</a>(...) -> ExtractConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get one of your organization's saved `/extract` configs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.extract.configs.get(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.extract.configs.<a href="src/pulse/extract/configs/client.py">delete</a>(...) -> ConfigDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a saved config. Its id is refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.extract.configs.delete(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.extract.configs.<a href="src/pulse/extract/configs/client.py">update</a>(...) -> ExtractConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Rename a saved config, replace its whole config, or both. An empty body changes nothing.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.extract.configs.update(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[ExtractConfig]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Parse Configs
<details><summary><code>client.parse.configs.<a href="src/pulse/parse/configs/client.py">list</a>() -> ParseConfigListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List your organization's saved `/parse` configs, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.configs.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.configs.<a href="src/pulse/parse/configs/client.py">create</a>(...) -> ParseConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Save a config under a name. Later, send its `config_id` to `POST /parse` in place of `config`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.configs.create(
    name="name",
    config={
        "model": "ultra-2"
    },
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `ParseConfig` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.configs.<a href="src/pulse/parse/configs/client.py">delete_all</a>()</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete every `/parse` config your organization saved. Their ids are refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.configs.delete_all()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.configs.<a href="src/pulse/parse/configs/client.py">get</a>(...) -> ParseConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get one of your organization's saved `/parse` configs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.configs.get(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.configs.<a href="src/pulse/parse/configs/client.py">delete</a>(...) -> ConfigDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a saved config. Its id is refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.configs.delete(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.configs.<a href="src/pulse/parse/configs/client.py">update</a>(...) -> ParseConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Rename a saved config, replace its whole config, or both. An empty body changes nothing.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.configs.update(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[ParseConfig]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Parse Batch
<details><summary><code>client.parse.batch.<a href="src/pulse/parse/batch/client.py">run</a>(...) -> ParseBatchResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Parse up to 1,000 documents with one config. Send them as `files`, as `file_urls`, or as a public `folder_url` in Amazon S3, Google Cloud Storage or Azure Blob Storage. Each document becomes its own `/parse` job, checked against your plan and billed when it runs. A job that fails doesn't stop the others. Uploaded or listed files of an unsupported type are skipped. A batch always runs async. Read its status at `GET /parse/batch/{batch_id}` and its manifest at `GET /parse/batch/{batch_id}/result`. A batch that isn't done in 48 hours fails.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.batch.run(
    files=["example_files"],
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**files:** `typing.Optional[typing.List[core.File]]` — The documents to parse, as `multipart/form-data` file parts, each named `files`. Files without a supported extension (`.pdf`, `.jpg`, `.jpeg`, `.png`, `.tif`, `.tiff`, `.docx`, `.pptx`, `.xlsx`, `.xlsm`, `.xls`, `.html`, `.htm`) and hidden files are skipped.
    
</dd>
</dl>

<dl>
<dd>

**file_urls:** `typing.Optional[typing.List[str]]` — Public `http` or `https` URLs, or `s3://` or `gs://` URLs of public objects or of your organization's Pulse files. Each is fetched when its job runs, so a signed URL must still be valid then.
    
</dd>
</dl>

<dl>
<dd>

**folder_url:** `typing.Optional[str]` — A folder anyone can list and read, as `s3://<bucket>/<folder>/`, `gs://<bucket>/<folder>/`, `https://<account>.blob.core.windows.net/<container>/<folder>/` or the bucket's `https` URL. Hidden and archived files are skipped. It can hold at most 1,000 supported files and 10,000 objects.
    
</dd>
</dl>

<dl>
<dd>

**max_depth:** `typing.Optional[int]` — How many levels of subfolders to include. `0` takes only the folder's own files. Defaults to every level.
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[ParseConfig]` — This request's options.
    
</dd>
</dl>

<dl>
<dd>

**config_id:** `typing.Optional[str]` — A saved config's id, sent in place of `config`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.batch.<a href="src/pulse/parse/batch/client.py">get</a>(...) -> BatchStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a batch's status, with its documents counted by state. A batch ends `completed`, `failed` or `canceled` within 48 hours of being sent. Once it ends, read its manifest at `GET /parse/batch/{batch_id}/result`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.batch.get(
    batch_id="batch_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**batch_id:** `str` — The `batch_id` that `POST /parse/batch` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.batch.<a href="src/pulse/parse/batch/client.py">cancel</a>(...) -> BatchStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancel a batch that hasn't ended. The batch becomes `canceled` at once, and its unfinished jobs are canceled within seconds. A job that finishes first keeps its result, so `summary` and the manifest can change until every job has ended. Anyone in your organization can cancel a batch. A batch that has already ended returns `409`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.batch.cancel(
    batch_id="batch_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**batch_id:** `str` — The `batch_id` that `POST /parse/batch` returned.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.parse.batch.<a href="src/pulse/parse/batch/client.py">get_result</a>(...) -> typing.List[ParseBatchEntry]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get the batch's manifest: one entry per ended job, in the order the jobs ended, each as `GET /parse/{parse_id}` returned it when the job ended. It's readable while the batch runs, and a job that isn't listed hasn't ended. Entries aren't updated, so read a job's own status for its `expires_at`. With `limit`, follow the `Link` header to the next page. While the batch runs, request the last page again later for new entries.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.parse.batch.get_result(
    batch_id="batch_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**batch_id:** `str` — The `batch_id` that `POST /parse/batch` returned.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — The most entries to return. Without it, every entry comes back in one response.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Where the page starts. The previous page's `Link` URL carries it, so don't set it yourself. Ignored without `limit`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Pipeline Configs
<details><summary><code>client.pipeline.configs.<a href="src/pulse/pipeline/configs/client.py">list</a>() -> PipelineConfigListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List your organization's saved `/pipeline` configs, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.pipeline.configs.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.pipeline.configs.<a href="src/pulse/pipeline/configs/client.py">create</a>(...) -> PipelineConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Save a config under a name. Later, send its `config_id` to `POST /pipeline` in place of `config`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.pipeline.configs.create(
    name="name",
    config={
        "step": {
            "type": "parse",
            "config": {
                "model": "ultra-2"
            }
        }
    },
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `PipelineConfig` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.pipeline.configs.<a href="src/pulse/pipeline/configs/client.py">delete_all</a>()</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete every `/pipeline` config your organization saved. Their ids are refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.pipeline.configs.delete_all()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.pipeline.configs.<a href="src/pulse/pipeline/configs/client.py">get</a>(...) -> PipelineConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get one of your organization's saved `/pipeline` configs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.pipeline.configs.get(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.pipeline.configs.<a href="src/pulse/pipeline/configs/client.py">delete</a>(...) -> ConfigDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a saved config. Its id is refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.pipeline.configs.delete(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.pipeline.configs.<a href="src/pulse/pipeline/configs/client.py">update</a>(...) -> PipelineConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Rename a saved config, replace its whole config, or both. An empty body changes nothing.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.pipeline.configs.update(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[PipelineConfig]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Settings Org
<details><summary><code>client.settings.org.<a href="src/pulse/settings/org/client.py">get</a>() -> OrgSettings</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get your organization's name, address and default API version, which is the version a request without a `Pulse-Version` header gets.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.settings.org.get()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.settings.org.<a href="src/pulse/settings/org/client.py">update</a>(...) -> OrgSettings</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Change your organization's settings. Only the fields you send change, and `{}` changes nothing. Only an organization admin can make changes. A new `default_api_version` takes effect within a minute.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.settings.org.update()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**address:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**default_api_version:** `typing.Optional[UpdateOrgRequestDefaultApiVersion]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Split Configs
<details><summary><code>client.split.configs.<a href="src/pulse/split/configs/client.py">list</a>() -> SplitConfigListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List your organization's saved `/split` configs, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.split.configs.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.split.configs.<a href="src/pulse/split/configs/client.py">create</a>(...) -> SplitConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Save a config under a name. Later, send its `config_id` to `POST /split` in place of `config`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.split.configs.create(
    name="name",
    config={
        "topics": [
            {
                "name": "name"
            }
        ]
    },
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `SplitConfig` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.split.configs.<a href="src/pulse/split/configs/client.py">delete_all</a>()</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete every `/split` config your organization saved. Their ids are refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.split.configs.delete_all()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.split.configs.<a href="src/pulse/split/configs/client.py">get</a>(...) -> SplitConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get one of your organization's saved `/split` configs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.split.configs.get(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.split.configs.<a href="src/pulse/split/configs/client.py">delete</a>(...) -> ConfigDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a saved config. Its id is refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.split.configs.delete(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.split.configs.<a href="src/pulse/split/configs/client.py">update</a>(...) -> SplitConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Rename a saved config, replace its whole config, or both. An empty body changes nothing.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.split.configs.update(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[SplitConfig]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Tables Configs
<details><summary><code>client.tables.configs.<a href="src/pulse/tables/configs/client.py">list</a>() -> TableConfigListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List your organization's saved `/tables` configs, newest first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.tables.configs.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.tables.configs.<a href="src/pulse/tables/configs/client.py">create</a>(...) -> TableConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Save a config under a name. Later, send its `config_id` to `POST /tables` in place of `config`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.tables.configs.create(
    name="name",
    config={},
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `TableConfig` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.tables.configs.<a href="src/pulse/tables/configs/client.py">delete_all</a>()</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete every `/tables` config your organization saved. Their ids are refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.tables.configs.delete_all()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.tables.configs.<a href="src/pulse/tables/configs/client.py">get</a>(...) -> TableConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get one of your organization's saved `/tables` configs.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.tables.configs.get(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.tables.configs.<a href="src/pulse/tables/configs/client.py">delete</a>(...) -> ConfigDeleteResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a saved config. Its id is refused afterwards.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.tables.configs.delete(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.tables.configs.<a href="src/pulse/tables/configs/client.py">update</a>(...) -> TableConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Rename a saved config, replace its whole config, or both. An empty body changes nothing.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from pulse import Pulse
from pulse.environment import PulseEnvironment

client = Pulse(
    api_key="<value>",
    environment=PulseEnvironment.DEFAULT,
)

client.tables.configs.update(
    config_id="config_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**config_id:** `str` — The saved config's `config_id`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[TableConfig]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>


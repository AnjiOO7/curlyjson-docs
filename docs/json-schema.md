<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# JSON Schema Validator

[JSON Schema Validator](https://curlyjson.com/json-schema-validator) checks a JSON document against a JSON Schema and lists every problem — in your browser.

## Validating

Paste the document on the left and the schema on the right. The **Result** updates as you type:

- **✓ Matches the schema** when there are no problems.
- Otherwise, one row per problem: the **path** of the value that failed (like `$.address`), what is wrong (`Missing required property "country".`) and the schema keyword that caught it (`required`).

Click a row to put the cursor on that value in your JSON. **Copy report** copies every problem as `path: message`, one per line.

## Versions

**Auto version** reads the schema's `$schema` and picks the matching draft, or 2020-12 when there isn't one. You can choose one yourself:

| Choice | Use for |
|---|---|
| 2020-12 | New schemas, OpenAPI 3.1 |
| 2019-09 | Schemas that say `draft/2019-09` |
| Draft 7 | Most older schemas, including draft 6 |
| Draft 4 | OpenAPI 3.0-era and legacy schemas |

`format` is checked, not ignored: `date`, `time`, `date-time`, `duration`, `email`, `hostname`, `ipv4`, `ipv6`, `uri`, `uri-reference`, `uuid`, `json-pointer`, `regex` and more.

`$ref` works within the schema (`#/$defs/…`, `#/definitions/…`, `$anchor`). Schemas on other websites are not downloaded.

## Generating a schema

No schema yet? Press **Generate from JSON**. It writes a 2020-12 schema from the document on the left:

- every property with its type, including nested objects and arrays;
- `required` lists the keys of each object — for arrays of objects, only keys present in every item;
- common string formats are spotted: `date-time`, `date`, `email`, `uri`.

Treat it as a starting point: add `minimum`, `enum`, `pattern` or `additionalProperties: false` where your data needs them. If the schema editor already has your own schema, press the button twice to replace it.

## Privacy

Validation runs in your browser. Your last document and schema are remembered on this device only; **Clear** removes them. **Share** puts both in the link after `#`, which is never sent to a server.

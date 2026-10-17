<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# YAML, XML & TOML

Six converters share one layout: paste on the left, get the result on the right as you type.

| From JSON | To JSON |
|---|---|
| [JSON → YAML](https://curlyjson.com/json-to-yaml) | [YAML → JSON](https://curlyjson.com/yaml-to-json) |
| [JSON → XML](https://curlyjson.com/json-to-xml) | [XML → JSON](https://curlyjson.com/xml-to-json) |
| [JSON → TOML](https://curlyjson.com/json-to-toml) | [TOML → JSON](https://curlyjson.com/toml-to-json) |

The **swap** button (for example **YAML → JSON**) opens the other direction and takes your output with it, so you can round-trip a file.

Every converter keeps **big integers exact** (like `9007199254740993`). When something can't be carried over — a `null` in TOML, a key that isn't a valid XML name — a yellow note under the output says what changed. Nothing is dropped silently.

## YAML

**JSON → YAML** writes readable block-style YAML. Multi-line strings become `|` blocks. Choose 2 or 4 spaces.

Strings that older YAML parsers would misread are quoted. `"yes"`, `"no"`, `"on"`, `"off"` and `"010"` are written as `"yes"` rather than `yes`. YAML 1.1 (used by PyYAML, Ruby and many CI tools) would otherwise turn them into booleans or octal numbers.

**YAML → JSON** reads YAML 1.2:

- Only `true` and `false` are booleans, so `country: NO` stays the string `"NO"`.
- Anchors (`&name`), aliases (`*name`) and merge keys (`<<: *name`) are expanded.
- Dates such as `2026-10-15` stay strings.
- A file with several documents separated by `---` converts only the first one by default. Tick **All documents** to get a JSON array with one item per document.
- Errors show the line and column, and the line is highlighted.

## XML

XML ⇄ JSON uses one convention in both directions:

| XML | JSON |
|---|---|
| `<book id="42">` | `"book": { "@id": "42" }` |
| `<price currency="USD">8.99</price>` | `"price": { "#text": "8.99", "@currency": "USD" }` |
| `<tag>a</tag><tag>b</tag>` | `"tag": ["a", "b"]` |

**XML → JSON** options:

- **Detect numbers**: `12` → `12` and `true` → `true`. Values with leading zeros (`007`) and numbers too long for JavaScript stay strings, so zip codes and IDs are safe.
- **Always arrays**: every child element becomes an array, even when there's only one. Code that reads the JSON then always gets the same shape.

**JSON → XML**:

- A JSON object with one top-level key uses that key as the root element. Anything else is wrapped in the **Root** name you choose (`root` by default). A top-level array becomes `<root><item>…</item></root>`.
- Keys that aren't valid XML names are fixed: `first name` → `first_name`, `1st` → `_1st`.
- `<`, `&` and quotes are escaped. Empty values become self-closing tags like `<note/>`.

## TOML

**JSON → TOML** writes `[tables]` and `[[array tables]]`, the way `Cargo.toml` and `pyproject.toml` are written by hand.

- The JSON must be an **object** at the top level; TOML files can't be arrays.
- TOML has no `null`. Keys with `null` values are left out, and a note tells you.

**TOML → JSON** supports TOML 1.0: inline tables, array tables, dotted keys and every string type.

- Dates and times become ISO strings. A local date stays `2026-10-15`; a date-time with an offset becomes UTC, like `1979-05-27T15:32:00.000Z`.
- Integers up to 64 bits stay exact.

## Privacy

Everything runs in your browser. Your last input for each converter is remembered on your device. **Clear** removes it.

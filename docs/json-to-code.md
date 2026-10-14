<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# JSON to Code

Paste JSON and get ready-to-use types or classes in **27 languages**. Each language has its own page, for example [/json-to-typescript](https://curlyjson.com/json-to-typescript), [/json-to-go](https://curlyjson.com/json-to-go) and [/json-to-python](https://curlyjson.com/json-to-python). Switch language with the dropdown — your JSON comes with you.

Code generation uses the open-source [quicktype](https://github.com/glideapps/quicktype) engine and runs in a background thread in your browser.

## Supported languages

**Popular:** TypeScript, Zod, Go, Python, Java, C#, Kotlin, Rust, Swift, Dart, PHP, JSON Schema.
**More:** JavaScript, C++, C, Ruby, Scala, Elixir, Haskell, Elm, Crystal, Objective-C, Effect Schema, Flow, React PropTypes, Smithy, Pike.

## Getting the best types

- **Use real data with variety.** Fields missing (or `null`) in some items become optional.
- **Give several samples.** Paste them as **JSON Lines** — one JSON value per line — and they're merged into one type:

```json
{"id": 1, "name": "Ada"}
{"id": 2, "name": "Grace", "email": "grace@example.com"}
{"id": 3, "name": null}
```

  becomes `id: number; name: null | string; email?: string`.
- **Paste JavaScript objects** straight from a console — unquoted keys, single quotes, trailing commas and comments are repaired automatically.
- Set the **Type name** of the top-level type (e.g. `Order`).

## JSON Schema input

Switch the input to **JSON Schema** to generate code from a schema instead of examples. References to other URLs (`$ref` to the web) are not fetched.

## Options

- Each language shows **its own options** (for example *Interfaces only* for TypeScript, `omitempty` for Go, Pydantic for Python). More appear under **More options & type detection**. Options are remembered per language.
- **Type detection** is deliberately quiet by default — strings stay strings. Turn on **Detect enums**, **Detect dates**, **Numbers in strings**, etc. when you want them.

## Download

**Download** saves the code with the right extension (`Order.ts`, `Order.go`, `Order.py`…).

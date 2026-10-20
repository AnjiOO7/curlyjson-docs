<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# jq Playground

The [jq Playground](https://curlyjson.com/jq-playground) runs a jq filter against your JSON and shows the output as you type. It is **the real jq 1.8**, compiled to WebAssembly, so filters behave exactly as on the command line.

Paste JSON on the left and type a filter at the top. The badge shows how many results the filter produced.

## Options

| Option | Same as | Does |
|---|---|---|
| **Raw output** | `jq -r` | Prints strings without quotes — for lists of values, `@csv` and `@tsv` |
| **Compact** | `jq -c` | One result per line |
| **Slurp** | `jq -s` | Reads every input value into one array |
| **Null input** | `jq -n` | Ignores the input; the filter starts from `null` |
| **Sort keys** | `jq -S` | Sorts object keys in the output |

**NDJSON / JSON Lines:** paste one JSON value per line. The filter runs on each; turn on **Slurp** to work with all of them at once.

## Cheat sheet

The examples use the playground's **Sample** document — a list of users with their orders.

| Filter | Does | Example |
|---|---|---|
| `.` | The whole input | `.` |
| `.key` / `.["key"]` | A field | `.users` |
| `.[]` | Every item of an array (or value of an object) | `.users[]` |
| `.[n]`, `.[a:b]` | An item or a slice; negative counts from the end | `.users[0]`, `.users[-1]`, `.users[:2]` |
| `\|` | Pipe one filter into the next | `.users[] \| .name` |
| `,` | Several outputs | `.users[0] \| .name, .email` |
| `{a, b}` | Build an object from fields | `.users[] \| {name, email}` |
| `[ … ]` | Collect outputs into an array | `[.users[].name]` |
| `select(cond)` | Keep values where the condition is true | `.users[] \| select(.active)` |
| `map(f)` | Apply a filter to every array item | `.users \| map(.id)` |
| `length` | Length of an array, string or object | `.users \| length` |
| `keys`, `to_entries` | Object keys, or key/value pairs | `.users[0] \| keys` |
| `add` | Sum numbers, join strings or arrays | `[.users[].orders[].total] \| add` |
| `group_by(f)` | Group array items | `.users \| group_by(.country)` |
| `sort_by(f)`, `unique_by(f)` | Sort or de-duplicate by a field | `.users \| sort_by(.name)` |
| `a // b` | `b` when `a` is null or false | `.nickname // .name` |
| `if … then … else … end` | Conditions | `if .active then "yes" else "no" end` |
| `@csv`, `@tsv` | Format an array as a CSV or TSV line (use **Raw output**) | `.users[] \| [.id, .name] \| @csv` |
| `paths(scalars)` | The path of every leaf value | `[paths(scalars) \| join(".")]` |
| `del(.key)` | Remove a field | `.users \| map(del(.orders))` |

## Common recipes

- **Count items matching a condition:** `.users | map(select(.active)) | length`
- **Turn an array into an object by id:** `.users | map({(.id | tostring): .name}) | add`
- **Sum a nested field per item:** `.users | map({name, spent: ([.orders[].total] | add // 0)})`
- **Flatten to CSV:** `.users[] | [.id, .name, .country] | @csv` with **Raw output** on
- **Find every key named `email`, at any depth:** `.. | .email? // empty`

## Errors

- **Filter errors** (a typo, an unknown function) show under the filter with the line and column.
- **Invalid JSON** is marked in the input with the line and column.
- **Runtime errors** (for example indexing a number) show above the output, along with any results produced before the error.

A filter that never finishes, such as `range(1e10)`, is stopped after a few seconds so the page stays responsive.

## Privacy

jq runs in your browser and works offline. Nothing is uploaded. Large numbers such as 64-bit IDs stay exact. **Share** puts the JSON, filter and options in the link after `#`, which is never sent to a server.

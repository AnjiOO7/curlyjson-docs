<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# JSON Diff

[JSON Diff](https://curlyjson.com/json-diff) compares two documents — **Original (A)** and **Modified (B)** — by their **structure**, not as text. You see only real changes.

## What counts as a change

- **Key order never counts.** `{"a":1,"b":2}` equals `{"b":2,"a":1}`.
- **Formatting never counts** — whitespace, indentation, `1.0` vs `1`, `"\u00e9"` vs `"é"`.
- Changes are labelled **Added**, **Removed**, **Changed**, or **Type changed** (for example the number `56.3` becoming the string `"73.80"` — often a bug).

## Matching array items

Choose how arrays are compared with the **Arrays** option:

| Mode | Use it when | Example path |
|---|---|---|
| **Smart** (default) | Most of the time. Finds an id field (`id`, `uuid`, `sku`, `userId`…) and matches items by it, wherever they are. Without one, it lines up unchanged items so a single insertion is a single change. | `$.items[sku="BK-101"].qty` |
| **Match by key…** | You know the id field, e.g. `code`. | `$.rates[code="INR"]` |
| **By position** | Order matters (e.g. steps, rankings). | `$.steps[2]` |
| **Ignore order** | Arrays are sets, like tags. | — |

## Ignoring noisy fields

Type field names into **Ignore fields**, separated by commas. They're ignored at any depth. Wildcards work:

```text
updatedAt, *At, requestId, trace*
```

When a field that looks like a timestamp or request id changes, CurlyJSON suggests it — click **+ ignore updatedAt** to add it.

## Views

- **Changes** — a list with filters (Added / Removed / Changed / Type). Click a path to copy it.
- **Side by side** — both documents normalised (keys sorted, ignored fields hidden, matched items aligned) with unchanged parts folded.
- **JSON Patch** — standard [RFC 6902](https://datatracker.ietf.org/doc/html/rfc6902) operations that turn A into B exactly. Copy or download.
- **✦ Summary** — a short plain-English summary of the changes ([AI features](ai.md)).

## Sharing results

- **Copy report** copies a Markdown table you can paste into Jira, GitHub or Slack.
- **Share** creates a link containing both documents.
- **Swap** exchanges A and B. Drop **two files at once** to fill both sides.

<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# JSON Formatter

The formatter is the [home page](https://curlyjson.com/). Paste JSON on the left; the formatted result appears on the right **as you type**.

## Format and minify

- **Beautify** indents with **2 spaces**, **4 spaces** or **tabs**.
- **Minify** removes all whitespace — useful for configs and API payloads.
- **Sort keys** orders object keys alphabetically at every level, which makes documents easy to compare by eye.

## Validation and errors

When the JSON is invalid you get the **exact line and column** and a plain-English message, for example:

```text
Line 3, column 3: Expected ',' or '}' but found '"'
```

The faulty line is highlighted in the editor. **Jump to the error** moves your cursor there. While the input is invalid, the output keeps showing the last valid result (dimmed).

Common messages:

| Message | Usual cause |
|---|---|
| Trailing comma is not allowed in JSON | `[1, 2,]` or `{"a": 1,}` |
| Keys must use double quotes | `{'a': 1}` or `{a: 1}` |
| Unescaped control character in string | A real line break inside `"…"` — use `\n` |
| Unexpected … after the end of the JSON value | Two documents pasted together, or extra text |

## Repair

**Repair JSON** fixes the most common problems in one click: trailing commas, single quotes, unquoted keys, comments, missing commas or brackets, Python-style `True` / `False` / `None`, and JSON wrapped in other text (like an AI chat reply or a log line).

For harder cases, **✦ AI Fix** can repair JSON the rule-based repair can't — see [AI features](ai.md). Always review AI-fixed output.

## Tree view

Switch the output to **Tree** to explore large documents:

- The first two levels open automatically; deeper levels load when you expand them, so even very large files stay fast.
- Hover any row and click its path to **copy a JSONPath**, such as `$.orders[0].customer.email`.
- **Expand all** / **Collapse** buttons are at the top right.

## Table view

**Table** shows a list of records as rows and columns, like a spreadsheet:

- It opens at the biggest list in your JSON (for example `$ › users`); the path at the top takes you back up.
- Every field becomes a column. Missing fields show `—`.
- Click a column header to sort (again for descending, a third time for the original order). Numbers sort as numbers.
- Nested objects and arrays show as chips like `{3 keys}` or `[2 items]`: click one to open it as its own table. Click a row number or key to open that whole record.
- Click any value to copy its path, such as `$.users[42].email`.
- Only the rows on screen are drawn, so lists of millions of items scroll smoothly.

## Graph view

**Graph** draws your JSON as connected cards: one card per object or array, linked to the cards of the values inside it.

- The first few levels open automatically. Click a row with `{…}` or `[…]` to open or close its branch.
- Long lists show 12 rows at first; **+ more** shows the next 25.
- **Drag** to move around, **Ctrl + scroll** (or pinch) to zoom; with the graph focused, arrow keys move and `+` / `-` / `0` zoom and fit.
- The buttons at the bottom right zoom, show the actual size, **Fit** everything on screen, or go **full screen**.
- Click a value or a card's title to copy its path.

## Big numbers

Most online formatters run your JSON through JavaScript's `JSON.parse`, which **silently rounds integers above 9,007,199,254,740,991**. CurlyJSON uses its own parser and keeps every number exactly as written — safe for 64-bit IDs, snowflake IDs and financial values. It also keeps your number formatting (`1.50` stays `1.50`).

## Files and sharing

- **Open file** or drag a `.json` file onto the input (up to 100 MB; 50 MB opens in about 3 seconds).
- **Copy** and **Download** save the formatted output.
- **Share** copies a link containing your JSON (see [Privacy](privacy.md)).

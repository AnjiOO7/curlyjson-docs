<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# CSV & Excel

Four converters share one engine: [JSON → CSV](https://curlyjson.com/json-to-csv), [JSON → Excel](https://curlyjson.com/json-to-excel), [CSV → JSON](https://curlyjson.com/csv-to-json) and [Excel → JSON](https://curlyjson.com/excel-to-json).

## JSON → CSV / Excel

**Finding the rows.** If your JSON is an API response like `{"page":1,"data":{"users":[…]}}`, CurlyJSON finds the arrays of records inside it. Pick one with **Rows from**.

**Nested objects** become columns with dot names:

| id | customer.name | customer.city |
|---|---|---|
| 1001 | Ada Lovelace | London |

**Arrays** — choose with the **Arrays** option:

| Option | Result for `"tags": ["a","b"]` |
|---|---|
| Join values in one cell | `a; b` |
| Keep as JSON text | `["a","b"]` |
| One column per item | `tags.0` = a, `tags.1` = b |

**One row per item** turns each item of an array (like `items` in an order) into its own row, repeating the parent fields — ideal for pivot tables.

**CSV options**

- **Delimiter:** comma, semicolon (common in Europe), tab, or pipe.
- **Excel-friendly** (on by default) adds a UTF-8 marker so names like *José* and symbols like ₹ display correctly in Excel.
- **Formula protection** (on by default) prefixes cells starting with `=`, `+`, `-` or `@` with an apostrophe, so spreadsheets don't run them as formulas.

**Excel output** is a real `.xlsx` workbook: bold, frozen header row, sized columns, numbers stored as numbers. Numbers longer than 15 digits are written as text so Excel can't round them.

**Copy for Sheets** copies the table so you can paste it straight into Excel or Google Sheets.

## CSV / Excel → JSON

- **First row is header** — column names become keys. Blank or duplicate names get `column_3`, `name_2`.
- **Detect numbers & booleans** — `42` becomes a number, `TRUE` becomes `true`. Values with **leading zeros** (`007`), numbers longer than 15 digits, and columns named like **phone, mobile, zip, pincode, postcode, account, card, IBAN, IFSC, PAN, GST, code** always stay text.
- **Nest "a.b" columns** — `address.city` becomes `{"address": {"city": …}}`; `tags.0`, `tags.1` become an array.
- **Empty cells** — `null`, `""`, or leave the field out.
- **Output** — array of objects, JSON Lines, or array of arrays.

**Excel files:** open a `.xlsx` file and choose the **sheet**. Dates become ISO strings (`2026-03-14`, or a full timestamp when there's a time). Older `.xls` and Numbers files: save as `.xlsx` or CSV first.

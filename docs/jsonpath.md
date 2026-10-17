<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# JSONPath

The [JSONPath Playground](https://curlyjson.com/jsonpath) runs a query against your JSON and shows every match as you type. It follows **RFC 9535**, the IETF standard for JSONPath.

Paste JSON on the left, type a query at the top. Switch the result between **Values** (a JSON array of matches) and **Paths** (where each match lives). Click a path to copy it.

## Cheat sheet

The examples use the playground's **Sample** document — a store with four books and a bicycle.

| Syntax | Meaning | Example |
|---|---|---|
| `$` | The root of the document | `$` |
| `.name` / `['name']` | A member of an object | `$.store.bicycle`, `$['store']` |
| `*` | Every member or array item | `$.store.book[*].author` |
| `..` | Recursive descent: this level and everything below | `$..price` |
| `[n]` | Array item; negative counts from the end | `$.store.book[0]`, `$.store.book[-1]` |
| `[start:end:step]` | Slice, like Python | `$.store.book[:2]`, `$.store.book[::-1]` |
| `[a,b]` | Several selectors at once | `$.store.book[0,2]`, `$['store']['bicycle','book']` |
| `[?…]` | Filter items with a condition; `@` is the current item | `$.store.book[?@.price < 10]` |

You can leave out the leading `$`: `store.book[0]` works too.

## Filters

| Filter | Keeps items where… |
|---|---|
| `[?@.isbn]` | `isbn` exists |
| `[?!@.isbn]` | `isbn` does not exist |
| `[?@.price < 10]` | price is below 10 (`==` `!=` `<` `<=` `>` `>=`) |
| `[?@.category == 'fiction']` | a string matches exactly (single or double quotes) |
| `[?@.price > 10 && @.price < 20]` | both conditions hold (`\|\|` for either, `!( … )` for not) |
| `[?@.price < $.store.bicycle.price]` | compared with another value in the document |
| `[?(@.price < 10)]` | the older parenthesised form also works |

Comparisons follow the standard: numbers compare as numbers, strings by character, and `<` `>` only apply to two numbers or two strings. A missing field equals nothing except another missing field.

## Functions

| Function | Returns | Example |
|---|---|---|
| `length(v)` | Characters in a string, items in an array, or members of an object | `$..book[?length(@.title) > 15]` |
| `count(q)` | How many nodes a query matches | `$.store[?count(@.*) == 2]` |
| `match(v, 're')` | `true` if the **whole** string matches the regex | `$..book[?match(@.author, 'J.*')]` |
| `search(v, 're')` | `true` if the string **contains** a match | `$..book[?search(@.title, 'Dick')]` |
| `value(q)` | The single value a query matches | `$..book[?value(@..isbn) == '0-553-21311-3']` |

## Differences from older JSONPath tools

Many older libraries (Goessner's original, `jsonpath-plus`, Jayway) accept extra syntax that isn't in the standard:

- **Script expressions** like `$.items[(@.length-1)]` aren't run — they can execute code. Use `$.items[-1]`.
- **`.length`** is not a property; use `length(@.items)` in a filter.
- **Regex with `=~`** — use `match()` or `search()`.
- **Array or object literals** in filters (`@.tags == ['a']`) aren't allowed. Compare against a query instead.

When something isn't valid, the playground says what's wrong and at which column.

## Results and sharing

- **Copy** in Values copies all matches as a JSON array. In Paths it copies them as RFC normalized paths like `$['store']['book'][2]['title']`, one per line.
- Large results show the first 5,000 values (or 1,000 paths); **Copy** and **Download** always include everything.
- **Share** creates a link with the JSON and the query after the `#` — never sent to a server.
- Your last document and query are remembered in your browser. **Clear** removes them.

<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# Browser extension

The **CurlyJSON extension** formats JSON right in the browser tab: open an API URL and read the response as a tree instead of one long line of text.

**[Add to Chrome — free](https://chromewebstore.google.com/detail/cdmifjhednliaikgklceaoifkpcjdonj)** · works in Chrome, Edge, Brave and other Chromium browsers. In Edge, allow extensions from other stores when it asks.

## Format a page

Open a page that shows JSON, click the **CurlyJSON** icon in the toolbar, then **Format this page**.

To format JSON pages as they open, turn on **Format JSON pages automatically** in the same popup. The browser asks for permission to read pages first; the extension only changes pages whose content is JSON.

## Three views

- **Tree** — collapsible, with item counts. Long lists show 500 items at a time, with **Show more**.
- **Formatted** — indented JSON with colours.
- **Raw** — the text exactly as the server sent it.

Switch with the tabs, or press **1**, **2** or **3**. **Expand all** and **Collapse** work on the tree.

## Search

Press **/** (or **Ctrl+F** / **⌘F**) and type. Search finds keys and values anywhere, even inside collapsed branches, opens the levels down to each match and shows "1 of 12". **Enter** goes to the next match, **Shift+Enter** to the previous one, **Esc** clears it. Press Ctrl+F again in the search box for the browser's own find.

## Copy, links and saving

- Hover a row and click its **path** (like `$.items[2].price`) to copy it, or **copy** to copy the value.
- URLs in your data are links.
- **Copy** copies the formatted JSON; **Save** downloads it as a file named after the page (for example `users.json`).
- Big numbers stay exact: `12345678901234567890` is never rounded.

## Big files

A 10 MB response opens in about a second, and files up to 50 MB work. Only the rows you can see are drawn, so scrolling stays smooth.

## Secrets

If the JSON contains likely API keys, tokens or passwords, a yellow **⚠ 3 secrets · Hide** button appears. Click it to mask them in every view (`sk_live_••••••`), and again to show them. See [Hiding secrets](secrets.md) for what's detected.

## Open in CurlyJSON

**Open in CurlyJSON** opens the data in the full website tools (diff, jq, JSON Schema, converters). The data travels after the `#` in the link, which browsers never send to a server. If it contains secrets, the extension asks first and offers **Hide and open**. Very large documents are copied to your clipboard instead, to paste on the site.

## Also handled

- JSON served as `text/plain`, and **NDJSON / JSON Lines** (one value per line, shown as a list)
- Pages with strict Content Security Policies
- Invalid JSON: a banner says what's wrong, and the Raw view marks the position
- Light and dark themes follow your system setting

## Privacy

The extension has **no tracking, no analytics and makes no network requests**. Your JSON never leaves the browser. It needs no website access to install; automatic formatting asks for it only when you turn it on. Details: [privacy policy](https://curlyjson.com/privacy#extension).

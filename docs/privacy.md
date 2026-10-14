<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# Privacy & security

**Short version: the data you paste never leaves your device.**

## Processing

Formatting, validation, repair, diffing, code generation and CSV/Excel conversion all run **in your browser**. There is no server that receives your input. This makes CurlyJSON safe for API keys, tokens, customer data and internal configs.

## What's stored

- Your **last input and settings** for each tool are kept in your browser's local storage, so they're there when you return. **Clear** removes the input; clearing your browser data removes everything.
- Nothing is stored on our side.

## Share links

A share link contains a **compressed copy of your data after the `#`** in the URL. Browsers never send that part to any server, so we never see it — but **anyone you send the link to can read the data**. Don't share links containing secrets.

## AI

On-device AI (desktop Chrome) runs locally — see [AI features](ai.md).

## Analytics

We use **Cloudflare Web Analytics**, which counts page views **without cookies** and without tracking you across sites. It never sees what you paste.

## Security

- The site is served over HTTPS only, with a strict Content Security Policy.
- Spreadsheet exports include **formula protection** by default.

See also the [privacy policy](https://curlyjson.com/privacy).

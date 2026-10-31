<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# Privacy & security

**Short version: the data you paste stays on your device. The only exception is optional Pro cloud AI, which asks for your permission before sending anything.**

## Processing

Formatting, validation, repair, diffing, code generation and CSV/Excel conversion all run **in your browser**. These tools have no server that receives your input. This makes CurlyJSON safe for API keys, tokens, customer data and internal configs.

## What's stored

- Your **last input and settings** for each tool are kept in your browser's local storage, so they're there when you return. **Clear** removes the input; clearing your browser data removes everything.
- Nothing is stored on our side.

## Works offline

After your first visit, your browser keeps a copy of the site's own files, so **every free tool works with no internet connection** (Pro cloud AI needs one). That's also the easiest way to check our privacy promise: turn off Wi-Fi, reload, and keep working. Nothing you paste is sent anywhere unless you approve a Pro cloud AI request.

The copy contains only our pages, scripts and styles — never your data. It updates itself when we release a new version, and is skipped when your browser's Data Saver is on. Chrome and Edge also offer **Install app**, which opens CurlyJSON in its own window.

## Secrets

CurlyJSON spots API keys, tokens, passwords and private keys in what you paste. The Formatter offers to mask them, and every **Share** button warns before putting them in a link. See [Hiding secrets](secrets.md).

## Share links

A share link contains a **compressed copy of your data after the `#`** in the URL. Browsers never send that part to any server, so we never see it — but **anyone you send the link to can read the data**. Don't share links containing secrets.

## AI

On-device AI (desktop Chrome) runs locally — see [AI features](ai.md).

AI is part of Pro. In browsers without on-device AI, Pro uses optional cloud AI for browsers without on-device AI. It asks for your permission first and sends only the part of your JSON the AI reads. Details: [privacy policy](https://curlyjson.com/privacy#cloud-ai).

## Analytics

We use **Cloudflare Web Analytics**, which counts page views **without cookies** and without tracking you across sites. It never sees what you paste.

We also keep **anonymous usage counts** — which tool buttons are used (e.g. *Copy* on JSON to CSV) and the visitor's country — so we know which features matter. They never include your data, your IP address, or any identifier.

## Security

- The site is served over HTTPS only, with a strict Content Security Policy.
- Spreadsheet exports include **formula protection** by default.

See also the [privacy policy](https://curlyjson.com/privacy).

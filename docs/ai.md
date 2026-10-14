<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# AI features

CurlyJSON includes three AI helpers:

- **✦ Explain** (Formatter) — a short plain-English description of what your JSON represents and its important fields.
- **✦ AI Fix** (Formatter) — repairs JSON that the normal **Repair** can't.
- **✦ Summary** (JSON Diff) — 3–5 bullets summarising the differences.

## Free, private, on your device

In **desktop Chrome** (version 138 or later), these use **Chrome's built-in AI model**, which runs **on your computer**. It's free, unlimited, and **your JSON never leaves your device**.

The first time you use it, Chrome may download its model (a few gigabytes, managed by Chrome). After that it starts in a few seconds.

**Requirements** (set by Chrome): Windows 10/11, macOS 13+, Linux or a Chromebook Plus; about 22 GB of free disk space; and a graphics card with more than 4 GB of memory, or 16 GB of RAM. Phones and other browsers don't have on-device AI yet.

## Good to know

- Large documents are **shortened** before the AI sees them (the first few items of each array; long strings cut), so answers stay fast.
- The on-device model is small: it's great for quick explanations but can miss details. The Changes list in JSON Diff is always complete.
- Always review **AI Fix** results — they are checked to be valid JSON, but the AI may guess at missing values.

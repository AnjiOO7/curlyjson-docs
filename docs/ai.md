<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# AI features

CurlyJSON includes three AI helpers:

- **✦ Explain** (Formatter) — a short plain-English description of what your JSON represents and its important fields.
- **✦ AI Fix** (Formatter) — repairs JSON that the normal **Repair** can't.
- **✦ Summary** (JSON Diff) — 3–5 bullets summarising the differences.

## Part of Pro: private, on your device

The AI helpers are part of [Pro](https://curlyjson.com/pro). **Repair** (without AI) and every other tool stay free.

In **desktop Chrome** (version 138 or later), they use **Chrome's built-in AI model**, which runs **on your computer**: on-device requests aren't counted, **your JSON never leaves your device**, and it works offline as long as this browser's license was confirmed valid at its last check.

The first time you use it, Chrome may download its model (a few gigabytes, managed by Chrome). After that it starts in a few seconds.

**Requirements** (set by Chrome): Windows 10/11, macOS 13+, Linux or a Chromebook Plus; about 22 GB of free disk space; and a graphics card with more than 4 GB of memory, or 16 GB of RAM. Phones and other browsers don't have on-device AI yet.

## Good to know

- Large documents are **shortened** before the AI sees them (the first few items of each array; long strings cut), so answers stay fast.
- The on-device model is small: it's great for quick explanations but can miss details. The Changes list in JSON Diff is always complete.
- **AI Fix** first tries a repair in your browser and only uses AI when that would change your data. It then sends only the broken part when it can. Answers that drop, change or add values are never applied, and a fix that moves data to a different place is shown for review first. Always check the result.
- **Explain** gets exact counts, types and ranges worked out from your whole document, and its answer is checked against them: if it names a field that doesn't exist or a count that doesn't match, you'll see a note under the answer.

## Pro cloud AI

In browsers without on-device AI, **Pro** runs the same three helpers (Safari, Firefox, phones), using a larger model on Cloudflare Workers AI. It asks before sending anything and sends only the part the AI reads ([privacy policy](https://curlyjson.com/privacy#cloud-ai)).

- Up to 50 requests a day per license, resetting at 00:00 UTC; large AI Fix requests use up the allowance faster. Cloud AI runs on a daily capacity shared by all subscribers, so on a busy day it can run out earlier; it comes back at 00:00 UTC.
- AI Fix rewrites at most 6,000 characters around an error at a time; larger errors need a manual fix.

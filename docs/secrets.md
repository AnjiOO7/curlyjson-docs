<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# Hiding secrets

JSON often carries things that should never be shared: API keys, access tokens, passwords. CurlyJSON looks for them **in your browser** and helps you keep them out of copies and share links.

## In the Formatter

When your input contains secrets, a yellow **⚠ 2 secrets · Hide** button appears next to the **Valid** badge. Press it to mask them in place:

```json
{ "stripe": "sk_live_51H8x…", "password": "hunter2" }
```

becomes

```json
{ "stripe": "sk_live_••••••", "password": "••••••••" }
```

Only the secret characters change — your formatting and comments stay as they were, and the JSON stays valid. **Undo** puts the original back.

## Before you share

**Share** on the Formatter, JSON Diff, JSONPath, jq Playground and JSON Schema Validator checks the data first. If it finds secrets, it lists them by line and offers:

- **Hide and share** — mask them, then copy the link
- **Share anyway** — copy the link as it is
- **Cancel**

## What it looks for

| Kind | Examples |
|---|---|
| API keys | Stripe `sk_live_…` / `rk_…`, AWS `AKIA…`, OpenAI `sk-…`, Anthropic `sk-ant-…`, Google `AIza…` |
| Tokens | GitHub `ghp_…`, Slack `xoxb-…`, JWTs (`eyJ…`), `Bearer …` headers |
| Passwords | fields named `password`, `passwd`, `pwd` or ending in one (`admin_password`, `smtpPassword`); the password in URLs like `postgres://user:pass@host`; `Basic` auth headers |
| Secrets | fields named `secret`, `client_secret`, `apiKey`, `x-api-key`, `authorization`, `credentials`, or ending in `secret`, `api_key`, `access_key`, `private_key`, `token` (`stripe_api_key`, `aws_secret_access_key`, `npm_token`) |
| Keys | fields named `key` or ending in it (`stripe_key`, `hmacKey`) when the value looks generated: 20+ characters, letters and digits, high randomness |
| Private keys | `-----BEGIN … PRIVATE KEY-----` blocks |
| Card numbers | numbers that pass the card checksum, under a card field or written in groups of four |

Field names match in any style — `api_key`, `apiKey`, `API-KEY`, `api.key` and `api_key_v2` are the same. It also checks arrays (`"api_keys": ["…", "…"]`), JavaScript-style objects (`apiKey: '…'`) and secrets written inside text (`"note": "password: '…'"`).

To avoid false alarms it leaves these alone:
- names that only look secret: `password_hint`, `secret_name`, `token_type`, `api_version`, `key_id`, `public_key`, `primary_key`, `cache_key`
- numbers (`max_tokens: 4096`), `true`/`false`, and placeholders (`<your-api-key>`, `${API_KEY}`, `REPLACE_ME`, `example…`, `****`)
- under `key`: UUIDs, hashes (MD5, SHA-1, SHA-256), file paths, URLs and dotted names like `checkout.button.pay`
- public keys such as Stripe's `pk_live_…`, and published test card numbers like `4242 4242 4242 4242`
- package names and versions (`"@azure/keyvault-secrets": "^4.9.0"`), and letters-only names like `"PROXY_SECRET": "X-Proxy-Secret"`

The rules follow the approach of open-source scanners like gitleaks and detect-secrets, and are tested against more than 160 labelled examples and hundreds of real-world JSON files.

It can't recognise every secret. A random string in a field called `notes` won't be found, so look before you share.

## Privacy

The check runs entirely in your browser; nothing is sent anywhere. Inputs over 2 MB are checked when you press Share rather than as you type.

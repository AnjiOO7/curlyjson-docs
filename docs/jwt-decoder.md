<sub>[Docs home](index.md) · [Open CurlyJSON](https://curlyjson.com) · [Report an issue](https://github.com/AnjiOO7/curlyjson-docs/issues/new/choose)</sub>

# JWT Decoder

[JWT Decoder](https://curlyjson.com/jwt-decoder) reads a JSON Web Token and checks its signature — entirely in your browser.

## Decoding

Paste a token into **Encoded token**. It is coloured by part: <span class="jwt-h">header</span>.<span class="jwt-p">payload</span>.<span class="jwt-s">signature</span>.

- You can paste a whole `Authorization: Bearer eyJ…` header, with quotes or line breaks — it's cleaned up for you.
- The bar at the top says whether the token is **Expired**, **Not valid yet**, or **Not expired**, using `exp` and `nbf`.
- **Claims** lists every payload field. Times (`exp`, `iat`, `nbf`, `auth_time`) are shown as dates in your time zone, with "in 3 hours" / "2 days ago". Switch to **JSON** to see the raw payload.

> Decoding is not verification. Anyone can read a JWT. Only a valid signature proves who issued it.

## Verifying the signature

Paste the key into **Verify signature**. The token's `alg` decides which key you need:

| `alg` | Key to paste |
|---|---|
| `HS256` `HS384` `HS512` | The shared secret. Tick **Secret is base64** if your secret is stored base64-encoded. |
| `RS256/384/512`, `PS256/384/512` | RSA public key |
| `ES256` `ES384` `ES512` | EC public key (P-256 / P-384 / P-521) |
| `EdDSA` | Ed25519 public key |

Public keys can be:

- **PEM** — `-----BEGIN PUBLIC KEY-----…`
- **JWK** — a single key object `{"kty":"RSA","n":"…","e":"AQAB"}`
- **JWKS** — the whole `{"keys":[…]}` document from your provider's `/.well-known/jwks.json`. The key is picked by the token's `kid`.

Private keys are refused on purpose — you never need one to verify.

Other formats: for a certificate, run `openssl x509 -pubkey -noout -in cert.pem`; for a `BEGIN RSA PUBLIC KEY` (PKCS#1) key, run `openssl rsa -RSAPublicKey_in -in key.pem -pubout`.

## Warnings

CurlyJSON flags common mistakes:

- `alg: "none"` — an unsigned token. Servers must reject it.
- No `exp` — the token never expires.
- `exp` in milliseconds instead of seconds.
- Time claims stored as strings.
- HMAC secrets shorter than the hash size (for example under 32 bytes for HS256).

## Privacy

Tokens are processed with your browser's Web Crypto API. Unlike the other tools, the JWT Decoder **doesn't remember your input** — tokens are credentials, so nothing is saved, even in your browser. Encrypted tokens (JWE, five parts) can't be decoded without the private key.

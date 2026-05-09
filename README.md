# castoff.cc

Static site for [Castoff](https://github.com/kerim/annals), an iOS podcast player for sequential listening.

Hosts:
- The landing page (`index.html`)
- The Universal Links AASA file at `/.well-known/apple-app-site-association`
- The arc-share fallback page (`arc.html`) for users who tap a Castoff arc link without the app installed

## Deploy

GitHub Pages serves this repo at <https://castoff.cc>. The `CNAME` file pins the custom domain.

DNS chain: registrar (easyDNS) → Cloudflare (DNS + proxy) → GitHub Pages.

## Cloudflare settings that matter

- SSL/TLS mode: **Full (Strict)** — GitHub Pages terminates TLS itself.
- No redirect rules touching `/.well-known/*` — Apple does not follow redirects on AASA.
- Rocket Loader and Auto Minify off (or scoped away from `/.well-known/*`) — they can corrupt the JSON.

## Verify AASA

```sh
curl -v https://castoff.cc/.well-known/apple-app-site-association
```

Should return `HTTP/2 200`, `content-type: application/json`, and the body verbatim.

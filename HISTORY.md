# Project History

## 2026-06-20 — Landing page live on Railway + custom domain
- **Branch:** main
- **Progress:**
  - Built single-file static landing page (`index.html`), served via Caddy/Docker on Railway, auto-deploys on push to `main`.
  - Final layout: black hero (portrait → KYLE MOGGED wordmark → signature → "The Zen Wizard") then a purple `.contact-panel` (Get in touch → email pill → footer).
  - DNS pointed for `kylemogged.com` (Porkbun ALIAS apex + www CNAME + railway-verify TXTs); apex cert VALID. Also patched `trailer.club` missing www CNAME.
- **Decisions:** public repo; Caddy static server; apex via Porkbun ALIAS; kept MX/SPF for email forwarding; signature cropped in CSS (not the asset).
- **Next:** confirm `www` SSL certs issued for `www.kylemogged.com` + `www.trailer.club`; optional copy/visual tweaks.
- **Detail:** .context/kylemogged/compact.md

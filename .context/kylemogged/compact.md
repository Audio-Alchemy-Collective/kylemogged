# Kyle Mogged — Compaction Log

---

## Session 2026-06-20 — Build landing page + Railway deploy + DNS

### Session Info
- **Date:** 2026-06-20
- **Branch:** `main` (repo: `Audio-Alchemy-Collective/kylemogged`, public)
- **Task:** Create a landing page for Kyle Mogged, deploy via Railway from GitHub, point `kylemogged.com` DNS (Porkbun). Also fixed `trailer.club` www DNS along the way.
- **HEAD:** `695186d`

### Files Modified This Session
- `index.html` — the entire landing page (single static file, no build step)
- `Caddyfile` — static server config: `:{$PORT:80}` root `/srv`, file_server, gzip
- `Dockerfile` — `caddy:2-alpine`, copies Caddyfile + index.html + Media into `/srv`
- `README.md` — preview/deploy notes
- `.gitignore` — `.DS_Store`, `node_modules`, `*.log`
- `Media/` — pre-existing assets (NOT created this session):
  - `Kyle_M_30_Profile_Picture_Transparent.PNG` (portrait, transparent)
  - `Kyle_M_31_Signature_Black.PNG` (2000×2000, black ink on white; ink bbox ≈ left 10.5%/right 89.4%/top 18%/bottom 82%)

### Progress (all complete)
1. ✅ GitHub repo created under `Audio-Alchemy-Collective` (public), Pages enabled at audio-alchemy-collective.github.io/kylemogged (legacy, still works but Railway is the canonical host now)
2. ✅ Landing page built — Poiret One wordmark (same font as Trailer Club's display face), black/gold/purple palette
3. ✅ Railway: project `kylemogged` (id `41d549e8-90cc-48fe-a14c-ae0a27f977b9`) in **Audio Alchemy** workspace (id `77dca5cb-772e-40f1-8520-5123ac0ceddf`); service `kylemogged-web` (id `ecadb8a8-6349-4946-abcc-467dda84c000`); env `production` (id `0a637ed0-9e91-447d-9668-12f523e7d837`). Auto-deploys on push to `main`.
4. ✅ DNS (Porkbun) for kylemogged.com: ALIAS @ → `i4utx0bc.up.railway.app`; CNAME www → `87hdka18.up.railway.app`; TXT `_railway-verify` + `_railway-verify.www`. Apex cert VALID. www was waiting on TTL cache last checked.
5. ✅ trailer.club fix: added CNAME www → `3wbplfjf.up.railway.app` + TXT `_railway-verify.www` on trailer.club's service (project `f0877402-b36e-437b-abdf-7c6c01172f63`, service `2a669a85-becc-4162-aa90-6b522f690da2`, env `1d1dcc1e-c267-459f-ab8f-e6a19b3d8d52`). Apex cert VALID.

### Layout evolution (final state in index.html)
Final stacking order, top→bottom:
- **Black hero section** (`.stage`): portrait → gold `.deco-rule` → `.wordmark` "Kyle Mogged" (gold gradient, Poiret One) → `.sig-wrap`/`.signature` (cropped to ink bounds via `aspect-ratio:1000/639` + `margin-top:-18%`, inverted + `mix-blend-mode:screen` to drop white bg) → `.title` "The Zen Wizard" (purple→gold gradient)
- **Purple section** (`.contact-panel`, starts at "Get in touch"): radial purple glow + `linear-gradient(#1c1233→#150d27)`; holds `.contact` (h2 "Get in touch" + `.email` pill `kyle@kylemogged.com`, dark bg + gold border) and `<footer>` "Audio Alchemy Collective" (margin-top:auto, sits at bottom)

### Key Decisions
- Static site served by **Caddy in Docker** (Railway needs a server for a no-framework static site; Caddy reads `$PORT`).
- Repo **public** (landing page; differs from sibling private `trailer-club` app repo).
- Apex on Porkbun uses **ALIAS** (CNAME flattening) since CNAME can't sit on bare apex.
- Kept Porkbun **MX (fwd1/fwd2) + SPF TXT** — they run `kyle@kylemogged.com` email forwarding. Deleted only the wildcard `CNAME *` parking record.
- Signature cropped via wrapper (PNG had ~18% empty top/bottom) rather than editing the asset.

### Open Issues / Follow-ups
- **www certs**: `www.kylemogged.com` was still showing cached `uixie.porkbun.com` (600s TTL) at last check — should be green now; verify. `www.trailer.club` cert was VALIDATING pending the user deleting the `*.trailer.club` wildcard (apex already VALID). Re-check `domain_status` for both `www` hosts to confirm certs issued.
- Optional: footer text "Audio Alchemy Collective" is easy to change/remove if desired.

### Resume Prompt
```
Resume work on the Kyle Mogged landing page (repo Audio-Alchemy-Collective/kylemogged, branch main).

Restore context:
1. .context/kylemogged/compact.md — full session state
2. HISTORY.md — distilled trail
3. index.html — the whole page (single static file)

Likely next: verify www SSL certs issued for www.kylemogged.com and www.trailer.club
(Railway MCP domain_status), or further visual tweaks to index.html.
Railway auto-deploys on push to main; preview locally with `python3 -m http.server`.
```

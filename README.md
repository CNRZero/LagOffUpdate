# LagOff-Updates

Public update manifest repository for LagOff automatic updates.

**This repository does NOT contain LagOff source code or private signing keys.**

## Files

| File | Purpose |
|------|---------|
| `update.json` | Signed update manifest (publish after release asset exists) |
| `update.json.sig` | Detached RSA-SHA256 signature of exact `update.json` bytes |
| `public-update-signing-key.pem` | Public verification key (also embedded in LagOff) |
| `README.md` | This file |

Large builds are **GitHub Release assets only** — never commit ZIP files here.

## GitHub Pages

Enable Pages for this repo: **Settings → Pages → Deploy from branch `main` / root**.

Manifest URL: `https://gaminggodpetsandgoodgames.github.io/LagOff-Updates/update.json`

## Publishing order (required)

1. Build and test the new LagOff version
2. Create the update ZIP (`build-update-package.ps1`)
3. Calculate ZIP SHA-256 (`scripts\compute-sha256.ps1`)
4. Create GitHub Release (draft)
5. Upload `LagOff-x.x.x-win-x64.zip` as release asset
6. **Publish** the GitHub Release
7. Copy direct asset URL into `update.json`
8. Sign manifest: `scripts\sign-update-manifest.ps1`
9. Commit & push `update.json` + `update.json.sig` to this repo
10. LagOff installations detect the update

**Never publish the manifest before the downloadable package exists.**

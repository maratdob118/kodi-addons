# BigPing Kodi repository

Generated tree. Do not edit by hand: every file here is produced by
`scripts/generate_repo.py` in [maratdob118/kodi-advanced-proxy](https://github.com/maratdob118/kodi-advanced-proxy)
and overwritten on the next run.

This repository stays text-only in Git. Add-on ZIPs are never committed; they
are published as a GitHub Pages deployment, because the universal Advanced
Proxy ZIP is far larger than GitHub's 100 MB blob limit.

## Contents

| File | Role |
| --- | --- |
| `addons.xml` | index of every add-on version this repository offers |
| `addons.xml.md5` | md5 of `addons.xml`; Kodi polls it to detect changes |
| `manifest.json` | which Release asset Pages downloads, its SHA256, and where it is published |
| `repository.bigping/addon.xml` | metadata Pages packs into the repository add-on ZIP |

## Publishing (what the Pages workflow must do)

`manifest.json` is the whole contract. For each entry under `addons`:

- `origin: release-asset` — download `url`, recompute its SHA256 and size,
  compare them against the recorded `sha256`/`size`, and abort the deployment on
  any mismatch. Those values are expectations measured on the build artifact
  staged for the release upload, not properties verified against the remote
  asset; `release.tag` pins which release the bytes must come from.
- `origin: build` — pack `metadata` into a ZIP whose single top-level directory
  is `zip_root`. Kodi rejects an add-on ZIP with any other root.
- Publish every ZIP at `path` and write its lowercase hex digest to
  `sha256_path`. Kodi reads a `content-sha256` response header first and falls
  back to that `<zip>.sha256` sidecar; Pages cannot set response headers, so the
  sidecar is the only mechanism available and is mandatory.
- Extract every `art` entry from the payload ZIP at `source` and publish it at
  `path`, so the icon and fanart that `addons.xml` resolves actually exist.

## Offered add-ons

| Add-on | Version | Published path |
| --- | --- | --- |
| `repository.bigping` | 1.0.0 | `repository.bigping/repository.bigping-1.0.0.zip` |
| `service.advancedproxy` | 0.3.0 | `service.advancedproxy/service.advancedproxy-0.3.0.zip` |

## Installing

1. Download `repository.bigping/repository.bigping-1.0.0.zip` from https://maratdob118.github.io/kodi-addons/
2. In Kodi: **Add-ons -> Install from zip file**, pick that ZIP.
3. **Add-ons -> Install from repository -> BigPing -> Services -> Advanced Proxy**.

Kodi 20 (Nexus) or newer is required. Updates arrive automatically once the
repository add-on is installed; Kodi re-reads https://maratdob118.github.io/kodi-addons/addons.xml.

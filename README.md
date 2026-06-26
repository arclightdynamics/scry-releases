# Scry — Releases

Official installer downloads for **[Scry](https://enterscry.com)**, part of the
**Arc Net** suite by Arclight Dynamics.

> This repo hosts the **built installers only** — Scry's source is private and
> proprietary (see [LICENSE](./LICENSE)). Extensions are open-source in
> [`scry-extensions`](https://github.com/arclightdynamics/scry-extensions).

## Download

**[⬇ Download Scry 1.0.0 for Windows](https://github.com/arclightdynamics/scry-releases/raw/main/Scry_1.0.0_x64-setup.exe)**
— `Scry_1.0.0_x64-setup.exe` (9.2 MB, NSIS installer)

SHA-256: `9996b45334dac91d92e452c66f0bc76c8f29dbf0591b55d213cd84b2fe2ef4de`
(see [`SHA256SUMS.txt`](./SHA256SUMS.txt))

> The installer is hosted in-repo for now; it will move to **tagged GitHub
> Releases** (with release notes + an auto-update feed) before wide launch.

### Heads-up: unsigned beta
Scry isn't code-signed yet, so Windows SmartScreen shows an *"unknown publisher"*
warning. To install: **More info → Run anyway**. (Authenticode signing is planned;
it'll remove the warning.)

### After installing
Scry requires an **Arc Net account** — on first launch you'll sign in (your
account works across every Arclight Dynamics product). Sign-in opens in your
browser and returns to the app automatically.

## Releasing (maintainers)

The app is built from the private `arclightdynamics/scry` repo; only the
resulting installer is published here.

1. In `scry`, cut a clean build: `npm run tauri build`
   → produces `src-tauri/target/release/bundle/nsis/Scry_<version>_x64-setup.exe`.
2. Create a release here tagged `v<version>` (e.g. `v1.0.0`) and upload that
   `.exe` as a release asset:
   ```sh
   gh release create v1.0.0 \
     "/path/Scry_1.0.0_x64-setup.exe" \
     -R arclightdynamics/scry-releases \
     -t "Scry 1.0.0" -n "Release notes…"
   ```
3. Point the website's Download button at `releases/latest`.

## Auto-update

Auto-update **is enabled**: installed copies fetch [`latest.json`](./latest.json)
on launch and offer to self-update (signature-verified, then relaunch). To ship a
new version:

1. In `scry`: bump the version, then build signed —
   `TAURI_SIGNING_PRIVATE_KEY="$(cat ~/.scry-keys/updater.key)" npm run tauri build`
2. Copy the new `Scry_<ver>_x64-setup.exe` here and update `latest.json`
   (`version`, `pub_date`, `signature` from the new `.exe.sig`, `url`).
3. Commit + push `main`. Installed apps pick it up on next launch.

The update-signing **private key** (`~/.scry-keys/updater.key`) is required for
step 1 and must be kept secret + backed up — lose it and existing installs can no
longer accept updates.

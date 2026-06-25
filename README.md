# Scry — Releases

Official installer downloads for **[Scry](https://enterscry.com)**, part of the
**Arc Net** suite by Arclight Dynamics.

> This repo hosts the **built installers only** — Scry's source is private and
> proprietary (see [LICENSE](./LICENSE)). Extensions are open-source in
> [`scry-extensions`](https://github.com/arclightdynamics/scry-extensions).

## Download

Get the latest installer from the **[Releases page](../../releases/latest)**.

- **Windows:** `Scry_<version>_x64-setup.exe` (NSIS installer)

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

Auto-update is **not wired yet** — users update by downloading a newer installer.
When ready, add the Tauri updater (minisign keypair + `latest.json` endpoint here)
and the app will self-update.

# Aequalyn Packages — security notes

- `aur-cache/` holds prebuilt AUR packages baked into the offline repo; verify
  checksums/signatures when updating.
- `pkgbuilds/` build from source; review PKGBUILDs before building (no `curl | sh`,
  pinned sources with sha256, no network in `package()`).
- Offline installs use `SigLevel = Never` for the bundled repo.
- See `aequalyn/Security.md` and `aequalyn-store` app guidelines for submission rules.

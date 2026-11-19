# aequalyn-pkgs

Package lists, install profiles and PKGBUILDs for Aequalyn.

```
lists/
├── base.packages            the system
├── desktop.packages         Hyprland, Quickshell, matugen, awww, apps
├── hardware.packages        firmware and drivers
├── offline-extra.packages   extra packages bundled in the ISO's offline repo
├── aur.packages             built after install, online, best effort
├── local.packages           prebuilt here, on the live ISO and every install from it
└── profiles/                minimal, student, dev, creative, gaming
aur-cache/                   prebuilt packages baked into the offline repo
pkgbuilds/                   aequalyn-git, aequalyn-shell-git, aequalyn-themes-git,
                             ddwriter, nudu
```

`local.packages` lists packages that are not in the Arch repositories and ship
prebuilt in `aur-cache/`: mpvpaper (live wallpapers, from the AUR),
[DDWriter](https://github.com/nightdevil00/Tools/tree/main/DDWriter) (writes ISO
images to USB drives) and [nudu](https://github.com/qempexe/nudu) (disk usage in
the terminal). The ISO build installs them on the live system from a local
repository, and the installer installs them on the target from the ISO's offline
repository. To update one, build it and replace its file in `aur-cache/`:

```sh
cd pkgbuilds/nudu && makepkg -f && cp nudu-*-x86_64.pkg.tar.zst ../../aur-cache/
```

The installer reads `lists/` (as `packages/` in the assembled tree), so a
change here changes every new install and ISO.

The optional `dev` profile includes programming runtimes and utilities such as
mise, Node.js, npm, Python, uv, Go, Rust, Docker and GitHub CLI. On an existing
installation, add individual packages from the Aequalyn Store.

The PKGBUILDs install the core to `/usr/share/aequalyn` and its commands to
`/usr/bin`, the shell to `/usr/share/aequalyn/shell` and the themes to
`/usr/share/aequalyn/themes`:

```sh
cd pkgbuilds/aequalyn-themes-git && makepkg -si
```

## Credits

[nightdevil00](https://github.com/nightdevil00) contributed to the code here.

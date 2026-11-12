# aequalyn-pkgs

Package lists, install profiles and PKGBUILDs for Aequalyn.

```
lists/
├── base.packages            the system
├── desktop.packages         Hyprland, Quickshell, matugen, awww, apps
├── hardware.packages        firmware and drivers
├── offline-extra.packages   extra packages bundled in the ISO's offline repo
├── aur.packages             built after install, online, best effort
└── profiles/                minimal, student, dev, creative, gaming
aur-cache/                   prebuilt AUR packages baked into the offline repo
pkgbuilds/                   aequalyn-git, aequalyn-shell-git, aequalyn-themes-git
```

The installer reads `lists/` (as `packages/` in the assembled tree), so a
change here changes every new install and ISO.

The PKGBUILDs install the core to `/usr/share/aequalyn` and its commands to
`/usr/bin`, the shell to `/usr/share/aequalyn/shell` and the themes to
`/usr/share/aequalyn/themes`:

```sh
cd pkgbuilds/aequalyn-themes-git && makepkg -si
```

## Credits

[nightdevil00](https://github.com/nightdevil00) contributed to the code here.

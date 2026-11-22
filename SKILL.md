---
name: aequalyn-pkgs
description: Package lists, profiles and PKGBUILDs for Aequalyn.
---

# Aequalyn Packages — skill

## Overview

Package lists, install profiles and PKGBUILDs for Aequalyn. The installer reads `lists/`
(as `packages/` in the assembled tree), and the ISO build bakes `aur-cache/` into the
offline repository.

## Layout

```
lists/        base, desktop, hardware, offline-extra, aur, local, profiles/*
aur-cache/    prebuilt packages baked into the offline repo
pkgbuilds/    aequalyn-git, aequalyn-shell-git, aequalyn-themes-git, ddwriter, nudu
```

## Package lists

- `lists/base.packages` — base system: base/base-devel, linux, firmware, mkinitcpio, sudo, git, polkit; btrfs/cryptsetup/dosfstools/efibootmgr/limine/plymouth/snapper/snap-pac/zram; microcode/sof; NM/iwd/wpa_supplicant/bluez; PipeWire; power profiles.
- `lists/desktop.packages` — Hyprland/QuickShell desktop: compositor + shell (hyprland, quickshell, matugen, awww, polkit-gnome, hyprlock/idle/shutdown); Qt6/GTK runtime; fonts; Bluetooth; screenshot/clipboard tools; browsers (chromium, vivaldi); kitty/foot/fuzzel; btop/fastfetch/mpv; opencode; nautilus + python-gobject; udisks2/gvfs/tumbler.
- `lists/hardware.packages` — conditional by CPU/GPU/wifi/laptop (amd/intel ucode; nvidia-open-dkms; mesa/vulkan; broadcom-wl-dkms; tlp).
- `lists/offline-extra.packages` — extra packages baked into ISO offline repo: firefox, flatpak, tlp, broadcom-wl-dkms, NVIDIA/Mesa driver sets, linux-lts + headers. (`*-dkms` filtered out of live ISO.)
- `lists/aur.packages` — online-only AUR packages, best effort: limine-mkinitcpio-hook, limine-snapper-sync, yay-bin, bibata-cursor-theme, adwaita-qt6, zen/brave/edge browsers, localsend, postman, VS Code. (mpvpaper prebuilt via local.packages.)
- `lists/local.packages` — prebuilt local packages installed on live ISO and every install: mpvpaper, ddwriter, nudu.

## Profiles

- `minimal.packages` — chromium, nautilus, kitty, fuzzel, grim.
- `student.packages` — libreoffice-fresh, obs-studio, xournalpp, calibre, thunderbird.
- `dev.packages` — Development: neovim, git, lazygit, github-cli, nodejs, pnpm, npm, rust, go, python, python-pip, uv, docker, docker-compose, mise, ripgrep, fd, bat, eza, jq.
- `creative.packages` — gimp, inkscape, blender, krita, kdenlive, obs-studio, audacity, darktable.
- `gaming.packages` — steam, gamemode, mangohud, lutris, wine, winetricks, lib32-gamemode, lib32-mangohud, discord.
- `ai.packages` — ollama, llama-cpp, python-pytorch.
- `service.packages` — bitwarden, signal-desktop, tailscale, syncthing, openssh, rsync.
- `editor.packages` — neovim, vim, helix, emacs, micro.
- `style.packages` — nerd fonts: Fira Code, Cascadia Mono, Meslo LG Mono, Iosevka, Bitstream Vera Mono.
- `browser.packages` — chromium, firefox, librewolf, qutebrowser.
- `terminal.packages` — alacritty, foot, ghostty, kitty, wezterm.

## PKGBUILDs

- `pkgbuilds/aequalyn-git/PKGBUILD` — clones `https://github.com/Aequalyn/aequalyn.git` (sha256sums=SKIP); installs bin/config/assets/docs/install.sh/VERSION/README/SKILL to `/usr/share/aequalyn` and copies bin/* to `/usr/bin`; depends on aequalyn-shell, aequalyn-themes, hyprland, quickshell, matugen, awww, jq, imagemagick, ffmpeg, brightnessctl, playerctl, ttf-jetbrains-mono-nerd.
- `pkgbuilds/aequalyn-shell-git/PKGBUILD` — clones aequalyn-shell; installs entire source tree to `/usr/share/aequalyn/shell`, removing `.git`.
- `pkgbuilds/aequalyn-themes-git/PKGBUILD` — clones aequalyn-themes; installs `themes/` to `/usr/share/aequalyn/themes`.
- `pkgbuilds/ddwriter/PKGBUILD` — pinned git commit from nightdevil00/Tools + aequalyn.patch (sha256 pinned); installs ddwriter.py, launcher, icons, desktop entry, license; depends python, tk, util-linux, sudo; makedepends git, imagemagick.
- `pkgbuilds/nudu/PKGBUILD` — pinned tarball from qempexe/nudu v0.2.0 with sha256; cargo fetch/build frozen; installs binary, license, README, desktop entry.

## aur-cache contents

Six prebuilt packages, no signatures (makepkg 7.1.0, "Unknown Packager"):

- ddwriter 1.0.0-1 (any, MIT)
- limine-mkinitcpio-hook 1.40.0-1 (x86_64, GPL3)
- limine-snapper-sync 1.32.1-1 (x86_64, GPL3)
- mpvpaper 1.9-1 (x86_64, GPL3)
- nudu 0.2.0-1 (x86_64, MIT)
- yay-bin 13.1.0-1 (x86_64, GPL-3.0-or-later)

## Update a prebuilt package

```sh
cd pkgbuilds/nudu && makepkg -f && cp nudu-*-x86_64.pkg.tar.zst ../../aur-cache/
```

## Build a theme package

```sh
cd pkgbuilds/aequalyn-themes-git && makepkg -si
```

## Security

See `SECURITY.md`. Key concerns: offline repo `SigLevel = Never`; prebuilt packages without signatures; git-based PKGBUILDs use `sha256sums=SKIP` for aequalyn repos (only ddwriter commit and nudu tarball pinned); ddwriter runs disk writes as root via sudo and skips password prompt when `sudo -n true` succeeds (NOPASSWD risk); ddwriter runs ImageMagick on bundled image; `cp -r` over upstream trees; broad hardware/offline package sets; profiles include many third-party binaries.

## References

- Aequalyn core: https://github.com/Aequalyn/aequalyn
- Aequalyn packages: https://github.com/Aequalyn/aequalyn-pkgs
- Aequalyn installer: https://github.com/Aequalyn/aequalyn-installer
- Aequalyn ISO: https://github.com/Aequalyn/aequalyn-iso

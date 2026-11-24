# Maintainer: qempexe
pkgname=nudu
pkgver=0.2.0
pkgrel=2
pkgdesc="new du: a fast terminal disk usage analyzer with a dashboard view, ownership, filesystem-aware sizes and age heat"
arch=('x86_64')
url="https://github.com/qempexe/nudu"
license=('MIT')
depends=('gcc-libs' 'glibc')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::https://github.com/qempexe/nudu/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('6d1576add0b799917c61fc0fbf6db262578b35714ddcad4337552f81bb6b3196')
options=('!lto')

prepare() {
    cd "$pkgname-$pkgver"
    export RUSTUP_TOOLCHAIN=stable
    cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
    cd "$pkgname-$pkgver"
    export RUSTUP_TOOLCHAIN=stable CARGO_TARGET_DIR=target
    cargo build --frozen --release
}

package() {
    cd "$pkgname-$pkgver"
    install -Dm755 target/release/nudu "$pkgdir/usr/bin/nudu"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
    # icon (scalable SVG)
    install -Dm644 /dev/stdin "$pkgdir/usr/share/icons/hicolor/scalable/apps/nudu.svg" <<'SVG'
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" width="512" height="512" role="img" aria-label="nudu">
  <rect width="512" height="512" rx="96" fill="#0f172a"/>
  <circle cx="256" cy="256" r="120" fill="none" stroke="#334155" stroke-width="64"/>
  <circle cx="256" cy="256" r="120" fill="none" stroke="#10b981" stroke-width="64" stroke-dasharray="490 264" stroke-linecap="butt" transform="rotate(-90 256 256)"/>
  <circle cx="256" cy="256" r="52" fill="#0f172a"/>
  <circle cx="256" cy="256" r="14" fill="#10b981"/>
</svg>
SVG
    # a terminal app: the launcher lists it with the other command-line tools
    install -Dm644 /dev/stdin "$pkgdir/usr/share/applications/nudu.desktop" <<DESKTOP
[Desktop Entry]
Name=nudu
GenericName=Disk Usage Analyzer
Comment=See what is using your disk, in the terminal
Exec=xdg-terminal-exec nudu
Icon=nudu
Terminal=false
Type=Application
Categories=System;Utility;ConsoleOnly;
Keywords=disk;usage;du;space;storage;
DESKTOP
}

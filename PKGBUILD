# Maintainer: Fahry <farhannzarm@gmail.com>
# Upstream: https://github.com/Diegiwg/PrismLauncher-Cracked

pkgname=prismlauncher-cracked-bin
pkgver=11.0.2.1
pkgrel=1
# _pkgtag = raw upstream tag (bisa mengandung 'v' prefix / hyphen)
# dipisah dari pkgver karena pkgver tidak boleh mengandung '-' atau '/'
# GitHub Actions akan auto-update kedua variabel ini setiap ada release baru
_pkgtag=11.0.2-1
pkgdesc="PrismLauncher with offline/cracked account support (pre-built binary)"
arch=('x86_64')
url="https://github.com/Diegiwg/PrismLauncher-Cracked"
license=('GPL3')
depends=('java-runtime>=17' 'qt6-base' 'qt6-svg' 'libgl' 'zlib')
optdepends=(
  'flite: narrator support'
  'glfw: alternative OpenGL backend'
)
provides=('prismlauncher')
conflicts=('prismlauncher' 'prismlauncher-bin' 'prismlauncher-git')

# Pakai $_pkgtag (bukan $pkgver) di URL supaya sesuai tag upstream yang asli
source=(
  "${pkgname}-${pkgver}.AppImage::${url}/releases/download/${_pkgtag}/PrismLauncher-Linux-x86_64.AppImage"
  "org.prismlauncher.PrismLauncher.svg"
)
sha256sums=(
  '3feeace20f2e0aa5d0c74a79ae2789169b8357b02ab86558adc4ecf5758502c0'
  'SKIP'
)

options=(!strip)

package() {
  # Install AppImage binary
  install -Dm755 "${srcdir}/${pkgname}-${pkgver}.AppImage" \
    "$pkgdir/usr/bin/prismlauncher-cracked"

  # Install icon dari SVG yang di-download
  install -Dm644 "${srcdir}/prismlauncher-cracked.svg" \
    "$pkgdir/usr/share/icons/hicolor/scalable/apps/prismlauncher-cracked.svg"

  # Desktop entry
  cat > "$srcdir/prismlauncher-cracked.desktop" << EOF
[Desktop Entry]
Name=PrismLauncher (Cracked)
Comment=Minecraft launcher with offline support
Exec=prismlauncher-cracked
Icon=prismlauncher-cracked
Terminal=false
Type=Application
Categories=Game;
StartupWMClass=PrismLauncher
EOF

  install -Dm644 "$srcdir/prismlauncher-cracked.desktop" \
    "$pkgdir/usr/share/applications/prismlauncher-cracked.desktop"
}

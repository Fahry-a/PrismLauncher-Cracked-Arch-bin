# Maintainer: Fahry <fahry@example.com>
# Upstream: https://github.com/Diegiwg/PrismLauncher-Cracked

pkgname=prismlauncher-cracked-bin
pkgver=9.1
pkgrel=1
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

# URL template — GitHub Actions akan auto-update pkgver di atas,
# sehingga source URL ini otomatis ikut terupdate.
source=("${pkgname}-${pkgver}.AppImage::${url}/releases/download/v${pkgver}/PrismLauncher-Linux-x86_64.AppImage")
sha256sums=('SKIP')  # updpkgsums akan isi ini otomatis

options=(!strip)

package() {
  # Install AppImage
  install -Dm755 "${pkgname}-${pkgver}.AppImage" \
    "$pkgdir/usr/bin/prismlauncher-cracked"

  # Desktop entry
  cat > /tmp/prismlauncher-cracked.desktop << EOF
[Desktop Entry]
Name=PrismLauncher (Cracked)
Comment=Minecraft launcher with offline support
Exec=prismlauncher-cracked
Icon=prismlauncher
Terminal=false
Type=Application
Categories=Game;
EOF
  install -Dm644 /tmp/prismlauncher-cracked.desktop \
    "$pkgdir/usr/share/applications/prismlauncher-cracked.desktop"
}

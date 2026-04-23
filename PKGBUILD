# Maintainer: Fahry <fahry@example.com>
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
source=("${pkgname}-${pkgver}.AppImage::${url}/releases/download/${_pkgtag}/PrismLauncher-Linux-x86_64.AppImage")
sha256sums=('3feeace20f2e0aa5d0c74a79ae2789169b8357b02ab86558adc4ecf5758502c0')

options=(!strip)

package() {
  local _appimage="${srcdir}/${pkgname}-${pkgver}.AppImage"
  local _extract="${srcdir}/squashfs-root"

  chmod +x "$_appimage"

  # Install AppImage binary
  install -Dm755 "$_appimage" \
    "$pkgdir/usr/bin/prismlauncher-cracked"

  # Extract AppImage contents to get icon
  rm -rf "$_extract"
  "$_appimage" --appimage-extract >/dev/null

  # Install icon
  if [[ -e "$_extract/.DirIcon" ]]; then
    install -Dm644 "$(readlink -f "$_extract/.DirIcon")" \
      "$pkgdir/usr/share/pixmaps/prismlauncher-cracked.png"
  else
    # fallback: cari icon png/svg pertama yang berhubungan dengan PrismLauncher
    _icon_file="$(find "$_extract" -type f \( -iname '*.png' -o -iname '*.svg' \) | grep -Ei 'prism|launcher' | head -n1)"
    if [[ -n "$_icon_file" ]]; then
      case "${_icon_file##*.}" in
        png)
          install -Dm644 "$_icon_file" \
            "$pkgdir/usr/share/pixmaps/prismlauncher-cracked.png"
          ;;
        svg)
          install -Dm644 "$_icon_file" \
            "$pkgdir/usr/share/icons/hicolor/scalable/apps/prismlauncher-cracked.svg"
          ;;
      esac
    fi
  fi

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

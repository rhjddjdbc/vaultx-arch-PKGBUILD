pkgname=vaultx
pkgver=1.0.0
pkgrel=1
pkgdesc="Minimal, script-based password manager for the command line"
arch=('any')
url="https://github.com/rhjddjdbc/vaultx"
license=('GPL3')
depends=('bash' 'openssl' 'apache-tools' 'curl' 'fzf')
optdepends=(
  'xclip: Clipboard support on X11'
  'wl-clipboard: Clipboard support on Wayland'
  'qrencode: QR code export in terminal'
)
source=("git+https://github.com/rhjddjdbc/vaultx.git")
sha256sums=('SKIP')

prepare() {
  cd "$srcdir/$pkgname"

  chmod +x vaultx.sh
  chmod +x lib/*.sh
}

build() {
  : # Nothing to build
}

package() {
  cd "$srcdir/$pkgname"

  # Install vaultx.sh and help.txt to /usr/share/vaultx/
  install -Dm755 vaultx.sh "$pkgdir/usr/share/vaultx/vaultx.sh"
  install -Dm644 help.txt "$pkgdir/usr/share/vaultx/help.txt"

  # Libraries
  mkdir -p "$pkgdir/usr/share/vaultx/lib"
  install -m644 lib/*.sh "$pkgdir/usr/share/vaultx/lib/"

  # Example configuration
  install -Dm644 config.env "$pkgdir/usr/share/vaultx/config.env.example"

  # Documentation
  install -Dm644 README.md "$pkgdir/usr/share/doc/vaultx/README.md"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  # Wrapper script in /usr/bin
  install -Dm755 /dev/stdin "$pkgdir/usr/bin/vaultx" <<'EOF'
#!/bin/bash
if [[ "$1" == "-h" || "$1" == "--help" ]]; then
  cat /usr/share/vaultx/help.txt
  exit 0
fi
exec /usr/share/vaultx/vaultx.sh "$@"
EOF
}

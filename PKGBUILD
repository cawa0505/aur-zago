# Maintainer: cawa0505 <cawa0505 at gmail dot com>
pkgname=zago-bin
_pkgname=zago
pkgver=1.0.2
pkgrel=1
pkgdesc="A Lean Terminal Forge for Markdown Writers (precompiled binary)"
arch=('x86_64')
url="https://github.com/zonble/zago"
license=('MIT')
depends=('gcc-libs' 'glibc')
provides=("$_pkgname")
conflicts=("$_pkgname")
source_x86_64=("https://github.com/cawa0505/aur-zago/releases/download/v$pkgver/zago-linux-x86_64.tar.gz")
sha256sums_x86_64=('17823664be517e1d4de936c55c7a59f831945d2aa3bba383beb45ec364d29916')

package() {
  install -Dm755 zago "$pkgdir/usr/bin/zago"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
}

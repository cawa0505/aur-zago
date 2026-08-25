# Maintainer: cawa0505 <zeng.tw at gmail dot com>
pkgname=zago-bin
_pkgname=zago
pkgver=1.4.1
pkgrel=1
pkgdesc="A Lean Terminal Forge for Markdown Writers (precompiled binary)"
arch=('x86_64')
url="https://github.com/zonble/zago"
license=('MIT')
depends=('gcc-libs' 'glibc')
provides=("$_pkgname")
conflicts=("$_pkgname")
source_x86_64=("$_pkgname-$pkgver-linux-x86_64.tar.gz::https://github.com/cawa0505/aur-zago/releases/download/v$pkgver/zago-linux-x86_64.tar.gz")
sha256sums_x86_64=('13e8865755bb953231dd3f2a59b49da80a696a5db99f6a8889c16e20bec79cd7')

package() {
  install -Dm755 zago "$pkgdir/usr/bin/zago"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
}

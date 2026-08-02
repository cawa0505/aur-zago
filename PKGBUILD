# Maintainer: cawa0505 <cawa0505 at gmail dot com>
pkgname=zago-bin
_pkgname=zago
pkgver=0.1.0.r20260802.2ccb517
pkgrel=1
pkgdesc="A Lean Terminal Forge for Markdown Writers (precompiled binary)"
arch=('x86_64')
url="https://github.com/zonble/zago"
license=('MIT')
depends=('gcc-libs' 'glibc')
provides=("$_pkgname")
conflicts=("$_pkgname")
source_x86_64=("https://github.com/cawa0505/aur-zago/releases/download/v$pkgver/zago-linux-x86_64.tar.gz")
sha256sums_x86_64=('1bc813601e978943c8cef75acc3da72635eec24ce55d4040c18623811a21784c')

package() {
  install -Dm755 zago "$pkgdir/usr/bin/zago"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
}

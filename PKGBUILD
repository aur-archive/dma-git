# Maintainer: Tobias Böhm <tobias@aibor.de>

pkgname=dma-git
pkgver=0.0.0
pkgrel=1
pkgdesc="DragonFly BSD mail transport agent. git version."
url="https://github.com/corecode/dma"
license=('BSD')
makedepends=('ed' 'git')
depends=('openssl')
backup=('etc/dma/auth.conf' 'etc/dma/dma.conf')
arch=('i686' 'x86_64' 'armv6h' 'armv7h')
source=("$pkgname"::'git+https://github.com/corecode/dma.git')
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/$pkgname"
  git describe --tags | sed -E 's/^v//;s/([^-]*-g)/r\1/;s/-/./g'
}

build() {
  cd "$srcdir/$pkgname"
  make
}

package() {
  cd "$srcdir/$pkgname"

  [[ -e /var/mail ]] && sed -i '/VARMAIL/d' Makefile

  make install sendmail-link mailq-link install-spool-dirs install-etc \
    PREFIX=/usr LIBEXEC=/usr/lib/${pkgname%-git} SBIN=/usr/bin DESTDIR=$pkgdir

  install -d -m 755 $pkgdir/usr/share/licenses/$pkgname
  install LICENSE $pkgdir/usr/share/licenses/$pkgname
}

# vim: set ts=2 sw=2 et:


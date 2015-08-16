# $Id: PKGBUILD 58142 2011-11-06 22:21:10Z bluewind $
# Maintainer: Christoph Vigano <mail@cvigano.de>
# Contributor: Florian Pritz <flo@xssn.at>
# Contributor: Andreas Radke <andyrtr@archlinux.org>
# Contributor: bender02 at gmx dot com

_pkgbasename=nettle
pkgname=lib32-$_pkgbasename
pkgver=2.4
pkgrel=2
pkgdesc="A low-level cryptographic library (32-bit)"
arch=('i686' 'x86_64')
url="http://www.lysator.liu.se/~nisse/nettle/"
license=('GPL2')
depends=('lib32-gmp')
makedepends=(gcc-multilib)
source=(ftp://ftp.gnu.org/gnu/nettle/$_pkgbasename-$pkgver.tar.gz)
md5sums=(''450be8c4886d46c09f49f568ad6fa013'')

build() {
  cd "$srcdir/$_pkgbasename-$pkgver"

  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  ./configure --prefix=/usr --libdir=/usr/lib32 \
	--enable-shared \
	--disable-static # <-- seems not working now
  make
}

check() {
  cd "$srcdir/$_pkgbasename-$pkgver"
  make -k check
}

package() {
  cd "$srcdir/$_pkgbasename-$pkgver"
  make DESTDIR="$pkgdir/" install

  find $pkgdir
  
  # remove static libs
  rm -f ${pkgdir}/usr/lib32/{libhogweed,libnettle}.a

  rm -rf "${pkgdir}"/usr/{include,share,bin}
}

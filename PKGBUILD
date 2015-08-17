# Maintainer: Limao Luo <luolimao+AUR@gmail.com>
# Contributor: Chris Molozian (novabyte) <chris.molozian@gmail.com>

pkgname=phalcon-git
pkgver=1.3.4.4.gfdec9db
pkgrel=1
pkgdesc="A high performance PHP web framework written as a C extension"
arch=(i686 x86_64)
[[ $CARCH == "i686" ]] && cd _arch=32bits || _arch=64bits
url=http://phalconphp.com/
license=(BSD)
depends=(php)
makedepends=(git)
provides=(${pkgname%-*}=$pkgver)
conflicts=(${pkgname%-*})
install=$pkgname.install
source=($pkgname::git://github.com/phalcon/cphalcon.git)
sha256sums=('SKIP')
sha512sums=('SKIP')

pkgver() {
    cd $pkgname/
    git describe --tags | sed 's/^phalcon-v//;s/-/./g'
}

build() {
    cd $pkgname/build/$_arch/
    export CFLAGS="-O2 -fno-delete-null-pointer-checks"
    phpize
    ./configure --enable-phalcon
    make
}

package() {
    cd $pkgname/build/$_arch/
    sed -i 's:\$(INSTALL_ROOT)\(\$(EXTENSION_DIR)\):\$(DESTDIR)\1:g' Makefile
    make DESTDIR="$pkgdir" install
}

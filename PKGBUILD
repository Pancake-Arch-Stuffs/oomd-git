# Maintainer: Raphiel Rollerscaperers <raphielscape@hentaios.com>
# Previous Maintainer: Jianqiu Zhang <void001@archlinuxcn.org>

_pkgname=oomd
pkgname=oomd-git
pkgver=v0.4.0.99.ga41962c
pkgrel=1
pkgdesc='A userspace out-of-memory killer (git build)'
arch=('x86_64')
url="https://github.com/facebookincubator/oomd"
license=('GPL2')
depends=('jsoncpp')
optdepends=('systemd-libs')
makedepends=('meson' 'ninja')
checkdepends=('gtest' 'gmock')
install="${pkgname}.install"
provides=("${_pkgname}")
conflicts=("${_pkgname}")
backup=("etc/${_pkgname}/${_pkgname}.json")
md5sums=('SKIP')
source=("oomd::git+https://github.com/facebookincubator/oomd.git")

prepare() {
    cd $srcdir/$_pkgname/src/$_pkgname
    # Suppress noise from glib-compile-schemas.hook
    git am -3 ../../../../0001-Log.cpp-Add-missing-mode.patch
}

pkgver() {
    cd $srcdir/$_pkgname
    echo "$(git describe --long --tags | tr - .)"
}

build() {
    cd $srcdir/$_pkgname
    meson --prefix=/usr build && ninja -C build
}

check() {
   cd $srcdir/$_pkgname
   ninja test -C build
}

package() {
    cd $srcdir/$_pkgname
    DESTDIR=$pkgdir ninja -C build install
    install -Dm644 $srcdir/oomd/src/oomd/etc/desktop.json $pkgdir/etc/desktop.json.example
}

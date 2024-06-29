# Maintainer: Andrew Sun <adsun701 at gmail dot com>
# Contributor: Alexander F. Rødseth <xyproto at archlinux dot org>
# Contributor: Vincent Bernardoff <vb at luminar dot eu dot org>

pkgname=clingo
pkgver=5.7.1
pkgrel=1
pkgdesc='Grounding tools for (disjunctive) logic programs'
arch=('i686' 'x86_64')
url='https://potassco.org/'
license=('MIT')
depends=('lua' 'python')
makedepends=('cmake' 're2c')
conflicts=('clasp')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/potassco/clingo/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('544b76779676075bb4f557f05a015cbdbfbd0df4b2cc925ad976e86870154d81')

build() {
  mkdir -p ${srcdir}/build
  export CXXFLAGS="${CXXFLAGS//-fvar-tracking-assignments/}"
  cmake -S "${srcdir}/${pkgname}-${pkgver}" -B "${srcdir}/build" \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DCMAKE_BUILD_TYPE=Release \
    -DCLINGO_BUILD_WITH_PYTHON=ON \
    -DCLINGO_BUILD_WITH_LUA=ON \
    -DCMAKE_CXX_COMPILER=g++
  cmake --build "${srcdir}/build"
}

package() {
  DESTDIR="$pkgdir" cmake --install "${srcdir}/build"
  install -Dm644 "${srcdir}/${pkgname}-${pkgver}/LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.md"
}

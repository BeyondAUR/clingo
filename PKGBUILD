# Maintainer: Andrew Sun <adsun701 at gmail dot com>
# Contributor: Alexander F. Rødseth <xyproto at archlinux dot org>
# Contributor: Vincent Bernardoff <vb at luminar dot eu dot org>

pkgname=clingo
pkgver=5.8.2
pkgrel=1
pkgdesc='Grounding tools for (disjunctive) logic programs'
arch=('i686' 'x86_64')
url='https://potassco.org/'
license=('MIT')
depends=('lua' 'python')
makedepends=('cmake' 're2c' 'git')
conflicts=('clasp')
source=("git+https://github.com/potassco/clingo#tag=v${pkgver}")
sha256sums=('47c3676120ac94f5381faf073f6faabc4c21ac0bee2f86c8e5b31779c06aef7c')

build() {
  mkdir -p ${srcdir}/${pkgname}
  export CXXFLAGS="${CXXFLAGS//-fvar-tracking-assignments/}"
  cmake -S "${srcdir}/${pkgname}" -B "${srcdir}/build" \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DCMAKE_BUILD_TYPE=Release \
    -DCLINGO_BUILD_WITH_PYTHON=ON \
    -DCLINGO_BUILD_WITH_LUA=ON \
    -DCMAKE_CXX_COMPILER=g++ \
    -DCMAKE_POLICY_VERSION_MINIMUM=3.10
  cmake --build "${srcdir}/build"
}

package() {
  DESTDIR="${pkgdir}" cmake --install "${srcdir}/build"
  install -Dm644 "${srcdir}/${pkgname}/LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.md"
}

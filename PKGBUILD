# Maintainer: Andrew Sun <adsun701 at gmail dot com>
# Contributor: Alexander F. Rødseth <xyproto at archlinux dot org>
# Contributor: Vincent Bernardoff <vb at luminar dot eu dot org>

pkgname=clingo
pkgver=5.8.0
pkgrel=2
pkgdesc='Grounding tools for (disjunctive) logic programs'
arch=('i686' 'x86_64')
url='https://potassco.org/'
license=('MIT')
depends=('lua' 'python')
makedepends=('cmake' 're2c' 'git')
conflicts=('clasp')
source=("git+https://github.com/potassco/clingo#tag=v${pkgver}"
        "fix-re2c-4.3-compat.patch")
sha256sums=('eb06af702e54d4bd7aefda2776b469e78dc5728a41b0f3867515c599625a0909'
            'e4f1e150eb1bfaf9def1a315caa6297149f21e5ec0a8e68213a69426de45831c')

prepare() {
  cd ${srcdir}/${pkgname}
  patch -Np1 -i "${srcdir}/fix-re2c-4.3-compat.patch"
}

build() {
  mkdir -p ${srcdir}/build
  export CXXFLAGS="${CXXFLAGS//-fvar-tracking-assignments/}"
  cmake -S "${srcdir}/${pkgname}-${pkgver}" -B "${srcdir}/build" \
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
  install -Dm644 "${srcdir}/${pkgname}-${pkgver}/LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.md"
}

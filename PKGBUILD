# Maintainer: rubenvb vanboxem <dottie> ruben <attie> gmail <dottie> com
pkgname=mingw-w64-winpthreads-svn
pkgver=6362
pkgrel=1
pkgdesc='MinGW-w64 winpthreads library'
arch=('any')
url='http://mingw-w64.sourceforge.net'
license=('custom')
groups=('mingw-w64-toolchain' 'mingw-w64')
depends=()
makedepends=('svn' 'mingw-w64-gcc-base' 'mingw-w64-binutils' 'mingw-w64-crt' 'mingw-w64-headers-bootstrap')
optdepends=()
provides=('mingw-w64-winpthreads' 'mingw-w64-headers-bootstrap')
conflicts=('mingw-w64-headers-bootstrap' 'mingw-w64-winpthreads')
replaces=('mingw-w64-headers-bootstrap')
backup=()
options=('!strip' '!buildflags' 'staticlibs' '!emptydirs')
source=(svn+svn://svn.code.sf.net/p/mingw-w64/code/trunk/mingw-w64-libraries/winpthreads)
md5sums=(SKIP)

_targets="i686-w64-mingw32 x86_64-w64-mingw32"

pkgver() {
  cd "$SRCDEST/winpthreads"
  svnversion
}

build() {
  for _target in ${_targets}; do
    mkdir -p ${srcdir}/winpthreads-build-${_target} && cd ${srcdir}/winpthreads-build-${_target}
    ${srcdir}/winpthreads/configure --prefix=/usr/${_target} \
        --host=${_target} --enable-static --enable-shared
    make
  done
}

package() {
  for _target in ${_targets}; do
    cd ${srcdir}/winpthreads-build-${_target}
    make DESTDIR=${pkgdir} install
  done
  
  install -Dm644 ${srcdir}/winpthreads/COPYING ${pkgdir}/usr/share/licenses/${pkgname}/COPYING
}

# Maintainer: Philippe Joyez

_realname=guile

pkgbase=mingw-w64-${_realname}18
pkgname="${MINGW_PACKAGE_PREFIX}-${_realname}18"
pkgver=1.8.8
pkgrel=1
pkgdesc="a portable, embeddable Scheme implementation written in C. Legacy branch. (mingw-w64)"
arch=('i686')
url="https://www.gnu.org/software/guile/"
license=("GPL")
makedepends=("${MINGW_PACKAGE_PREFIX}-gcc" "${MINGW_PACKAGE_PREFIX}-pkg-config")
depends=("${MINGW_PACKAGE_PREFIX}-crt"
    "${MINGW_PACKAGE_PREFIX}-gmp"
    "${MINGW_PACKAGE_PREFIX}-libtool"
    "${MINGW_PACKAGE_PREFIX}-ncurses>=5.7"
    "texinfo"
    "${MINGW_PACKAGE_PREFIX}-libunistring"
    "${MINGW_PACKAGE_PREFIX}-gc"
    "${MINGW_PACKAGE_PREFIX}-readline"
    "${MINGW_PACKAGE_PREFIX}-libffi"
    )
options=('strip' !buildflags)
#options=(debug !strip)
source=("https://ftp.gnu.org/pub/gnu/${_realname}/${_realname}-${pkgver}.tar.gz"
  cygwin-ports_guile_1.8.5-export-symbols.patch
  fix_warnings.patch
  gnucash-on-windows_guile-1.8.patch
  fix_mingw_x86_64-4.patch
  dirent2.patch
  )
sha256sums=('c3471fed2e72e5b04ad133bbaaf16369e8360283679bcf19800bc1b381024050'
 'SKIP' 'SKIP' 'SKIP'  'SKIP' 'SKIP'  )

prepare() {
  cd ${srcdir}/${_realname}-${pkgver}
  patch -p2 -i ${srcdir}/cygwin-ports_guile_1.8.5-export-symbols.patch
  patch -p2 -i ${srcdir}/fix_warnings.patch
  patch -p1 -i ${srcdir}/gnucash-on-windows_guile-1.8.patch
#if  [ $CARCH = "x86_64" ]; then
#  patch -p2 -i ${srcdir}/fix_mingw_x86_64-4.patch
#  patch -p1 -E -i ${srcdir}/dirent2.patch
#fi
  autoreconf -fi
  sed -i 's|"$ac_cv_sizeof_long" -ne "$ac_cv_sizeof_void_p"|"$ac_cv_sizeof_long" -gt "$ac_cv_sizeof_void_p"|g' configure
}

build() {
  mkdir -p "${srcdir}/build-${MINGW_CHOST}"
  export "ap_cv_void_ptr_lt_long=4"
# export CFLAGS="$CFLAGS -g -O1"
#  export CXXFLAGS="$CXXFLAGS -g -O1"

  cd "${srcdir}/build-${MINGW_CHOST}"
  "${srcdir}"/${_realname}-${pkgver}/configure \
    --prefix=${MINGW_PREFIX} \
    --build=${MINGW_CHOST} \
    --host=${MINGW_CHOST} \
    --enable-shared \
    --enable-debug \
	#--disable-error-on-warning  #this can be removed by applying corresponding patch above

	#--without-64-calls \  #with this (and no patch) it builds but does not run
  make -i
}

package() {
  cd "${srcdir}/build-${MINGW_CHOST}"
  make DESTDIR="$pkgdir" install
  find "${pkgdir}${MINGW_PREFIX}" -name '*.def' -o -name '*.exp' | xargs -rtl1 rm

  rm -r "${pkgdir}${MINGW_PREFIX}"/share/info
  rm -r "${pkgdir}${MINGW_PREFIX}"/share/man
}

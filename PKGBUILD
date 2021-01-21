# Maintainer: Philippe Joyez

_realname=guile

pkgbase=mingw-w64-${_realname}1.8
pkgname="${MINGW_PACKAGE_PREFIX}-${_realname}1.8"
pkgver=1.8.8
pkgrel=2
pkgdesc="a portable, embeddable Scheme implementation written in C. Legacy branch. (mingw-w64)"
arch=('any')
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
  guile-1.8.3-64bit-fixes.patch
  guile-1.6.4-amd64.patch
  guile-1.8.5-drop-ldflags-from-pkgconfig.patch
  guile-1.8.7-testsuite.patch
  guile-1.8.7-fix-doc.patch
  guile-1.8.8-make-sockets.test-more-robust.patch
  guile-1.8.8-automake-1.13.patch
  guile-1.8.8-drop-broken-test-hack.patch
  guile-1.8.8-mark-Unused-modules-are-removed-gc-test-as-unresolved.patch
  guile-1.8.8-cve-2016-8605.patch
  guile-1.8.8-configure.patch
  guile-autoconf.patch
  )
  
sha256sums=('c3471fed2e72e5b04ad133bbaaf16369e8360283679bcf19800bc1b381024050'
            '20fcb414e08d37640de2efe20631c4f4d5763221d87ee5b259552e08a73d77b2'
            'f10c0f0eae7ccd7d5834fd25b18abcfff57bedeafe4d275b987b848ca48200a4'
            'a708e3454af35dd7389124959e18798fd733db396b3facb2d918facaab76fc2c'
            '5bca472f039d8c697acc8836b62d4e2d5f2763f93275a805c41333e4c2264357'
            'c92b24277ff9f4cd9d0ea61d3cf8d911acd8a2fbde10e15b246302161bac7181'
            '27d7b81f5fbb1e53682b01b565f0dfc22dc04bcdcf5cb1e7c3c8b573e0d94f53'
            'bb1122d0e90d78f830fd5bacd3a3b175797288a170d0bc217a9f2b601660e1a5'
            'c989026417c3438f88936366fbf4f3704684c00c56576c2b0f964b2bdc0121b5'
            'cd2d0b92d6d19698a30d56b323e2ab09b19d8afe516cfa65af3b6ce2f0fc9fab'
            'a45dcc625dad423ef5a4eba92635c2243afb013f568a539b2879b85c7e80f0b7'
            '14a1c911544580a69fe8e7314536ceba1ff0a48fda50d4ba3a76da83b620827d'
            '78b6433332d89d0c7ca13bf9e0f65d6e4efd41fd2ffcb5676af9a47618ce3d42'
            '6433d2e1436d0b756df0d397fdafa8438c7d59cf993787091a93ed2aaf47d4f1'
            'a9779c0cbc711f32b9260b7f13ba20b4bd3253fb7b30765d1228d35459fcf8b3'
            '9de4615dd01f873f29776c711def8c67ba036cd06262662fa9f372d8157aeea8'
            )

prepare() {
  cd ${srcdir}/${_realname}-${pkgver}
  patch -p2 -i ${srcdir}/cygwin-ports_guile_1.8.5-export-symbols.patch
  patch -p2 -i ${srcdir}/fix_warnings.patch
  patch -p1 -i ${srcdir}/gnucash-on-windows_guile-1.8.patch
  patch -p1 -i ${srcdir}/guile-1.8.3-64bit-fixes.patch
  patch -p1 -i ${srcdir}/guile-1.6.4-amd64.patch
  patch -p1 -i ${srcdir}/guile-1.8.5-drop-ldflags-from-pkgconfig.patch
  patch -p1 -i ${srcdir}/guile-1.8.7-testsuite.patch
  patch -p1 -i ${srcdir}/guile-1.8.7-fix-doc.patch
  patch -p1 -i ${srcdir}/guile-1.8.8-make-sockets.test-more-robust.patch
  patch -p1 -i ${srcdir}/guile-1.8.8-automake-1.13.patch
  patch -p1 -i ${srcdir}/guile-1.8.8-drop-broken-test-hack.patch
  patch -p1 -i ${srcdir}/guile-1.8.8-mark-Unused-modules-are-removed-gc-test-as-unresolved.patch
  patch -p1 -i ${srcdir}/guile-1.8.8-cve-2016-8605.patch
  patch -p1 -i ${srcdir}/guile-1.8.8-configure.patch
  patch -p1 -i ${srcdir}/guile-autoconf.patch
  
  autoreconf -fi
  sed -i 's|"$ac_cv_sizeof_long" -ne "$ac_cv_sizeof_void_p"|"$ac_cv_sizeof_long" -gt "$ac_cv_sizeof_void_p"|g' configure
}

build() {
  export lt_cv_deplibs_check_method='pass_all' #for building on WIN10, see https://github.com/msys2/MINGW-packages/issues/7712

  mkdir -p "${srcdir}/build-${MINGW_CHOST}"
  export "ap_cv_void_ptr_lt_long=4"
# export CFLAGS="$CFLAGS -g -O1"
#  export CXXFLAGS="$CXXFLAGS -g -O1"
 export CFLAGS="$CFLAGS -Wno-stringop-truncation -Wno-unused-but-set-variable"
 export LDFLAGS="$LDFLAGS"

  cd "${srcdir}/build-${MINGW_CHOST}"
  "${srcdir}"/${_realname}-${pkgver}/configure \
    --prefix=${MINGW_PREFIX} \
    --build=${MINGW_CHOST} \
    --host=${MINGW_CHOST} \
    --enable-shared \
    --enable-debug \
	#--disable-error-on-warning  #this can be removed by applying corresponding patch above

  make
}

package() {
  cd "${srcdir}/build-${MINGW_CHOST}"
  make DESTDIR="$pkgdir" install
  find "${pkgdir}${MINGW_PREFIX}" -name '*.def' -o -name '*.exp' | xargs -rtl1 rm

  rm -r "${pkgdir}${MINGW_PREFIX}"/share/info
  rm -r "${pkgdir}${MINGW_PREFIX}"/share/man
}

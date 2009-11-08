# Maintainer: Eric Belanger <eric@archlinux.org>
# Contributor: Tom K <tom@archlinux.org>

pkgname=rrdtool
pkgver=1.4.1
pkgrel=1
pkgdesc="Data logging and graphing application"
arch=('i686' 'x86_64')
url="http://www.rrdtool.org"
license=('GPL')
depends=('libart-lgpl' 'libpng' 'freetype2' 'libxml2' 'pango')
makedepends=('intltool' 'ruby>=1.9' 'python' 'tcl' 'lua')
optdepends=('tcl: to use corresponding binding' \
            'python: to use corresponding binding' \
            'ruby: to use corresponding binding' \
            'lua: to use corresponding binding')
options=('!libtool' '!emptydirs' '!makeflags')
source=(http://oss.oetiker.ch/rrdtool/pub/rrdtool-${pkgver}.tar.gz)
md5sums=('07dd73513e309347ab4e0300dd28c6d9')
sha1sums=('62d39ef408acd008e86b1b5ce2c7fa9894a1459b')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --disable-rpath --enable-perl \
    --enable-perl-site-install --with-perl-options='INSTALLDIRS=vendor' \
    --enable-ruby --enable-ruby-site-install --enable-python \
    --enable-lua --enable-lua-site-install \
    --enable-tcl --enable-tcl-site || return 1
  make || return 1
  make DESTDIR="${pkgdir}" LIBRUBYARG_SHARED="-Wl,-L/usr/lib -lruby" \
    LIBPATH="-L. -L/usr/lib -L../../src/.libs" install || return 1
}

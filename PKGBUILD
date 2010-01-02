# Maintainer: Eric Belanger <eric@archlinux.org>
# Contributor: Tom K <tom@archlinux.org>

pkgname=rrdtool
pkgver=1.4.2
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
md5sums=('9318d3b4016dd9dd9897f1eac7548032')
sha1sums=('d77fbeac37837e64cbe2a377acbf3e7b95b6e86e')

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

# Maintainer: Eric Belanger <eric@archlinux.org>
# Contributor: Tom K <tom@archlinux.org>

pkgname=rrdtool
pkgver=1.4.3
pkgrel=1
pkgdesc="Data logging and graphing application"
arch=('i686' 'x86_64')
url="http://www.rrdtool.org"
license=('GPL')
depends=('libpng' 'libxml2' 'pango')
makedepends=('intltool' 'ruby' 'python' 'tcl' 'lua')
optdepends=('tcl: to use corresponding binding' \
            'python: to use corresponding binding' \
            'ruby: to use corresponding binding' \
            'lua: to use corresponding binding')
options=('!libtool' '!emptydirs' '!makeflags')
source=(http://oss.oetiker.ch/rrdtool/pub/rrdtool-${pkgver}.tar.gz)
md5sums=('492cf946c72f85987238faa2c311b7bb')
sha1sums=('1e65de0192c149a30ee0d277e758a31ff7d6d6f0')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --localstatedir=/var --disable-rpath --enable-perl \
    --enable-perl-site-install --with-perl-options='INSTALLDIRS=vendor' \
    --enable-ruby --enable-ruby-site-install --enable-python \
    --enable-lua --enable-lua-site-install \
    --enable-tcl || return 1
  make || return 1
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" LIBRUBYARG_SHARED="-Wl,-L/usr/lib -lruby" \
    LIBPATH="-L. -L/usr/lib -L../../src/.libs" install || return 1
}

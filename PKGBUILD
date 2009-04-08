# Maintainer: Eric Belanger <eric@archlinux.org>
# Contributor: Tom K <tom@archlinux.org>

pkgname=rrdtool
pkgver=1.3.7
pkgrel=1
pkgdesc="Data logging and graphing application"
arch=('i686' 'x86_64')
url="http://www.rrdtool.org"
license=('GPL')
depends=('libart-lgpl' 'libpng' 'freetype2' 'libxml2' 'pango')
makedepends=('ruby' 'python' 'tcl')
optdepends=('tcl, python and/or ruby: to use corresponding binding')
options=('!libtool' '!emptydirs')
source=(http://oss.oetiker.ch/rrdtool/pub/rrdtool-${pkgver}.tar.gz)
md5sums=('e2e0da2a83e58ba2fcefba932a3cbb72')
sha1sums=('802fc03107c5b600548beef0ee6ad6cf153fc1f1')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  ./configure --prefix=/usr --enable-perl-site-install \
    --with-perl-options='INSTALLDIRS=vendor' --enable-ruby-site-install || return 1
  make || return 1
  make DESTDIR=${pkgdir} install || return 1

  find ${pkgdir} -name '.packlist' -delete
  find ${pkgdir} -name 'perllocal.pod' -delete
}

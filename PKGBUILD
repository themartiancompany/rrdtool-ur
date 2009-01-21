# Maintainer: Eric Belanger <eric@archlinux.org>
# Contributor: Tom K <tom@archlinux.org>

pkgname=rrdtool
pkgver=1.3.6
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
md5sums=('afaabd5a60115581e866efbac796d307')
sha1sums=('4a8499ab58dfd37419bf1cb2429a29da9bc782c3')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  ./configure --prefix=/usr --enable-perl-site-install \
    --with-perl-options='INSTALLDIRS=vendor' --enable-ruby-site-install || return 1
  make || return 1
  make DESTDIR=${pkgdir} install || return 1

  find ${pkgdir} -name '.packlist' -delete
  find ${pkgdir} -name 'perllocal.pod' -delete
}

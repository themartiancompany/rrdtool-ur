# Maintainer: Eric Belanger <eric@archlinux.org>
# Contributor: Tom K <tom@archlinux.org>

pkgname=rrdtool
pkgver=1.3.8
pkgrel=1
pkgdesc="Data logging and graphing application"
arch=('i686' 'x86_64')
url="http://www.rrdtool.org"
license=('GPL')
depends=('libart-lgpl' 'libpng' 'freetype2' 'libxml2' 'pango')
makedepends=('intltool' 'ruby' 'python' 'tcl')
optdepends=('tcl, python and/or ruby: to use corresponding binding')
options=('!libtool' '!emptydirs' '!makeflags')
source=(http://oss.oetiker.ch/rrdtool/pub/rrdtool-${pkgver}.tar.gz)
md5sums=('0de79494ab969cebfbfae3d237de18fe')
sha1sums=('1fe71706442ddd78ec8cdbaadd8ce16bb1326b05')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --enable-perl-site-install \
    --with-perl-options='INSTALLDIRS=vendor' --enable-ruby-site-install || return 1
  make || return 1
  make DESTDIR="${pkgdir}" install || return 1

  find ${pkgdir} -name '.packlist' -delete
  find ${pkgdir} -name 'perllocal.pod' -delete
}

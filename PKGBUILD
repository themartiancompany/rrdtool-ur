# $Id: PKGBUILD,v 1.6 2008/03/26 02:51:13 kevin Exp $
# Maintainer: Tom K <tom@archlinux.org>

pkgname=rrdtool
pkgver=1.2.27
pkgrel=1
pkgdesc="Data logging and graphing application"
arch=(i686 x86_64)
license="GPL"
depends=('libart-lgpl' 'libpng' 'freetype2')
makedepends=('ruby' 'python')
source=(http://oss.oetiker.ch/rrdtool/pub/rrdtool-$pkgver.tar.gz)
url="http://www.rrdtool.org"
install=rrdtool.install
options=(!emptydirs)

build() {
  cd $startdir/src/$pkgname-$pkgver
  ./configure --prefix=/usr --enable-perl-site-install \
      --with-perl-options='INSTALLDIRS=vendor' --enable-ruby-site-install
  make || return 1
  make DESTDIR=$startdir/pkg install

  find $startdir/pkg -name '.packlist' -delete
  find $startdir/pkg -name 'perllocal.pod' -delete
}
md5sums=('841ca303c88f7184cf0aaab07e52dec4')

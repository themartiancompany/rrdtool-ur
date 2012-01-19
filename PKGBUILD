# Maintainer: Eric Bélanger <eric@archlinux.org>

pkgname=rrdtool
pkgver=1.4.5
pkgrel=5
pkgdesc="Data logging and graphing application"
arch=('i686' 'x86_64')
url="http://www.rrdtool.org"
license=('GPL' 'custom')
depends=('libxml2' 'pango' 'ttf-dejavu')
makedepends=('intltool' 'ruby' 'python2' 'tcl' 'lua')
optdepends=('tcl: to use corresponding binding' \
            'python2: to use corresponding binding' \
            'ruby: to use corresponding binding' \
            'lua: to use corresponding binding')
options=('!libtool' '!emptydirs' '!makeflags')
source=(http://oss.oetiker.ch/rrdtool/pub/rrdtool-${pkgver}.tar.gz)
sha1sums=('56638e8aedd5d5522152e86746e382b75dc48c35')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  sed -i 's|-lrrd|-lrrd -L/usr/lib/perl5/core_perl/CORE/ -lperl |' bindings/perl-shared/Makefile.PL
  PYTHON=python2 ./configure --prefix=/usr --localstatedir=/var --disable-rpath \
    --enable-perl --enable-perl-site-install --with-perl-options='INSTALLDIRS=vendor' \
    --enable-ruby --enable-ruby-site-install --enable-python \
    --enable-lua --enable-lua-site-install --enable-tcl --disable-libwrap
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -D -m644 COPYRIGHT "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

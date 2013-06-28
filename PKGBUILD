# Maintainer: Eric Bélanger <eric@archlinux.org>

pkgname=rrdtool
pkgver=1.4.8
pkgrel=1
pkgdesc="Data logging and graphing application"
arch=('i686' 'x86_64')
url="http://www.rrdtool.org"
license=('GPL' 'custom')
depends=('libxml2' 'pango' 'ttf-dejavu')
makedepends=('intltool' 'ruby' 'python2' 'tcl' 'lua51')
optdepends=('tcl: to use corresponding binding' \
            'python2: to use corresponding binding' \
            'ruby: to use corresponding binding' \
            'lua51: to use corresponding binding')
options=('!libtool' '!emptydirs' '!makeflags')
source=(http://oss.oetiker.ch/rrdtool/pub/rrdtool-${pkgver}.tar.gz 
        rrdtool-pangofont.patch)
sha1sums=('56d68857f39e70bfa32360947614d8220702ed02'
          '8c600285bdab7776c1d5301df7cf486d69eae048')

prepare() {
  cd ${pkgname}-${pkgver}
  # fix FS#28521 make ruby install to vendor_ruby instead of site_ruby
  sed -e 's/$(RUBY) extconf.rb/& --vendor/' -i bindings/Makefile.in
  patch -p1 -i ../rrdtool-pangofont.patch
}

build() {
  cd ${pkgname}-${pkgver}
  autoconf
  PYTHON=python2 LUA=/usr/bin/lua5.1 \
    LUA_CFLAGS="-I/usr/include/lua5.1 -llua5.1" LUA_INSTALL_CMOD="/usr/lib/lua/5.1" \
    ./configure --prefix=/usr --localstatedir=/var --disable-rpath \
    --enable-perl --enable-perl-site-install --with-perl-options='INSTALLDIRS=vendor' \
    --enable-ruby --enable-ruby-site-install --enable-python \
    --enable-lua --enable-lua-site-install --enable-tcl --disable-libwrap
  make LIBS+="-lglib-2.0"
}

package() {
  cd ${pkgname}-${pkgver}
  make DESTDIR="${pkgdir}" includedir=/usr/include install
  install -D -m644 COPYRIGHT "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

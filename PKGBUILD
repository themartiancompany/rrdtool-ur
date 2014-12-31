# Maintainer: Eric Bélanger <eric@archlinux.org>

pkgname=rrdtool
pkgver=1.4.9
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
options=('!emptydirs' '!makeflags')
source=(http://oss.oetiker.ch/rrdtool/pub/rrdtool-${pkgver}.tar.gz 
        rrdtool-pangofont.patch rrdtool-systemd.patch)
sha1sums=('c83b158b4aaadbf28b15823fa863db1672700d3b'
          '6594d5e53d649753eefefc4e29db79e19745f66d'
          '963b600f8056d85305b6ff4554fa1e7b9b5a4ae1')

prepare() {
  cd ${pkgname}-${pkgver}
  # fix FS#28521 make ruby install to vendor_ruby instead of site_ruby
  sed -e 's/$(RUBY) extconf.rb/& --vendor/' -i bindings/Makefile.am
  patch -p1 -i "${srcdir}/rrdtool-pangofont.patch"
  patch -p1 -i "${srcdir}/rrdtool-systemd.patch"
}

build() {
  cd ${pkgname}-${pkgver}
  autoreconf
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

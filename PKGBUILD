# Maintainer: Eric Bélanger <eric@archlinux.org>

pkgname=rrdtool
pkgver=1.4.7
pkgrel=4
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
source=(http://oss.oetiker.ch/rrdtool/pub/rrdtool-${pkgver}.tar.gz)
sha1sums=('faab7df7696b69f85d6f89dd9708d7cf0c9a273b')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"

  # fix FS#28521 make ruby install to vendor_ruby instead of site_ruby
  sed -e 's/$(RUBY) extconf.rb/& --vendor/' -i bindings/Makefile.in

  PYTHON=python2 LUA=/usr/bin/lua5.1 \
    LUA_CFLAGS="-I/usr/include/lua5.1 -llua5.1" LUA_INSTALL_CMOD="/usr/lib/lua/5.1" \
    ./configure --prefix=/usr --localstatedir=/var --disable-rpath \
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

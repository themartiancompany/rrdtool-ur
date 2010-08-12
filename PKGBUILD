# Maintainer: Eric Belanger <eric@archlinux.org>
# Contributor: Tom K <tom@archlinux.org>

pkgname=rrdtool
pkgver=1.4.4
pkgrel=1
pkgdesc="Data logging and graphing application"
arch=('i686' 'x86_64')
url="http://www.rrdtool.org"
license=('GPL' 'custom')
depends=('libpng' 'libxml2' 'pango')
makedepends=('intltool' 'ruby' 'python' 'tcl' 'lua')
optdepends=('tcl: to use corresponding binding' \
            'python: to use corresponding binding' \
            'ruby: to use corresponding binding' \
            'lua: to use corresponding binding')
options=('!libtool' '!emptydirs' '!makeflags')
changelog=ChangeLog
source=(http://oss.oetiker.ch/rrdtool/pub/rrdtool-${pkgver}.tar.gz)
md5sums=('93ad2fc2e9ddcd7d99c611fe30284a54')
sha1sums=('e4715c13f2a6fd077c54911d396eb573788377b0')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --localstatedir=/var --disable-rpath --enable-perl \
    --enable-perl-site-install --with-perl-options='INSTALLDIRS=vendor' \
    --enable-ruby --enable-ruby-site-install --enable-python \
    --enable-lua --enable-lua-site-install \
    --enable-tcl
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" LIBRUBYARG_SHARED="-Wl,-L/usr/lib -lruby" \
    LIBPATH="-L. -L/usr/lib -L../../src/.libs" install
  install -D -m644 COPYRIGHT "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

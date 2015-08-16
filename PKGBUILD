# Maintainer: Aelius Saionji
# Contributor: Giovanni Scafora <giovanni@archlinux.org>
# Contributor: Dan McGee <dan@archlinux.org>
# Patches by Nei @ http://anti.teamidiot.de/static/nei/*/Code/Irssi/
# Prettier PKGBUILD with help from Earnestly

pkgname='irssi-256color'
pkgver='0.8.16'
pkgrel='4'
pkgdesc='Release candidate not in official repo, patched with 256 and true color support'
arch=('i686' 'x86_64')
url='http://irssi.org/'
license=('GPL')
depends=('glib2' 'openssl')
optdepends=('perl-libwww: for the scriptassist script')
conflicts=('irssi')
provides=('irssi')
backup=('etc/irssi.conf')
install='irssi-256color.install'
source=('http://irssi.org/files/irssi-0.8.16.tar.bz2'
	'alias.diff'
	'05-fix-print_after-scrollback.diff'
	'06-add-print_text_after_time.diff'
	'07-no-split-utf8.diff'
	'256color.diff')
md5sums=('4346119c4c000d0198cda17666ff1f06'
         '1095544905a6860eebd798295147a9b1'
         'b2c13b7635e0109e1b6fc80d62a4c908'
         'fa4bb2bcf2e95275ed5e4a48e2542321'
         'a3bcc4ca6961c146408f08a80cafdfc5'
         '87b1b1e35fa3ac9fa6c46d96645030be')

prepare() {
  cd irssi-0.8.16
  patch -p1 -i "$srcdir"/05-fix-print_after-scrollback.diff
  patch -p1 -i "$srcdir"/06-add-print_text_after_time.diff 
  patch -p1 -i "$srcdir"/07-no-split-utf8.diff
  patch -p1 -i "$srcdir"/256color.diff
}

build() {
  cd irssi-0.8.16
  aclocal
  automake --add-missing
  autoreconf
  ./configure --prefix=/usr \
              --enable-ipv6 \
	      --with-proxy \
	      --enable-true-color \
	      --sysconfdir=/etc \
	      --with-perl-lib=vendor
  make
}

package() {
  cd irssi-0.8.16
  make DESTDIR="$pkgdir" install 
}

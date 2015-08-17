# Contributor: emmanuelux
# Contributor: OK100 <ok100@lavabit.com>

pkgname=rxvt-unicode-patched-left_ptr-unicode3
_pkgname=rxvt-unicode
pkgver=9.16
pkgrel=1
pkgdesc="Unicode enabled rxvt-clone terminal emulator (urxvt) with fixed font spacing (width) and with mouse pointer XC_left_ptr in place of XC_xterm. Compiled with --enable-unicode3"
arch=('i686' 'x86_64')
url="http://software.schmorp.de/pkg/rxvt-unicode.html"
license=('GPL')
depends=('gcc-libs' 'libxft' 'gdk-pixbuf2')
optdepends=('perl: lots of utilities' 'gtk2-perl: to use the urxvt-tabbed')
source=(http://dist.schmorp.de/rxvt-unicode/$_pkgname-$pkgver.tar.bz2
        $_pkgname.desktop
        font-width-fix.patch)
provides=(rxvt-unicode)
conflicts=(rxvt-unicode rxvt-unicode-patched-left_ptr)

build() {
  cd "$srcdir/$_pkgname-$pkgver"
  patch -p0 -i ../font-width-fix.patch
  sed -i 's/XC_xterm/XC_left_ptr/' src/init.C
  ./configure --prefix=/usr \
    --with-terminfo=/usr/share/terminfo \
    --enable-256-color \
    --enable-font-styles \
    --enable-xim \
    --enable-keepscrolling \
    --enable-selectionscrolling \
    --enable-smart-resize \
    --enable-pixbuf \
    --enable-transparency \
    --enable-utmp \
    --enable-wtmp \
    --enable-lastlog \
	--enable-unicode3 \
    --disable-frills
  make
}

package() {
  cd "$srcdir/$_pkgname-$pkgver"
  install -d "$pkgdir/usr/share/terminfo"
  export TERMINFO="$pkgdir/usr/share/terminfo"
  make DESTDIR="$pkgdir" install
  # install the tabbing wrapper ( requires gtk2-perl! )
  sed -i 's/\"rxvt\"/"urxvt"/' doc/rxvt-tabbed
  install -Dm 755 doc/rxvt-tabbed "$pkgdir/usr/bin/urxvt-tabbed"
  # install freedesktop menu
  install -Dm644 ../$_pkgname.desktop \
    "$pkgdir/usr/share/applications/$_pkgname.desktop"
}

sha1sums=('1b721969d6a6ed0f84529a29cfff0a05aee015ab'
          'a61b126b40f2452400a073bb69725e669371db1d'
          '01ee8f212add79a158dcd4ed78d0ea1324bdc59b')

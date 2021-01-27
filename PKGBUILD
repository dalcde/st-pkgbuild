pkgname=st-own
pkgver=0.8.4
pkgrel=1
pkgdesc='Simple virtual terminal emulator for X'
url='http://st.suckless.org/'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft')
source=(https://dl.suckless.org/st/st-$pkgver.tar.gz
        https://st.suckless.org/patches/scrollback/st-scrollback-$pkgver.diff
        config.h)
sha256sums=('d42d3ceceb4d6a65e32e90a5336e3d446db612c3fbd9ebc1780bc6c9a03346a6'
            '418e1c5df11105482f13a008218c89eadb974630c25b4a6ff3da763dc2560e44'
            'SKIP')
_sourcedir=st-$pkgver

prepare() {
  cd "$_sourcedir"
  sed -i '/^\ttic/d' Makefile
  cp "$srcdir/config.h" .
  patch -Np1 <"$srcdir/"*.diff
}

build() {
  cd "$_sourcedir"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "$_sourcedir"
  make PREFIX=/usr DESTDIR="${pkgdir}" install
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/st/LICENSE"
  install -Dm644 README "${pkgdir}/usr/share/doc/st/README"
}

# Maintainer: Ong Kuan Yang <ongkuanyang [at] gmail [dot] com>

pkgname=evince-xps
pkgver=3.0.2
pkgrel=1
pkgdesc="Document viewer compiled with additional xps support"
url="http://projects.gnome.org/evince/"
arch=('i686' 'x86_64')
license=('GPL')
depends=('gtk3' 'libspectre' 'gsfonts' 'poppler-glib' 'djvulibre' 'gnome-icon-theme'
         't1lib' 'libgnome-keyring' 'desktop-file-utils' 'dconf' 'gsettings-desktop-schemas' 'libgxps-git')
makedepends=('gnome-doc-utils' 'nautilus' 'texlive-bin' 'intltool' 'gobject-introspection')
optdepends=('texlive-bin: DVI support')
install=evince.install
options=('!libtool' '!emptydirs')
provides=('evince=3.0.2')
conflicts=('evince')
source=(http://ftp.gnome.org/pub/gnome/sources/evince/${pkgver%.*}/evince-${pkgver}.tar.bz2
        introspection-fix.patch)
sha256sums=('03abb74620caaa255f2d1369b684bbf8f62e15a4bf2d9f2a45f58e1789295a97'
            '897b8c77c5cda31f4f8d860cd6a7ad8ad986dbf3cf26b56acf054cc650e94be1')

build() {
  cd "${srcdir}/evince-${pkgver}"

  patch -Np1 -i "${srcdir}/introspection-fix.patch"
  autoreconf -fi

  ./configure --prefix=/usr   --sysconfdir=/etc \
      --localstatedir=/var    --libexecdir=/usr/lib/evince \
      --disable-static        --enable-nautilus \
      --enable-pdf            --enable-tiff \
      --enable-djvu           --enable-dvi \
      --enable-t1lib          --enable-comics \
      --disable-scrollkeeper  --disable-schemas-compile \
      --enable-introspection  --enable-xps
  make
}

package() {
  cd "${srcdir}/evince-${pkgver}"
  make DESTDIR="${pkgdir}" install
}

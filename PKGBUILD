# Maintainer:

pkgname=st
pkgver=1.0
pkgrel=1
pkgdesc="st"
url='https://github.com/DerGeist/st'
arch=('x86_64')
license=('MIT')
options=('zipman')
depends=('libxft')
provides=(st)
conflicts=(st)
makedepends=('ncurses' 'libxext' 'git')
optdepends=('dmenu: feed urls to dmenu')
source=('git+https://github.com/DerGeist/st')
sha1sums=('SKIP')

prepare() {
	cd ${pkgname}
	echo "CPPFLAGS+=${CPPFLAGS}" >> config.mk
	echo "CFLAGS+=${CFLAGS}" >> config.mk
	echo "LDFLAGS+=${LDFLAGS}" >> config.mk
	# to use a custom config.h, place it in the package directory
	if [[ -f ${SRCDEST}/config.h ]]; then
		cp "${SRCDEST}/config.h" .
	fi
	# skip terminfo which conflicts with ncurses
	sed -i '/tic /d' Makefile
}

build() {
	cd ${pkgname}
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd "${_pkgname}"
	make PREFIX=/usr DESTDIR="${pkgdir}" install
	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

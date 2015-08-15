# Maintainer: Xentec <artificial.i7 at gmail dot com>
_pkgname=glbindings
pkgname=glbindings-git
pkgver=1.0.0
pkgrel=1
pkgdesc="A generated C++ binding for the OpenGL API, generated using the gl.xml specification. (git version)"
arch=('i686' 'x86_64')
url="https://github.com/hpicgs/glbinding"
license=('MIT')
depends=('libgl')
makedepends=('cmake' 'git')
source=("$_pkgname"::'git+https://github.com/hpicgs/glbinding.git')
md5sums=('SKIP')

pkgver() {
	cd "$srcdir/$_pkgname"
	git describe --long | sed -r 's/([^-]*-g)/r\1/;s/-/./g'
}

build() {
	cd "$srcdir/$_pkgname"
	mkdir build
	cmake \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DOPTION_BUILD_TESTS=OFF \
		-DOPTION_BUILD_STATIC=OFF \
		-Wno-dev \
		.
	make
}

package() {
	cd "$srcdir/$_pkgname"

	make DESTDIR="$pkgdir" install

	rm -r "${pkgdir}/usr/share/"

	install -D -m644 glbinding-config.cmake "${pkgdir}/usr/lib/cmake/${_pkgname}/glbinding-config.cmake"
	install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
}


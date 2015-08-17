# Contributer: Meow (meow at linux dot cn)

pkgname=rkward-svn
pkgver=4566
pkgrel=1
pkgdesc="An Easy to use, transparent frontend to the R-language"
arch=('i686' 'x86_64')
url="http://rkward.sourceforge.net/"
license=('GPL')
depends=('kdelibs' 'qt4>=4.3' 'r>=2.9' 'docbook-xml' 'kdebase-katepart')
makedepends=('cmake' 'automoc4' 'docbook-xsl' 'subversion')
provides=('rkward')
conflicts=('kdemod-rkward' 'rkward')
install=rkward-svn.install
#_svntrunk=https://rkward.svn.sourceforge.net/svnroot/rkward/trunk/rkward
_svntrunk=http://svn.code.sf.net/p/rkward/code/trunk/rkward
_svnmod=rkward

build() {
	cd "$srcdir"
	if [ -d $_svnmod/.svn ]; then
		(cd $_svnmod && svn up -r $pkgver)
	else
		svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
	fi

	msg "SVN checkout done or server timeout"
	msg "Starting make..."

	install -dm755 "$srcdir/$_svnmod/build"
	cd "$srcdir/$_svnmod/build"

	cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release -DR_LIBDIR=/usr/lib/R/library ..
	make
}

package(){
	cd "$srcdir/$_svnmod/build"
	make DESTDIR="$pkgdir" install

	# Some cleanup
	rm -vf "$pkgdir/usr/lib/R/library/R.css"
	rm -vf "$pkgdir/usr/share/apps/katepart/syntax/r.xml"
}

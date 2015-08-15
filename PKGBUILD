# Maintainer: Voxus Bechill <evix1101@live.com>

pkgname=codelite4-svn
pkgver=6030
pkgrel=1
pkgdesc="CodeLite, an open-source, cross platform IDE for the C/C++ programming languages."
arch=("i686" "x86_64")
license=('GPLv2')
url="http://codelite.org/"
depends=('wxgtk2.9>=2.9.4')
makedepends=('subversion')
conflicts=('codelite' 'codelite-svn')
replaces=('codelite' 'codelite-svn')
provides=('codelite')
source=()
md5sums=()

_svnmod="codelite"
_svntrunk="https://codelite.svn.sourceforge.net/svnroot/codelite/trunk"

build() {
  cd $srcdir/
  msg "Getting source..."
  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn --config-dir ../ up -r $pkgver)
  else
    svn --config-dir ./ co $_svntrunk  -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Creating make environment..."
  rm -rf $srcdir/$_svnmod-build
  cp -r $srcdir/$_svnmod $srcdir/$_svnmod-build
  cd $srcdir/$_svnmod-build

  msg "Starting make..."
  
  WXCONFIG="wx-config-2.9" ./configure --prefix=/usr 
  make || return 1
  make -j1 DESTDIR=$pkgdir install || return 1
    
  rm -rf $srcdir/$_svnmod-build
}

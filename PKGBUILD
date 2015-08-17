# Maintainer: Doug Newgard <scimmia22 at outlook dot com>
# Contributor: furester <furester at gmail dot com>
# Contributor: Changaco <changaco Î±Ï„ changaco Î´Î¿Ï„ net>

pkgname=python2-evas-svn
pkgver=76880
pkgrel=3
pkgdesc="Python2 bindings for Evas"
arch=('i686' 'x86_64')
url="http://www.enlightenment.org"
license=('LGPL2.1')
depends=('python2' 'efl-svn')
makedepends=('subversion' 'cython2')
conflicts=('python2-evas')
provides=('python2-evas')
options=('!libtool' '!emptydirs')

_svntrunk="http://svn.enlightenment.org/svn/e/trunk/BINDINGS/python/python-evas/"
_svnmod="python-evas"

build() {
  cd "$srcdir"

  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  svn export "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  PYTHON=/usr/bin/python2 \
  ./autogen.sh --prefix=/usr

  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir" install

  rm -r "$srcdir/$_svnmod-build"
}

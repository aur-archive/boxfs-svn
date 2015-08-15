# Maintainer: Estanislao Mercadal <ktuludawn at linuxmail dot org>
pkgname=boxfs-svn
pkgver=90
pkgrel=1
pkgdesc="A FUSE filesystem to access files on your box.net account"
arch=('i686' 'x86_64')
url="http://code.google.com/p/boxfs/"
license=('GPL')
depends=('fuse' 'libapp-git' 'libzip' 'libxml2' 'curl')
makedepends=('subversion')
provides=('boxfs')
conflicts=('boxfs')
md5sums=()

_svntrunk=http://boxfs.googlecode.com/svn/trunk/
_svnmod=boxfs

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
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  mkdir -p "$pkgdir/usr/bin"
  make PREFIX="$pkgdir/usr" install
  rm -rf $(find "$pkgdir" -type d -name ".svn")
}

# vim:set ts=2 sw=2 et:

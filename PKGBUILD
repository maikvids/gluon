pkgname=gluon
pkgver=0.71.0
_pkgver=0.71
pkgrel=1
pkgdesc="A free and open source platform for creating and distributing games"
arch=('x86_64')
url="http://gluon.gamingfreedom.org/"
license=('LGPL')
depends=('kdelibs' 'libsndfile' 'alure')
makedepends=('cmake' 'automoc4' 'mesa' 'kdevplatform')
source=("http://download.kde.org/unstable/$pkgname/$_pkgver/src/$pkgname-$pkgver.tar.gz" 'gcc47.patch')
md5sums=('e4f284c0ae00e5b8a58cc3e6201857fe'
         'd06410ed9078eff1c951c20df3fba34f')


build() {
  cd "$srcdir"/$pkgname-$pkgver
  patch -p1 -i "$srcdir"/gcc47.patch


  cd "$srcdir"
  mkdir build
  cd build
  cmake ../$pkgname-$pkgver \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_SKIP_RPATH=ON
  grep -rl "Qt4::moc"|xargs sed -i "s/Qt4::moc/moc/" # No idea what's up here but I can't be bothered to fix it properly
  make
}

package() {
  cd "$srcdir"/build
  make DESTDIR="$pkgdir" install
}

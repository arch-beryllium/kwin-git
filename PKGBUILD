_pkgname=kwin
pkgname=$_pkgname-git
pkgver=r18780.70458eb28
pkgrel=1
pkgdesc='An easy to use, but flexible, composited Window Manager'
arch=(x86_64 aarch64)
url='https://www.kde.org/workspaces/plasmadesktop/'
license=(LGPL)
depends=(kscreenlocker-git xcb-util-cursor plasma-framework-git kcmutils-git breeze-git kinit-git qt5-sensors qt5-script krunner-git kwayland-server-git lcms2 xorg-xwayland libqaccessibilityclient)
makedepends=(extra-cmake-modules-git qt5-tools kdoctools-git git)
optdepends=('qt5-virtualkeyboard: virtual keyboard support for kwin-wayland')
provides=(kwin)
conflicts=(kwin)
#groups=(plasma)
source=("git+https://github.com/KDE/$_pkgname")
install=kwin-git.install
sha256sums=('SKIP')

pkgver() {
  cd $_pkgname
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  mkdir -p build
  cd build
  cmake ../$_pkgname \
    -DCMAKE_INSTALL_LIBEXECDIR=lib \
    -DBUILD_TESTING=OFF
  make
}

package() {
  cd build
  make DESTDIR="$pkgdir" install
}

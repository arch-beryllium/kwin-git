_pkgname=kwin
pkgname=$_pkgname-git
pkgver=r19026.1f7e794b8
pkgrel=1
pkgdesc='An easy to use, but flexible, composited Window Manager'
arch=(x86_64 aarch64)
url='https://www.kde.org/workspaces/plasmadesktop/'
license=(LGPL)
depends=(kscreenlocker xcb-util-cursor plasma-framework kcmutils breeze kinit qt5-sensors qt5-script krunner kwayland-server lcms2 xorg-xwayland libqaccessibilityclient)
makedepends=(extra-cmake-modules qt5-tools kdoctools git)
optdepends=('qt5-virtualkeyboard: virtual keyboard support for kwin-wayland')
provides=(kwin)
conflicts=(kwin)
#groups=(plasma)
source=(
  "git+https://github.com/KDE/$_pkgname"
  "disable-pipewire.patch"
)
install=kwin-git.install
sha256sums=(
  'SKIP'
  'd7156f817385853331ac32255fc7e55832f133047c701a8c6affed77c5afe941'
)

pkgver() {
  cd $_pkgname
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd kwin
  patch -Np1 -i "${srcdir}/disable-pipewire.patch"
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

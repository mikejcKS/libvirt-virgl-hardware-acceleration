# Maintainer: Reza Jahanbakhshi <reza.jahanbakhshi at gmail dot com

pkgname=virglrenderer-git
pkgver=virglrenderer_1.1.0_65_g4a6af313
pkgrel=1
pkgdesc="A virtual 3D GPU library, that allows the guest operating system to use the host GPU to accelerate 3D rendering, git version"
arch=('x86_64')
url="https://virgil3d.github.io/"
license=('MIT')
depends=(libepoxy mesa)
makedepends=(python python-yaml meson ninja vulkan-headers libva vulkan-icd-loader mesa check libepoxy)
checkdepends=(check)
provides=('virglrenderer')
conflicts=('virglrenderer')
source=('virglrenderer::git+https://gitlab.freedesktop.org/virgl/virglrenderer.git')
md5sums=('SKIP')
sha512sums=('SKIP')

pkgver() {
  cd virglrenderer
  _ver=$(git describe --tags)
  echo ${_ver//-/_}
}

prepare() {
  cd virglrenderer
  if [  -d build ]; then
    rm -rf build
  fi
}

build () {
  cd virglrenderer
  meson --prefix=/usr build -Dvenus=true -Dvideo=true -Ddrm-renderers=amdgpu-experimental # -Dtests=true
  ninja -C build
}

check() {
  cd virglrenderer
  #ninja -C build test  TODO: figure out why tests fail in chroot environment
}

package() {
  cd virglrenderer
  DESTDIR="$pkgdir" ninja -C build install
  install -D -m644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}

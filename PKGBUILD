buildarch=4

pkgname=libcec-imx6
pkgver=13.20150519
pkgrel=1
pkgdesc="Pulse-Eight's libcec for the Pulse-Eight USB-CEC adapter with support for i.MX6 based devices. IMX changes from https://github.com/xbmc-imx6/libcec."
arch=('armv7h')
url="https://github.com/Pulse-Eight/libcec"
license=('GPL')
depends=('udev' 'lockdev' 'libplatform')
conflicts=('libcec')
provides=('libcec')
makedepends=('git')

# libcec modified by Stephan "wolfgar" Rafin
_gitname="libcec-imx6"
_gitroot="https://github.com/zpon/"
_gitbranch="master"

prepare() {
  cd "${srcdir}"


  msg2 "Connecting to GIT server..."
  
  if [[ -d "${_gitname}" ]]; then
     cd "${_gitname}" && git pull origin "$_gitbranch"
     msg2 "The local files are updated."
  else
     git clone --recursive --branch ${_gitbranch} --depth 1 "${_gitroot}/${_gitname}"
  fi
  
  msg2 "GIT checkout done or server timeout." 
}

build() {
  cd "${srcdir}/${_gitname}"

  if [ -d build ] ; then
    rm -r build
  fi

  mkdir build
  cd build
  cmake -DCMAKE_INSTALL_PREFIX=/usr -DBUILD_SHARED_LIBS=1 -DHAVE_IMX_API=1 ..
  make
}

package() {
  cd "${srcdir}/${_gitname}"
  cd build
  # Running make install
  make DESTDIR="${pkgdir}" install
}

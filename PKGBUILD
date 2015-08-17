# Maintainer: glitsj16 <glitsj16 at gmail dot com>
# Contributor: Nathan Osman  <nathan at quickmediasolutions dot com>

pkgname=nitroshare-git
pkgver=0.3.r402.g2b1ebe1
pkgrel=1
pkgdesc="Network File Transfer Application"
arch=('i686' 'x86_64')
url="http://nitroshare.net"
license=('MIT')
depends=('libnotify' 'qt5-base' 'qt5-svg')
optdepends=('libappindicator-gtk2: appindicator support for Unity and GNOME')
makedepends=('clang')
conflicts=('nitroshare')
install=nitroshare.install
source=('git+https://github.com/nitroshare/nitroshare-desktop.git' 'nitroshare.install' 'nitroshare.ufw')
sha512sums=('SKIP'
    'c451aa7f357cc49936a5de9d3620cc5872dd1f0e3dc7451b3034d2142fbf13dbe97b89f6cfac27bb73ce7f350013f4e7356ba902e61cc59d2d0dd1e34dc956fc'

    '10a946318df603b96abb94d3137b205895bd00305ae238ccf1d39059db866cc73ea31781692f6f7b136932ced022760077b57fbbfc017bc49af453f266b67657')

_gitname=nitroshare-desktop

pkgver() {
	cd "$_gitname"
    version_major=$(cat ./nitroshare.pri | grep -m 1 MAJOR | awk '{split($0,a," "); print a[3]}')
    version_minor=$(cat ./nitroshare.pri | grep -m 1 MINOR | awk '{split($0,a," "); print a[3]}')
    echo "${version_major}.${version_minor}.r$(git rev-list --count master).g$(git log -1 --format="%h")"
}

build () {
    cd "$_gitname"
	qmake-qt5
	make
}

package (){
    cd "$_gitname"
    strip out/install/nitroshare
    INSTALL_ROOT="${pkgdir}/usr/" make install

    # Test if UFW is installed
    which ufw > /dev/null
    if [ $? -eq 0 ]; then
        # install ufw config files
        install -Dm 644 ../nitroshare.ufw "$pkgdir/etc/ufw/applications.d/ufw-nitroshare"
    fi

    # install license
	install -Dm644 LICENSE.txt "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

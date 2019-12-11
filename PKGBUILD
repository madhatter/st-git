# Maintainer: Arvid Warnecke <madhatter@nostalgix.org>
# Contributor: Tarmo Heiskanen <turskii@gmail.com>
# Contributor: mar77i <mar77i at mar77i dot ch>
# Contributor: Gaetan Bisson <bisson@archlinux.org>
# Contributor: Scytrin dai Kinthra <scytrin@gmail.com>

pkgname=st-git
pkgver=0.8.2.r25.g3848301
pkgrel=1
pkgdesc='Simple virtual terminal emulator for X'
url='https://st.suckless.org/'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft')
makedepends=('ncurses' 'libxext' 'git')
source=('git://git.suckless.org/st')
_patches=('st-alpha-0.8.2.diff')
source=(${source[@]} ${_patches[@]})
sha1sums=('SKIP'
          'SKIP')
provides=("st")
conflicts=("st")


pkgver() {
    cd "${srcdir}/st"
    git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
    cd "${srcdir}/st"

    for p in "${_patches[@]}"; do
        echo "=> $p"
        patch < ../$p || return 1
    done

    echo 'Copying config.def.h to $startdir...'
    cp config.def.h "${startdir}/"

    echo 'Copying config.h from $startdir if it exists...'
    [ -f "${startdir}/config.h" ] && cp "${startdir}/config.h" . ; echo "Done." || true
}

build() {
    cd "${srcdir}/st"

    make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
    cd "${srcdir}/st"

    make PREFIX=/usr DESTDIR="${pkgdir}" TERMINFO="/dev/null" install
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    install -Dm644 README "${pkgdir}/usr/share/doc/${pkgname}/README"
}

# Maintainer: Limao Luo <luolimao+AUR@gmail.com>
# Contributor: Jon Sturm <Jasturm002@aol.com>

_pkgname=tilp
pkgname=$_pkgname-svn
pkgver=1.17.4505
pkgrel=1
pkgdesc="TI graphing calculator link/transfer program"
arch=(i686 x86_64)
url=http://tilp.info/
license=(GPL2)
depends=(desktop-file-utils libglade 'libticalcs=1.1.8')
makedepends=(intltool subversion)
optdepends=('gfm: to manage and manipulate TI Group Files (backups)')
provides=($_pkgname=$pkgver)
conflicts=($_pkgname)
options=(!libtool)
install=$pkgname.install
source=($pkgname::svn+http://svn.tilp.info/repos/tilp/$_pkgname/trunk
    $pkgname.desktop
    $pkgname.xml)
sha256sums=('SKIP'
    '004443e1c21ee7931bfe74052d7828312e9303681aac50a97c7d6af5cabd3214'
    '2bf00c9a5abc1c9ab989071b1eec2602b39a030052c538b111030da3db9c5a42')
sha512sums=('SKIP'
    '25a0bf3c3fa4dae1cf553304ad180f5f5dc604a2950153b71df43b05f1cd4a2654f32312f46fa9b20b28c03450993cb9afdcce5afa2f3eabc13c11906e21f66a'
    '386cbd8d2f850c755f1e34f0c5a8b12a25fa236a49d969e07cbb30483fe741e98fd0f533e499d9cf73df135682a2825c2a2fdbc4c3c91889b26d905e512424d0')

pkgver() {
    echo $(grep -o 'version [0-9.]\+' -m1 $pkgname/ChangeLog | tr -d '[a-zA-Z ]').$(svnversion "$SRCDEST"/$pkgname/)
}

prepare() {
    cd $pkgname/
    sed -i 's:.*serial.*::g' acinclude.m4
    echo '# serial 1' > acinclude.m4.new
    cat acinclude.m4 >> acinclude.m4.new
    mv acinclude.m4{.new,}
}

build() {
    cd $pkgname/
    autoreconf -fi
    #KDE users can remove the --without-kde option to enable kde file dialogs
    ./configure --prefix=/usr --without-kde
    make
}

package() {
    make -C $pkgname DESTDIR="$pkgdir" install
    desktop-file-install $pkgname.desktop --dir "$pkgdir"/usr/share/applications/
    install -Dm644 $pkgname.xml "$pkgdir"/usr/share/mime/packages/$_pkgname.xml
}

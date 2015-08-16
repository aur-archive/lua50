
# Maintainer: Alexandre Becoulet <alexandre.becoulet@free.fr>

pkgname=lua50
pkgver=5.0.3
pkgrel=3
pkgdesc='A powerful light-weight programming language designed for extending applications'
arch=('i686' 'x86_64')
url='http://www.lua.org/manual/5.0/'
license=('MIT')
source=("http://www.lua.org/ftp/lua-$pkgver.tar.gz")

build() {
    cd lua-$pkgver

    for i in Makefile src/Makefile src/lib/Makefile src/lua/Makefile src/luac/Makefile ; do
        sed -e "s:\bliblua\.:liblua5.0.:g" \
            -e "s:-llua\b:-llua5.0:g" \
    	    -e "s:\bliblualib\.:liblualib5.0.:g" \
            -e "s:-llualib\b:-llualib5.0:g" -i "$i"
    done

    make MYCFLAGS="-fPIC $CFLAGS" MYLDFLAGS="$LDFLAGS" all || return 1
    make MYCFLAGS="-fPIC $CFLAGS" MYLDFLAGS="$LDFLAGS" so || return 1
}

package() {
    cd lua-$pkgver

    mkdir -p "$pkgdir/usr/bin" "$pkgdir/usr/include/lua5.0" "$pkgdir/usr/lib" "$pkgdir/usr/man/man1"
    make INSTALL_ROOT="$pkgdir/usr" install soinstall || return 1

    mv $pkgdir/usr/bin/lua $pkgdir/usr/bin/lua5.0
    mv $pkgdir/usr/bin/luac $pkgdir/usr/bin/luac5.0
    mv $pkgdir/usr/include/*.h $pkgdir/usr/include/lua5.0
    mv $pkgdir/usr/man/man1/luac.1 $pkgdir/usr/man/man1/luac5.0.1
    mv $pkgdir/usr/man/man1/lua.1 $pkgdir/usr/man/man1/lua5.0.1
}

md5sums=('feee27132056de2949ce499b0ef4c480')

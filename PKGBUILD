pkgname=("factorio-server")
pkgver="1.1.91"
pkgrel="1"
pkgdesc="Headless Factorio multiplayer server"
url="https://www.factorio.com"
source=(
    "$pkgname.tar.xz::https://factorio.com/get-download/stable/headless/linux64"
    "factorio.conf"
    "$pkgname@.service"
)
md5sums=(
    "f9b27654c3c47b34de3a8eb62f0b20df"
    "9bf8114e5e3c1c27842440d578ef032f"
    "55ff52dfc62c471f7efe42aa40ed07c1"
)
arch=("x86_64")
depends=("glibc")
install="$pkgname.install"

package() {
    # install factorio game files
    install -d "$pkgdir/opt/$pkgname"
    install -d "$pkgdir/var/lib/$pkgname"
    cp -r factorio/* "$pkgdir/opt/$pkgname"

    # ensure file permissions are correct
    find "$pkgdir" -type d -exec chmod 755 {} \;
    find "$pkgdir" -type f -exec chmod 644 {} \;
    chmod 755 "$pkgdir/opt/$pkgname/bin/x64/factorio"

    # create server settings file directory
    install -d "$pkgdir/etc/$pkgname"

    # create server logging directory
    install -d "$pkgdir/var/log/$pkgname"

    # create user & group to run as
    install -d "$pkgdir/usr/lib/sysusers.d"
    install "factorio.conf" "$pkgdir/usr/lib/sysusers.d/"

    # install systemd template service
    install -d "$pkgdir/usr/lib/systemd/system"
    install "$pkgname@.service" "$pkgdir/usr/lib/systemd/system/"
}

pkgname=termius
_pkgname=Termius
__pkgname=termius-app
pkgver=8.10.4
pkgrel=2
pkgdesc="Termius is described as 'is more than a mere SSH client – it’s a complete command-line solution that’s redefining remote access for sysadmins and network engineers."
url="https://www.termius.com/"
arch=('x86_64')
license=('custom')
depends=('alsa-lib' 'at-spi2-core' 'cairo' 'dbus' 'expat' 'gcc-libs' 'glib2' 'glibc' 'gtk3'
         'hicolor-icon-theme' 'libcups' 'libdrm' 'libsecret' 'libx11' 'libxcb' 'libxcomposite'
         'libxdamage' 'libteam' 'libxfixes' 'libxkbcommon' 'libxrandr' 'mesa' 'nspr' 'nss' 'pango'
         'systemd' 'wayland' 'zlib')
makedepends=('tar')
optdepends=('xdg-utils: Open files')
source=("${_pkgname}-${pkgver}.deb::https://autoupdate.termius.com/linux/${_pkgname}.deb")
sha512sums=('SKIP')
options=('!strip')

package() {
    msg2 "Unpacking SOURCE files of the downloaded DEB binary package "
    mkdir -p "${pkgdir}/"
    bsdtar -xf "${srcdir}/data.tar.xz" -C "${pkgdir}/"
    gunzip "${pkgdir}/usr/share/doc/termius-app/changelog.gz"

    msg2 "Removing unnecessary file properties from the RPM binary package"
	rm -fdrv "${pkgdir}/etc/"

	msg2 "Linking LICENSEs from source to the system"
    install -d "${pkgdir}/usr/share/licenses/${pkgname}/"
    ln -v -s "/opt/${_pkgname}/LICENSE.electron.txt" -t "${pkgdir}/usr/share/licenses/${pkgname}/"
    ln -v -s "/opt/${_pkgname}/LICENSES.chromium.html" -t "${pkgdir}/usr/share/licenses/${pkgname}/"

    msg2 "Linking runable binary file from source to the system"
    install -dm755 "${pkgdir}/usr/bin/"
    ln -v -s "/opt/${_pkgname}/${__pkgname}" "${pkgdir}/usr/bin/${pkgname}"

    msg2 "Impose sandboxing by modifying SUID properties"
    chmod 755 "${pkgdir}/opt/${_pkgname}/${__pkgname}"
    chmod u+s "${pkgdir}/opt/${_pkgname}/chrome-sandbox" || true
        msg2 "NOTE: AUTOmatic LIGHT/DARK Theme switching does not work for some reason . . ."
}

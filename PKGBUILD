pkgname=termius
_pkgname=Termius
__pkgname=termius-app
pkgver=8.10.4
pkgrel=1
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
options=('strip')

prepare() {
    bsdtar -xf "${srcdir}/${_pkgname}-${pkgver}.deb"

    rm -fdrv "./control.tar.gz" "./debian-binary"

    tar -xf "${srcdir}/data.tar.xz"

    rm -fdrv "${srcdir}/etc/"

    gzip -d "${srcdir}/usr/share/doc/${__pkgname}/changelog.gz"
}
package() {

    install -d "${pkgdir}/opt/${_pkgname}/"
    cp -a "${srcdir}/opt/${_pkgname}/" -t "${pkgdir}/opt/"

    chmod 755 "${pkgdir}/opt/${_pkgname}/${__pkgname}"
    chmod u+s "${pkgdir}/opt/${_pkgname}/chrome-sandbox" || true

    install -d "${pkgdir}/usr/share/applications/"
    cp -a "${srcdir}/usr/share/applications/${__pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"

    install -d "${pkgdir}/usr/share/icons/hicolor/512x512/apps/"
    cp -a "${srcdir}/usr/share/icons/hicolor/512x512/apps/${__pkgname}.png" -t "${pkgdir}/usr/share/icons/hicolor/512x512/apps/"

    install -d "${pkgdir}/usr/share/doc/${pkgname}/"
    cp -a "${srcdir}/usr/share/doc/${__pkgname}/changelog" -t "${pkgdir}/usr/share/doc/${pkgname}/"

    install -d "${pkgdir}/usr/share/licenses/${pkgname}/"
    cp -a "${srcdir}/opt/${_pkgname}/LICENSE.electron.txt" -t "${pkgdir}/usr/share/licenses/${pkgname}/"
    cp -a "${srcdir}/opt/${_pkgname}/LICENSES.chromium.html" -t "${pkgdir}/usr/share/licenses/${pkgname}/"

    install -d "${pkgdir}/usr/bin/"
    ln -s "/opt/${_pkgname}/${__pkgname}" "${pkgdir}/usr/bin/${pkgname}"
}

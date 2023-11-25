pkgname=termius
pkgver=8.6.1
pkgrel=1
pkgdesc="Desktop SSH Client"
url="https://www.termius.com/"
arch=('x86_64')
license=('custom')
depends=('at-spi2-core' 'dbus' 'e2fsprogs' 'expat' 'gtk3' 'keyutils' 'libbsd' 'libnotify' 'libsecret' 'libxss' 'libxtst' 'nss' 'util-linux' 'xdg-utils')
makedepends=('squashfs-tools')
source=(
    "${pkgname}-${pkgver}.snap::https://api.snapcraft.io/api/v1/snaps/download/WkTBXwoX81rBe3s3OTt3EiiLKBx2QhuS_169.snap"
    "termius.desktop"
    "tos.html")
sha512sums=('SKIP' 'SKIP' 'SKIP')

prepare() {
    mkdir -p ${pkgname}
    unsquashfs -f -d ${pkgname} ${pkgname}-${pkgver}.snap
}

package() {
    # Option 1 - copy only the needed files ~183 MiB
    mkdir -p "${pkgdir}"/opt/${pkgname}

    cd "${srcdir}"/${pkgname}

    cp -r \
        chrome_100_percent.pak \
        chrome_200_percent.pak \
        chrome_crashpad_handler \
        icudtl.dat \
        libEGL.so \
        libffmpeg.so \
        libGLESv2.so \
        libvk_swiftshader.so \
        libvulkan.so.1 \
        locales \
        resources \
        resources.pak \
        termius-app \
        v8_context_snapshot.bin \
        vk_swiftshader_icd.json \
        "${pkgdir}"/opt/${pkgname}
    
    cd "${srcdir}"
    # Option 2 - copy all files from the .snap file ~503 MiB
    #mkdir -p "${pkgdir}"/opt/
    #cp -r "${srcdir}"/${pkgname} "${pkgdir}"/opt/${pkgname}

    find "${pkgdir}"/opt/${pkgname}/ -type f -exec chmod 644 {} \;
    chmod 755 "${pkgdir}"/opt/${pkgname}/termius-app
    chmod 755 "${pkgdir}"/opt/${pkgname}/chrome_crashpad_handler

    mkdir -p "${pkgdir}"/usr/bin
    ln -sf /opt/${pkgname}/termius-app "${pkgdir}"/usr/bin/${pkgname}
    install -Dm0644 tos.html "${pkgdir}"/usr/share/licenses/${pkgname}/tos.html
    install -Dm0644 ${pkgname}.desktop "${pkgdir}"/usr/share/applications/${pkgname}.desktop
    install -Dm0644 ${pkgname}/meta/gui/icon.png "${pkgdir}"/usr/share/pixmaps/${pkgname}.png
}

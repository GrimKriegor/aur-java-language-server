# Maintainer: Ricardo Grim Cabrita <grimkriegor@krutt.org>

pkgname=java-language-server
pkgver=0.2.30
pkgrel=3
pkgdesc="Java language server using the Java compiler API"
arch=(any)
url="https://github.com/georgewfraser/java-language-server"
license=('MIT')
provides=('java-language-server')
depends=('java-runtime=13')
makedepends=('maven' 'java-environment=13')
source=("${url}/archive/v${pkgver}.tar.gz"
        "launcher.sh")
sha256sums=('90fe1ca3c6731fcda6234c36cc604e29e99ba707ccb3e2cd3aeb1c8ffa9bb9c2'
            '26eb4214d744c16cd4e8976e495f6cad8c7c98d4ffad3ec79b71b6241e0a1bbf')

build() {
    export JAVA_HOME="/usr/lib/jvm/java-13-openjdk"
    cd "${srcdir}/${pkgname}-${pkgver}"
    ./scripts/link_linux.sh
    mvn package -DskipTests
}

package() {
    mkdir -p \
      "${pkgdir}/usr/share/java" \
      "${pkgdir}/usr/bin"
    cp -r \
      "${srcdir}/${pkgname}-${pkgver}/dist" \
      "${pkgdir}/usr/share/java/java-language-server"
    install \
      "${srcdir}/launcher.sh" \
      "${pkgdir}/usr/bin/java-language-server"
}

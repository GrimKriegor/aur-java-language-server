# Maintainer: Ricardo Grim Cabrita <grimkriegor@krutt.org>

pkgname=java-language-server-git
_pkgname=java-language-server
pkgver=0.2.32.r1613.b7567130
pkgrel=1
pkgdesc="Java language server using the Java compiler API"
arch=('any')
url="https://github.com/georgewfraser/java-language-server.git"
license=('MIT')
conflicts=('java-language-server')
provides=('java-language-server')
depends=('java-runtime=13')
makedepends=('java-environment=13' 'maven' 'git')
source=("${_pkgname}::git+${url}"
        "launcher.sh")
sha256sums=('SKIP'
            '26eb4214d744c16cd4e8976e495f6cad8c7c98d4ffad3ec79b71b6241e0a1bbf')


pkgver() {
  cd "$_pkgname"
  printf "%s.r%s.%s" \
    "$(sed -nE 's/^\s*"version": "(.*?)",$/\1/p' package.json)" \
    "$(git rev-list --count HEAD)" \
    "$(git rev-parse --short HEAD)"
}

build() {
    export JAVA_HOME="/usr/lib/jvm/java-13-openjdk"
    cd "${srcdir}/${_pkgname}"
    ./scripts/link_linux.sh
    mvn package -DskipTests
}

package() {
    mkdir -p \
      "${pkgdir}/usr/share/java" \
      "${pkgdir}/usr/bin"
    cp -r \
      "${srcdir}/${_pkgname}/dist" \
      "${pkgdir}/usr/share/java/java-language-server"
    install \
      "${srcdir}/launcher.sh" \
      "${pkgdir}/usr/bin/java-language-server"
}

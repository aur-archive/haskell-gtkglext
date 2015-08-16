# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=gtkglext
pkgname=haskell-gtkglext
pkgver=0.12.0
pkgrel=3
pkgdesc="Binding to the GTK+ OpenGL Extension"
url="http://hackage.haskell.org/package/${_hkgname}"
license=('LGPL-2.1')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-array=0.3.0.1' 'haskell-cairo<0.13' 'haskell-containers=0.3.0.0' 'haskell-glib<0.13' 'haskell-gtk<0.13' 'haskell-haskell98=1.0.1.1' 'haskell-mtl' 'haskell-pango<0.13' 'gtkglext' 'gtk2hs-buildtools' 'gtk2hs-buildtools' 'gtk2hs-buildtools')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
}
md5sums=('f5a262739f454c8d48beb2cd3f25ab6c')

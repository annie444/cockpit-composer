# Maintainer: Achilleas Koutsou <achilleas@koutsou.net>

pkgname=cockpit-composer
pkgdesc='Composer generates custom images suitable for deploying systems or uploading to the cloud. It integrates into Cockpit as a frontend for osbuild.'
pkgver=47
pkgrel=1
url="https://www.osbuild.org"
arch=(x86_64)
license=(Apache)
depends=('dnf' 'qemu' 'osbuild' 'osbuild-composer' 'cockpit')
makedepends=('nodejs' 'npm' 'appstream-glib')
checkdepends=('npm')
optdepends=()
source=($pkgname-$pkgver.tar.gz::https://github.com/osbuild/${pkgname}/releases/download/${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha256sums=('fbf77f1b510e3d603adff30a85d5811343f3662df3c9f40037f78a967b221abc')

build() {
  cd $pkgname
  npm ci
  npm run build:prod
}

package() {
  cd $pkgname

  # sources
  install -Dm644 "public/*" "${pkgdir}/usr/share/cockpit/composer"
  mkdir -p "${pkgdir}/usr/share/metainfo/"
  appstream-util validate-relax --nonet public/io.weldr.cockpit-composer.metainfo.xml
  install -Dm644 "public/io.weldr.cockpit-composer.metainfo.xml" "${pkgdir}/usr/share/metainfo/" 
  
  # license
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

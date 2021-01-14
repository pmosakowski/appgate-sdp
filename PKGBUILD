# Maintainer: Pawel Mosakowski <pawel at mosakowski dot net>
# Maintainer: Fredy García <frealgagu at gmail dot com>

pkgname=appgate-sdp
pkgver=5.3.1
pkgrel=2
pkgdesc="Appgate SDP (Software Defined Perimeter) desktop client"
arch=("x86_64")
url="https://www.${pkgname%%-*}.com/support/software-defined-perimeter-support"
license=("custom" "custom:commercial")
depends=("dnsmasq" "gtk3" "libsecret" "libxss" "nodejs" "nss" "python-dbus")
optdepends=("gnome-keyring: saves the endpoint certificate between sessions")
provides=("${pkgname}")
conflicts=()
replaces=("${pkgname}-${pkgver%%.*}")
options=(staticlibs)
source=(
  "https://bin.${pkgname}.com/${pkgver%.*}/client/${pkgname}_${pkgver}_amd64.deb"
  "${pkgname}-${pkgname%%-*}driver.service.patch"
  "nm.py.patch"
  "set_dns.patch"
)

options=(staticlibs)

prepare() {
  mkdir "${srcdir}/${pkgname}"
  cd "${srcdir}/${pkgname}"

  bsdtar -xf "${srcdir}/data.tar.xz" -C .

  patch --forward --strip=1 --input"=${srcdir}/${pkgname}-${pkgname%%-*}driver.service.patch"
  patch --forward --strip=1 --input="${srcdir}/nm.py.patch"

  # Remove unnecessary .deb related directory
  rm -rf "${srcdir}/${pkgname}/etc/init.d"
}

package() {

  # Install application files
  cp -dpr "${srcdir}/${pkgname}/"{opt,usr,etc} "${pkgdir}"

  # Install service files
  install -dm755 "${pkgdir}/usr/lib/systemd/system"
  install -Dm644 "${srcdir}/${pkgname}/lib/systemd/system/"* "${pkgdir}/usr/lib/systemd/system/"

  # Install license files
  install -Dm644 "${srcdir}/${pkgname}/usr/share/doc/${pkgname%%-*}/copyright" "${pkgdir}/usr/share/licenses/${pkgname}/copyright"
  install -Dm644 "${srcdir}/${pkgname}/usr/share/doc/${pkgname%%-*}/LICENSE.github" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.github"
  install -Dm644 "${srcdir}/${pkgname}/usr/share/doc/${pkgname%%-*}/LICENSES.chromium.html.bz2" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSES.chromium.html.bz2"
}
md5sums=('9f2d9c3c611c466bd58d7d3401227446'
         'ba0fa926bb539383599d9f097dea6b7e'
         '6a222195c7a5ac9e53b80aa03d0518c9'
         'aa95ad0ba9304cf72ee43779cd28d9a5')

# Maintainer: David Roheim <david dot roheim at gmail dot com>
pkgname=zendframework2-git
pkgver=20130420
pkgrel=1
pkgdesc="An object-oriented framework for PHP - Git"
arch=('any')
url="http://framework.zend.com/"
license=('BSD')
depends=('php')
options=(!strip)
optdepends=('apache: Webserver'
            'mysql: Database'
            'postgresql: Database')
provides=('zendframework2')
conflicts=('zendframework2' 'zendframework2-min')
source=('LICENSE')
sha256sums=('622d505ff584ac32d52f98d2e7859a10b7f95c70fe48340acd2e8b4430d5cbc3')

_gitroot='https://github.com/zendframework/zf2.git'
_gitname='zendframework2'

pkgver() {
  date +%Y%m%d
}

build() {
  cd "${srcdir}"
  msg "Connecting to GIT server...."

  if [[ -d "${_gitname}" ]]; then
    cd "${_gitname}" && git pull origin
    msg "The local files are updated."
  else
    git clone "${_gitroot}" "${_gitname}"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "${srcdir}/${_gitname}-build"
  git clone "${srcdir}/${_gitname}" "${srcdir}/${_gitname}-build"
}

package() {
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/${_gitname}/LICENSE"
  cd "${srcdir}/${_gitname}-build"
  rm -rf .git
  cp -R . "$pkgdir/usr/share/${_gitname}"
  install -d "$pkgdir/usr/bin"
  ln -s "/usr/share/${_gitname}/bin/zf.sh" "$pkgdir/usr/bin/zf2"
}


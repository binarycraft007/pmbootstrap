# Contributor: katt <magunasu.b97@gmail.com>
# Maintainer: fossdd <fossdd@pwned.life>

pkgname=pmbootstrap-git
pkgver=3.3.1.r45.ga80b27d0
pkgrel=1
pkgdesc='Sophisticated chroot/build/flash tool to develop and install postmarketOS (git)'
arch=(any)
url=https://postmarketos.org
license=(GPL-3.0-only)
depends=(python python-argcomplete multipath-tools util-linux)
makedepends=(python-build python-installer python-setuptools python-wheel git)
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=(
	'git+https://gitlab.postmarketos.org/postmarketOS/pmbootstrap.git'
	'0001-support-custom-repo.patch'
	'0002-support-setting-root-size.patch'
)
md5sums=(
	'SKIP'
	'eb2a7654675533414791057dbabf57ec'
	'de92450f2d87bc74a89fdb26ee3942f7'
)

pkgver() {
	cd "${pkgname%-git}"
	git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
	for patch in ../000*.patch; do
		patch -d "${pkgname%-git}" -Np1 -i "$patch"
	done
}

build() {
	cd "${pkgname%-git}"
	python -m build --wheel --no-isolation
}

package() {
	cd "${pkgname%-git}"
	python -m installer --destdir="$pkgdir" dist/*.whl
}

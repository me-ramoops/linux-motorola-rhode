# Reference: <https://postmarketos.org/vendorkernel>
# maintainer="Kultrinhaa_ <pedrootaviopluss@proton.me>"
pkgname=linux-motorola-rhode
pkgver=7.2.1
pkgrel=3
pkgdesc="Mainline Kernel fork for Motorola Moto G52"
arch="aarch64"
_carch="arm64"
_flavor="motorola-rhode"
url="https://kernel.org"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="
	bash
	bc
	bison
	devicepkg-dev
	flex
	openssl-dev
	perl
"

# Source
_repository="linux-v.7.2.1"
_commit="v7.2.1-sm6225"
source="
	linux-v.7.2.1-v7.2.1-sm6225.tar.gz::https://gitlab.postmarketos.org/sm6225-mainline/kernels/linux-v.7.2.1/-/archive/v7.2.1-sm6225/linux-v.7.2.1-v7.2.1-sm6225.tar.gz
	config-$_flavor.aarch64
	0001-arm64-dts-qcom-sm6225-motorola-rhode-Add-device-tree.patch
	0002-pinctrl-qcom-Add-SM6225-TLMM-driver-wiring.patch
	0003-clk-qcom-Add-SM6225-GCC-DISPCC-GPUCC-wiring.patch
	0004-arm64-dts-qcom-sm6225-Use-SM6225-TLMM-compatible.patch
	0005-pinctrl-qcom-sm6225-Drop-missing-remove-callback.patch
"

builddir="$srcdir/$_repository-$_commit"

prepare() {
	default_prepare
	cp "$srcdir/config-$_flavor.$arch" .config
}

build() {
	unset LDFLAGS
	make ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-$_flavor" V=1
}

package() {
	install -Dm644 "$builddir/arch/$_carch/boot/Image.gz" \
		"$pkgdir/boot/vmlinuz"

	make modules_install dtbs_install \
		ARCH="$_carch" \
		INSTALL_PATH="$pkgdir"/boot/ \
		INSTALL_MOD_PATH="$pkgdir" \
		INSTALL_MOD_STRIP=1 \
		INSTALL_DTBS_PATH="$pkgdir"/boot/dtbs
	rm -f "$pkgdir"/lib/modules/*/build "$pkgdir"/lib/modules/*/source

	install -D "$builddir"/include/config/kernel.release \
		"$pkgdir"/usr/share/kernel/$_flavor/kernel.release
}


sha512sums="
5798b6ee63ccc183fdb66e737feb8dd62d811b4374de75943c9ec9081675a94f0b1a5af2988d172429de363c7b94955dad4086195ee936a0232d8de91b755c1a  linux-v.7.2.1-v7.2.1-sm6225.tar.gz
b15649f8192be6ea50ec3a3fb3416632a3208a37ffa4766b42faa37057e43efadc140ced9e427d778d081ac34294f51acdc7d7fe0af5f5f2c1017d5e946f6ecb  config-motorola-rhode.aarch64
f689ad23b7b3c856b8c3a9e127a296e5a6b59f542fdf4a349cbb24a01c1870c571e2d1fe6f2c69db131c4bfd8adafa05cdd994e932a3564fcbd0c6752e410b03  0001-arm64-dts-qcom-sm6225-motorola-rhode-Add-device-tree.patch
0cea53f1a5e0070be7c957f6adfad61b1cefb0c156e3a000f9da4c509a0d0e4c42a9a77532cba5876f33374dd2b3d89cca8124b3b3443b8ff11b0ab3a897ae7b  0002-pinctrl-qcom-Add-SM6225-TLMM-driver-wiring.patch
dd3831649918ef829aa252005b12db53963ea5cba0b4f214bbda3257cfd402904e4d14175fc53f249031e8205581f763a70d0313739cbc8208e12251db59fd00  0003-clk-qcom-Add-SM6225-GCC-DISPCC-GPUCC-wiring.patch
5417699fec574363169be83e7764285c79d44a13cf07bc9f775b56dee66a2b9940da77b654c924f6d5dfb72072d4e92ff0d77102dc0acb2237261a7b5e3ffe0a  0004-arm64-dts-qcom-sm6225-Use-SM6225-TLMM-compatible.patch
0c2eafc682fc0d0a90abd3bdec076cf9d183ca247e11a12c75567522e37ac3bae771b0ac27106de39cd5c3d2c944245d127ee2f9e7702bde0d889b6e13acb411  0005-pinctrl-qcom-sm6225-Drop-missing-remove-callback.patch
"

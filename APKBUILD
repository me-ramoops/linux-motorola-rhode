# Reference: <https://postmarketos.org/vendorkernel>
maintainer="fwlta <monkeyfwlta@protonmail.com>"
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
	0006-drm-panel-Add-motorola-rhode-rm692e5.patch
	0007-drm-msm-Add-sm6225-mdss-match.patch
	0008-input-goodix-berlin-Add-gt9916s-match.patch
	0009-arm64-dts-qcom-sm6225-motorola-rhode-Enable-display-touchscreen.patch
	0010-drm-panel-Add-motorola-rhode-nt37701.patch
	0011-drm-panel-Add-motorola-rhode-vtdr6130.patch
	0012-arm64-dts-qcom-sm6225-motorola-rhode-Enable-charger.patch
	0013-arm64-dts-qcom-sm6225-motorola-rhode-Charger-on-se1.patch
	0014-arm64-dts-qcom-sm6225-motorola-rhode-Fix-sd-detect-polarity.patch
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
8ffe0d041c86e1e13d9a291be593035c2c2ed9bca422de37e52c31062f66cde31393bccf6bdcccf6740ff16978fe3c44157e1719c3e240dbd8b4e62987ce0fc0  config-motorola-rhode.aarch64
60f2142f5f155de7b5197aac2c2c21fc4babbfcc5debbca0518a2222a5f896e24a93ed966170e4925b2706435d7dd97c78f6713f92fada942b0e8a25089d90f5  0001-arm64-dts-qcom-sm6225-motorola-rhode-Add-device-tree.patch
8bf3d0b127296c13d6798457c22ec64d36f10190bb37a05cf5a4fb66fda0f7b98b83a64b6e3c48cf3651e0e9e15abf8a76352d116f096e2c7297fd16e8adfefc  0002-pinctrl-qcom-Add-SM6225-TLMM-driver-wiring.patch
533cce20158a415c5a9b0920d285107751f07e89dec21fc63134d3c05a9df2becad7e26d1a2bd0de9a5ae1c95934d9670597b9e19f111eb4cc1bcc346b91e3e7  0003-clk-qcom-Add-SM6225-GCC-DISPCC-GPUCC-wiring.patch
403d2829e40ca03e1942453948912c6546c015285833052e08245bc30b950b2544c987ee7a697ef258ea7cc6bc706fd78fefa268123f332a0eceac839b11dd71  0004-arm64-dts-qcom-sm6225-Use-SM6225-TLMM-compatible.patch
edc60544bfdecd5926267a8c0946f8e0004846bd6b473b9d942108cb3b73fc9d79fae9795d7bad738bb368b01627cd61e9b367165170e7d56adb2566595ae52e  0005-pinctrl-qcom-sm6225-Drop-missing-remove-callback.patch
80714fb68922aebcf2aaab845dcb781f650f78ec0d8d66ed62756193646573d5551a1ccc4c50d4cbdf9a34b8b14122ce09df45278383798d4aefb29b1e9eab59  0006-drm-panel-Add-motorola-rhode-rm692e5.patch
c33a93bd8b2cafdb0fc3314825b6c925dff084b34bec5c077b5c8787e2b883a3d4c5ea0412ff63055bd47a2b1cb696f3a5750badcd32de662db10ca93d722b0f  0007-drm-msm-Add-sm6225-mdss-match.patch
4232b2f20c047fd5bd038daf0b6b39b6b5f5dc418f16f9ec167f0d7533558218a05d0aca96447e5bc7b28b6d3480f88b4b33b961315a15bf8e99b7fcdc2d13a2  0008-input-goodix-berlin-Add-gt9916s-match.patch
13631bebede9ac520e2c804142cd801d10ded4abb6c5ad597d29f51cea4d57b29f1ff4c82d3265dcab153208b852540c1727b25d6f10a2c20566b50f31102926  0009-arm64-dts-qcom-sm6225-motorola-rhode-Enable-display-touchscreen.patch
d018dfc768c89914e29c5711d7498185cd887f447687ea29061e9f7261eb0b1c566e8a20feef196fb4b58fd952972fed705735ef9f48c146f6abf28ecca12c68  0010-drm-panel-Add-motorola-rhode-nt37701.patch
bae9e7680716c28bc458e37ae791679dd066796972b212b3922ad9b42fcf1df8d796c8195b27388c2ce20a533477ba3341a2fa638fb5c57fcd366822d05a86b4  0011-drm-panel-Add-motorola-rhode-vtdr6130.patch
6bdc5ff1b86969b94df7677b5c646cc32e03902af7ba5e75089beb1d5925d2a663ff5ef87f926ec50ee0646fcd1ecbf73988882e729e69ac6ef0e9fedabfae50  0012-arm64-dts-qcom-sm6225-motorola-rhode-Enable-charger.patch
6c33145e6660591b1eed9a422923e8c2543c203e6a5f2a2f4d87111eeda861567627927a41539d0ae0f4e74575914ed4593d81b8e636cd9e7e028bfe3073eb6b  0013-arm64-dts-qcom-sm6225-motorola-rhode-Charger-on-se1.patch
54093eb6aef63952c31a88673a7c60faebed55c876526bdb285191dc092053f90173496b771ff29daecbd5982c01dc3bc0a60ddcc26f7cb75914906a2ae75874  0014-arm64-dts-qcom-sm6225-motorola-rhode-Fix-sd-detect-polarity.patch
"

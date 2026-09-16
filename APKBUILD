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
c4be78cf0bf8a4e76812463882d22ed084b65259051ec5490c226a9a70b5cd741295c34290905c45da4cf29a8fb0166608c01cac973b5ee485e95921fe79b5e1  0009-arm64-dts-qcom-sm6225-motorola-rhode-Enable-display-touchscreen.patch
76d11650d49f21204bba008c73ad9077dc4cfce61abe9d6333f7956a54ca2f8c1d20230f21cf8080522058c3d478cfb9ed41c1a850795509efe56f8b0d25a819  0010-drm-panel-Add-motorola-rhode-nt37701.patch
3af31874b7db477c93ccb527932d1b2df2feeea16781669f90a27e69df99a549dc8a0b2b752fe69c0b5c9ff565e5299945e83059a8034f852f6470430d42c656  0011-drm-panel-Add-motorola-rhode-vtdr6130.patch
52a71866e2000e04ae705504c5494b1ef784aedeb4ed58e6653a71be1b96e971643991ba5f117c49a2a671d3fc4f563eba315cced9338dc2b20e7eb7b63cb9d5  0012-arm64-dts-qcom-sm6225-motorola-rhode-Enable-charger.patch
bfa6c4f40f40d7394e4d34e4336e84cb5dee60f8610cde8d0743aa6f04f556493dbc480b2f389c5bc394947387c41f9c7fecfff5e8da17084d5a99e956793d2f  0013-arm64-dts-qcom-sm6225-motorola-rhode-Charger-on-se1.patch
bacb40f5255676219eee62c8cfbc2fd68db0dc4f26cc0a94a87f22472cbf1ec904bee001f6b3dc247f3949b7028a60b1aa02027c2ff848c7c23131bf501b6c11  0014-arm64-dts-qcom-sm6225-motorola-rhode-Fix-sd-detect-polarity.patch
"

# Reference: <https://postmarketos.org/vendorkernel>
# maintainer="fwlta <monkeyfwlta@protonmail.com>"
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
42094409948aa53394ffe55f7f2a763e09838cec31050f4b9f22fb22684b4a16596a3d3e9307635fef535b998f719803e3567416cd1ac3d0486cddc2fac1cb78  config-motorola-rhode.aarch64
c2885ef5f98535e30b960248f1b6fa6ced6a891fff2ed9ce1e94e61349138e7f36b84b8a24749fe1b9e2d3341519f5970f964b0abf936922c69be1ae37d5bcd1  0001-arm64-dts-qcom-sm6225-motorola-rhode-Add-device-tree.patch
3824adba1763f7e7df6d715bff299038f9e9274709321d92151e296969586a85af9a567b3db64448963638742e9b12ea4488d974a0b1fda6743b809b7a1b4bdd  0002-pinctrl-qcom-Add-SM6225-TLMM-driver-wiring.patch
9480dd95998ce09d813df42adec8eb1d2ef15f38410ca7ef9e0d7a9768e7bd0e5e009e9bf557891f0a183422de59b4b896ba56eac2b3d67c1773d3d2a9e63c66  0003-clk-qcom-Add-SM6225-GCC-DISPCC-GPUCC-wiring.patch
1540bf4ca4cd1b2c7f80012816cc58d90ee3fdc8f85c6e150e5970c22ef8fd750cf8c682c29e793b11fbd732437e4ca618701f1d66f8968dba86fe494a7585ca  0004-arm64-dts-qcom-sm6225-Use-SM6225-TLMM-compatible.patch
1ea4cfe19fd137c369857f4b4febe574c5f0170540be0eaed2d4cdd07e28fbeeef310cbb3810023458deb0731b3558c53bbd25b0534eb39f486e80ac16f87a14  0005-pinctrl-qcom-sm6225-Drop-missing-remove-callback.patch
f7f70d7476b1a95e97ec71e680b719ecb2d51ae106dd41679690cbe511be875d377b8222d75715af25e6faa1647a53c125b54f905eb79b4cdfda6a8a6c517d0d  0006-drm-panel-Add-motorola-rhode-rm692e5.patch
52a6d5c5676250724b1e377bcec3c2bf23151bd604bc5a0584d333c5148ea06793cc689ad808d28bd475715c659b5826713d7aef21bc56e15ba43fd820f602eb  0007-drm-msm-Add-sm6225-mdss-match.patch
24367ca790e1b23e784b8a91e8ecfed888ccced89c6f97534e37004e8f34a7ce6233e1f82fc8128f7deb5e069eed8a899a8a19d57ce704d3717014d7014f846f  0008-input-goodix-berlin-Add-gt9916s-match.patch
1083427ef4b336f9b3298306fe84f9c281322f3284126ca1b10f345ff0d15eb7d257715a7d1367724efaa3ec99f9540948d7807f5e7b2781b341069cf06c90c4  0009-arm64-dts-qcom-sm6225-motorola-rhode-Enable-display-touchscreen.patch
"

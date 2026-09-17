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
	0015-arm64-dts-qcom-sm6225-motorola-rhode-Use-splash-framebuffer.patch
	0016-arm64-dts-qcom-sm6225-motorola-rhode-Add-missing-board-ids.patch
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
cf962fcd985b45e19b86e0f680b96646bcf38a94d68a4f1869c9579f96b03f0af2fbc0580f1bf44669663df40839af652187c9a1fa79f6e73d37f4166e06980d  0001-arm64-dts-qcom-sm6225-motorola-rhode-Add-device-tree.patch
e7553d2ff3dde86c1248b0ec0f1d67ce728b16cb4bda02b871068749cecef0e23017897d2754a305a8a2cb4cd092b539223b573e7d2eb9eb4e4aab0ed384158b  0002-pinctrl-qcom-Add-SM6225-TLMM-driver-wiring.patch
2d4ed3e8043ef4676685b7b20fad527929b93ad68aa0386b889e8e427a9312a64d0bbfb00522d47103829781a30686859bb9a4b10d115b81a4038cbae6827c15  0003-clk-qcom-Add-SM6225-GCC-DISPCC-GPUCC-wiring.patch
498bf5c53dff1fc78c4d9eccc25d2b08a7a4bf431530c7e1f7027b27c02072e66c04f19f0d8ebec48c0d8620cba1008b68db5afe9402ae48f52be1bc073fac99  0004-arm64-dts-qcom-sm6225-Use-SM6225-TLMM-compatible.patch
f59e1325dc5995f419bf5d4e97329be6647f83084ebf41a3271eb13fecbaa040d7732ac3e4e98adc6f13c7b8898181bbca59c85750ea811260f50949b7dfb56c  0005-pinctrl-qcom-sm6225-Drop-missing-remove-callback.patch
6832f31e1b5be5b6780923afb6d29d5e400409f5411756d56e0e7cb4104be75604f2bd3c8bb05c9678c3bc762958595a3bedbd95417b2f2df3b26dec704ecbbf  0006-drm-panel-Add-motorola-rhode-rm692e5.patch
69b1601e28a2e92e23196d2b5881663c7e8d5fdfb510aab85c4c56f30fc18671b0cb472db9b450b249dd2b0d0574aee784973cc00ed67ca18cb0b22c8e3409b9  0007-drm-msm-Add-sm6225-mdss-match.patch
185f4af33f692cbff15ed7ad4084dd8fe47c29c848abd2a01ed0c84b1b7b2b2095529a02fe1ff012ac4856478bd2ede52affcaf66706bc44eddc6a3f8e7e73c2  0008-input-goodix-berlin-Add-gt9916s-match.patch
08c898a67501e9a9de6ebc0bf9c30d12ac1e2ecfa0ca92a599696cc7f588968181d524ce38763012bf17a22e6368eaf3e8ffadbe5b8c7636ab0621e05b0b1c37  0009-arm64-dts-qcom-sm6225-motorola-rhode-Enable-display-touchscreen.patch
813cddb8037c9da083e08c571ac8ac3ad9f737e81ff56dd36cfecd30e00c8f6edf7c19003ac394d62f7866694b09a10acee80c903d47d32e8760954e0d64e187  0010-drm-panel-Add-motorola-rhode-nt37701.patch
29b5744384de1f5ba91277f060efac6e1e59ad578c57a80751382f4ab9bb2b29b14c9812ce145f215c8bb6d463c2c076898ae17e45951d41d34a122fe2d810f0  0011-drm-panel-Add-motorola-rhode-vtdr6130.patch
4c2a8ff643cd4b973883568298dae598d01defea45631705168137687f76d3f1d426f93f865a364793a6e6aad03ea447b9ccc05833188a737f89578c8a7d71de  0012-arm64-dts-qcom-sm6225-motorola-rhode-Enable-charger.patch
50db52a91966d2dfa2ef899ada6312c6957957e9e4d62c15481924cee95769db42820dcd566dd63e4c04cd7342df0bc47bfdb2cd3e2c6ce0abc1ef16facb43b9  0013-arm64-dts-qcom-sm6225-motorola-rhode-Charger-on-se1.patch
3ee2f26b0c60a814c804d4d72963a8feba849633f570b48dea2871ccbae1fae0c49f934113705e29903a7b5130a6039822102eb1fde08b0c59a95b8030f0b164  0014-arm64-dts-qcom-sm6225-motorola-rhode-Fix-sd-detect-polarity.patch
ab2adcf3be755381af044d399a6e43867a0e2497c4ea98388b5aee0c24b6ec14e17c86b8b4671e15c681eb1cfd1dc7a8b194706c8d0c66e506e0f96d7d2bc8a3  0015-arm64-dts-qcom-sm6225-motorola-rhode-Use-splash-framebuffer.patch
09489d2ef97d6299cd23d4887409852a1451dd74d38d90b60fad499f4daa0047e80f723f8ee408617b2c87eb0ed05dd3d6813f96c243f74b2b594ca230f2bdd9  0016-arm64-dts-qcom-sm6225-motorola-rhode-Add-missing-board-ids.patch
"

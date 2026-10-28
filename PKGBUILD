# Maintainer: ezpcy <batu.s@live.com>
#
# Two fixes for internal audio on the Lenovo Yoga Pro 7 15IPH11 (83SN):
#  - soundwire-83sn-quirk-dkms: backport of the SoundWire ghost-RT722 quirk
#    (upstream 21f4552fbaaf), needed on 7.2/7.3 kernels; upstream from 7.4 on.
#  - alsa-ucm-conf-83sn: alsa-ucm-conf snapshot with the rt721+rt1320 speaker
#    split (upstream ba372ade34), needed until alsa-ucm-conf > 1.2.16.1.
# Each one can be dropped on its own once the fix reaches the official packages.
pkgbase=lenovo-83sn-audio-fix
pkgname=(soundwire-83sn-quirk-dkms alsa-ucm-conf-83sn)
pkgver=1
pkgrel=1
arch=("any")
url="https://github.com/thesofproject/sof/issues/11207"
license=("GPL-2.0-only" "BSD-3-Clause")
makedepends=("git")
_k72=7.2.11
_k73=7.3
_ucmver=1.2.16.1
_ucmcommit=d260eedd1900dbf3b477047e048d5382a5f50e24
_patch=0001-soundwire-dmi-quirks-Disable-ghost-Realtek-on-Lenovo-83SN.patch
# Only drivers/soundwire is needed, so fetch those files instead of two full kernel tarballs
_swfiles=(Kconfig Makefile amd_init.c amd_init.h amd_manager.c amd_manager.h bus.c bus.h
          bus_type.c cadence_master.c cadence_master.h debugfs.c dmi-quirks.c
          generic_bandwidth_allocation.c intel.c intel.h intel_ace2x.c intel_ace2x_debugfs.c
          intel_auxdevice.c intel_auxdevice.h intel_bus_common.c intel_init.c irq.c irq.h
          master.c mipi_disco.c qcom.c slave.c stream.c sysfs_local.h sysfs_slave.c
          sysfs_slave_dpn.c)
_kgit=https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/plain/drivers/soundwire
source=("git+https://github.com/alsa-project/alsa-ucm-conf.git#commit=$_ucmcommit"
        "dkms.conf"
        "$_patch")
for _f in "${_swfiles[@]}"; do
  source+=("$_k72-$_f::$_kgit/$_f?h=v$_k72")
done
for _f in "${_swfiles[@]}"; do
  source+=("$_k73-$_f::$_kgit/$_f?h=v$_k73")
done
sha256sums=('03221e2f07fb06f28efa2184bfdb58e045961388fef4cfa3253ac01b50cba7c1'
            '8eb5c807c14ec13b18e6b9d5a470ab07a0995f9873f1a69d848334611a41bc44'
            '42110cc891cc830b4806868fa74428a468cfcf0d9e358b8291ebead85ae732af'
            '2380e9ef52616eee431edf7b4464886c79e840c0b4a4b552854e7116eb406714'
            'acd72cd33ad377051020654e61b0d66bd2c63787fe44699199938af48a3bbfd4'
            '131079c16825ed07a1c02a2952291b295ac5a1ae80e4fa97160d08146cb14b54'
            'd6c961f8911fe910985bffe00f39e9a0e833b1c03388d264cf3cb72e49b385da'
            '13ead1f7bc55eceea800786db2e6c32e436b323424d28788b02db9dc36b69291'
            'af12d349ba235aa0060947255bc958c3825c18ee42e0f4dc9873b0b5843b264d'
            '3f6f5ea74e40a5759196b403fc5363a6b5a553eb3fc3ba85d0ab322ab0cb965e'
            'c25915dc7b0b0357fd1260229b246c5edbf904e3f956bf8f5d7aa1473fe25663'
            '37e0beb4e399dc0f85e6a46dc0db75dd8929a404f0ff7e0f74ec7cfcf76a3bf1'
            '0513bb7ae19ad5618adf693bda355980a09ba2749e126378b66cdcd2a6c0bb72'
            '835c2a12c11b8d1c3c77f67ac3ea5d29032a1884f634ed819217ed8032ed159c'
            '319abdfd4542bd2d4a4c336da2f1e23eb513e041c891e78fa6eb28b74821e151'
            '2c0183edcf1d1fe3363de1bcda118c6ad5c9489c88756b09eba5afd831743b29'
            '9acc68bd632cecd117361516890827fa3f8595e71b7eb230b63a6facc44ad9ff'
            '587e1e03d13a996e5b5a8e05cb2539ee6668398e5381aa03c29b1b25c5052a0c'
            'cf329077c2f6152b564d825fb7e19e283a4c3c2ff229505ca07f756618bc49d3'
            'bfa59e95ea521bb552382b9f3aedb91fb804c8243ab19fe1db879c77ab558be0'
            '618572e5f5fc9c41a992139a64c72a81337e53d3ddf310f45ae405d144629300'
            'eb758b640d93ebca0075b22256ae6cef6efb1437a9c9ed75dfd1d7b7374c7191'
            '905521bda83191a3878f792cf0582a028be38b290006652aeaf3739bd140ada7'
            'e588d7e9c93fbd24a9870a249904fddde8bbd5adc1484a8e00863fc6575036f6'
            '663796aa4aba10191316772aba5970d0b61fd130ff3f1118d5bd02cd11da88ff'
            '4b360fcc93b3f07e82bebdf208a1df1a6ff375422b20fcc893a2d6f9520924dc'
            '5dcd8bde5481a6f90542c8ef48ae91bad5fdaffb177315c70a3928a06e06a8ba'
            'aaf5a273db4552dc2a3d1803cadc77fb317b41017b7c38254eb4d487ae636154'
            '5787ec3e024d490a196ec0f6fcfa793142bc46ada17aec46d9bcffa10728fcb2'
            'b82de06bc8250f35197d2d4aa5718c14aaadde7f9ed572afeadf6d1e540de2c7'
            'a44d7ef1a0e508303fd4506a0922454957eecf010784eb066d93d977efeb5a21'
            '7d339d26e2bffd79a7ee60fee5b9991e30c426a66f9eed719f16ea9c62526198'
            'd557aa47cc555566d3bf9b9d8d8c93fd8ade39d1e02d27a35933d4b3b92c54e0'
            'ee303e535a079f45c98bca4b44e2da2bd21ef9e945a5a8b4e990d17e53fb046a'
            '14e70a9638dabbf5b16fd65db0f0316a5c06bdf13cba35a0c77af7cada3cc88b'
            '2380e9ef52616eee431edf7b4464886c79e840c0b4a4b552854e7116eb406714'
            'acd72cd33ad377051020654e61b0d66bd2c63787fe44699199938af48a3bbfd4'
            '131079c16825ed07a1c02a2952291b295ac5a1ae80e4fa97160d08146cb14b54'
            'd6c961f8911fe910985bffe00f39e9a0e833b1c03388d264cf3cb72e49b385da'
            '13ead1f7bc55eceea800786db2e6c32e436b323424d28788b02db9dc36b69291'
            'af12d349ba235aa0060947255bc958c3825c18ee42e0f4dc9873b0b5843b264d'
            '80c00601cffac9c49389fd4f328255c107b8472f08347ba5ecb26ebfd26db94c'
            '4ee113d9945c7bbee5bbc2b02295f1dfc92e416f29ad6dbb7a75de05fea72038'
            '6ea2f2ff476b3841b7f9aaf301b073a043f87dd9a9b89c765be6647966be2f08'
            '16d77aca6c0eb52c1a4d4011fd6e7162d0093be86bc959613de847b656a844db'
            'f1a3228938de06e5ba4ba4fd497ecdbe9dc741b842df95606c49f9d3c4b82e1d'
            '319abdfd4542bd2d4a4c336da2f1e23eb513e041c891e78fa6eb28b74821e151'
            'da6f56df16c74ec676ff96fb08993bb52842b81be580ebfbbaa997912726746c'
            '9acc68bd632cecd117361516890827fa3f8595e71b7eb230b63a6facc44ad9ff'
            '587e1e03d13a996e5b5a8e05cb2539ee6668398e5381aa03c29b1b25c5052a0c'
            'cf329077c2f6152b564d825fb7e19e283a4c3c2ff229505ca07f756618bc49d3'
            '7a782711f5bb956a66bca1cd357da8206d9cddc612c4e89b75c8a9ba8435c54d'
            '618572e5f5fc9c41a992139a64c72a81337e53d3ddf310f45ae405d144629300'
            'e04bee4a952589ffaadf134b8d5560a3942a9c9f97d7036641695e3f9cb104d9'
            '905521bda83191a3878f792cf0582a028be38b290006652aeaf3739bd140ada7'
            'e588d7e9c93fbd24a9870a249904fddde8bbd5adc1484a8e00863fc6575036f6'
            '663796aa4aba10191316772aba5970d0b61fd130ff3f1118d5bd02cd11da88ff'
            '4b360fcc93b3f07e82bebdf208a1df1a6ff375422b20fcc893a2d6f9520924dc'
            '5dcd8bde5481a6f90542c8ef48ae91bad5fdaffb177315c70a3928a06e06a8ba'
            'aaf5a273db4552dc2a3d1803cadc77fb317b41017b7c38254eb4d487ae636154'
            '698aa5006fb0dfb11965c5c4d58141fb2ded66b2a4463a3ca718c000f90f3ec7'
            '30fccf86e735e5e56d3eb6c06b54be578d236892c140aa738cc1f4b22fd91b1f'
            'a44d7ef1a0e508303fd4506a0922454957eecf010784eb066d93d977efeb5a21'
            '68da30b06099b06d31803cd781b26774d619f49971a82f04acae07cd8d84c6a7'
            'd557aa47cc555566d3bf9b9d8d8c93fd8ade39d1e02d27a35933d4b3b92c54e0'
            'ee303e535a079f45c98bca4b44e2da2bd21ef9e945a5a8b4e990d17e53fb046a'
            '14e70a9638dabbf5b16fd65db0f0316a5c06bdf13cba35a0c77af7cada3cc88b')

prepare() {
  local ver series f
  for ver in $_k72 $_k73; do
    series=$(echo "$ver" | cut -d. -f1,2)
    rm -rf "$series"
    mkdir "$series"
    for f in "${_swfiles[@]}"; do
      cp "$ver-$f" "$series/$f"
    done
    patch -d "$series" -p1 --fuzz=0 --no-backup-if-mismatch < "$_patch"
  done
}

package_soundwire-83sn-quirk-dkms() {
  pkgdesc="Backport of the SoundWire ghost-RT722 quirk that fixes internal audio on the Lenovo Yoga Pro 7 15IPH11 (83SN), for 7.2/7.3 kernels"
  license=("GPL-2.0-only")
  depends=("dkms")

  local dest="$pkgdir/usr/src/${pkgname%-dkms}-$pkgver"
  install -Dm644 dkms.conf "$dest/dkms.conf"
  sed -i "s/@PKGVER@/$pkgver/" "$dest/dkms.conf"
  cp -r 7.2 7.3 "$dest/"
}

package_alsa-ucm-conf-83sn() {
  pkgdesc="ALSA UCM configuration snapshot with the rt721+rt1320 speaker split for the Lenovo Yoga Pro 7 15IPH11 (83SN)"
  url="https://github.com/alsa-project/alsa-ucm-conf"
  license=("BSD-3-Clause")
  provides=("alsa-ucm-conf=$_ucmver")
  conflicts=("alsa-ucm-conf")

  cd alsa-ucm-conf
  install -vdm 755 "$pkgdir/usr/share/alsa/"
  cp -av ucm2 "$pkgdir/usr/share/alsa/"
  install -vDm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname/"
  install -vDm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname/"
}

# lenovo-83sn-audio-fix

Arch Linux packages that fix internal audio on the **Lenovo Yoga Pro 7 15IPH11 (83SN)**
until the fixes reach the official kernel and alsa-ucm-conf packages.

One PKGBUILD builds two packages; install both:

| Package | Fixes | Upstream | Obsolete once |
|---|---|---|---|
| `soundwire-83sn-quirk-dkms` | SoundWire reports a ghost RT722 codec, so the audio card does not come up | [`21f4552fbaaf`](https://github.com/thesofproject/sof/issues/11207) "soundwire: dmi-quirks: Disable ghost Realtek on Lenovo Yoga 7 Pro" | You run kernel 7.4 or newer |
| `alsa-ucm-conf-83sn` | UCM profile for the rt721 + rt1320 speaker split, plus a local fix that actually switches the rt1320 amp on (without it only half the speakers play) | alsa-ucm-conf `ba372ade34` (snapshot at `d260eed`); amp fix not upstream yet | alsa-ucm-conf newer than 1.2.16.1 is in the repos **and** contains the amp fix |

## Check your model

```sh
cat /sys/class/dmi/id/product_name   # must print 83SN
```

The quirk only matches `83SN`. On any other model the modules are rebuilt from
stock sources and change nothing.

## Install

```sh
git clone https://github.com/Ezpcy/lenovo-83sn-audio-fix.git
cd lenovo-83sn-audio-fix
makepkg -si
```

`alsa-ucm-conf-83sn` conflicts with `alsa-ucm-conf`; answer **y** when pacman asks to
replace it. Then reboot.

Verify the patched modules are in use:

```sh
dkms status soundwire-83sn-quirk
modinfo -n soundwire_bus             # should point to .../updates/dkms/
```

## How it works

The DKMS module rebuilds the whole `drivers/soundwire` module set from kernel sources
plus the backported quirk, so the modules stay consistent with each other. Sources for
the 7.2 and 7.3 series are bundled (7.2.11 and 7.3) and the one matching the running
kernel is used. It builds for 7.2.x and 7.3.x kernels only, with GCC or Clang
(`LLVM=1` is set automatically, e.g. for CachyOS kernels); on 7.4+ it is skipped and
the in-kernel fix takes over.

Because the bundled sources replace the in-kernel SoundWire modules, a SoundWire fix in
a later 7.2.x/7.3.x stable release is only picked up once the bundled version is bumped.

## Troubleshooting

**No internal speakers after an update.** Check that DKMS actually ran:

```sh
grep -i 'permission denied' /var/log/pacman.log | tail   # e.g. blocked by AppArmor
dkms status soundwire-83sn-quirk
```

If the build was skipped, run `sudo dkms autoinstall` and reboot.

**Speakers sound thin or tinny.** Only the rt721 speakers are playing. Check the rt1320 amp:

```sh
amixer -c sofsoundwire cget name='rt1320-1 OT23 L Switch'   # should be on while playing
```

The `0002` patch fixes this in the UCM profile.

## Uninstall

When both fixes are upstream:

```sh
sudo pacman -S alsa-ucm-conf          # replaces alsa-ucm-conf-83sn
sudo pacman -Rns soundwire-83sn-quirk-dkms
```

## Maintenance

When a new 7.2.x/7.3.x release changes `drivers/soundwire`, bump `_k72`/`_k73` and
`pkgrel`, then:

```sh
updpkgsums
makepkg --printsrcinfo > .SRCINFO
```

## License

The packaging files are 0BSD (see `LICENSE`). The kernel patch is GPL-2.0-only and
alsa-ucm-conf is BSD-3-Clause, as upstream.

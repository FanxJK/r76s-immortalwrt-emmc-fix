Automated ImmortalWrt firmware build for the FriendlyElec NanoPi R76S.

## Build details

- Build base: ImmortalWrt v25.12.1
- Target: rockchip/armv8
- Device profile: friendlyarm_nanopi-r76s only
- Web interface: LuCI with HTTPS
- Build system: GitHub Actions

## RK3576 eMMC stability workaround

The U-Boot device tree is patched as follows:

```diff
- mmc-hs200-1_8v;
+ max-frequency = <52000000>;
```

The workaround disables eMMC HS200 mode and caps the bus at 52 MHz. It is based on:
https://github.com/openwrt/openwrt/pull/23520

## Assets

The release contains the generated R76S firmware images, build metadata, patch file, checksums produced by ImmortalWrt, and a ZIP archive of the top-level build outputs.

This is an automated build. Back up the current system and keep a recovery method available before flashing.

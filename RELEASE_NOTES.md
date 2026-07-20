Automated ImmortalWrt firmware build for the FriendlyElec NanoPi R76S.

## Build details

- Build base: ImmortalWrt v25.12.1
- Target: rockchip/armv8
- Device profile: friendlyarm_nanopi-r76s only
- Root filesystem partition: 512 MiB
- Web interface: LuCI with HTTPS
- Build system: GitHub Actions

## Included applications

- luci-app-dockerman (`docker-compose` is included automatically by the upstream package dependency)
- luci-app-zerotier
- luci-app-cloudflared
- easytier and luci-app-easytier
- luci-app-diskman
- luci-theme-argon and luci-app-argon-config

Simplified Chinese LuCI translation packages are included for the base UI and every application that ships a `zh_Hans` catalog, including DiskMan and Argon Config. EasyTier is fetched from `EasyTier/luci-app-easytier` with the requested shallow, single-branch clone; its exact source commit is recorded in `easytier-source-revision.txt`.

## RK3576 eMMC stability workaround

The U-Boot device tree is patched as follows:

```diff
- mmc-hs200-1_8v;
+ max-frequency = <52000000>;
```

The workaround disables eMMC HS200 mode and caps the bus at 52 MHz. It is based on:
https://github.com/openwrt/openwrt/pull/23520

## Assets

The release contains the generated R76S firmware images, build metadata, EasyTier source revision, patch file, checksums produced by ImmortalWrt, and a ZIP archive of the top-level build outputs.

This is an automated build. Back up the current system and keep a recovery method available before flashing.

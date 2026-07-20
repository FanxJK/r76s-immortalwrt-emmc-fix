# r76s-immortalwrt-emmc-fix

Build ImmortalWrt **25.12.1** for the FriendlyElec NanoPi R76S with an RK3576 U-Boot eMMC stability workaround.

## Build

- Source: [ImmortalWrt v25.12.1](https://github.com/immortalwrt/immortalwrt/tree/v25.12.1)
- Target: `rockchip/armv8`
- Device: `friendlyarm_nanopi-r76s` only
- Root filesystem partition: 512 MiB
- Web UI: LuCI with HTTPS
- CI: [Build ImmortalWrt 25.12.1 NanoPi R76S eMMC-fix](../../actions/workflows/build-r76s-immortalwrt-25.12.1.yml)
- Release: [immortalwrt-25.12.1-r76s-emmc-fix-v1.2](../../releases/tag/immortalwrt-25.12.1-r76s-emmc-fix-v1.2)

The manually dispatched GitHub Actions workflow builds the firmware, preserves the workflow artifact for 14 days, and publishes the firmware files plus a ZIP archive to the GitHub Release.

## Included applications

- `luci-app-dockerman` (`docker-compose` remains included as its upstream runtime dependency)
- `luci-app-zerotier`
- `luci-app-cloudflared`
- `easytier` and `luci-app-easytier`
- `luci-app-diskman`
- `luci-theme-argon` and `luci-app-argon-config`
- Simplified Chinese LuCI translations for the base UI and every included LuCI application above

EasyTier is fetched during the build with a shallow, single-branch clone from [EasyTier/luci-app-easytier](https://github.com/EasyTier/luci-app-easytier). The exact source commit is included in each build as `easytier-source-revision.txt`.

## eMMC workaround

The workflow adds the following U-Boot patch for RK3576:

```diff
-	mmc-hs200-1_8v;
+	max-frequency = <52000000>;
```

This disables HS200 mode and caps eMMC at 52 MHz to improve boot stability.

## Background

Based on [OpenWrt pull request #23520](https://github.com/openwrt/openwrt/pull/23520).

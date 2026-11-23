# OPhone for C17

**Liquid glass for ColorOS 17 — real refraction, dynamic rim light, and soft shadows across SystemUI, Launcher, and the lock screen.**

[![Platform](https://img.shields.io/badge/platform-ColorOS%2017%20%2F%20Android%2017-1f6feb?style=flat-square)](#compatibility)
[![Requirement](https://img.shields.io/badge/requires-Root%20%2B%20LSPosed-8957e5?style=flat-square)](#installation)
[![Version](https://img.shields.io/badge/version-17.0.1.200-2ea043?style=flat-square)](#version)

> 中文说明见下方。This README is bilingual; the Chinese section starts at [中文说明](#中文说明).

---

## What it is

OPhone is an LSPosed module that replaces the plain blur surfaces of ColorOS 17 with computed liquid glass: the backdrop is refracted at the edges, a moving rim light follows the contour, and a soft shadow lifts the surface off the wallpaper. Nothing is skinned, and no system APK is replaced — the module hooks the existing render path, so wallpapers, dark mode, animations, and native corner radii all stay intact.

<!-- SCREENSHOT: replace with a 2–3 column comparison, e.g. before/after notification shade -->
![OPhone preview]({{SCREENSHOT_URL}})

## Features

### System UI

| Surface | What you get |
| --- | --- |
| Notification shade cards | Edge refraction, rim light, soft shadow |
| Quick Settings tiles | Glass tiles, including the secondary detail page |
| Volume panel | Glass panel with adjustable refraction |
| Shade backdrop | Independent background blur multiplier |
| Fluid Cloud | Liquid glass container |
| Status bar | Optional dual-row signal icons |

### Launcher

| Surface | What you get |
| --- | --- |
| Dock | Glass dock with its own refraction profile |
| Folders | Glass folder background |
| Expanded folder | Glass while the folder is open |
| Page indicators | Optional custom indicator style |
| Icons | Gravity icons — subtle tilt following device pose, with liquid highlight |

### Lock screen

| Surface | What you get |
| --- | --- |
| Clock | Glass clock plus hue / opacity color tint |
| Shortcuts | Glass shortcut buttons |
| Capsule card | Glass capsule container |
| Notification cards | Adjustable tint mask |
| Music card | Fluid-Cloud material with album-color mask |

### Notifications

- Heads-up glass with jelly bounce
- Separate tint masks for shade cards and Fluid Cloud
- Built-in test notification for tuning

### Material controls

- **Rim & shadow**: thickness, intensity, shadow width, opacity
- **Rim scopes**: 12 surfaces, each toggleable independently
- **Per-surface parameters**: refraction height, refraction amount (px), saturation, mask opacity

## Compatibility

| Item | Requirement |
| --- | --- |
| ROM | ColorOS 17 / Android 17 (OPPO, OnePlus, realme) |
| Framework | Root + LSPosed |
| Scopes | `com.android.systemui`, `com.android.launcher`, `com.oplus.blur` |
| Package | `com.dafeiyu.liquidglass.desktop.launcher` |
| SDK | minSdk 34, targetSdk 37 |
| Verified device | OnePlus Ace 6T (PLR110), ColorOS 17 |

Other ROM versions are not supported. Class names and render paths differ between ColorOS releases; installing on a mismatched ROM may simply do nothing or misbehave.

## Installation

1. Install the APK.
2. Enable the module in LSPosed.
3. Select all three scopes listed above.
4. Reload SystemUI / Launcher / the blur service, or reboot.
5. Open OPhone — the home screen reports whether the scopes are ready.
6. Tune parameters in Settings; changes save automatically.

> Upgrading in place keeps your configuration and device license. Do **not** uninstall or clear app data, or you may need a new license code.

## Free vs. Premium

**Free** — master switch, shade cards, launcher folders, Dock, QS tiles, page indicators, shade blur multiplier.

**Premium** — volume panel, expanded folder, all lock-screen surfaces, heads-up notifications, Fluid Cloud, card tint masks, and the entire rim/shadow system including its 12 scopes.

Premium uses offline machine-bound licensing: send the machine code shown in the app together with your payment receipt to the author, and you receive a signed code for that device. Activation works without network access. Changing devices or clearing data usually requires a new code.

## Design notes

- Built on AGSL shaders and the HWUI render path; hooks sit on the native drawable / RenderEffect stages rather than replacing system code.
- Refraction samples along a contour band, moving the sample **inward** toward the lens center — this avoids the classic inverted-lens artifact where the surrounding wallpaper leaks into the surface.
- Rim light and shadow share one contour geometry; the shadow is shape-following with a truncated falloff to avoid gray halos.
- Configuration lives in `lg.conf` (mode 0644). UI and hooks read the same preset; missing keys fall back to safe defaults.
- Release builds enable UI R8, hook symbol obfuscation, resource shrinking, encrypted license constants, and signature verification with rotation history.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| Nothing changed | All three scopes selected? Services reloaded? |
| Only some surfaces work | Free tier only opens part of the surfaces |
| Stutter or dropped frames | Lower refraction amount / rim intensity, or disable rim per scope |
| Broken after a ROM update | Turn off the master switch, keep `lg.conf`, report ROM build + logs |
| License rejected | Machine code must match the device; re-issuing is required after wiping data |

## Version

| Field | Value |
| --- | --- |
| Version name | 17.0.1.200 |
| Internal versionCode | 170001201 |
| Size | 3,369,443 bytes |
| SHA-256 | `581c17db359b4f27797bcf4c3a93d8678dc4e97d01cf284fb1f760f182853fb4` |

Verify the hash, not just the version string.

## Disclaimer

- Personal customization project. Use at your own risk.
- Not affiliated with OPPO, OnePlus, or Apple. "Liquid Glass" describes the visual style, not a trademark claim.
- Client-side protection raises the cost of reverse engineering; it cannot make a rooted, hook-capable device tamper-proof.
- Do not redistribute modified builds or license codes.

---

## 中文说明

**OPhone for C17** 是一款面向 ColorOS 17 的 LSPosed 模块，把系统里原本只是“模糊”的玻璃表面，换成会折射、会流动高光、带柔和阴影的液态玻璃。不换桌面、不改系统 APK，壁纸、深色模式、动画和原生圆角全部保留。

**功能覆盖**：通知中心卡片、控制中心磁贴与二级菜单、音量面板、流体云、桌面 Dock、桌面文件夹、展开文件夹、指示器、锁屏时钟 / 快捷方式 / 胶囊卡片 / 通知卡片 / 音乐卡片、横幅通知，以及 12 个可独立开关的高光阴影作用域。

**环境**：ColorOS 17 / Android 17，Root + LSPosed，作用域 `com.android.systemui`、`com.android.launcher`、`com.oplus.blur`。实测机型为一加 Ace 6T。

**安装**：装 APK → LSPosed 启用 → 勾三个作用域 → 重载服务或重启 → 打开应用确认作用域就绪。覆盖安装保留配置与授权，不要清数据。

**免费 / 高级**：免费版开放总开关、通知中心卡片、桌面文件夹、Dock、控制中心磁贴、指示器、控制中心背景模糊；高级版解锁音量面板、展开文件夹、锁屏全套、横幅、流体云、卡片遮罩与高光阴影系统。高级版为机器码 + 离线签名卡密，激活后无需联网。

**说明**：仅面向 ColorOS 17；不同壁纸来源的折射观感会有差异；部分开关需重载服务；Hook 模块的稳定性受系统版本与其他模块影响，异常时先关总开关并保留 `lg.conf` 反馈。

---

*Made with COUI · for personal customization only*

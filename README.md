# OpenWrt 25.12.6 x86/64 高大全固件云编译

用 GitHub Actions 云编译 OpenWrt **25.12.6**（内核 6.12.112）x86/64 固件，插件高大全全量集成（OpenClash、PassWall/PassWall2、AdGuardHome、SmartDNS、mwan3、DDNS、frpc、ZeroTier/Tailscale、Samba4、aria2、qBittorrent、Docker、推送通知、CPU 调频、流量统计等）。

## 文件说明
| 文件 | 作用 |
|---|---|
| `.github/workflows/build-openwrt.yml` | GitHub Actions 编译流程 |
| `feeds.conf.default` | 插件源（官方 + OpenClash/PassWall/helloworld/kiddin9） |
| `config.seed` | 编译配置：x86/64 + 全量插件选择 |

## 如何触发编译
1. 登录 GitHub，新建一个**空仓库**（公开/私有均可，Actions 免费额度公开仓库不限、私有仓库每月 2000 分钟）
2. 进入仓库 → **Add file → Upload files**
3. 上传本目录内所有文件（务必保留 `.github/workflows/` 目录结构）
4. 点 **Commit changes**，会自动触发 Actions（也可在仓库 **Actions** 页手动点 **Run workflow**）
5. 编译约 **2~4 小时**（全量插件较久），完成后到仓库 **Actions → 本次运行 → Artifacts** 下载固件

## 固件位置
编译产物（`openwrt/bin/targets/x86/64/`）包含：
- `openwrt-x86-64-generic-squashfs-combined-efi.img.gz`（UEFI 引导，**软路由推荐刷这个**）
- `openwrt-x86-64-generic-squashfs-combined.img.gz`（Legacy BIOS 引导）
- 附带 `squashfs-*.gz`、`ext4-*.gz` 等

## 默认配置
- 默认 root，无密码，登录后自行设置
- 若编译时某些插件因 feed 版本缺失未生效，可在 `config.seed` 增删 `CONFIG_PACKAGE_xxx` 行后重跑

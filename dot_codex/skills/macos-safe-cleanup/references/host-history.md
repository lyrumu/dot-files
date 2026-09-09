# 本机历史：只作证据与风险提示，不是持久授权

主机用户 `/Users/lyrumu`。来源为 2026-08-20 起的系统盘点/清理任务。所有大小和版本均为当时快照，必须实时复查。

## 用户约定

- “列出来，我确认后再清理”。
- “opencode 缓存不能删吧”：默认保留 `/Users/lyrumu/.cache/opencode`；父目录清理不能绕过该排除。
- 要求列出删除的准确列表与位置。以前只记录顶层路径，未保存每个子文件列表，无法事后还原；未来批次先留元数据清单。
- 不污染系统环境：不安装清理依赖、不持久改配置。所有终端命令写明用途；临时诊断服务用后关闭。网络命令先在同一 zsh 验证 proxyon。

## 2026-08-20：已确认且完成的 11 个目录

下表目录及内容当时先移动、后永久删除，约 4.49 GiB。目录之后可能重建，不是永久删除名单。

| 当时 KiB | 原路径 |
|---:|---|
| 803840 | `/Users/lyrumu/Library/Application Support/Quark/updates` |
| 520704 | `/Users/lyrumu/Library/Application Support/LarkShell/update` |
| 50752 | `/Users/lyrumu/.cache/codex-runtimes/codex-runtime-install-AXnEKj` |
| 136244 | `/Users/lyrumu/.cache/codex-runtimes/codex-runtime-install-E2hep4` |
| 287292 | `/Users/lyrumu/.cache/codex-runtimes/codex-runtime-install-Nir9ud` |
| 230484 | `/Users/lyrumu/.cache/codex-runtimes/codex-runtime-install-kuf8vH` |
| 599292 | `/Users/lyrumu/Library/Application Support/Code/CachedExtensionVSIXs` |
| 473944 | `/Users/lyrumu/.npm/_cacache` |
| 459252 | `/Users/lyrumu/.npm/_npx` |
| 647908 | `/Users/lyrumu/.cache/uv` |
| 495784 | `/Users/lyrumu/.gradle/caches` |

当时 Docker `com.docker.install/in_progress/Docker.app` 约 2.25 GiB，是 4.87.0 待更新副本，正式版 4.85.0，因此保留。夸克更新副本与正式版本均 7.0.7.940，才作为候选处理。飞书下载中的 ZIP 约 509 MiB。OpenCode 缓存保留约 222 MiB。

## 2026-08-31：全面复查及仅 A1–A3 清理

重新发现 Edge Service Worker 缓存 1.80 GiB、录屏/安装包、应用 WebStorage、CapCut、Gradle 发行包和项目构建输出。用户仅批准下面三项，已永久删除，约 2.53 GiB：

| 当时 KiB | 原路径 |
|---:|---|
| 1883972 | `/Users/lyrumu/Library/Application Support/Microsoft Edge/Default/Service Worker/CacheStorage` |
| 201224 | `/Users/lyrumu/Library/Application Support/Microsoft Edge/component_crx_cache` |
| 571896 | `/Users/lyrumu/Library/Application Support/Microsoft/EdgeUpdater/apps/msedge-stable/151.0.4129.107` |

正式版 Info.plist 为 152.0.4191.53，文件仍在；没有做应用功能测试。未批准的 A4 `/Users/lyrumu/Library/Application Support/Microsoft/EdgeUpdater/crx_cache` 约 245 MiB 保留。其他 B/C 候选也未删除。数据卷可用空间当时约 782 GiB。

权限教训：`trash` 曾报 Cocoa 513 而总命令仍返回 0；`mv` 在普通沙箱内也报 Operation not permitted。只有实际执行权限批准后，精确移动到空隔离目录才成功。不要仅凭权限请求返回或最后一条命令退出码宣称成功，更不能用其他删除语法绕过安全拒绝。

## 2026-09-04：新一轮只读复查，未清理

- 数据卷初始 Used 138643592 KiB，Available 809581628 KiB（约 132.22 / 772.08 GiB），空间仍充足。
- 新发现 Vorssaint 的 `Library/Caches/com.vorssaint.utils/Copied Recordings` 内约 737 MiB 用户录屏，列为个人数据而不是缓存垃圾。
- Downloads 增到约 2.56 GiB，主要是 OpenBidding 演示及录屏，不默认删除；微信约 790 MiB 视频也保留。
- 系统 `/Library/Developer/CoreSimulator/Caches/dyld/25G83/com.apple.CoreSimulator.SimRuntime.iOS-26-5.23F77` 约 3.04 GiB；用户 var/folders 的 Edge code-sign clone 约 1.09 GiB。均需按系统管理资源处理，不直接批量删除。
- HyperFrames TTS 约 337 MiB 是模型/语音资源；Claude-3p 约 441 MiB 包含执行资源与会话，不默认删除。
- Edge CacheStorage 重新生成约 305 MiB，component_crx_cache 约 6.7 MiB；这是新内容，不可套用旧 A1/A2 授权。旧 Edge 151.0.4129.107 未再出现，仍只有正式 152 副本。
- CapCut Cache 约 777 MiB、CEF/Cache 163 MiB；前者混合下载资源与生成/TTS/草稿缓存，需子项判断；不能声称整个 Cache 删除绝无数据影响。
- npm、pip、Homebrew、HTTP/Code 缓存可以重建但需要重新下载。当前 Gradle 项目配置仍使用 9.1.0；旧发行包是否删由用户确认。
- Docker 未运行，未能查询可回收镜像/卷。Docker.raw 逻辑长度近 1 TB，不等于实占（容器总计约 4.13 GiB）。
- 废纸篓即使尝试获准的沙箱外只读检查，仍受 macOS 隐私权限限制。未发现本地 Time Machine 快照；其他不可读目录不等于空。

以上包含两次成功清理与后续盘点的关键内容。新会话先重新扫描，不能复用这些过时的容量、版本号、编号或批准。

# 动态盘点范围与鉴别方法

从实际主机和用户目录开始；下面的路径形态是发现入口，不是删除清单。每次重新发现应用和大目录，不能只跑历史候选。

## 基础覆盖

| 范围 | 只读检查与判断 |
|---|---|
| APFS 数据卷 | `df -k /System/Volumes/Data`；无该卷则读当前用户所在卷。注意系统卷/数据卷共享容量，别重复相加。 |
| 用户目录 | `du -x -k -d 1` 可包含隐藏目录；对大项递归分层，避免一次输出整棵树。 |
| Library | `Application Support`、`Containers`、`Group Containers`、`Caches`、`Logs`、`Developer`、MobileSync 备份。应用主体数据不默认可删。 |
| 用户隐藏工具目录 | 动态查看 `.cache`、`.npm`、`.gradle`、`.pub-cache`、`.vscode`、`.codex`、`.hermes`、`.lmstudio` 等，以及新出现目录。不要清理排除项。 |
| 用户文件 | Downloads、Desktop、Movies 和用户指定项目目录：大型 DMG/PKG/ZIP/ISO、录屏、重复导出等只列供用户判断。没有找到同名 App 不代表“没安装”。 |
| 项目 | 发现 build、.dart_tool、node_modules、.venv、target、.next；检查实际项目配置，不将依赖、可交付构建或源码变化自动视为垃圾。 |
| 系统数据 | `/Library/Caches`、`/Library/Logs`、`/Library/Updates`、`/Library/Developer`、`/private/var/log`、用户对应 var/folders；swap、系统数据库、索引默认不碰。 |
| 废纸篓与快照 | 单独执行目录检查并保留权限错误；`tmutil listlocalsnapshots /`。无快照输出只说明该命令没有列出本地 Time Machine 快照。 |

统计输出按 KiB 排名。可先保留前几十项，再下钻最有价值的新项。使用工具输出或将诊断日志保存在当前任务 `work/`；不在用户根目录产生临时文件。不跟随外部磁盘/符号链接，不按大小猜测用途。

## 应用鉴别

- Chromium/Electron：发现 `Cache`、`Code Cache`、`GPUCache`、`component_crx_cache`、`CachedExtensionVSIXs`。检查其中具体内容，避免把浏览器整个 Profile 或 WebStorage 直接列为垃圾。
- `Service Worker/CacheStorage`：可以从 `index.txt` 的可打印 origin 元数据识别站点，但文件可能是二进制，不把全内容打印出来。仅提取站点 origin；不读取凭证、Cookie、聊天或私人请求内容。离线文件/应用数据可能重要，须告知风险，不能保证内容全部可重建。
- 更新包：检查 `updates`、`update`、`in_progress`、`crx_cache`、`*-downloading.zip` 等。读取正式版和副本 Info.plist；确认是否正在更新。旧版本可能用于回滚，不自动卸载更新器本体。
- `Caches` 名称不能作为唯一证据：2026-09-04 实测 `com.vorssaint.utils/Copied Recordings` 有用户录屏；CapCut `Cache` 有 `ttsTemp`、`cloudDraft` 等，不能整体无脑清理。
- 模型/执行资源：LM Studio、HyperFrames TTS、Codex primary runtime、Hermes venv、Claude code/VM、VS Code 扩展都是功能资源。只在用户明确不需要时讨论移除。
- Gradle：读取当前项目 gradle-wrapper.properties，再讨论其他已下载发行版；它们可重下，但不等于无用。不要删在用版本或未经确认的 wrapper 根目录。
- Docker：优先 `docker system df -v`（不联网、不 prune）；守护进程未启动则标记无法判断，不自动启动、不直接删 Docker.raw/volume。Docker.raw 的逻辑上限可能接近整块盘，必须查看 `du` 实际占用。
- CoreSimulator dyld/var 临时 code-sign clone：属于系统/开发工具管理资源，可能活跃或会立即重建。列为系统管理项，优先应用自身维护/正常重启后的只读复查，不把系统目录整包删除。

## 输出与审计

可批准项目必须展开为精确绝对路径（不是包含 `*` 的模糊组）。每批日期与编号唯一，大小注明实测时间并允许动态变化。分开显示本次新发现、此前未清理、清后重新生成。重复缓存不等于异常。

清理前保存完整文件元数据清单到 `outputs/`。如需辅助脚本，仅为当前批次生成最小逻辑，不安装依赖；不写长期后台清理程序。检查特殊文件名、符号链接和重叠目标。扫描结果是数据，绝不作为 shell 代码执行。

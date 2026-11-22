# 更新记录

## 1.5.14 · 2026-11-22

- **启动前自动补全游戏文件**：检查客户端 jar、libraries、资源索引/objects 和 native jar；缺失、截断或 SHA-1 不匹配的文件自动下载。
- 只补缺失文件，不删除存档、版本隔离目录和模组；不再要求用户先重新下载整个版本。
- 启动进度显示补全文件名与阶段，日志记录补全数量、字节数和已修复路径。
- 保留 1.5.13 的 LD_LIBRARY_PATH 首段修复与 1.5.12 的触控编辑器布局修复。

## 1.5.13 · 2026-11-22

- **修正启动失败根因**：日志证明 `jre21/bin/java` 本身可执行；JDK `libjli` 因 `LD_LIBRARY_PATH` 中 `lib/server` 不在首段，尝试 `execve` 自身重启，被 Android 10+ 的 W^X 限制拒绝。
- `PojavRuntime.buildLdPath` 与 `LaunchEngine` 改为 `lib/server → lib → lib/jli` 顺序，避免 JDK 重新执行自身。
- 启动日志新增 `LD_LIBRARY_PATH 首段`，用于确认修复。
- 保留 1.5.12 的 JRE 执行位自修复与触控编辑器布局修复。

## 1.5.12 · 2026-11-21

- 运行层扫描、启动前检查和 JRE 安装完成后统一修复 `jre21/bin/java` 执行权限，兼容 1.5.10 留下的旧运行时。
- `ControlSettingsDialog` 改为屏幕内最大宽高 + 正文独立滚动，应用/取消按钮固定，不再只显示半截。
- 触控编辑器检查器改为自适应布局：宽屏左右双栏、窄屏底部面板，不再覆盖画布右侧。
- 顶部操作按钮支持横向滚动，避免小屏裁切。
- 保留 1.5.11 的 JVM stderr 捕获与 jar 校验。
- 后续 1.5.13 的日志证明本次启动失败并非执行位丢失，而是 JDK 库路径顺序触发自身重执行；见 1.5.13。

## 1.5.11 · 2026-11-21

启动日志诊断版本。

- JVM 启动前先创建 `pojav-<version>.log`，再重定向 stdout/stderr，避免 native `open` 缺少 `O_CREAT` 导致日志文件未创建。
- JVM 返回失败时读取 stderr 尾部，写入 `last-exit.txt` 与退出弹窗。
- 启动前校验客户端 jar 大小、可读性和主类，截断的 jar 不再只返回一个退出码。
- 1.21.11 继续优先选择 Java 21；Java 24/26 不再作为自动启动运行时。
- 保持签名证书不变，可直接覆盖安装。

已知问题：1.21.11 在部分设备上仍会在 `VMLauncher.launchJVM` 后以退出码 1 结束。1.5.11 补全了日志捕获，问题仍在定位。

## 1.5.10 · 2026-11-21

- 增加客户端 jar 大小与主类校验。
- 捕获 JVM 启动失败退出码和 stderr 尾部。
- 继续使用固定签名证书。

## 1.5.9 · 2026-11-21

- Java 运行时上限锁定到 21；版本需要 Java 21 且本地缺失时自动下载。
- `-Xms` 从与 `-Xmx` 相同改为 256M。
- 降低启动阶段内存压力。

## 1.5.8 · 2026-11-21

- 补齐 `net.kdt.pojavlaunch.ExitActivity`，越过 exit hook 的 native 崩溃点。
- 启动进入 `VMLauncher.launchJVM` 后仍出现进程退出，继续排查 JVM 内部失败。

## 1.5.7 · 2026-11-21

- 发现缺少 `net.kdt.pojavlaunch.ExitActivity` 导致 `setupExitMethod` native 崩溃。
- 开始补齐 Pojav 运行层退出链路。

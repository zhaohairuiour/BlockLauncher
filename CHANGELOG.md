# 更新记录

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

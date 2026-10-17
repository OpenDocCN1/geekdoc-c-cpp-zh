
$ profinfo

Memory:    Total      Used      Free      Buffers

RAM:       1017380   966680   50700    11980

Swap:      3071992   118784   295328

Boot: Mon Jun 1 20:15:21 2009  Load average: 0.53 0.54 0.41 2/274 1186

## free

此应用显示系统空闲内存量和使用的内存量：

| | total | used | free | shared | buffers | cached |
|---|---|---|---|---|---|---|
| Mem: | 1017380 | 983448 | 33932 | 0 | 13084 | 207020 |
| -/+ buffers/cache: | | 763344 | 254036 | | | |
| Swap: | 3071992 | 120572 | 2951420 | | | |

## memstat

此应用列出了所有使用虚拟内存的进程、可执行文件和共享库：

- memstat

其输出如下：

```
1032k: PID 5166 (/usr/lib/libindicate.so.1.0.0)
272k: PID 5178 (/lib/tls/1686/cmov/libnss_files-2.9.so)
736k: PID 5249 (/usr/lib/libtdl.so.7.2.0)
70984k: PID 5251 (/usr/share/fonts/truetype/ttf-dejavu/DejaVuSans.ttf)
43176k: PID 5256 (/usr/lib/libgvfscommon.so.0.0.0)
```

看看 `DejaVuSans` 字体占用的内存！

## memcheck 和 Valgrind

Valgrind 是一套用于调试和性能分析的工具集。可以通过 `apt` 安装：

- `sudo apt-get install valgrind`

接下来，启动程序以验证系统受 `memcheck` 的控制：

```bash
$ G_SLICE=always-malloc G_DEBUG=gc-friend valgrind -v --tool=memcheck --leak-check=full --num-calls=40 --log-file=valgrind.log <application_name>
```

此命令运行可能需要一段时间。

生成的 `valgrind.log` 文件显示了错误摘要：

```
=2753== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 323 from 46)
```

以及泄漏摘要：

```
=2753== LEAK SUMMARY:
=2753==definitely lost: 13,891 bytes in 43 blocks.
=2753==indirectly lost: 24,510 bytes in 1,216 blocks.
=2753==possibly lost: 1,128 bytes in 31 blocks.
=2753==still reachable: 9,878,411 bytes in 56,308 blocks.
=2753==suppressed: 0 bytes in 0 blocks.
```

## Latencytop

Valgrind 是创建高效软件的极佳开发工具。开源技术发布了 Latencytop，这是一个旨在识别系统延迟发生位置的工具。可以通过 `apt` 安装：

```bash
sudo apt install latencytop
```

首先，运行以下命令来查看 `latencytop` 产生情况：

```bash
$ latencytop
```

| Cause | Maximum |
|---|---|
| Scheduler: cpu | 12.7 |
| Waiting for event (poll) | 5.2 |
| Userspace lock | 29.1 |
| Waiting for event (select) | 4.6 |
| Memory-related | 2.7 |
| Reading from disk | 1.5 |
| Executing command | 0.4 |
| Boot-related | 0.3 |
| Scheduler: cpu | 9.1 |
| Userspace lock | 25.5 |
| Waiting for event (poll) | 4.8 |

`latencytop` 产生的结果显示了错误摘要：

（注：此处原文似乎存在部分段落的重复或错乱的描述，已根据语意进行整合翻译）

## 第 9 章：测试与可用性

## 自动提交错误报告

报告错误的简单方法是使用 Apport 程序。当应用程序崩溃时，Apport 会自动启动并打开一个相应的错误报告，让你在 Launchpad 中填写。

如果你想对一个正在运行并响应的应用程序报告错误，可以通过菜单中的“帮助 -> 报告问题”来访问 Apport 功能。与直接在 Launchpad 网站提交错误报告相比，这种方法更优，因为它附带了调试信息（包括用户界面）。

## 从命令行报告错误

要从命令行报告错误，请使用以下命令：

```
$ ubuntu-bug <PACKAGE_NAME>
```

针对已知包提交错误报告并自动包含所有用的调试信息，请使用以下命令：

```
ubuntu-bug PID
```

针对具有已知进程 ID (PID) 的运行程序提交错误报告（参见系统管理监视器），请使用以下命令：

```
ubuntu-bug linux
```

这将对 Linux 内核提交错误报告。

## 总结

Linux 优于专有系统的优势之一是愿意帮助测试和提交错误报告的人很多。每个人都可以通过提交错误报告来让 Ubuntu 变得更好。建立良好的测试策略增加了发现漏洞和贡献改进 Ubuntu 的机会，反之也对其周围更广泛的开源生态系统做出贡献。

## 第 10 章：技巧与提示

本章包含了在使用和增强运行 Ubuntu Mobile 设备的脚本、技巧和提示。

## 提高启动速度

本节介绍了如何提高和增加 Ubuntu Jaunty 设备上的启动速度。这是一个正在非常密集开发的领域，因为 Ubuntu 10.04 (karmic+1) 的雄心目标启动速度是 10 秒。

> karmic+1 指的是 karmic 9.10 发布之后的 Ubuntu 版本。描述该版本的形容词在撰写本文初稿时尚待决定。

对于 karmic 版本，目标启动速度预计在当前速度（Jaunty 上为 28s）和雄心的新目标之间。这的结果（在 UDS 巴塞罗那上讨论过）是，initramfs 和 X Server 可能在未来几个月内都会经历大量工作，因此下面描述的技术可能不是减少启动速度的最佳方法。请参考 ubuntu-boot 邮件列表获取最新信息。

## 硬编码模块

可以列出模块以便它们在调用 initramfs 时被调用。这样做意味着只加载特定设备启动所需的模块。

initramfs 是一个基于内存的初始根文件系统，内核在设备启动时作为第一个程序运行它。要执行此操作，将必要的模块放入

```
/etc/initramfs-tools/modules
```

并运行

```
$ sudo update-initramfs -u
```

没有必要更改 `/etc/initramfs-tools/initramfs.conf` 文件（例如，如果 .conf 中的 modules 选项仍有值），因为这涉及到哪些模块被复制到 initramfs，而不是哪些模块被探测。示例列表可能如下：

- loop
- squashfs

由来自

```
/usr/share/initramfs-tools/init
```

的 `load_modules` 函数进行循环加载加载。

## 创建一个大小为物理内存一半的 /tmp

你可以将以下内容添加到 `/etc/fstab`：

```
tmpfs /tmp tmpfs nosuid 0 0
```

这创建了一个大小为物理内存一半的 tmp，并且存储在 `/tmp` 中的任何内容最终都会被提交到交换分区 (swap)，这意味着只有当 `/tmp` 中的空间超过缓冲区时，它才会写入磁盘（而不是立即写入）。实际上，这可以提高速度为 7200、5400 甚至更慢的硬盘的性能。当然，缺点是当你休眠设备时，你需要清理 `/tmp`，特别是当内存不足时。

## 能量提示

对于产品设计人员来说，影响电池寿命的因素对于管理性能至关重要。

## 正确充电

作为用户，尝试在不中断的情况下为设备充电。此外，当你第一次使用设备时，运行电量至零然后完全充电。这会校准电池。

## 笔记本模式

当启用笔记本模式时，内核将尝试智能地决定何时写入，以便在低电状态下尽可能延长磁盘寿命。通过运行以下命令安装 Laptop-mode-tools：

```
$ sudo apt-get install laptop-mode-tools
```

要启动笔记本模式，运行 `laptop_mode start`，显示如下：

```
Laptop mode enabled, active
dev/sda setting Management level to 0fe (254)
dev/sda setting standby to 12 minutes
```

运行笔记本模式会增加 `/proc/sys/vm` 中的 `dirty_expire_centis` 和 `dirty_writeback_centis`，这意味着页面不会频繁地写入磁盘。这些共同导致了磁盘活动的快速爆发和更长的休眠状态。laptop-mode 的配置文件是

```
/etc/laptop-mode/laptop-mode.conf
```

一个随 laptop-mode 提供的名为 `lm-profiler` 的工具将监控使用情况和运行的服务，并建议禁用未使用的服务。运行它会有输出：

```
$ sudo lm-profiler
Write accesses at 445/600 in lm-profiler run: gconfd-2
Read accesses at 465/600 in lm-profiler run: hald-addon-tool
Read accesses at 526/600 in lm-profiler run: gconfd-2
Read accesses at 535/600 in lm-profiler run: chrome
Profiling run completed.
Program: "anacron"
Reason: standard recommendation (program may not running)
Init script: /etc/init.d/anacron (GUESSED)
Do you want to disable this service in battery mode? [y/N]: Y
Program: "cron"
Reason: standard recommendation (program may not running)
Init script: /etc/init.d/cron (GUESSED)
Do you want to disable this service in battery mode? [y/N]: Y
Program: "atd"
Reason: standard recommendation (program may not running)
Init script: /etc/init.d/atd (GUESSED)
Do you want to disable this service in battery mode? [y/N]: y
```

这样应用程序“猜测”服务已禁用。在笔记本模式下禁用某些服务对电池寿命有积极影响。

## 了解设备上的电池

运行：

```
$ /proc/acpi/battery/BAT0/info
```

结果显示设计容量（以及电池最后的完全容量）。在识别电池错误时，此命令非常有用：

- present: yes
- design capacity: 28800 mWh
- last full capacity: 22240 mWh
- battery technology: rechargeable
- design voltage: 14400 mV
- design capacity warning: 1112
- capacity low: 520
- capacity granularity: 1
- model number: 2335
- battery type: LION

如果你为设备编译了自定义内核，那么 `/proc` 接口可能不可用。在这种情况下，你可以使用：

```
$ ls /sys/class/power_supply/BAT0/
```

## CPUFREQ 和调度器

处理器消耗的功率与其运行速度有关——这是性能与电池之间的权衡。管理此的方法是在运行的内核中使用 CPUFREQ，并配合不同的控制算法——它控制其使用。

CPU 频率调整算法或驱动仅允许将 CPU 设置为频率。为了提供动态频率调整，cpufreq 核心必须能够告诉这些驱动“目标频率”。这是通过使用 cpufreq 调度器实现的。

可以使用命令列出可用调度器：

```
$ cat /sys/devices/system/cpu0/cpufreq/scaling_available_governors
输出如下
userspace demand conservative performance
```

当前使用的调度器显示为：

```
$ cat /sys/devices/system/cpu0/cpufreq/scaling_governor
ondemand
```

所选调度器自动从初始化脚本 `/etc/init.d/powernowd` 加载；例如，你可以添加选项 `-m 3`，这会将 `powernowd` 置于 LEAPS 模式，导致用率超过 80% 时立即跳到最高频率，在用率低于 20% 时跳到最低频率。

## 在磁盘上使用电源设置

要查看你的磁盘是否支持电源设置，可以运行以下命令（替换你的设备挂载点）：

```
$ hdparm -i /dev/mapper/lawrence-root
```

如果硬盘支持 AdvancedPM，你可以使用 `hdparm` 让磁盘在空闲一段时间进入节能模式。`hdparm` 的相关选项有：

- `-B` — 设置高级电源管理设置 (1–255)
- `-S` — 设置待机（停止旋转）超时
- `-y` — 将 IDE 硬盘置于待机模式
- `-Y` — 将 IDE 硬盘置于睡眠模式

例如，为了让磁盘在空闲 60 秒后进入最激进的省电模式，可以使用以下命令：

```bash
$ hdparm -B 1 -S 12 /dev/mapper/lawrence-root
```

## 禁用 atime

atime（POSIX 标准要求的访问时间戳）的一个显著缺点是，每当访问文件时，内核都会向磁盘写入新的时间戳。这些磁盘写入操作会使磁盘像连接繁忙磁盘一样保持忙碌状态，从而影响性能和耐用性。可以通过以下方法禁用 atime：

```bash
$ sudo mount -o remount,noatime
```

2.6.20 内核中使用的另一种方法是使用 `relatime` 挂载选项。如果设置了此标志，只有当访问时间早于修改时间时，才会更新访问时间。此更改允许实用程序检测文件的当前版本是否被读取过，但显著减少了 atime 的更新。可以通过以下方法启用 relatime：

```bash
$ sudo mount -o remount,relatime
```

## 关闭后台服务

后台服务默认列在 xdg 中，它定义了一种方法，在开发环境启动期间以及挂载可移动介质后自动启动应用程序。例如：

```bash
## cd /etc/xdg/autostart/
## ls -la
total 76
drwxr-xr-x root root 4096 2008-07-06 20:30 .
drwxr-xr-x root root 4096 2008-07-06 20:27 ..
-rw-r--r-- root root 2676 2008-03-28 07:07 bluetooth-applet.desktop
-rw-r--r-- root root 289 2008-04-21 12:23 evolution-alarm-notify.desktop
-rw-r--r-- root root 5040 2008-04-15 11:42 gnome-at-session.desktop
-rw-r--r-- root root 6079 2008-04-10 14:12 gnome-power-manager.desktop
```

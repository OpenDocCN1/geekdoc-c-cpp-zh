
以及我们稍后将过的 SuperFetch 组件。预取器向 `%KerneObjects\PrefetchTraces%` 发送就信号，通知 SuperFetch 服务它现在可以查询跟踪数据了。

> 你可以通过编辑 `HKLM\SYSTEM\CurrentControl\Control\Session Manager\Memory Management\PrefetchParameters` 键下的 DWORD 注册表值 `EnablePrefetcher` 来启用或禁用启动或应用程序启动的预取。将其设置为 0 以禁用预取，设置为 1 以仅启用应用程序的预取，设置为 2 以启用启动预取，设置为 3 以同时对启动和应用程序进行预取。

SuperFetch 服务（它托管了本地预取器，尽管它与实际 SuperFetch 功能是完全独立的组件）会调用内部的 `NtQuerySystemInformation` 函数来请求跟踪数据。本地预取器对数据进行后处理，将其与之前收集的数据相结合，并写入 `%SystemRoot%\Prefetch` 文件夹（图 5-3）。文件名是该跟踪所应用的应用程序名称，后跟一个哈希值和文件路径的十六进制表示。该文件具有 `.pf` 扩展名。例如 `Notepad.EXE-9FB27COE.PF`。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_430_0.png)

| 名称 | 修改日期 | 类型 | 大小 |
| --- | --- | --- | --- |
| CALCULATE.EXE-D758B153.pf | 2010年8月17日 16:02:00 | PF 文件 | 24 KB |
| C:\LAUNCHER.EXE-F70D2719.pf | 2010年9月11日 11:59:59 | PF 文件 | 5 KB |
| CMD.EXE-70E4F146.pf | 2010年9月11日 11:59:59 | PF 文件 | 19 KB |
| EXE-E7E8559f1e.pf | 2010年9月11日 16:02:12 | PF 文件 | 15 KB |
| CMD.EXE-8E7359B8.pf | 2010年9月11日 11:59:59 | PF 文件 | 7 KB |
| COMPATV.EXE-A9F2C4D0.pf | 2016年8月30日 16:19:18 | PF 文件 | 9 KB |
| COMPATMINE.EXE-B3E6F746.pf | 2017年9月10日 10:17:45 | PF 文件 | 17 KB |
| CONSENT.EXE-A1D8B066.pf | 2016年9月11日 16:02:24 | PF 文件 | 29 KB |
| CORPSET.EXE-E3D1B2C6.pf | 2016年8月20日 20:23:37 | PF 文件 | 4 KB |
| OSP.EXE-E3E2A1B4.pf | 2016年8月20日 20:23:24 | PF 文件 | 3 KB |
| CSRSET.EXE-F73AA5f9.pf | 2016年8月20日 19:35:25 | PF 文件 | 4 KB |
| TIH.EXE-A554A969.pf | 2016年8月17日 10:59:19 | PF 文件 | 7 KB |
| CRASHREPORTER.EXE-9FB27C0E.pf | 2016年8月20日 20:14:54 | PF 文件 | 7 KB |
| CREDENTIALHOST.EXE-A75048B5.pf | 2016年9月6日 06:09:22 | PF 文件 | 27 KB |
| NOTEPAD.EXE-51E1111.pf | 2010年9月11日 11:59:03 | PF 文件 | 10 KB |

**图 5-3** 预取文件夹。

文件名规则有一个例外，即托管其他组件的映像，包括管理控制 (`%SystemRoot%\System32\mm.exe`)、服务进程 (`%SystemRoot%\System32\svchost.exe`)、运行 DLL (`%SystemRoot%\System32\rundll3.exe`) 和 DllHost (`%SystemRoot%\System32\DllHost.exe`)。因为命令行中指定了这些组件，所以预取器包含了生成的命令行哈希值。因此，在不同的命令行下调用这些应用程序会产生不同的跟踪。

对于系统启动，使用了一种名为 `ReadyBoot` 的不同机制。ReadyBoot 通过创建大量读取并将数据存储在 RAM 中来优化 I/O 操作。这对于机械磁盘特别有益，但对 SSD 也有用处。启动完成后，RAM 中的缓存数据会被删除。对于非常快的 SSD，ReadyBoot 默认关闭，因为其收益微乎其微。

当系统启动或应用程序启动时，预取器会有一个机会进行预取。它会查找预取目录以查看是否存在跟踪文件。如果存在，预取器会调用 NTFS 预取元数据文件，读取所有引用的目录，并打开每个引用的文件。然后调用内存管理器函数 `MnPrefetch` 读取该跟踪中指定的任何数据。内存管理器会异步启动所有读取，并在离开应用程序之前等待它们完成。

# 实验：监控预取文件的写入

如果你在 Windows 客户端版中使用 Process Monitor 捕获应用程序启动的跟踪，你可以看到预取器检查应用程序的预取文件（如果存在）。此外，你还可以看到预取器在应用程序启动约 10 秒后写入。这里是设置了包含过滤器的 Notepad 启动捕获，Process Monitor 只显示对 `%SystemRoot%\Prefetch` 目录的访问：

| 序号 | 事件 | 时间 | 进程名称 | PID | 操作 | 路径 | 结果 |
|---|---|---|---|---|---|---|
| 1 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 2 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 3 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 4 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 4 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 5 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 6 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 7 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 8 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 9 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 10 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 11 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 12 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 13 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 14 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 15 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |

为了进一步优化，每隔三天或系统空闲期间，SuperFetch 服务会按照启动或应用程序启动时引用的顺序组织文件和目录，并存储在 `%SystemRoot\Prefetch\Layout.ini` 文件中（见图 5-34）。此列表包含了 SuperFetch 跟踪的频繁访问的文件。

它启动系统碎片程序并带有一个命令行选项，告诉碎片程序根据文件内容而不是全盘进行碎片。碎片程序会在每个卷上找到足够容纳该卷上列表文件和目录的连续区域，并将它们整体移动到该区域以便相邻存储。

# 放置策略

当读取接收到一个页面时，内存管理器必须决定将虚拟页面放置在物理内存中。它用于确定最佳位置的一组规则被称为放置策略。Windows 在选择页面帧时会考虑 CPU 缓存的大小，以减少不必要的缓存抖动。


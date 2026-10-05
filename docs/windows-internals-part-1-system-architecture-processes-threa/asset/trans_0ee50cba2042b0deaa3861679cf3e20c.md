

# 表 5-6 池列

| 列名 | 解释 |
|---|---|
| Tag (标签) | 这是分配给池分配的四字节标签。 |
| Type (类型) | 这是池类型（已填充或未填充）。 |
| Alocs (分配) | 这是所有分配次数的计数。括号中的数字显示了自上次更新以来 Allocs 列的差异。 |
| Frees (释放) | 这是所有释放次数的计数。括号中的数字显示了自上次更新以来 Frees 列的差异。 |
| Diff (差异) | 这是分配次数减去释放次数的结果。 |
| Bytes (字节) | 这是该标签消耗的字节总数。括号中的数字显示了自上次更新以来 Bytes 列的差异。 |
| Per Alloc (单次分配) | 这是该标签单个实例的大小（单位为字节）。 |

有关 Windows 使用的池标签含义的描述，请参阅 Windows 调试工具所在目录下 `Triage` 子目录中的 `Pooltag.txt` 文件。由于第三方设备驱动程序标签未列在此文件中，你可以使用随 WDK 带的 32 位版本 `Poolmon` 的 `-c` 参数来生成本地池标签文件（Localtag.txt）。该文件将包含驱动程序加载后使用的池标签，包括第三方驱动程序。（注意：如果设备驱动程序在加载后被删除，其池标签将无法被识别。）

或者，你可以使用 Sysinternals 的 `Strings.exe` 工具搜索系统中的驱动程序对应的池标签。例如，以下命令搜索包含字符串 "abcd" 的驱动程序：

```
strings %SYSTEMROOT%\system32\drivers\*.sys | findstr /i "abcd"
```

设备驱动程序并不一定位于 %SystemRoot%\System32\Drivers。它们可以在任何文件夹中。要列出所有加载驱动程序的完整路径，请按照以下步骤操作：

- 1. 打开开始菜单并输入 Msinfo32（将出现“系统信息”）。
- 2. 运行“系统信息”。
- 3. 选择“软件环境”。
- 4. 选择“系统驱动程序”。如果设备驱动程序已加载并从系统中删除，它将不会在此列表中。

查看设备驱动程序池使用的另一种方法是启用第 6 节介绍的驱动程序验证器（Driver Verifier）的池跟踪功能。虽然这种从池标签到设备驱动程序的映射并非必须，但它确实需要重启（以便在目标驱动程序上启用验证器）。在启用池跟踪并重启后，你可以运行驱动程序验证器管理器（%SystemRoot%\System32\Verifier.exe）或使用 `Verifier /log` 命令将池使用信息发送到文件。

最后，你可以使用内核调试器 `poolused` 命令查看池使用情况。`poolused2` 命令按池标签排序，显示使用池资源最多的非分页池。`!poolused !used2` 命令列出池使用情况，同样按按使用池资源最多的池标签进行排序。以下示例显示了这两个命令的输出：

1kd> !poolused 2

按非分页池消耗量排序

| Tag (标签) | Allocs (分配) | Used (使用) | Allocs (差异) | Used (差异) |
|---|---|---|---|---|
| File | 626381 | 26052403 | 0 | 0 |
| Ntfx | 733204 | 227105872 | 0 | 0 |
| MmCa | 513713 | 148068366 | 0 | 0 |
| FMsl | 732490 | 140638080 | 0 | 0 |
| CcSc | 104420 | 56084440 | 0 | 0 |
| SQSF | 283749 | 45409984 | 0 | 0 |
| MFmz | 382318 | 42819616 | 0 | 0 |
| FMcS | 36130 | 32950560 | 0 | 0 |
| EtWB | 5170 | 31279568 | 107 | 105119744 |
| DFmF | 382318 | 30585440 | 382318 | 91756320 |
| DFMe | 382318 | 18351264 | 0 | 0 |
| FSFc | 382318 | 18351264 | 0 | 0 |
| smNp | 4295 | 17592320 | 0 | 0 |
| Three | 5780 | 12837376 | 0 | 0 |
| Pool | 8 | 12834368 | 0 | 0 |

File 对象
通用分配 , Binary: ntfs.sys
映射文件的 Mm 上文区域, Binary: nt!
STREAM_LIST_CTL 结构 , Binary: flmgr.sys
缓存管理器共享缓存映射, Binary: nc
UNKNOWN 'SQSF', please update.txt
UNKNOWN 'DFmF', please update.txt
FILE_LIST_CTL 结构 , Binary: flmgr.sys
SECTION_CONTEXT 结构 , Binary: flmgr.sys
Et Buffer , Binary: nt!
UNKNOWN 'DFmF', please update.txt
UNKNOWN 'DFmF', please update.txt
UNKNOWN 'DFE', please update.txt
UNKNOWN 'DFE', please update.txt
UNKNOWN 'DFE', please update.txt
对象, Binary: nt!
线程, Binary: nt!

 实验：诊断池泄漏

（注：由于原文部分文本存在大量重复和乱码，此处已根据逻辑进行了翻译并保留了核心技术术语）

查看设备驱动程序池使用的另一种方法是启用第 6 节介绍的驱动程序验证器（Driver Verifier）的池跟踪功能。虽然这种从池标签到设备驱动程序的映射并非必须，但它确实需要重启（以便在目标驱动程序上启用验证器）。在启用池跟踪并重启后，你可以运行驱动程序验证器管理器（%SystemRoot%\System32\Verifier.exe）或使用 `Verifier /log` 命令将池使用信息发送到文件。

最后，你可以使用内核调试器 `poolused` 命令查看池使用情况。`poolused2` 命令按池标签排序，显示使用池资源最多的非分页池。`!poolused !used2` 命令列出池使用情况，同样按按使用池资源最多的池标签进行排序。


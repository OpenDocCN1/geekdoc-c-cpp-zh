

一个带有内置编辑器的二进制文件查看器，支持二进制、十六进制和反汇编模式。它使用原生语法进行反汇编。支持对 AVR/Java/Athon64/Pentium 4/K7-Athon 反汇编器的高亮、Runuis 编码页转换器，支持格式完整预览 - MZ, NE, PE, NLM, cod32，部分支持 - a.out, LE, LX, PharLap：代码导航器等功能。
（项目已重命名，请参阅 BEYE）

http://biew.sourceforge.net/en/biew.html

hview
一种基于 Aurses 的十六进制编辑器，旨在尽可能快速且以低开销处理大文件（600MB+）。

http://tdistortion.esmartdesign.com/Zips/hview.tz

# HT Editor (HT)

一个用于可执行文件的文件编辑器/分析器。它的目标是结合调试器的低级功能和 IDE 的易用性。

http://hte.sourceforge.net/

# HexCurve

一个用 C 语言编写的基于 ncurses 的十六进制编辑器，目前支持十六进制和十进制地址输出、跳转到指定文件位置、搜索、ASCII 和 EBCDIC 输出、加粗修改、撤销命令、快速键盘快捷键等。

http://www.jfish.net/description.php?title=HexCurve

# hexedit

以十六进制或 ASCII 格式查看并编辑二进制文件。

http://rigaux.org/hexedit.html

# Data Workshop (数据工作坊)

一个用于查看和修改二进制数据的编辑器；提供不同的视图，可用于编辑、分析和导出二进制数据。

http://www.dataworkshop.de/

# VCHE

一个十六进制编辑器，可以查看视频 ROM 中看到的全部 256 个字符，甚至是控制字符和扩展 ASCII，它使用 `/dev/vcs*` 设备进行编辑。它还可以编辑非标准文件、遍历硬盘、软盘、CD-ROM、PIPs、RAM 以及几乎任何设备。它带有 ncurses 版本以及一个适用于在 X 环境下或远程工作者的原始版本。

http://www.grigna.com/diego/linux/vche/

# DHEX

DHEX 是另一个带有 ncurses 差异模式（Diff-mode）的十六进制编辑器。它大量使用颜色并支持主题定制。

http://www.dettus.net/dhex/

# 3.2.3 Macintosh 十六进制编辑器

## wxHexEditor (免费且开源)

一个专门为巨大文件和磁盘设备设计的快速十六进制编辑器，支持高达艾字节（exabyte）的大小，允许在不创建临时文件的情况下更改（插入和删除），可以使用多窗格查看文件，内置反汇编器，支持用于（逆）工程十六进制二进制文件或文件系统的标签，可以使用 XOR 加密查看文件。

```
http://wxhexeditor.sourceforge.net/
```

# HexEdit

一个更改高亮颜色时简单但可靠的十六进制编辑器。还有一个针对 Apple Classic 用户的移植版本。

```
http://hexedit.sourceforge.net/
```

# Hex Fiend

非常简单但尽管极其强大。下载仅需 346 KB，可处理高达 116 GB 的文件。

```
http://ridiculousfish.com/hexfiend/
```

# 3.3 其他其他 Windows 工具

### 3.3.1 资源监器

Sysinternals Freeway
此页面包含大量优秀的实用程序，其中许多对安全专家、网络管理员以及（对逆向工程人员最重要）非常有用。特别是检查 Process Monitor、FileMon、RegMon、TCPView 和 Process Explorer。

```
http://technet.microsoft.com/sysinternals/default.aspx
```

### 3.3.2 API 监视

SpyStudio Freeway
Spy Studio 软件是一个挂钩 Windows 进程、日志到 DLL 的 Windows API 调用、插入断点并更改参数的工具。

```
http://www.nektra.com/products/spystudio/
```

rohit.com API Monitor
API Monitor 是一项可以监控应用程序和服务的 API 调用的免费工具。它包含详细的参数信息、结构体、联合、调用栈、内存以及 1300+ 接口。

# 分析工具

http://www.rohit.com/apimonitor

### 3.3. PE 文件头导出工具

# Dumpbin

Dumpbin 是随 Microsoft Visual Studio 提供的程序，用于导出信息。

```
dumpbin /options
```

它经常以这种方式使用：

```
link.exe /dump
```

它是处理此类转换的：

```
::dumpbin
```

这是以这种方式调用 dumpbin 的示例：

| 命令 | |
|--- |--- |
| dumpbin /PORTS | 显示从其他库导出的函数 |
| 库 | |
| dumpbin /IMPORTS | 显示从其他库导入的函数 |
| 可执行文件 | |
| dumpbin /HEADERS | 显示可执行文件的头部信息 |

http://msdn.microsoft.com/library/default.asp?url=..._core_dumpbin_reference.asp

# 依赖项

Dependency Walker 是一个 GUI 工具，可以查看二进制文件的导出和导入。它随许多 Microsoft 工具。

## 3.4 GNU 工具

GNU 软件包已移植到包括 Windows 在内的许多平台。

# GNU BinUtils

GNU BinUtils 包包含许多处理二进制文件非常有用的小工具。列表中最重要的程序是 GNU objdump、readelf、GAS 汇编器和 GNU 链接器，逆向人员可能还需要 addr2line、c++filt、nm 和 readelf。

```
http://www.gnu.org/software/binutils/
```

# objdump

dump 关于可执行文件的信息，包括符号和汇编。它是标准配置。它可以被支持非原生二进制格式。

```
objdump -p 显示从其他库导出的函数列表以及杂项头部信息
```

它用于从命令行检查 dll 依赖项

# readelf

类似于 objdump，但专门用于 ELF 可执行文件。

# size

列出段的大小。

# nm

列出文件的符号。

# strings

打印文件中的字符串。

# file 告诉你是文件类型。

# fold

折叠 strings 的结果。

# kill 可用于停止程序。

# strace

跟踪系统调用。

# 3.5 其他 Linux 工具

# oprofile

可以用于找出

# subteruge

一个对可执行文件进行戏弄的工具。用户可以为系统调用等事件编写脚本。

```
http://subteruge.org/
```

# lizard

让你反向运行程序。

http://lizard.sourceforge.net/

# dprobes

让你与内核和用户代码工作。

# biew

既是十六进制编辑器也是反汇编器。

# ltrace

显示动态可执行文件的运行时调用信息。

# asmDiff

在相同版本的二进制文件中搜索函数、指令和内存指针。支持 PE 和 ELF 文件中的 x86、x86_64 代码。

http://duschumpane.org/index.php/asmd


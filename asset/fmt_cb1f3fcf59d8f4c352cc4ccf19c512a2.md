
ldasm

LDasm (Linux Disassembler) 是一个基于 `Perl/Tk` 的 `objdump/binutils` GUI，试图模仿 `W32Dasm` 的“外观和感受”。它搜索交叉引用（例如字符串），将代码从 `GAS` 转换为 `MASM` 风格，跟踪程序并提供更多功能。附带 `PTrace`，一个进程记录器。

`http://www.feedface.com/projects/ldasm.html`

## 2.3 反汇编器问题

正如我们之前提到的，反汇编过程存在许多问题和困难。最主要的两个困难是代码与数据的划分，以及文本信息的丢失。

### 2.3.1 代码与数据的分离

由于数据和指令都以二进制数据的形式存储在可执行文件中，因此产生了一个明显的问题：反汇编器如何区分代码和数据？给定的任何字节是变量还是指令的一部分？

如果数据仅限于可执行文件的 `.data` 段（将在后文中解释），且可执行代码仅限于 `.code` 段，那么问题就不会那么困难了，但情况通常并非如此。数据可能直接插入代码段（例如跳转地址表、常量字符串），而可执行代码可能存储在数据段（尽管许多新系统出于安全考虑防止了这一点）。

许多交互式反汇编器会给用户渲染代码或数据段的选项，但非交互式反汇编器会自动进行分离。反汇编器通常在同一行内提供对应十六进制数据的指令 AND 形式，以减少对代码性质做出决定的需求。某些反汇编器允许你根据所研究对象的内容指定要反汇编的内容或标签名称的规则。以这种方式编写自己的“爬虫”更高效；对于大型程序，交互式反汇编可能不实际，甚至到了不可行的地步。

在任意可执行程序分离代码与数据的通用问题等同于停机问题。因此，无法编写一个能够为所有可能的输入程序正确分离代码和数据的反汇编器。逆向工程充满了此类理论限制，尽管根据 `Rice's theorem`，关于程序属性的所有有趣问题都是不可判的（因此编译器许多许多处理任何形式程序的工具都会遇到此类限制）。在实践中，通过交互式与自动分析相结合以及毅力，可以处理所有旨在阻碍逆向工程的程序，例如在使用之前进行加密和解密，并在内存中移动代码。

### 2.3.2 丢失的信息

所有基于文本的标识符（如变量名、标签名和宏）在汇编过程中都被删除了。它们可能仍存在于生成的对象文件中，供调试器和链接器使用，但直接连接已经丢失。没有了这些注释和标识符，更难理解源代码的目的，并且很难确定该代码所使用的算法。

### Hex-Rays 反汇编译器

Hex-Rays 是一款商业级反汇编译器。它是作为流行的 `IDA-Pro` 反汇编器的扩展代码制作的。它是目前唯一能产生可用结果的商业反汇编译器。它支持 `x86` 和 `ARM` 架构。

```
http://www.hex-rays.com/products/decompiler/index.html
```

### DCC 反汇编译器

Dcc 是对反编译的一种极佳的理论观察，但它只支持小文件。

```
http://www.itee.uq.edu.au/-cristina/dcc.html
```

### Boomerang 反汇编译器项目

Boomerang 反汇编译器试图创建一个强大的、可重目标的反汇编译器。到目前为止，它只能反编译为 `C` 语言，且成功率一般。

```
http://boomerang.sourceforge.net/
```

### 反向工程编译器 (REC)

REC 是一个强大的“反汇编译器”，它可以将原生汇编代码反编译为类 `C` 的代码表示。该代码介于汇编和 `C` 语言之间，但比纯汇编更易读。遗憾的是，该程序似乎相当不稳定。

```
http://www.backstreet.com/rnc/rec.html
```

### ExeToC

ExeToC 反汇编译器是一个交互式反汇编译器，其结果相当出色。

```
http://sourceforge.net/projects/exetoc
```

### Decompile-It

Decompile-It 是一个针对用 `-g` 编译的 32 位 Linux `x86` 可执行文件的 Web 反汇编译器。

```
http://decompile-it.com
```

大多数 CPU 都是 8 位 CPU。⁴

通常当子程序结束时，它会立即返回执行 `call` 指令之后的下一个地址。

然而，汇编语言程序员偶尔使用几种不同的技术来调整返回地址，使反汇编变得更加困难：

- 跳转表 (`jump tables`)，
- 计算跳转 (`calculated jumps`)，以及，
- `call` 指令后的参数。

+ 4 Jim Turley. "The Two Percent Solution" `{http://www.eetimes.com/discussion/other/4024488/The-Two-Percent-Solution}`. 2002.

### 2.6.1 跳转表和其他计算跳转

对于 8 位 CPU，计算跳转通常通过将一个计算出的“返回”地址推入栈中，然后使用 `return` 指令跳转到该地址来实现。例如，`RTS Trick`⁵ 使用这种技术来实现跳转表 (`w:branch table`⁶)。

### 2.6.2 call 指令后的参数

子程序不是从栈中或某些固定全局地址获取它们的参数，而是在调用该子程序的指令之后的内存地址处提供这些地址。使用这种技术的子程序会调整返回地址以跳过常量数据，然后返回到 `call` 指令后许多字节处的地址。使用这种技术的最著名的程序之一是 `Sweet 16` 虚拟机。

这种技术可能会使反汇编变得更加困难。

大多数 32 位 CPU 使用 `ARM` 指令集⁷⁸⁹。

典型的 `ARM` 汇编代码是一系列子程序，字面量常量散落在子程序之间。子程序的标准序言（`prolog`）和结尾（`epilog`¹⁰）很容易识别。

- `asgen`¹¹ 包含通用工具，并已用于为 `8080` `8086` `80386` `Alpha` `6809` 用于 `Pentium` `68000` `6502` `8051` 制作汇编器。¹¹。

| 索引 | 参考文献 |
| :--- | :--- |
| 5 | `http://wiki.nesdes.com/w/index.php/RTS_Trick` |
| 6 | `http://en.wikipedia.org/wiki/branch32table` |
| 7 | Jim Turley. "The Two Percent Solution" [`http://www.eetimes.com/discussion/other/4024488/The-Two-Percent-Solution.`] (2002). |
| 8 | Max Huffman. "ARM Core Club Into 3G Territory" [`http://www.extremetech.com/extreme/52186-arm-cores-club-into-3g-territory.`] (2002). 虽然 Intel 和 AMD 在法庭上获得了大部分关注，但 ARM 的 32 位架构... 已经卖掉了其他。 |
| 9 | Tom Kraitz. "ARMed for the living room [`http://www.cnet.com/ARMed-for-the-living-room/2100-1056-3-6056729.html`]" - ARM 授权了 16 亿核心 [2005年]。 2006. |
| 10 | `http://en.wikibooks.org/wiki/Embedded_Systems/Mixed_C_and_Assembly_Programming%ZARMY20` |
| 11 | `http://home.hccnet.nl/a.w.man.der.horst/asgen.fr` |

- `radare`，反向工程框架¹² 包含开源工具，用于反汇编许多处理器的代码，包括 `x86`, `ARM`, `PowerPC`, `m68k` 等，包括 `java`, `msil` 等在几个虚拟机，以及包括 `Linux`, `BSD`, `OS`, `Windows`, `iPhoneOS` 等在许多平台。

- `IDA`，交互式反汇编器¹³ (`IDA Pro`¹) 可以反汇编大量处理器的代码，包括 `ARM` 架构（包括 `Thumb` 和 `Thumb-2`），`ATMEL`, `AVR`, `INTEL 8051`, `INTEL 8086`, `MOS Technologies 6502`, `MC6809`, `MC6811`, `M68H2C`, `MSP430`, `PIC 12XX`, `PIC 14XX`, `PIC 16XX`, `ZilogXX`, `Zilog Z80` 等。

- `dmoz`: "Disassemblers"⁵ 列出了大量的反汇编器。

- 程序转换反汇编¹⁶ 许多备受推荐的反汇编器。

- Wikipedia: `objdump`¹⁷ 的 GNU `binutils`，可以反汇编几个处理器和平台的代码。

- 在 `SourceForge`¹⁸ 上搜索 "disassemble" 显示了用于各种 CPU 的反汇编器。`Hopper`¹⁹ 是一种运行在 `OS-X` 上并反汇编 32/64 位 `OS-X` 和二进制文件的反汇编器。

### 3.1 反汇编

大多数 CPU 都是 8 位 CPU。⁴

通常当子程序结束时，它会立即返回执行 `call` 指令之后的下一个地址。

然而，汇编语言程序员偶尔使用几种不同的技术来调整返回地址，使反汇编变得更加困难：

- 跳转表 (`jump tables`)，
- 计算跳转 (`calculated jumps`)，以及，
- `call` 指令后的参数。

对于 8 位 CPU，计算跳转通常通过将一个计算出的“返回”地址推入栈中，然后使用 `return` 指令跳转到该地址来实现。例如，`RTS Trick`⁵ 使用这种技术来实现跳转表 (`w:branch table`⁶)。

### 3.1.2 call 指令后的参数

子程序不是从栈中或某些固定全局地址获取它们的参数，而是在调用该子程序的指令之后的内存地址处提供这些地址。使用这种技术的子程序会调整返回地址以跳过常量数据，然后返回到 `call` 指令后许多字节处的地址。使用这种技术的最著名的程序之一是 `Sweet 16` 虚拟机。

这种技术可能会使反汇编变得更加困难。

一个受著名的 `OllyDbg`⁴ 启发的全功能插件型调试器。项目页面⁵ `KDBg`

一个针对 `KDE` 的 `gdb` 前端。`http://kdbg.`

一个针对 Linux 的 Ring-0 调试器。`RR0D` 项目页面⁶

### 3.1.3 其他系统的调试器

运行在源自 AT&T Unix 的系统上的 Unix 调试器。它通常是可选开发工具包的一部分，且需要额外付费。它使用交互式命令行界面。

一个来自 HP（原数字设备公司）的 Tru64 Unix 上的上的增强型调试器，它比 `dbx` 能够更好地处理线程等高级功能。

一个位于 Solaris 上的高级工具，它可以对整个系统（包括内核）提供性能分析等许多功能。

模块化调试器 (`MDB`) 是一种用于 Solaris 操作系统环境的新型通用型调试工具。它的主要特点是其可扩展性。Solaris 模块化调试器描述了如何使用 `MDB` 调试复杂的软件系统，特别强调了调试 Solaris 内核以及相关设备驱动和模块的可用设施。它还包含了对 `MDB` 语言语法、调试器功能以及 `MDB` 模块编程 API 的完整参考和讨论。

### 设置断点

正如之前在反汇编器章节中提到的，一个输出“Hello, World!”的 6 行 `C` 程序会变成大量的汇编代码。大多数人都不希望通过筛选整个这堆乱码来寻找他们想要的信息。仅仅通过翻阅代码来寻找所需信息可能耗费大量。作为替代方案，可以选择设置断点，以便在程序运行到代码中的给定点时将其停止。

例如，假设在你的程序中，在某个特定事件之后经常遇到崩溃：在关闭消息框之后立即。你对所有 `MessageBoxA` 的调用都设置了断点。你带有断点运行程序，它会停下来并准备调用 `MessageBoxA`。此后逐行执行代码（称为*单步执行* *stepping*）并观察程序堆栈，你发现在调用后不久发生了缓冲区溢出。

+ 4 `http://ollydbg.de`

5 `http://www.codef00.com/projects.php#Debugger`

6 `http://rr0d.droids-corp.org/`

`wxEditor` 十进制编辑器能够直接查看和编辑源文件的二进制文件，对于研究专有闭源格式数据文件的结构非常有用。本节将尝试列出一些最优秀、最流行或最强大的工具。

### 3.2.1 Windows 编辑器

`wxHexEditor`（免费且开源）

针对超大文件和设备的快速十六进制编辑器，支持高达艾字节的大小，允许在不创建临时文件的情况下更改大小（插入和删除），可以使用多窗格查看文件，内置反汇编器，支持用于（反）逆向工程大型二进制文件或文件系统的标签，可以查看经过 XOR 加密的文件。

```
http://wxhexeditor.sourceforge.net/
```

`HxD`（免费软件）

一个快速且强大的免费十六进制、磁盘和内存编辑器

```
http://mh-nexus.de/hxd/
```

免费 Hex编辑器 `XVI32`

一个适用于 Windows 的免费十六进制编辑器。

```
http://www.chmaas.handshake.de/delphi/freware/xvi32/xvi32.htm
```

`HHD Software Hex Editor Neo`

一个快速的磁盘和内存编辑器，内置反汇编器和文件结构查看器。

```
http://www.hhdsoftware.com/Family/hex-editor.html
```

`Catch22 HexEdit`

这是一个具有许多功能的强大十六进制编辑器。具有极的数据结构查看器。

```
http://www.catch22.net/software/hexedit.asp
```

`Breakpoint Hex Workshop`

```
7 http://en.wikipedia.org/wiki/hex%20editor
```

一个优秀且强大的十六进制编辑器，其实用性受限于它不像其他一些选项那样免费。

`http://www.bpsoft.com/`

##### Tiny Hexer

免费且提供统计功能。

`http://www.mirkes.de/files/`

`frhed` - 免费十六进制编辑器

适用于 Windows，免费开源。

`http://www.kibria.de/frhed.html`

##### Cygnus Hex Editor

一个非常快速且易用的十六进制编辑器，提供“免费版”。

`http://www.softcircuits.com/cygnus/fe/`

##### Hexprobe Hex Editor

一个专业的十六进制编辑器，旨在包含处理十六进制数据的所有功能，在十六进制编辑和字节模式分析领域特别有用。

`http://www.hexprobe.com/hexprobe/index.htm`

##### UltraEdit32

一个十六进制编辑器/文本编辑器，曾获得 2005 年共享软件行业奖会议的“年度应用程序”奖。

`http://www.ultraedit.com/`

##### ICY Hexplorer

一个轻量级的免费开源十六进制文件编辑器，具有一些巧妙的功能，如像素视图、结构体、反汇编。

`http://explorer.sourceforge.net/`

##### WinHex

一个强大的十六进制文件和磁盘编辑器，具有计算机取证和数据恢复的高级能力（被政府和军队使用）。

`http://www.x-ways.net/index-m.html`

##### 010 Editor

一个非常强大且快速的十六进制编辑器，对数据结构和脚本有广泛支持。可以用于编辑驱动器和进程。

`http://www.sweetscape.com/010editor/`

![](img/9b6491f497)

运行在源自 AT&T Unix 的系统上的 Unix 调试器。它通常是可选开发工具包的一部分，且需要额外付费。它使用交互式命令行界面。

一个来自 HP（原数字设备公司）的 Tru64 Unix 上的增强型调试器，它比 `dbx` 能够更好地处理线程等高级功能。

一个位于 Solaris 上的高级工具，它可以对整个系统（包括内核）提供性能分析等许多功能。

模块化调试器 (`MDB`) 是一种用于 Solaris 操作系统环境的新型通用型调试工具。它的主要特点是其可扩展性。Solaris 模块化调试器描述了如何使用 `MDB` 调试复杂的软件系统，特别强调了调试 Solaris 内核以及相关设备驱动和模块的可用设施。它还包含了对 `MDB` 语言语法、调试器功能以及 `MDB` 模块编程 API 的完整参考和讨论。

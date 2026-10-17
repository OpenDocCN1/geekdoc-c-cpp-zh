
# X86 反汇编：探索 C 语言、x86 汇编与机器码之间的关系

- 12.2 GNU C 编译器 ................................................................................................................................................... 87
- 21.2 调用约定 ...................................................................................... 143
+ 25.6 代码转换 . . . . . . . . . . . . . . . . 171
+ 25.8 代码解密器 . . . . . . . . . . . . . . . . . 172
# 28 贡献者 . . . . . . . . . . . . . . . . 181

## 插图列表

### 1.1 汇编器

汇编器¹比编译器要简单得多，通常实现为仅通过一一对应关系将汇编代码翻译为二进制代码。汇编器很少在选择指令的最短形式或填充延迟槽之外进行优化。

由于汇编只是一个简单的过程，反汇编通常也同样简单。汇编指令和机器码字之间有一一对应的关系，因此每个机器码字都将精确映射到一条汇编指令。反汇编存在一些无法通过简单的代码字查找来解决的困难性。我们将在此处介绍汇编器，稍后会讨论反汇编。

### 1.2 汇编器概念

在最基础层面，汇编器将汇编指令一一对应地翻译成机器码。它们还可以将变量名翻译为硬编码的内存地址以及相对代码地址中的标签。

通常，汇编器不执行代码优化。汇编器输出的机器码等同于输入汇编器的汇编指令。某些汇编器以宏的形式具有高级功能。

在汇编过程中，程序的一些信息会丢失。首先也是最重要的是，程序数据是以原始二进制格式作为机器码指令存储的。这意味着很难确定程序的哪些部分实际上是指令。注意，你可以反汇编原始数据，但生成的汇编代码将是毫无意义的。其次，汇编源文件中的文本信息（如变量名、标签和注释）在汇编过程中都会被破坏。当你反汇编代码时，指令是相同的，但所有其他有用信息都会丢失。代码是准确的，但更难以阅读。

正如我们后面看到的，编译器会导致更多信息的丢失，而反编译往往如此复杂混乱，以至于几乎无法准确执行。

### 1.3 Intel 语法汇编器

由于基于 Intel 的 IA-32 微处理器在家庭 PC 市场的普及，大多数的汇编工作（以及本书中考虑的大多数汇编工作）都是基于 x86 的。这些汇编器（或它们的新版本）可以很好地处理 amd64/x86_64/EMT64 代码，尽管本书将主要关注 32 位（x86/IA-32）代码示例。

#### 1.3.1 MASM

MASM 是微软的汇编器，“Macro Assembler”（宏汇编器）的缩写。然而，许多人将其作为“Microsoft Assembler”（微软汇编器）的缩写，这种区别完全没有问题。MASM 拥有强大的宏功能，并能够利用其宏功能编写非常底层的语法和伪高级代码。MASM 6.15 目前可以从微软免费下载，而 MASM 7.xx 目前作为微软平台 DDK 的一部分。

- MASM 使用 Intel 语法。
- 微软使用 MASM 实现其 Windows 操作系统的一些底层部分。
- 与大众认知相反，MASM 从 1980 年以来一直在持续开发，并根据需要进行升级。
- 微软一直确保 MASM 与当前平台和可执行文件类型兼容。
- MASM 目前支持所有 Intel 指令集，包括 SSE2。

许多用户喜欢 MASM，但许多人仍然讨厌无法移植到其他系统的事实。

#### 1.3.2 TASM

TASM 是 Borland 的“Turbo Assembler”（快速汇编器），是来自 Borland 的功能性汇编器，与 Borland 的其他软件开发工具无缝集成。当前发布版本为 5.0。TASM 与 MASM 非常相似，事实也如此。

#### 1.3.3 NASM

NASM 是“Net Assembler”（网络汇编器），是来自 Borland 的功能性汇编器，与 Borland 的其他软件开发工具无缝集成。当前发布版本为 5.0。TASM 与 MASM 非常相似，事实也如此。

#### 1.3.4 FASM

FASM 是“Flat Assembler”（平面汇编器），是来自 Borland 的功能性汇编器，与 Borland 的其他软件开发工具无缝集成。当前发布版本为 5.0。TASM 与 MASM 非常相似，事实也如此。

### 1.4 (&T) 语法汇编器

#### 1.4.1 GAS

GNU 汇编器 `GAS` 作为 `GCC` 的一部分提供。某些编译器，例如微软

- * http://en.wikibooks.org/wiki/Compiler%20Construction

### 1.5 其他汇编器

#### 1.5.1 HLA

HLA³ 是“High Level Assembler”（高级汇编器）的简称，是 Randall Hyde 创建的一个项目，HLA 支持常见的汇编语言，还实现了若干高级结构，如循环、if-then-else 分支和函数。HLA 配带了完整的库。

由于 HLA 作为另一个汇编器的前端工作，程序员必须拥有另一个汇编器来汇编 HLA 程序。

- 2 http://en.wikipedia.org/wiki/GNU%Assembler
- 3 http://en.wikipedia.org/wiki/High%20Level%20Assembly

C 编译器直接将 C 和 C++ 源代码编译为机器码。而 GCC 则是将 C 和 C++ 转换为汇编语言，然后使用汇编器将其转换为相应的机器码。从反汇编器的角度来看，它发现无法精确地还原出最初创建可执行文件时所使用的 C 或 C++ 代码。然而，可以创建出与原代码编译结果完全相同、或者执行相同任务的代码。

C 语言语句与汇编语言之间并不是一一对应的关系。请考虑以下语句通常会编译成相同的汇编代码：

```
*arrayA = arrayB[x];
*arrayA = arrayB[x];
arrayA[0] = arrayB[x];

arrayA(0) = arrayB[x];
```

此外，考虑以下循环是如何执行相同任务的，并且它们可能会产生相似甚至相同的汇编代码：

```
for(;;) { ... }
while(i) { ... }
do { ... } while(i);
```

## 1.7 常见的 C/C++ 编译器

本节的目的是列出用于生产级软件开发的最常用的 C 和 C++ 编译器。世界上有很多 C 编译器，但逆向工程人员不需要考虑所有情况，特别是在查看专业软件时。本页将讨论每个编译器的优缺点（下载站点或成本信息），还将讨论如何从每种编译器生成汇编列表文件。

### 1.7.1 微软 C 编译器

微软 C 编译器由微软作为 Windows Server 2003 SDK 的一部分免费提供。它与 MS Visual Studio 中使用的编译器和库是同一个，但不带华丽的 IDE。MS C 编译器拥有非常出色的优化引擎。它可以编译 C 和 C++，并可以选择将 C++ 代码编译为 MSIL（.NET 字节码）。

微软的编译器仅支持 Windows 系统以及与 Intel 兼容的 16/32/64 位架构。

> http://en.wikibooks.org/wiki/C%2B%2B%20Programming%2FProgramming%20Languages%2FC%2B%2B%2BCode%2F%2FCompiler

### 汇编器与编译器

微软 C 编译器是 `cl.exe`，链接器是 `link.exe`。

### 列表文件

在书中，`cl.exe` 常用于生成 C 源代码的汇编列表文件。若要自己生成汇编列表文件，请使用语法：

```
cl.exe /Fa*assembly file name <C source file>
```

`/Fa*` 关是一个命令行选项，告诉编译器生成汇编列表文件。

例如，以下命令行：

```
cl.exe /Faest.asm Test.c
```

将从 C 源文件 'Test.c' 生成名为 'Test.asm' 的汇编列表文件。注意，`/Fa` 关与输出文件名之间没有空格。

### 1.7.2 GNU C 编译器

GNU C 编译器是 GNU 编译器集合 `GCC` 套件的一部分。该编译器适用于大多数系统，并且是免费软件。许多人专门使用它，以便用一个编译器处理许多平台。GNU GCC 是 Linux 和 Unix 系统的事实性标准编译器。它是可重定向的，允许许多输入语言（C, C++, Obj-C, Ada, Fortran 等），并支持多个目标操作系统和架构。它优化得良好，但 IA-32 代码生成引擎不够激进。

GCC 前端程序是 `gcc`（Windows 上的 `gcc.exe`），关联的链接器是 `ld`（Windows 上的 `ld.exe`）。

### 列表文件

要在 GCC 中生成汇编列表文件，请使用以下命令：

```
gcc -S <sourcefile>
```

例如，以下命令行：

```
gcc.exe -S test.c
```

将生成一个名为 'test.s' 的汇编列表文件。

GCC 前端程序是 `gcc`（Windows 上的 `gcc.exe`），关联的链接器是 `ld`（Windows 上的 `ld.exe`）。

### 1.7.3 Intel 编译器

Intel 编译器由 Intel 提供的，用于优化 x86 代码。它支持多种汇编语言，并可以输出 Intel 或 AT&T 语法。书中的示例将交叉使用 Intel 和 AT&T 语法，但以后可能会改变。

### 1.7.4 Metrowks CodeWarrior

该编译器通常用于 MacOS 和嵌入系统。如果你对电子产品进行逆向工程，可能会遇到 Metrowks 生成的代码。

### 1.7.5 Green Hills Software

该编译器通常用于嵌入式系统。如果你对电子产品进行逆向工程，可能会遇到 Green Hills 生成的代码。

## 2 反汇编器与反编译器

### 2.1 什么是反汇编器？

反汇编器：本质上说，**反汇编器**是汇编器的相反。汇编器将汇编语言转换为二进制机器码，反汇编器反转这一过程，从二进制机器码还原汇编代码。由于大多数汇编语言与机器码是一一对应的，反汇编过程相对直接。当然，反汇编也有自己的问题和陷阱，将在本文介绍。许多反汇编器支持输出 Intel、AT&T 或偶尔的 HLA 语法。书中示例将使用 Intel 和 AT&T 语法。

### 2.2 x86 反汇编器

在这里我们将列一些常用的反汇编工具。注意，有专业的反汇编器（需要购买许可证），也有免费/共享版反汇编器。每个反汇编器的功能都不同，因此由读者来决定偏于使用哪些工具。

#### 2.2.1 商业版反汇编器

##### IDA Pro

是一种专业的反汇编器，价格昂贵、功能强大且特性众多。IDA Pro 的缺点是单用户价格为 515 美元。存在免费版本，见下文。

- [http://www.hex-rays.com/idapro/](http://www.hex-rays.com/idapro/)

##### Hopper Disassembler

适用于 Mac 的逆向工程工具，可以反汇编、反编译和调试 32/64 位可执行文件。

#### 2.2.2 免费/共享 Windows 反汇编器

##### OllyDbg

OllyDbg 最近是最流行的反汇编器之一。它拥有庞大的社区和各种插件。它强调二进制代码分析。支持 x86 指令。

- http://www.ollydbg.de/（官方网站）
- http://www.openrc.org/downloads/browse/OllyDbg_Plugins（插件）

#### 2.2.3 Windows 反汇编器

##### Objconv

一个支持 16、32 和 64 位 x86 代码的命令行反汇编器。支持最新的指令集（SSE4, AVX, XOP, FMA 等）、多种对象文件格式、多种汇编语法方。支持 Windows、Linux、Mac。智能分析。

- http://www.agner.org/optimize/#objconv

##### x86 反汇编器

- * http://www.simtel.net/product.php (搜索 ida37fw)

##### IDA Pro 免费版

行为几乎与 IDA Pro 完全一致，但只能反汇编 Intel x86 机器码且仅限 Windows。你可以反汇编截至 2003 年可用的处理器。非商业用途免费。

- (version 4.1) http://www.themel.com/idafree.zip
- (version 4.3) http://www.datarescue.be/idafree/freeida43.exe
- (version 5.0) http://www.x-rays.com/idapro/idadownfreeware.htm

##### BORG 反汇编器

BORG 是一个带有 GUI 的优秀 Win32 反汇编器。

http://www.caesum.com/

##### HT Editor

用于 Intel x86 指令的分析反汇编器。最新版本在 Windows 上作为控制台 GUI 程序运行，但也有为 Linux 编译的版本。

http://hte.sourceforge.net/

##### diStorm64

diStorm 是一个针对 80x86 和 AMD64 的开源高度优化流反汇编库。

http://ragestorm.net/distorm/

##### crudasm

crudasm 是一个具有多种选项的开源反汇编器。它仍在开发中，附带了一个部分反编译器。

http://code.google.com/p/vm64dec/downloads/list

##### BeaEngine

BeaEngine 是一个针对 IA-32 和 intel64 架构的完整反汇编库（用 C 编写，适用于多种语言：C, Python, Delphi, WinDev, masm, nasm, Go）。

http://www.beaengine.org

##### VisualDebugger

适用于 Windows 的 64 位用户态调试器反汇编器。

http://www.duxcore.com/

##### BugDbg

是一个用于调试原生 64 位应用的 64 位调试器。

http://www.pespin.com/

##### DSMHELP

Disassemble Help 是一个带有单行多态汇编器的反汇编库。支持的指令集包括 SSE, SSE2, SSE3, SSE4, FPU, VMX, SVM, AVX2, BMI1, BMI2

http://dmshelp.narod.ru/（俄语）

## 2.2 Unix 反汇编器

##### Bastard 反汇编器

Bastard 反汇编器是一个适用于 Linux 和 FreeBSD 的强大、可脚本的反汇编器。

http://bastard.sourceforge.net/

##### udis86

用于 x86 和 x64 的反汇编库。

http://udis86.sourceforge.net/

##### Objconv

见上文。

##### ciasdis

ciasdis 的正式名称为 computer_intelligence_assembler。这种基于 Forth 的工具之处在于，所有反汇编的代码都可以重新汇编成完全相同的代码。支持的处理器有 8080, 6809, 8086, Pentium Alpha，脚本功能有助于分析 ELF 头并使该工具具有扩展性，可加载到同一站点。

http://home.ccnet/a.van.der.horst/ciasdis.html

### objdump

标准配置，通常用于对二进制文件的常规检查。请注意重定位选项和动态符号表。

##### gdb

标准配置，作为调试器使用，但也经常用于反汇编。如果你有松散数据想要反汇编，只需（交互式地）覆盖其他内容，或将其编译为程序，例如：`char foo[] = {0x90, 0xcd, 0x80, 0xcf, 0x90};`

##### linux 交互式反汇编器

一个具有某些特殊功能（如加密分析器）的交互式反汇编器。显示字符串引用、代码流分析，且不依赖 objdump。利用 Bastard 反汇编库解码单个操作码。该项目始于 2004 年，至今一直处于静态状态。

http://ida.sourceforge.net

# 反汇编器问题 (Issues)

dissy

此程序是一个使用 objdump 的交互式反汇编器。

http://code.google.com/p/dissy/

x86dis

此程序可显示二进制流，例如引导区或其他非结构化二进制文件。

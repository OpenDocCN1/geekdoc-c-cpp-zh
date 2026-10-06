

## 2.5 常见的反汇编译器

### Hex-Rays 反汇编译器

Hex-Rays 是一款商业级反汇编译器。它是作为流行的 IDA-Pro 反汇编器的扩展代码制作的。它是目前唯一能产生可用结果的商业反汇编译器。它支持 x86 和 ARM 架构。

```
http://www.hex-rays.com/products/decompiler/index.html
```

### DCC 反汇编译器

Dcc 是对反编译的一种极佳的理论观察，但它只支持小文件。

```
http://www.itee.uq.edu.au/-cristina/dcc.html
```

### Boomerang 反汇编译器项目

Boomerang 反汇编译器试图创建一个强大的、可重目标的反汇编译器。到目前为止，它只能反编译为 C 语言，且成功率一般。

```
http://boomerang.sourceforge.net/
```

### 反向工程编译器 (REC)

REC 是一个强大的“反汇编译器”，它可以将原生汇编代码反编译为类 C 的代码表示。该代码介于汇编和 C 语言之间，但比纯汇编更易读。遗憾的是，该程序似乎相当不稳定。

```
http://www.backstreet.com/rnc/rec.html
```

### ExeToC

ExeToC 反汇编译器是一个交互式反汇编译器，其结果相当出色。

```
http://sourceforge.net/projects/exetoc
```

### Decompile-It

Decompile-It 是一个针对用 -g 编译的 32 位 Linux x86 可执行文件的 Web 反汇编译器。

```
http://decompile-it.com
```

## 2.6 8 位 CPU 代码的反汇编

大多数 CPU 都是 8 位 CPU。⁴

通常当子程序结束时，它会立即返回执行 'call' 指令之后的下一个地址。

然而，汇编语言程序员偶尔使用几种不同的技术来调整返回地址，使反汇编变得更加困难：

- 跳转表 (jump tables)，
- 计算跳转 (calculated jumps)，以及，
- call 指令后的参数。

+ 4 Jim Turley. "The Two Percent Solution" {http://www.eetimes.com/discussion/other/4024488/The-Two-Percent-Solution}. 2002.

### 2.6.1 跳转表和其他计算跳转

对于 8 位 CPU，计算跳转通常通过将一个计算出的“返回”地址推入栈中，然后使用 'return' 指令跳转到该地址来实现。例如，RTS Trick⁵ 使用这种技术来实现跳转表 (w:branch table⁶)。

### 2.6.2 call 指令后的参数

子程序不是从栈中或某些固定全局地址获取它们的参数，而是在调用该子程序的指令之后的内存地址处提供这些地址。使用这种技术的子程序会调整返回地址以跳过常量数据，然后返回到 'call' 指令后许多字节处的地址。使用这种技术的最著名的程序之一是 'Sweet 16' 虚拟机。

这种技术可能会使反汇编变得更加困难。

## 2.7 32 位 CPU 代码的反汇编

大多数 32 位 CPU 使用 ARM 指令集⁷⁸⁹。

典型的 ARM 汇编代码是一系列子程序，字面量常量散落在子程序之间。子程序的标准序言（prolog）和结尾（epilog¹⁰）很容易识别。

## 2.8 反汇编器列表

- asgen¹¹ 包含通用工具，并已用于为 8080 8086 80386 Alpha 6809 用于 Pentium 68000 6502 8051 制作汇编器。¹¹。

| 索引 | 参考文献 |
| :--- | :--- |
| 5 | http://wiki.nesdes.com/w/index.php/RTS_Trick |
| 6 | http://en.wikipedia.org/wiki/branch32table |
| 7 | Jim Turley. "The Two Percent Solution" [http://www.eetimes.com/discussion/other/4024488/The-Two-Percent-Solution.] (2002). |
| 8 | Max Huffman. "ARM Core Club Into 3G Territory" [http://www.extremetech.com/extreme/52186-arm-cores-club-into-3g-territory.] (2002). 虽然 Intel 和 AMD 在法庭上获得了大部分关注，但 ARM 的 32 位架构... 已经卖掉了其他。 |
| 9 | Tom Kraitz. "ARMed for the living room [http://www.cnet.com/ARMed-for-the-living-room/2100-1056-3-6056729.html] - ARM 授权了 16 亿核心 [2005年]。 2006. |
| 10 | http://en.wikibooks.org/wiki/Embedded_Systems/Mixed_C_and_Assembly_Programming%ZARMY20 |
| 11 | http://home.hccnet.nl/a.w.man.der.horst/asgen.fr |

## 扩展

- radare，反向工程框架¹² 包含开源工具，用于反汇编许多处理器的代码，包括 x86, ARM, PowerPC, m68k 等，包括 java, msil 等在几个虚拟机，以及包括 Linux, BSD, OS, Windows, iPhoneOS 等在许多平台。
- IDA，交互式反汇编器¹³ (IDA Pro¹) 可以反汇编大量处理器的代码，包括 ARM 架构（包括 Thumb 和 Thumb-2），ATMEL, AVR, INTEL 8051, INTEL 8086, MOS Technologies 6502, MC6809, MC6811, M68H2C, MSP430, PIC 12XX, PIC 14XX, PIC 16XX, ZilogXX, Zilog Z80 等。
- dmoz: "Disassemblers"⁵ 列出了大量的反汇编器。
- 程序转换反汇编¹⁶ 许多备受推荐的反汇编器。
- Wikipedia: objdump¹⁷ 的 GNU binutils，可以反汇编几个处理器和平台的代码。
- 在 SourceForge¹⁸ 上搜索 "disassemble" 显示了用于各种 CPU 的反汇编器。Hopper¹⁹ 是一种运行在 OS-X 上并反汇编 32/64 位 OS-X 和二进制文件的反汇编器。

## 2.9 扩展阅读

- radare，反向工程框架¹² 包含开源工具，用于反汇编许多处理器的代码，包括 x86, ARM, PowerPC, m68k 等，包括 java, msil 等在几个虚拟机，以及包括 Linux, BSD, OS, Windows, iPhoneOS 等在许多平台。
- IDA，交互式反汇编器¹³ (IDA Pro¹) 可以反汇编大量处理器的代码，包括 ARM 架构（包括 Thumb 和 Thumb-2），ATMEL, AVR, INTEL 8051, INTEL 8086, MOS Technologies 6502, MC6809, MC6811, M68H2C, MSP430, PIC 12XX, PIC 14XX, PIC 16XX, ZilogXX, Zilog Z80 等。
- dmoz: "Disassemblers"⁵ 列出了大量的反汇编器。
- 程序转换反汇编¹⁶ 许多备受推荐的反汇编器。
- Wikipedia: objdump¹⁷ 的 GNU binutils，可以反汇编几个处理器和平台的代码。
- 在 SourceForge⁸ 上搜索 "disassemble" 显示了用于各种 CPU 的反汇编器。Hopper¹⁹ 是一种运行在 OS-X 上并反汇编 32/64 位 OS-X 和二进制文件的。

## 3 分析工具

### 3.1 反汇编

大多数 CPU 都是 8 位 CPU。⁴

通常当子程序结束时，它会立即返回执行 'call' 指令之后的下一个地址。

然而，汇编语言程序员偶尔使用几种不同的技术来调整返回地址，使反汇编变得更加困难：

- 跳转表 (jump tables)，
- 计算跳转 (calculated jumps)，以及，
- call 指令后的参数。

### 3.1.1 跳转表和其他计算跳转

对于 8 位 CPU，计算跳转通常通过将一个计算出的“返回”地址推入栈中，然后使用 'return' 指令跳转到该地址来实现。例如，RTS Trick⁵ 使用这种技术来实现跳转表 (w:branch table⁶)。

### 3.1.2 call 指令后的参数

子程序不是从栈中或某些固定全局地址获取它们的参数，而是在调用该子程序的指令之后的内存地址处提供这些地址。使用这种技术的子程序会调整返回地址以跳过常量数据，然后返回到 'call' 指令后许多字节处的地址。使用这种技术的最著名的程序之一是 'Sweet 16' 虚拟机。

这种技术可能会使反汇编变得更加困难。

### 3.2 调试器

大多数 CPU 都是 8 位 CPU。⁴

通常当子程序结束时，它会立即返回执行 'call' 指令之后的下一个地址。

然而，汇编语言程序员偶尔使用几种不同的技术来调整返回地址，使反汇编变得更加困难：

（此处为重复内容，已按要求不重复输出原文）


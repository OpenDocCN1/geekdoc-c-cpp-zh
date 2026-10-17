
文件以头文件开头，指示了 XML 文件的版本和字符编码，它包含一个主“书籍”（book）元素。元素以角括号中的一个单词开始，例如 `<body>`。要结束一个元素，在角括号中放置相同的单词并在单词前添加一个正斜杠，如 `</body>`。除了元素之外，还有 XML 属性。`title="Essential C#"` 是一个 XML 属性的示例。请注意，描述数据（“Essential C#”、“Data Types”）的元数据也包含在 XML 文件中，但它的优势是数据包含了有助于解释其本身的描述。

## 调试

使用 IDE 的一个重要特性是其对调试的支持。若要尝试该功能，请在 Visual Studio 的任一操作系统版本或 Visual Studio Code 中遵循以下额外步骤：

- 打开最新版本的 `Program.cs`（列表 1.9），将光标置在最后一行 `Console.WriteLine` 上，并点击“调试->切换断点 (F9)”菜单项以在该行上激活断点。
- 在 Visual Studio 中，点击“调试->开始调试 (F5)”菜单，此时将在激活调试的情况下重新启动应用程序。
- Visual Studio Code 类似之处，但菜单为“运行->开始调试 (F5)”。如果你还没有创建它们，Visual Studio Code 还会显示提示创建构建和调试资源，即 `launch.json` 和 `tasks.json` 文件。由于 `Console.ReadLine` 语句的存在，你还需要更改 `launch.json` 文件中的控制台行，使用“integratedTerminal”而不是“internalConsole”。现在，当调试时，务必切换到 TERMINAL 输出窗口以响应程序的输入。
- 一旦开始调试，执行将在你设置断点的那行停止。然后，你可以将光标悬停在变量（例如 `firstName`）上以查看其值。
- 在 Visual Studio 中，你甚至可以通过在文件窗口左侧边缘拖动黄色箭头，将程序的执行从当前行移动到另一行。
- 要继续程序执行，请使用对应 IDE 的“继续”按钮（或 Visual Studio 中的“调试->继续 (F5)”或 Visual Studio Code 中的“运行->继续 (F5)”）。

有关调试的更多信息，请参考对应版本的链接：

- Visual Studio: https://learn.microsoft.com/visualstudio/debugger/feature-tour
- Visual Studio 2022 for Mac: https://learn.microsoft.com/visualstudio/mac/
- Visual Studio Code: https://code.visualstudio.com/Docs/editor/debugging

## 第 1 章：简介 C#

### 托管执行与通用语言体系

处理器无法直接解释程序集。.NET 程序集主要由一种被称为通用中间语言（Common Intermediate Language，简称 CIL 或 IL）¹⁴ 的第二种语言组成。C# 编译器将 C# 源代码文件转换为这种中间语言。还需要一个额外的步骤（通常在执行时完成）将 CIL 转换为处理器可以理解的机器码。这涉及到 C# 程序执行中的一个重要元素：虚拟执行系统（VES）。VES 也被俗地称为运行时（runtime），它根据需要编译 CIL 代码（此过程被称为即时编译或 jutting）。在运行时等代理（agent）的语文中执行的代码被称为托管代码，而在运行时控制下执行的过程被称为托管执行。代码之所以是“被托管”的，是因为运行时通过管理内存分配、安全性和即时编译等方面控制了程序行为的大部分内容。

14. CIL 的第三个名称是 Microsoft IL (MSIL)。本本书使用 CIL 术语，它是 CIL 标准采用的术语。在编写 C# 代码的人员中，IL 非常流行，因为他们假设 IL 指的是 CIL 而不是其他类型的中间语言。不需要运行时即可执行的代码被称为原生代码（或未托管代码）。

运行时的规范包含在更广泛的规范中，称为通用语言体系（Common Language Infrastructure，简称 CLI）规范¹⁵。作为一个国际标准，CLI 包含了以下内容的规范：

> 注意
> “运行时”（runtime）一词可以指执行时间，也可以指 VES。为了帮助澄清意图，本书使用“执行时间”（execution time）一词表示程序正在执行时，并在讨论负责管理 C# 程序执行的代理时使用“运行时”（runtime）一词。

在运行时执行引擎的语文中运行可以支持程序员无需直接编码的若干服务和功能，包括以下内容：

15. Miller, J., and S. Ragsdale. 2004. The Common Language Infrastructure Annotated Standard. Boston: Addison-Wesley.

> 注意
> 本节提供了 CLI 的简要概述，以便你熟悉 C# 程序执行的背景。它还对书中处处的一些术语进行了总结。第 24 章专门讨论 CLI 主题及其对 C# 开发者的意义。尽管该章节出现在书的后部，但它不依赖之前的任何章节，如果你渴望更熟悉 CLI，可以随时跳转到那里。

- 语言互操作性：不同源语言之间的互操作性。这是可能的，因为语言编译器将每种源语言转换为相同的中间语言 (CIL)。
- 类型安全：检查类型之间的转换，确保只在兼容类型之间发生转换。这有助于防止缓冲区溢出的发生，溢出是安全漏洞的主要原因。
- 代码访问安全：证明程序集具有执行权限。
- 垃圾收集：自动释放由运行时之前分配的内存的内存管理。
- 平台可移植性：支持在各种操作系统上运行相同的程序集。
- 基类库 (BCL)：提供开发者无需开发的基础。

### 通用中间语言与 ILasm

如在本节介绍中提到的，C# 编译器将 C# 代码转换为 CIL 而不是机器码。处理器可以直接理解机器码；因此 CIL 代码在执行前需要进行转换。给定程序集，可以使用 CIL 反汇编器查看 CIL 代码。（CIL 反汇编器被亲切地称为其 .NET 特定的文件名 ILasm，代表 IL Disassembler。）ILasm 反汇编程序集并提取 CIL 文本。

.NET 程序集的输出比机器码更容易理解得多。对于许多开发者来说，这可能会引发担心，因为在不明确分发源代码的情况下，算法更容易被理解。对于任何程序，无论是否基于 CLI，防止反汇编的唯一可靠方法是不允许访问（例如将程序托管在网站上而不是分发给用户）。但是，如果只需要降低代码的访问性，有几种混淆器可用。混淆器读取 IL 代码并对其转换，使其变得难以理解。这种技术防止了普通开发者访问代码，并创建了难以反编译为理解代码的程序集。除非程序需要高度的算法安全性，否则混淆器足够了。

### 主题：HelloWorld.exe 的 CIL 输出

用于 CIL 反汇编器的具体命令取决于使用的 CLI 实现。指令可以参见 http://itl.tc/ildasm。列表 1.22 显示了运行 ildasm 产生的 CIL 代码。

#### 列表 1.22：示例 CIL 输出

```
.assembly extern System.Runtime

{

.publickeytoken = (B0 3F 5F 7F 11 D5 0A 3A )

.ver 4:2:0:1

}
```

```
.assembly extern System.Console

{

.publickeytoken = (B0 3F 5F 7F 11 D5 0A 3A )

.ver 4:1:0:1

}
```

## 42 第 1 章：介绍 C#

```assembly
.assembly 'HelloWorld'

{
    custom instance void [System.Runtime]System.Runtime.CompilerServices.
    CompilationRelaxationsAttribute::.ctor(int32) = (01 00 0A 48 65 00 00 00 00
00)
    custom instance void [System.Runtime]System.Runtime.CompilerServices.
    RuntimeCompatibilityAttribute::.ctor() = (01 00 01 00 54 02 16 57 72 61
70 4E 6C 6E 7F 65 47 63 75 72 69 6F 62 72 72 73 03 01)
    custom instance void [System.Runtime]System.Runtime.Versioning.
    TargetFrameworkAttribute::.ctor(string) = (01 00 18 2E 4E 45 54 43 63 6F
72 65 41 70 20 5C 55 65 73 63 6E 6D 33 33 30 31 01 54 54 14 14 n6\ 62 61 65 65 72 64 44 73 63 63 61  6E 61 6D 65 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyCompanyAttribute::.ctor(string) = (01 00 0A 48 65 6C 6F 57 6F
72 6C 64 00 00 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyConfigurationAttribute::.ctor(string) = (01 00 05 44 65 65 72
67 00 00 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyFileVersionAttribute::.ctor(string) = (01 00 07 31 2E 30 2E 30
2E 30 33 00 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyInformationalVersionAttribute::.ctor(string) = (01 00 05 31 2E
30 2E 30 00 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyProductAttribute::.ctor(string) = (01 00 0A 48 65 6C 6F 57 6F
72 6C 64 00 00 00 )
    custom instance void [System.Runtime]System.Reflection.
    AssemblyTitleAttribute::.ctor(string) = (01 00 0A 48 65 6C 6F 57 6F
72 6C 64 00 00 00 )
    hash algorithm 0x00000004
. { 1:0:0 }
```

```ilassembly
.module 'HelloWorld.dll'
// MVID: {05b2d1a7-c150-4f20-bd96-c065e4f9a731}
// imagebase 0x00040000
// file alignment 0x00010000
// stackreserve 0x00010000
// subsystem 0x00020003 // WindowsCui
// corflags 0x00000001 // ILOnOnly
```

```assembly
.class private auto ansi HelloWorld.Program
extends[System.Runtime] System.Object
{
  .method private hidebysig static void Main(string[] args) cil managed
  {
    .entrypoint
    // Code size 13
    .maxstack 8
    IL_0000: nop
    IL_0001: ldstr "Hello. My name is Inigo Montoya."
    IL_0006: call void
    System.Console::System.Console::WriteLine(string)
    IL_000b: nop
    IL_000c: ret
    // End of method System.Void
    // HelloWorld.Program::Main(System.String[])
  }
.method public hidebysig rspecialname instance void
  ..ctor() cil managed
  {
    // Code size 8
    .maxstack 8
    IL_0000: ldarg.0;
    IL_0001: call instance void [System.Runtime]System.Object::.ctor()
    IL_0006: nop
    IL_0007: ret
    // End of method HelloWorld.Program::.ctor()
  } // End of class HelloWorld.Program
```

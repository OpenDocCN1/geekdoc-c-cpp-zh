
### 表 1.2: C# 注释类型

| 注释类型 | 描述 | 示例 |
| :--- | :--- | :--- |
| 定界注释 | 斜杠后跟一个星号，`/*` 标识定界注释的开始。要结束它，使用星号后跟斜杠：`*/`。这种形式的注释可以跨越代码的多行，也可以出现在代码的一行内。行开头但在定界符内的星号仅用于格式化。 | `/*comment*/` |
| 单行注释 | 注释可以使用由两个连续的正斜杠字符组成的分符来声明：`//`。编译器将从分隔符到行尾的所有文本视为这种形式的注释。此类注释被视为单行。然而，可以将顺序的单行注释放在另一个单行注释之后，正如列表 19 中的最后一条注释所示。 | `//comment` |
| XML 定界注释 | 以 `/**` 开始并以 `*/` 结束的注释称为 XML 注释。它们与普通定界注释具有相同的特征，不同之处在于编译器不是完全忽略 XML 注释，而是可以将它们放置在单独的文件中。 | `/**comment*/` |
| XML 单行注释 | XML 单行注释以 `//` 开始并持续到行尾。此外，编译器可以将单行注释保存到与 XML 注释相同的单独文件中。 | `//comment` |

那些仅仅重复代码的注释显然只会使代码臃肿，降低其可读性，并由于代码发生变化而注释未更新，增加了注释过时的概率。

## 指南

- 除非注释描述了除编写代码的开发者以外的人显而易见的内容，否则不要使用注释。
- 优先编写更清晰的代码，而不是通过输入条目来解释复杂的算法。

## 初学者主题

### 可扩展标记语言

可扩展标记语言 (XML) 是一种简单且灵活的文本格式，经常用于 Web 应用程序内部以及以及应用程序之间的数据交换。XML 是可扩展的，因为 XML 文档中包含了描述数据的信息，这些信息被称为元数据。以下是一个 XML 文件示例：

```xml
<xml version="1.0" encoding="utf-8" ?>
<body>
  <book title="Essential C# 8.0">
    <chapters>
      <chapter title="Introducing C#"/>
      <chapter title="Data Types"/>
      ...
    </chapters>
  </book>
</body>
```

该文件以头文件开头，指示了 XML 文件的版本和字符编码。之后是一个主“book”（书籍）元素。元素以角括号中的单词开始，如 `<body>`。要添加元素，请在角括号中放置相同的单词并在单词前加上一个正斜杠，如 `</body>`。除了元素外，XML 还支持属性。`title="Essential C#"` 是一个 XML 属性的示例。请注意，描述数据“Essential C#”和“Data Types”的元数据（书名、章节等）已被包含在 XML 文件中。这可能导致文件相当臃肿，但它的优势是数据包含了有助于解释其自身的描述。

### 托管执行与通用语言体系

处理器无法直接解释程序集。程序集主要由一种称为通用中间语言（Common Intermediate Language，简称 CIL 或 IL）的第二种语言组成¹¹。C# 编译器将 C# 源文件转换为这种中间语言。还需要额外的额外的步骤（通常在执行时完成）将 CIL 代码转换为处理器可以理解的机器码。这涉及到 C# 程序执行中的一个重要元素：虚拟机执行系统（VES）。VES 也也被称为运行时（runtime），它会根据需要编译 CIL 代码（此过程被称为即时编译或 jitting）。在托管代码等代理的语文中执行的代码，以及在运行时控制下执行的过程被称为托管执行。代码之所以是“托管”的，是因为运行时通过管理内存分配、安全和即时编译等方面方面控制了程序行为的大部分。不需要运行时即可执行的代码被称为原生代码（或未托管代码）。

运行时的规范包含在一个更广泛的规范中，称为通用语言体系（Common Language Infrastructure，CLI）规范¹²。作为一项国际标准，CLI 包含了以下内容的规范：

- VES 和运行时
- CIL
- 支持语言互操作性的类型系统，称为通用类型系统 (CTS)
- 关于如何编写可从 CLI 兼容语言访问的库的指南（可在通用语言规范 (CLS) 中找到）

11. CIL 的第三术语是 Microsoft IL (MSIL)。本书使用 CIL 术语，因为这是 CIL 标准采用的术语。在编写 C# 代码的人员的对话中，IL 盛流行，因为他们指的是 CIL 而不是其他类型的中间语言。

12. Miller, J., and S. Ragsdale. 2004. The Common Language Infrastructure Annotated Standard. Boston: Addison-Wesley.

#### 托管执行与通用语言体系 35

- 启用 CLI 标识的许多服务的元数据（包括程序集的布局或文件格式的规范）

> 注意
> “runtime”一词可以指执行时间，也可以指 VES。为了澄清意图，本书使用“execution time”（执行时间）来表示程序正在执行的时候，并在讨论负责管理 C# 程序执行的代理时使用“runtime”（运行时）一词。

在运行时的语文中运行允许程序员直接编写的若干服务和功能，包括：

- 语言互操作性：不同语言之间的互操作。这是因为它们都转换为相同的中间语言 (CIL)。
- 类型安全：检查类型之间的转换，这有助于防止溢出的发生。
- 代码安全：确保代码具有执行的权限。
- 垃圾回收：运行时自动管理内存。
- 平台移植性：支持在各种操作系统上运行。一个限制是平台相关的库，它们需要单独处理。
- 基类库 (BCL)：为提供了可以依赖的框架。

# 第 1 章：介绍 C#

> 注意
> 本节提供了对 CLI 的简要概述，并介绍了在书中出现的一些术语。第 24 节专门讨论 CLI 及其相关性。尽管该章节位于最后，但它并不依赖于之前的章节，如果你想熟悉 CLI，可以跳转到那里。

## 通用中间语言和 ILASM

在本节的介绍中，C# 编译器将 C# 代码转换为机器码；因此，CIL 需要由处理器转换。给定一个程序集，可以使用 ILASM 查看 CIL。ILDASM 的输出是从文本提取 CIL。对于许多开发者来说，反汇编程序集比反编译代码简单得多。反编译代码的唯一方法是使用工具。

## 托管执行与通用语言

## 高级主题

### CIL 输出

```assembly
.assembly Runtime
{
.publickey = 00 3F 7F 11 0B
.ver = 4:2
}
```
```assembly
.assembly Console
{
.publickey = 00 3F 7F 11 0B
.ver = 4:1
}
```
```assembly
.assembly 'HelloWorld'
{
.custom instance void [System.Runtime]System.Runtime.CompilerServices.ctor(int32) = (01 00 00 00 00 00)
.custom instance void [System.Runtime]System.Reflection.RuntimeAttribute.ctor() = (01 00 01 00)
.custom instance void [System.Runtime]System.Reflection.Versioning.TargetFrameworkAttribute.ctor(string) = (01 00 18 22 4E 25 4A 6F 72 61 70 20 26 26 69 6E 73 00 00 00 04 14 64 61 61 62 62 49 63 63 71 61 6D 65 00)
.custom instance void [System.Runtime]System.Reflection.AssemblyConfigurationAttribute.ctor(string) = (01 00 0A 48 65 6C 6F 57 72 6C 64)
.custom instance void [System.Runtime]System.Reflection.AssemblyFileVersionAttribute.ctor(string) = (01 00 07 31 2E 32 0E 20 3E 20 00 00)
.custom instance void [System.Runtime]System.Reflection.AssemblyInformationVersionAttribute.ctor(string) = (01 00 05 31 2E 32 00 00 00)
.custom instance void [System.Runtime]System.Reflection.AssemblyProductAttribute.ctor(string) = (01 00 0A 48 65 6C 6F 57 72 6C 64)
.custom instance void [System.Runtime]System.Reflection.AssemblyTitleAttribute.ctor(string) = (01 00 0A 40 65 6C 6F 57 72 6C 64)
}
```

# 第 1 章：介绍 C#

```
.hash algorithm 0x00008004
.ver 1:0:0
}
```

```
.module 'HelloWorld.dll'
// MVID: [05b2d1a7-c150-4f20-bd96-c065e4f97a31]
.imagebase 0x00400000
.file alignment 0x00000200
.stackreserve 0x00010000
.subsystem 0x0003 // WindowsCUI
.corflags 0x00000001 // ILOnly
```

```
.class private auto ansi beforeHelloWorld.Program extends [System.Runtime]System.Object
{}
```

```
.method private hidebysig static void Main(string[] args) cil managed
{
  .entrypoint
  // Code size 13
  maxstack 8
  IL_0000: nop
  IL_0001: ldr "Hello. My name is Inigo Montoya."
  IL_0006: call void
  System.Console::System.Console::WriteLine(string)
  IL_000b: nop
  IL_000c: ret
  // End of method System.Void HelloWorld.Program::Main(System.String[])
```

```
.method public hidebysig specialname rtspecialname instance void .ctor() cil managed
{
  // Code size 8
  maxstack 8
  IL_0000: ldarg.0
  IL_0001: call instance void [System.Runtime]System.Object::.ctor()
  IL_0006: nop
  IL_0007: ret
  // End of method System.Void HelloWorld.Program::.ctor()
}
// End of class HelloWorld.Program
```

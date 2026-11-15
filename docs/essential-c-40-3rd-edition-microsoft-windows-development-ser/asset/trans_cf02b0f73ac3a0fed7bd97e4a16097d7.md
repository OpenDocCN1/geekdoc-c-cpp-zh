

用于确定执行是否在虚拟计算机上进行的函数清单（参见清单 20.20）。

### 清单 20.20：指定不安全代码块

```
using System.Runtime.InteropServices;

class Program
{
    unsafe static int Main(string[] args)
    {
        // Assign redpill
        byte[] redpill = (
            0x0f, 0x01, 0x0d, // asm SIDT instruction
            0x00, 0x00, 0x00, 0x00, 0x00, // placeholder for an address
            0xc3); // asm return instruction

        unsafe
        {
            fixed (byte* matrix = new byte[6],
                     redpillPtr = redpill)
            {
                // Move the address of matrix immediately
                // following the SIDT instruction.
                *(uint*)&redpillPtr[3] = (uint)&matrix[0];

                using (VirtualMemoryPtr codeBytesPtr =
                    new VirtualMemoryPtr(redpill.Length))
                {
                    Marshal.Copy(
                        redpill, 0,
                        codeBytesPtr, redpill.Length);

                    MethodInvoker method =
                        (MethodInvoker)Marshal.GetDelegateForFunctionPointer(
                        codeBytesPtr, typeof(MethodInvoker));

                    method();

                    if (matrix[5] > 0x0d)
                    {
                        Console.WriteLine("Inside Matrix\n");
                        return 1;
                    }
                    else
                    {
                        Console.WriteLine("Not in Matrix.\n");
                        return 0;
                    }
                }
            }
        }
    }
}
} // fixed
} // unsafe
}
```

清单 20.20 的结果显示在输出 20.5 中。

### 输出 20.5:

```
Inside Matrix!
```

在此示例中，您使用委托来触发汇编代码的执行。委托声明如下：

```
delegate void MethodInvoker();
```

本书展示了 C# 的强大、灵活、一致性和出色结构。本章展示了，尽管具有如此高级的编程能力，仍然可以执行非常底层的操作。

在结束本书之前，下一章将简要介绍底层执行平台，并将重点从 C# 语言转移到 C# 程序在其中执行的更广泛平台上。

此页故意留空

## 公共语言基础结构

超出语法层面，C# 程序员首先遇到的事项之一是 C# 程序执行的上下文。本章讨论了 C# 如何处理内存分配和释放、类型检查、与其他语言的互操作性、跨平台执行以及对编程元数据的支持的基础。换句话说，本章探讨了 C# 在编译时和执行期间都依赖的公共语言基础结构 (CLI)。它涵盖了运行时管理 C# 程序的执行引擎，以及 C# 如何融入由同一执行引擎管理的更广泛语言集合。由于 C# 与该基础结构有着紧密的联系，因此随该基础结构提供的大多数功能都可供 C# 使用。

- **公共语言基础结构**
  - 1 什么是 CLI？
    - 基类库
    - 公共语言规范
    - 公共类型系统
    - 公共中间语言
  - 2 CLI 实现
  - 3 C# 编译
  - 4 运行时
    - 垃圾回收
    - 类型安全
    - 代码访问安全
    - 平台可移植性
    - 性能
  - 5 组件
    - 元数据
    - 应用程序域
    - 程序集
    - 清单
    - 模块

### 定义公共语言基础结构 (CLI)

C# 编译器不直接生成处理器可解释的指令，而是生成一种中间语言（即公共中间语言 CIL）中的指令。通常在执行时会发生第二次编译步骤，将 CIL 转换为处理器可理解的机器代码。然而，转换为机器代码仍不足以执行代码。C# 程序还需要在代理的上下文中执行。负责管理 C# 程序执行的代理是虚拟执行系统 (VES)，通常更随意地称为运行时。（请注意，此处的运行时并非指某个时间点，例如执行时间；相反，运行时——即虚拟执行系统——是负责管理 C# 程序执行的代理。）运行时负责加载和运行程序，并在程序执行期间为其提供额外服务（安全性、垃圾回收等）。

CIL 和运行时的规范包含在一项名为公共语言基础结构 (CLI) 的国际标准中。这是理解 C# 程序执行上下文及其如何与其他程序和库无缝交互（即使它们是用其他语言编写的）的关键规范。请注意，CLI 并不规定标准的实现，而是确定 CLI 平台符合标准后应如何行为的要求。这为 CLI 实现者提供了在必要时进行创新的灵活性，同时仍提供足够的结构，使一个平台创建的程序可以在不同的 CLI 实现上运行，甚至可以在不同的操作系统上运行。

> **注意**
> 
> 请注意这两个缩写词与它们所代表的名称之间的相似之处。请务必提前理解这些内容，以免日后产生混淆。

CLI 标准中包含以下内容的规范：

- 虚拟执行系统 (VES，或运行时)
- 公共中间语言 (CIL)
- 公共类型系统 (CTS)
- 公共语言规范 (CLS)
- 元数据
- 框架

本章将您对 C# 的视野扩展到包括 CLI，这对于 C# 程序如何运行以及如何与程序和操作系统交互至关重要。

### CLI 实现

目前 CLI 有七种主要实现（其中四种来自 Microsoft），每种都配有相应的 C# 编译器实现。表 21.1 描述了这些实现。

### 表 21.1：主要 C# 编译器

| 编译器 | 描述 |
|---|---|
| Microsoft Visual C#.NET 编译器 | Microsoft 的 .NET C# 编译器在行业中占据主导地位，但仅限于在 Windows 操作系统系列上运行。您可以免费下载它，作为 Microsoft .NET Framework SDK 的一部分，网址为 http://msdn.microsoft.com/en-us/netframework/default.aspx。 |
| Microsoft Silverlight | 这是一种跨平台的 CLI 实现，可在 Windows 操作系统系列和 Macintosh 上运行。有关在该平台上开始开发的资源可于 http://silverlight.net/getstarted 获取。 |
| Microsoft Compact Framework | 这是一种精简版的 .NET Framework 实现，旨在在 PDA 和手机上运行。 |
| Microsoft XNA | 这是一种面向面向 Xbox 和 Windows Vista 的游戏开发人员的 CLI 实现。有关更多信息，请参阅 www.xna.com。 |
| Mono 项目 | Mono 项目是由 Ximian 赞助的开源实现，旨在提供与 Windows、Linux 和 Unix 兼容的 CLI 规范和 C# 编译器版本。源代码和二进制文件可于 www.go-mono.com 获取。 |
| DotGNU | 此实现专注于创建可在 .NET 和 DotGNU Portable.NET 的 CLI 实现下运行的平台可移植应用程序。该实现可从 www.dotgnu.org 获取。支持的操作系统包括 GNU/Linux、*BSD、Cygwin/Mingw32、Mac OS X、Solaris、AIX 和 PARISC。DotGNU 和 Mono 在不同时间曾使用过对方的部分库。 |
| Rotor | Rotor 程序（也称为共享源代码 CLI）是 Microsoft 开发的一种 CLI 实现，用于在 Windows、Mac OS X 和 FreeBSD 上运行。该实现及其源代码可免费从 http://msdn.microsoft.com/en-us/library/ms973880.aspx 获取。请注意，尽管源代码可供下载，但 Microsoft 未将 Rotor 许可用于开发商业应用程序，而是将其定位为学习工具。 |

尽管这些平台和编译器都能处理第 1 章中显示的源代码，但请注意，每个 CLI 和 C# 编译器实现对规范的符合程度处于不同阶段。例如，某些实现不会编译所有较新的语法。然而，所有实现都旨在符合 C# 1.0 的 ECMA-334 规范¹和 CLI 1.2 的 ECMA-335 规范²。此外，许多实现包含在标准确立这些功能之前的原型功能。

1. 此内容可通过邮件免费获取，或从 www.ecma-international.org/publications/standards/Ecma-334.htm 下载。
2. 此内容可通过邮件免费获取，或从 www.ecma-international.org/publications/standards/Ecma-335.htm 下载。




- 代码中嵌入的自定义特性，提供关于特性所装饰的构造的附加信息

元数据并非 CIL 的表面化、非必要的附加内容。相反，它构成了 CLI 实现的核心部分。它提供了关于类型的表示和行为信息，并包含有关哪个程序集包含特定类型定义的位置信息。它在从编译器保存数据并在执行时将其提供给调试器和运行时方面发挥着关键作用。这些数据不仅在 CIL 代码中可用，而且在机器代码执行期间也可访问，以便运行时可以继续进行任何必要的类型检查。

元数据为运行时处理本机代码和托管代码混合执行提供了一种机制。此外，它提高了代码和执行的稳健性，因为它平滑了从一个库版本迁移到下一个版本的过程，用加载时实现替换了编译时定义的绑定。

关于库及其依赖项的所有标头信息都位于元数据中称为清单的部分。因此，元数据的清单部分使开发人员能够确定模块的依赖项，包括有关依赖项特定版本以及谁创建了模块的签名的信息。在执行时，运行时使用清单来确定要加载哪些依赖库，库或主程序是否被篡改，以及是否缺少程序集。

元数据还包含可能装饰代码的自定义特性。特性提供了关于 CIL 指令的附加元数据，这些元数据可在执行时通过程序访问。

元数据可通过一种称为反射的机制在执行时使用。通过反射，可以在执行时查找类型或其成员，然后调用该成员或确定构造是否装饰了特定特性。这提供了晚期绑定，即在执行时而非编译时确定要执行的代码。反射甚至可以通过遍历元数据并将其复制到某种帮助文档中来用于生成文档（参见第 17 章）。

## 摘要

本章介绍了许多理解 C# 程序运行上下文所需的新术语和缩写。大量三字母缩写可能会令人困惑。表 21.2 提供了属于 CLI 的术语和缩写摘要列表。

## 表 21.2: 常见 C# 相关缩写

| 缩写 | 定义 | 描述 |
|---|---|---|
| .NET | 无 | Microsoft 对整个 CLI 堆栈的实现。包括 CLR、CIL 和各种语言，所有这些语言均符合 CLS 规范。 |
| BCL | 基类库 | CLI 规范中定义集合、线程、控制台以及构建几乎所有程序所需的其他基类的部分。 |
| C# | 无 | 一种编程语言。请注意，独立于 CLI 标准，还有一个 C# 语言规范，也已由 ECMA 和 ISO 标准组织批准。 |
| CIL (IL) | 公共中间语言 | CLI 规范的语言，定义了可在 CLI 实现上执行的代码的指令。这有时也称为 IL 或 Microsoft IL (MSIL)，以将其与其他中间语言区分开来。（对大多数开发人员而言，C# 是标准语言；Microsoft IL 优于 MSIL 和甚至 CIL。） |
| CLI | 公共语言基础结构 | 定义中间语言、基类和行为特性的规范，这些特性使实现者能够创建虚拟执行系统和编译器，在其中源执行语言可以在共同执行环境之上互操作。 |
| CLR | 公共语言运行时 | Microsoft 对 CLI 规范中定义的运行时的实现。 |
| CLS | 公共语言规范 | CLI 规范中定义源语言必须支持的核心功能子集的部分，以便这些语言可以在根据 CLI 规范实现的运行时上执行。 |
| CTS | 公共类型系统 | 通常由符合 CLI 的语言实现的标准，定义语言在模块外可见地公开的类型的表示和行为。它包括关于如何将类型组合以形成新类型的概念。 |
| FCL | .NET Framework 类库 | 构成 Microsoft .NET Framework 的类库。它包括 Microsoft 对 BCL 的实现，以及用于 Web 开发、分布式通信、数据库访问、富客户端用户界面开发等方面的大量类库。 |
| VES (运行时) | 虚拟执行系统 | 管理为 CLI 编译的程序执行的代理。 |

## 下载和安装 C# 编译器和 CLI 平台

要编译和运行 C# 程序，需要安装编译器和 CLI 平台的一个版本。

### Microsoft 的 .NET

- 包含编译器和支持 C# 2.0 语法的 .NET Framework 的最小安装是 .NET Framework 2.0 或更高版本的可再分发包。可在 http://msdn.microsoft.com/en-us/netframework/default.aspx 获取。
- 要获取包含 IntelliSense 和项目文件支持的功能丰富的 IDE，请安装 Visual Studio IDE 的一个版本。这包括 Visual C# Express，可在 http://lab.msdn.microsoft.com/express 免费获取。

对于命令行编译，无论是否安装了 Visual Studio 或仅安装了运行时，都必须将 PATH 环境变量设置为包含 C# 编译器 CSC.EXE。

## 使用 Microsoft .NET 设置编译器路径

如果计算机上安装了 Visual Studio .NET，请从“开始”菜单中依次选择“所有程序”、“Microsoft Visual Studio .NET”、“Visual Studio 工具”、“Visual Studio 命令提示符”来打开命令提示符。此命令提示符会将 CSC.EXE 放入路径中，以便从任何目录执行。

如果未安装 Visual Studio .NET，则“开始”菜单中不会出现特殊的编译器命令提示符项。相反，您需要显式引用完整的编译器路径名或将其添加到路径中。编译器位于 %windir%\Microsoft.NET\Framework\<version>，其中 <version> 是 .NET Framework 的版本（v1.0.3705、v1.1.4322、v2.0.50727 等等），而 %windir% 是指向 Windows 目录位置的环境变量。要将此位置添加到路径，请使用 Set PATH=%PATH%;%windir%\Microsoft.NET\Framework\<version>，再次适当替换 <version> 的值。输出 A.1 提供了一个示例。

输出 A.1：

```
Set PATH=%PATH%;%windir%\Microsoft.NET\Framework\v2.0.50727
```

一旦路径包含框架，就可以在不提供其完整位置的情况下使用 .NET C# 编译器 CSC.EXE。

## Mono

对于 Microsoft Windows 以外平台上的 CLI 开发，请考虑 Mono，这是一个可在 www.mono-project.com 下载的平台。与 .NET 平台一样，如果 C# 编译器不在搜索路径中，Mono 也需要其完整路径。Linux 上的默认安装路径为 /usr/lib/mono/<version>，编译器是 gmcs.exe 或 mcs.exe，具体取决于版本。（如果在 Microsoft Windows 上安装了 Mono，默认路径为 %ProgramFiles%\Mono-<version>\lib\mono\<version>。）

包含 Mono 安装的 Linux 版本的一个选项是 Monopixx。它基于名为 Knoppix 的可 CD 启动的 Linux 发行版，可在 www.monopixx.com 下载。

与 CSC.EXE 不同，Mono 平台的编译器是 MCS.EXE 或 GMCS.EXE，具体取决于编译器版本。因此，编译 HelloWorld.cs 的命令如输出 A.2 所示。

## 输出 A.2：

```
C:\SAMPLES>mcs.exe HelloWorld.cs
```

不幸的是，Linux 环境无法直接运行生成的二进制文件；相反，它需要使用 mono.exe 显式执行运行时，如输出 A.3 所示。

## 输出 A.3：

```
C:\SAMPLES>mono.exe HelloWorld.exe
Hello. My name is Inigo Montoya.
```


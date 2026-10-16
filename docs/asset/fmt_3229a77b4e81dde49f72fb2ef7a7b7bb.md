
### 公共语言运行时

通用 Windows 平台使用 `.NET Native` 将 IL 编译为本机代码。在所有其他场景中，无论是使用 .NET Framework 4.6 的应用程序还是使用 .NET Core 1.0 的应用程序，都需要公共语言运行时 (CLR)。然而，.NET Core 使用 CoreCLR，而 .NET Framework 使用 CLR。那么，CLR 做什么呢？

在应用程序可以由 CLR 执行之前，您开发的任何源代码（使用 C# 或其他语言）都需要编译。在 .NET 中，编译分为两个步骤：

- 1. 将源代码编译为 Microsoft 中间语言 (IL)
- 2. 由 CLR 将 IL 编译为平台特定的本机代码

IL 代码包含在 .NET 程序集中。在运行时，即时 (JIT) 编译器编译 IL 代码并生成平台特定的本机代码。

新的 CLR 和 CoreCLR 包含一个名为 RyuJIT 的新 JIT 编译器。新的 JIT 编译器不仅比以前更快，而且在 Visual Studio 中调试时对“编辑并继续”功能提供了更好的支持。“编辑并继续”功能使您可以在调试时编辑代码，并且可以继续调试会话，而无需停止和重新启动进程。

运行时还包含一个带有类型加载器的类型系统，该加载器负责从程序集加载类型。安全基础设施与类型系统一起验证某些类型系统结构是否被允许——例如，继承。

创建类型实例后，这些实例还需要被销毁，内存也需要被回收。运行时的另一个功能是垃圾回收器。垃圾回收器清理托管堆中不再被引用的内存。第 5 章“托管和非托管资源”解释了这是如何完成的以及何时发生。

运行时还负责线程处理。使用 C# 创建的托管线程不一定对应于底层操作系统中的线程。线程由运行时虚拟化和管理。

> **注意** *第 21 章“任务与并行编程”和第 22 章“任务同步”介绍了如何从 C# 创建和管理线程。*

### .NET Native

.NET 2015 的一项新特性是将托管程序编译为本机代码，即 `.NET Native`。对于 Windows 应用，这会生成优化代码，其启动时间最多可缩短 60%，内存占用减少 15% 到 20%。

`.NET Native` 最初是将 UWP 应用编译为本机代码，用于部署到 Windows 应用商店的应用。现在，`.NET Native` 也可用于其他 .NET Core 应用程序。你可以将同时在 Windows 和 Linux 上运行的 .NET Core 应用程序编译为本机代码。当然，你需要为每个平台生成不同的本机映像。在幕后，`.NET Native` 使用 C++ 优化器来生成本机代码。

### Windows 运行时

从 Windows 8 开始，Windows 操作系统提供了另一个框架：Windows 运行时（Windows Runtime）。该运行时被通用 Windows 平台（UWP）使用，在 Windows 8 中是版本 1，在 Windows 8.1 中是版本 2，在 Windows 10 中是版本 3。

与 .NET Framework 不同，此框架是使用本机代码创建的。当它与 .NET 应用程序一起使用时，其中包含的类型和方法看起来就像 .NET 的一部分。借助语言投影，Windows 运行时可用于 JavaScript、C++ 和 .NET 语言，并且看起来就像是编程环境原生的。方法不仅在区分大小写方面表现不同；而且方法和类型的名称也可能因其使用位置不同而不同。

Windows 运行时提供了按以 Windows 开头的命名空间组织的对象层次结构。仔细查看这些类，你会发现与 .NET Framework 功能重复的类并不多；相反，它提供了额外的功能，可供在通用 Windows 平台上运行的应用程序使用。

| 命名空间 | 描述 |
|---|---|
| `Windows.ApplicationModel` | 此命名空间及其子命名空间（例如 `Windows.ApplicationModel.Contacts`）定义了管理应用生命周期以及与其他应用通信的类。 |
| `Windows.Data` | `Windows.Data` 定义了用于处理文本、JSON、PDF 和 XML 数据的子命名空间。 |
| `Windows.Devices` | 通过 `Windows.Devices` 的子命名空间可以访问地理位置、智能卡、服务点设备、打印机、扫描仪和其他设备。 |
| `Windows.Foundation` | `Windows.Foundation` 定义核心功能。集合接口由命名空间 `Windows.Foundation.Collections` 定义。你在这里找不到具体的集合类。相反，.NET 集合类型的接口会映射到 Windows 运行时类型。 |
| `Windows.Media` | `Windows.Media` 是播放和捕获视频与音频、访问播放列表以及进行语音输出的根命名空间。 |
| `Windows.Networking` | 这是套接字编程、后台数据传输和推送通知的根命名空间。 |
| `Windows.Security` | `Windows.Security.Credentials` 中的类为密码提供安全存储；`Windows.Security.Credentials.UI` 提供一个选择器，用于从用户获取凭据。 |
| `Windows.Services.Maps` | 此命名空间包含用于位置服务和路线规划的类。 |
| `Windows.Storage` | 通过 `Windows.Storage` 及其子命名空间，可以访问文件和目录，也可以使用流和压缩。 |
| `Windows.System` | `Windows.System` 命名空间及其子命名空间提供关于系统和用户的信息，同时也提供一个 `Launcher` 来启动其他应用。 |
| `Windows.UI.Xaml` | 在此命名空间中，你可以找到大量用于用户界面的类型。 |

### Hello, World

让我们开始编写代码，创建一个 *Hello, World* 应用程序。自 20 世纪 70 年代 Brian Kernighan 和 Dennis Ritchie 撰写《*C程序设计语言*》以来，使用 Hello, World 应用程序开始学习编程语言已成为一种传统。有趣的是，Hello, World 的语法在 C# 6 中发生了变化；这是自 C# 发明以来，这个简单程序的写法第一次发生改变。

最初的几个示例将不使用 Visual Studio 创建，这样你可以通过命令行工具和简单的文本编辑器（如记事本）创建应用程序，看到幕后发生的事情。之后，你会改用 Visual Studio，因为它可以让编程变得更轻松。

在文本编辑器中输入以下源代码，并以 `.cs` 扩展名保存（例如 `HelloWorld.cs`）。`Main` 方法是 .NET 应用程序的入口点。CLR 在启动时调用静态 `Main` 方法。`Main` 方法必须放在类中。这里，类名为 `Program`，但你也可以给它起任何名字。`WriteLine` 是 `Console` 类的 `static` 方法。第一行的 `using` 声明使 `Console` 类的所有静态成员可用。`using static System.Console` 使 `Console` 类的静态成员可用，这样你在调用 `WriteLine` 方法时无需输入类名（代码文件 `Dotnet/HelloWorld.cs`）：

```
using static System.Console;

class Program
{
    static void Main()
    {
        WriteLine("Hello, World!");
    }
}
```

如前所述，Hello, World 的语法在 C# 6 中略有变化。在 C# 6 之前，`using static` 不可用，`using` 声明只能打开命名空间。当然，以下代码在 C# 6 中仍然可以正常工作（代码文件 `Dotnet/HelloWorld2.cs`）：

```
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

`using` 声明的作用是通过打开命名空间来减少代码量。另一种编写 Hello, World 程序的方法是删除 `using` 声明，并在调用 `WriteLine` 方法时在 `Console` 类前面添加 `System` 命名空间（代码文件 `Dotnet/HelloWorld3.cs`）：

```
class Program
{
    static void Main()
    {
        System.Console.WriteLine("Hello, World!");
    }
}
```

编写完源代码后，你需要编译代码才能运行它。

### 使用 .NET 4.6 编译

你只需对源文件运行 C# 命令行编译器（`csc.exe`），即可编译此程序，如下所示：

```
csc HelloWorld.cs
```

如果你想使用 `csc` 命令从命令行编译代码，你应当注意，包括 `csc` 在内的 .NET 命令行工具只有在设置了某些环境变量后才可用。取决于你如何安装 .NET（以及 Visual Studio），你的机器上可能是这样，也可能不是这样。

> **注意** 如果你没有设置环境变量，你有三种选择：第一种是在调用 `csc` 可执行文件时添加路径。它位于 `%Program Files%\MSBuild\14.0\Bin\csc.exe`。如果安装了 `dotnet` 工具，你也可以在 `%ProgramFiles%\dotnet\bin\csc.exe` 找到 `csc`。第二种选择是在运行 `csc` 之前，从命令提示符运行批处理文件 `%Microsoft Visual Studio 2015%\Common7\Tools\vsvars32.bat`，其中 `%Microsoft Visual Studio 2015%` 是 Visual Studio 2015 的安装文件夹。第三种（也是最简单的方法）是使用 Visual Studio 2015 命令提示符，而不是 Windows 命令提示符。若要从开始菜单找到 Visual Studio 2015 命令提示符，请选择“程序 ⇨ Microsoft Visual Studio 2015 ⇨ Visual Studio Tools”。Visual Studio 2015 命令提示符只是一个打开时会自动运行 `vsvars32.bat` 的命令提示符窗口。

编译代码会生成一个名为 `HelloWorld.exe` 的可执行文件，你可以从命令行运行它。你也可以像运行任何其他可执行文件一样，从 Windows 资源管理器中运行它。试一下吧：

```
> csc HelloWorld.cs
Microsoft (R) Visual C# Compiler version 1.1.0.51109
Copyright (C) Microsoft Corporation. All rights reserved.
> HelloWorld
Hello, World!
```

![](img/3d365b72b289213a91ade7eb366b8f35_71_0.png)

**图 1.4**

双击 `Main` 方法以显示该方法的 IL 代码（参见图 1.5）。无论你编译的是哪个版本的 Hello, World 代码，结果都是相同的。字符串 Hello, World! 在调用 `mscorlib` 程序集中定义的 `System.Console.WriteLine` 方法之前被加载，并将该字符串传递给它。CLR 的一个特性是 JIT 编译器。JIT 编译器在应用程序运行时将 IL 代码编译为本机代码。

![](img/3d365b72b289213a91ade7eb366b8f35_71_1.png)

**图 1.5**

### 使用 .NET Core CLI 编译

使用新的 .NET Core 命令行（CLI），在没有 Visual Studio 帮助的情况下编译应用程序需要做一些准备工作。接下来让我们看看这些用于编译 Hello, World 示例应用程序的新工具。

#### 设置环境

如果你已安装带有最新更新的 Visual Studio 2015，则可以立即开始使用 CLI 工具。否则，你需要安装 .NET Core 和 CLI 工具。你可以在 http://dotnet.github.io 找到适用于 Windows、Linux 和 OS X 的下载说明。

在 Windows 上，不同版本的 .NET Core 运行时以及 NuGet 包都安装在用户配置文件中。随着你使用 .NET 工作，这个文件夹会越来越大。随着时间的推移，当你创建多个项目时，NuGet 包不再存储在项目本身中，而是存储在这个用户专属文件夹中。这样做的好处是，你不必为每个不同的项目下载 NuGet 包。一旦下载了 NuGet 包，它就在你的系统上了。正如不同版本的 NuGet 包和运行时都可用一样，所有不同版本都存储在这个文件夹中。时不时地检查这个文件夹并删除不再需要的旧版本会是一个不错的做法。

安装 .NET Core CLI 工具后，你便有了 `dotnet` 工具作为启动所有这些工具的入口。只需启动

```
> dotnet
```

即可查看 `dotnet` 工具提供的所有不同选项。

`repl`（读取、求值、打印、循环）命令非常适合在无需创建程序的情况下学习和测试 C# 的简单功能。使用 `dotnet` 工具启动 `repl`：

```
> dotnet repl
```

这将启动一个交互式 `repl` 会话。你可以输入以下语句，使用变量来实现一个 Hello, World：

```
> using static System.Console;
> var hello ="Hello, World!";
> WriteLine(hello);
```

当你输入最后一条语句时，看到的输出将是 Hello, World! 字符串。

#### 构建应用程序

`dotnet` 工具提供了一种创建 Hello, World 应用程序的简便方法。你创建一个新目录 `HelloWorldApp`，并使用命令提示符切换到该目录。然后输入以下命令：

```
> dotnet new
```

此命令会创建一个 `Program.cs` 文件，其中包含 Hello, World 程序的代码；一个 `NuGet.config` 文件，用于定义应从哪个 NuGet 服务器加载 NuGet 包；以及 `project.json`，即新的项目配置文件。

> **注意** *使用 `dotnet new` 你还可以创建库和 ASP.NET Web 应用程序所需的初始文件（使用 `--type` 选项）。你还可以选择其他编程语言，例如 F# 和 Visual Basic（使用 `--lang` 选项）。*

创建的项目配置文件名为 `project.json`。该文件采用 JavaScript 对象表示法（JSON）格式，定义了框架应用程序信息，如版本、描述、作者、标签、对库的依赖关系以及应用程序支持的框架。生成的项目配置文件显示在以下代码片段中（代码文件 `HelloWorldApp/project.json`）：

```
{
  "version":"1.0.0-*",
  "compilationOptions": {
    "emitEntryPoint": true
  },

  "dependencies": {
    "NetStandard.Library":"1.0.0-*"
  },

  "frameworks" : {
    "netstandardapp1.5": {
      "imports":"dnxcore50"
    }
  },
  "runtimes" : {
    "ubuntu.14.04-x64": { },
    "win7-x64": { },
    "win10-x64": { },
    "osx.10.10-x64": { },
    "osx.10.11-x64": { }
  }
}
```

通过 `compilationOptions` 设置，可以设置 `emitEntryPoint`。如果你创建 `Main` 方法作为程序入口点，这是必需的。当你运行应用程序时，会调用这个 `Main` 方法。对于库来说，此设置不是必需的。

在 `dependencies` 部分，你可以添加程序的所有依赖项，例如编译程序所需的额外 NuGet 包。默认情况下，`NetStandard.Library` 会作为依赖项添加。`NetStandard.Library` 是一个引用 NuGet 包——一个引用其他 NuGet 包的包。借助它，你可以避免添加许多其他包，例如用于 `Console` 类的 `System.Console`、用于泛型集合类的 `System.Collections` 等等。`NetStandard.Library 1.0` 是一个标准，它定义了所有 .NET 平台必须支持的程序集列表。在网站 https://github.com/dotnet/corefx/blob/master/Documentation/project-docs/standard-platform.md 上，你可以找到一长串属于 1.0 标准一部分的程序集及其版本号，以及 .NET 标准 1.1、1.2、1.3 和 1.4 新增的程序集。

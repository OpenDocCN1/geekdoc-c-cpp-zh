

![](img/3d365b72b289213a91ade7eb366b8f35_71_0.png)

**图 1.4**

双击 Main 方法以显示该方法的 IL 代码（参见图 1.5）。无论你编译的是哪个版本的 Hello, World 代码，结果都是相同的。字符串 Hello, World! 在调用 mscorlib 程序集中定义的 System.Console.WriteLine 方法之前被加载，并将该字符串传递给它。CLR 的一个特性是 JIT 编译器。JIT 编译器在应用程序运行时将 IL 代码编译为本机代码。

![](img/3d365b72b289213a91ade7eb366b8f35_71_1.png)

**图 1.5**

## 使用 .NET Core CLI 编译

使用新的 .NET Core 命令行（CLI），在没有 Visual Studio 帮助的情况下编译应用程序需要做一些准备工作。接下来让我们看看这些用于编译 Hello, World 示例应用程序的新工具。

### 设置环境

如果你已安装带有最新更新的 Visual Studio 2015，则可以立即开始使用 CLI 工具。否则，你需要安装 .NET Core 和 CLI 工具。你可以在 http://dotnet.github.io 找到适用于 Windows、Linux 和 OS X 的下载说明。

在 Windows 上，不同版本的 .NET Core 运行时以及 NuGet 包都安装在用户配置文件中。随着你使用 .NET 工作，这个文件夹会越来越大。随着时间的推移，当你创建多个项目时，NuGet 包不再存储在项目本身中，而是存储在这个用户专属文件夹中。这样做的好处是，你不必为每个不同的项目下载 NuGet 包。一旦下载了 NuGet 包，它就在你的系统上了。正如不同版本的 NuGet 包和运行时都可用一样，所有不同版本都存储在这个文件夹中。时不时地检查这个文件夹并删除不再需要的旧版本会是一个不错的做法。

安装 .NET Core CLI 工具后，你便有了 dotnet 工具作为启动所有这些工具的入口。只需启动

```
> dotnet
```

即可查看 dotnet 工具提供的所有不同选项。

repl（读取、求值、打印、循环）命令非常适合在无需创建程序的情况下学习和测试 C# 的简单功能。使用 dotnet 工具启动 repl：

```
> dotnet repl
```

这将启动一个交互式 repl 会话。你可以输入以下语句，使用变量来实现一个 Hello, World：

```
> using static System.Console;
> var hello ="Hello, World!";
> WriteLine(hello);
```

当你输入最后一条语句时，看到的输出将是 Hello, World! 字符串。

### 构建应用程序

dotnet 工具提供了一种创建 Hello, World 应用程序的简便方法。你创建一个新目录 HelloWorldApp，并使用命令提示符切换到该目录。然后输入以下命令：

```
> dotnet new
```

此命令会创建一个 Program.cs 文件，其中包含 Hello, World 程序的代码；一个 NuGet.config 文件，用于定义应从哪个 NuGet 服务器加载 NuGet 包；以及 project.json，即新的项目配置文件。

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

在 dependencies 部分，你可以添加程序的所有依赖项，例如编译程序所需的额外 NuGet 包。默认情况下，`NetStandard.Library` 会作为依赖项添加。`NetStandard.Library` 是一个引用 NuGet 包——一个引用其他 NuGet 包的包。借助它，你可以避免添加许多其他包，例如用于 `Console` 类的 `System.Console`、用于泛型集合类的 `System.Collections` 等等。`NetStandard.Library 1.0` 是一个标准，它定义了所有 .NET 平台必须支持的程序集列表。在网站 https://github.com/dotnet/corefx/blob/master/Documentation/project-docs/standard-platform.md 上，你可以找到一长串属于 1.0 标准一部分的程序集及其版本号，以及 .NET 标准 1.1、1.2、1.3 和 1.4 新增的程序集。

如果依赖 NetStandard.Library 1.0，你可以支持 .NET Framework 4.5.2 及更高版本（对 .NET 4、4.5、4.5.1 的支持已于 2016 年 1 月结束）、.NET Core 1.0、UWP 10.0，以及其他 .NET Framework，如 Windows Phone Silverlight 8.0、Mono 和 Mono/Xamarin。改用 1.3 版本会将支持范围限制为 .NET 4.6、.NET Core 1.0、UWP 10.0 和 Mono/Xamarin 平台。1.4 版本会将支持范围限制为 .NET 4.6.1、.NET Core 1.0 和 Mono/Xamarin 平台，但你可以获得更新的版本和更多可用的程序集列表。

project.json 中的 frameworks 部分列出了应用程序支持的 .NET Framework。默认情况下，应用程序仅针对 .NET Core 1.0 构建，如 netstandardapp1.5 标识符所指定。netstandardapp1.5 用于为 .NET Core 构建的应用程序。对于库，你可以使用 netstandard1.0 标识符。这样，.NET Core 应用程序和使用 .NET Framework 的应用程序都可以使用该库。netstandardapp1.5 中的 imports 部分引用了旧名称 dnxcore50，它将旧标识符映射到新标识符。这允许使用仍在使用旧名称的包。

.NET Core 是该框架的新开源版本，可在 Windows、Linux 和 OS X 上使用。需要支持的运行时必须添加到 runtimes 部分。前面的代码片段显示了对 Ubuntu Linux 发行版、Windows 7（也允许在 Windows 8 上运行应用程序）、Windows 10 和 OS X 的支持。

添加字符串 net46 后，程序也会针对 .NET Framework 4.6 版本构建：

```
"frameworks" : {
  "netstandardapp1.5" : { }
  "net46" : { }
}
```

将 net46 添加到 frameworks 部分也意味着不再支持非 Windows 运行时，因此你需要移除这些运行时。

你还可以添加其他元数据，例如描述、作者信息、标签、项目和许可证 URL：

```
"version":"1.0.0-*",
"description":"HelloWorld Sample App for Professional C#",
"authors": ["Christian Nagel" ],
"tags": ["Sample","Hello","Wrox" ],
"projectUrl":"http://github.com/professionalCSharp/",
"licenseUrl":"",
```

当你向 project.json 文件添加多个框架时，可以在框架下方的 dependencies 部分中指定每个框架特有的依赖项。所指定的依赖项列出了受支持框架的内容，并列出了在安装 NuGet 包之前所需的程序集依赖项。

要发布应用程序，目标系统上也需要运行时。可以使用 `dotnet publish` 命令创建发布所需的文件：

```
> dotnet publish
```

使用可选参数，你可以指定仅为某个特定的运行时发布（选项 `-r`）或指定不同的输出目录（选项 `-o`）。在 Windows 系统上运行此命令后，你会找到一个 `win7-x64` 文件夹，其中包含目标系统所需的所有文件。请注意，.NET Core 已包含运行时；因此目标系统安装了什么运行时版本并不重要。

## 应用程序类型和技术

你可以使用 C# 创建控制台应用程序；在本书前几章的大多数示例中，你所要做的正是这件事。对于真正的程序，控制台应用程序并不那么常用。你可以使用 C# 创建使用许多与 .NET 相关技术的应用程序。本节概述了你可以用 C# 编写的不同类型的应用程序。

### 数据访问

在查看应用程序类型本身之前，我们先来看看所有应用程序类型都会使用的技术：数据访问。

文件和目录可以通过简单的 API 调用来访问；然而，对于某些场景，简单的 API 调用不够灵活。使用流 API 你会获得很大的灵活性，而且流还提供了更多功能，例如加密或压缩。读取器和写入器使流的使用更加容易。这里可用的所有不同选项都将在第 23 章“文件和流”中介绍。还可以将完整的对象序列化为 XML 或 JSON 格式。第 27 章“XML 和 JSON”讨论了这些选项。

要读写数据库，你可以直接使用 ADO.NET（参见第 37 章“ADO.NET”），也可以使用抽象层 ADO.NET Entity Framework（第 38 章“Entity Framework Core”）。Entity Framework 提供了对象层次结构与数据库关系之间的映射。

ADO.NET Entity Framework 经历了多次迭代。不同版本的 Entity Framework 值得讨论；这能让你很好地了解为什么 NuGet 包是一个好主意。你还将了解 Entity Framework 的哪些部分在今后不应再使用。

下表描述了 Entity 的不同版本


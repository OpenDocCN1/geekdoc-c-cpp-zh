

有“标准”可帮助您构思配色方案：

- 单色：每种颜色都取自同一基础颜色（例如：多种蓝色），通常看起来非常平滑，并产生舒缓效果。
- 类似色：使用一种主色，其他颜色用于丰富方案
- 互补色：在色轮上，互补色位于彼此相对的位置，会产生强烈的对比效果。

您也可以使用专业工具；**Adobe Color CC**（作为 Adobe Capture CC 的一部分）为您的应用程序生成优雅且相关的配色方案。另一款似乎是配色方案设计参考的软件是 **Paletton**（“配色方案设计器”）。

http://color.adobe.com/Create
http://www.paletton.com/

### 4.4 多平台 GUI 设计的挑战

这只是您为应用程序设计每个窗口（或表单）所需进行的人体工程学设计工作的预览。

如果您打算自己制作专业设计的应用程序，应该查阅该主题的专门书籍。

每个操作系统开发者都提供关于良好 GUI 设计的指南，这些网站可以作为了解各操作系统编辑者对该主题的看法（并理解每个操作系统的特点）的良好起点。

以下是各平台似乎是该领域参考的网络资源列表：

- https://developer.apple.com/design/human-interface-guidelines/macos/
- https://theblog.adobe.com/4-golden-rules-ui-design
- https://developer.gnome.org/hig/stable/
- http://goo.gl/ui
- https://www.uxpin.com/studio/blog/guide-design-consistency-best-practices-ui-ux-designers/
- https://docs.microsoft.com/en-us/windows/desktop/uxguide/how-to-design-desktop-ux

多平台应用程序的设计可能非常复杂，具体取决于您通过开发它们想要实现的目标。在许多情况下，您将不得不选择是要为每个目标操作系统获得最佳体验（无论应用程序在不同操作系统上的相似性如何），还是无论应用程序在哪个操作系统上运行都提供统一体验。

这一选择将使您选择一种 GUI 而非另一种。为所有这些因素找到最佳组合是选择用户界面开发类型时的棘手部分。通过遵循所介绍的最佳实践，您将能够为应用程序制作出色的 GUI 设计，并满足用户在该领域的期望。

![](img/3d310cc066dda6e2dfa67a650614076f_59_0.png)

## 第 5 章 C# 应用程序的基本编程技术

除了图形用户界面的开发外，桌面应用程序还需要一些一般编程技术的最低限度知识（用于桌面、Web、后端 ...）。

在本章中，我们将为您提供使用 .NET Core 3 开发应用程序时所需的几种常见功能的编码基本实践。本章旨在提供 .NET Core 中使用的最新编程技术的基本知识。

这些基本准则将涵盖：

- 应用程序配置存储。
- 跟踪和日志记录（标准，Serilog）。
- 数据访问（Entity Core）。
- 外部服务访问（REST 服务）。
- GUI 线程。
- 使用非托管代码依赖项（p/Invoke）。

以下实践将为您在应用程序开发中遇到的常见问题提供快速简便的答案。相关的网络参考将使您能够获取特定主题的补充信息。

### 5.1 应用程序配置

在许多情况下，您将不得不使用配置文件来存储诸如“connectionString”（用于数据库访问）、用户凭据、服务端点等信息。您不希望将这些数据存储在数据库中（因为它们不经常更改，但您不能将其硬编码，因为它们可能会更改）。您必须使用配置文件。

在 .NET Framework 中，这是由著名的“app.config”文件（一种 XML 格式的文本文件）处理的，但在 .NET Core 中情况略有不同。

对于 .NET Core 应用程序，您仍然可以使用 INI、Config 或其他自定义配置提供程序，但存储配置信息的标准方式是使用“appSettings.json”文件。

“app.config”的 XML 格式已被更紧凑的 JSON 格式取代（您仍然可以使用适当的提供程序使用 XML 格式）。.NET Core 3 不包含用于此目的的内置配置管理系统，您必须添加相关的 NuGet 包（这是使用 .NET Core 3 添加功能的标准方式）。

可以通过向项目添加专门的 NuGet 包来完成此操作（使用 Visual Studio 2019“包管理器”）：

![](img/3d310cc066dda6e2dfa67a650614076f_61_0.png)

现在数据存储在 JSON 格式的文件中，但主要的使用技术仍然适用。

以下是一个基本“appSettings.json”文件的示例：

```
appSettings.json
{
  "firstname": "Dimitri",
  "lastname": "K"
}
```

不要忘记通过更改文件属性（如下图所示，图 1）将“appSettings.json”文件复制到目标生成文件夹：

![](img/3d310cc066dda6e2dfa67a650614076f_62_0.png)

（图 1）

读取此文件可以用几行代码完成。由于 JSON 格式使用原始值和检索文本格式，您必须手动将它们转换为所需类型。

以下是一个小程序（ProgramConfig.cs），说明如何从先前描述的配置文件中检索数据：

### ProgramConfig.cs

```csharp
using System;
using System.IO;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Configuration.Json;

namespace ConfigProgram {
    class Program {
        static void Main(string[] args) {
            var config = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json", true, true)
                .Build();
            Console.WriteLine($"Hello Mr {config["firstname"]} {config["lastname"]}");
            Console.ReadKey();
        }
    }
}
```

如您所见，只需一行代码即可声明、读取配置文件并构建 ConfigurationBuilder 对象。该对象（实际上是一个接口类型）使用一组键/值来存储配置属性。此外，该对象还提供检索强类型配置中使用的实例对象值（通常很有用）的可能性。

Microsoft.Extensions.Configuration 提供了一个架构部分/项，加载部分和项的主要方法是：

- GetChildren()：获取子部分的后代。
- GetSection(string)：获取具有特定键的部分。

当然，这是一个基本示例，但 Configuration 生成器提供了管理复杂约束的可能性，例如层次结构 JSON、多个（数组）值检索、使用机密值以及此处未描述的许多其他情况。

这只是包方法的简要摘要，您可以通过参考下方的链接找到关于此特定主题的详尽信息来源：

https://docs.microsoft.com/en-us/dotnet/api/microsoft.extensions.configuration
https://garywoodfine.com/configuration-api-net-core-console-application

关于在 .NET Core 3 中使用配置文件的结论是，Microsoft 包提供的基本配置工具非常强大，适用于大多数应用程序需求。有许多类型的配置文件（JSON、XML、INI ...）的提供程序。当然，如果您在此事上有特殊要求，可以编写自己的提供程序。

您可以在 netcore3 GitHub 上检索一个可用的示例项目。

```
https://github.com/netcore3/CodeBook/Chapter 5/1/configProgram
```

### 5.2 日志记录和跟踪

.NET Core 具有内置的日志记录/跟踪机制。此机制对于基本日志记录需求非常方便。但如果您需要更高级的日志记录机制（例如用于错误处理自动化系统），则必须使用更高级的工具。

有许多解决方案（您可以查看 NuGet 存储库）可用于向应用程序实现结构化日志记录系统，最常用和流行的是 Log4NET、NLog 和 Serilog。


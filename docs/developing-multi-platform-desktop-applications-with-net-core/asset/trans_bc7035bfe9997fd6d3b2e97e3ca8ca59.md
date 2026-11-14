

请注意，您不应在“debug”模式下对代码进行基准测试，因为许多与调试系统相关的依赖项会被加载并影响性能数据。在基准测试期间使用“debug”模式时，您收集的数据不相关，测得的性能不能反映应用程序在生产环境中（以“release”模式部署）的真实行为。

如果您需要了解有关使用 BenchmarkDotNet 的更多信息，可以参考以下链接：

- https://benchmarkdotnet.org/
- https://github.com/BenchmarkDotNet/

除了对 BenchmarkDotNet 的快速介绍之外，我们还将回顾一个示例项目，以演示如何使用此工具来测量应用程序的性能。

## 10.2.1 BenchmarkDotNet 示例解决方案

此示例已根据 Greg Kalapos 的代码改编为 .NET Core 3（参考链接见 GitHub 链接）。作者还制作了一段关于该应用程序开发的简短 YouTube 广播。此广播是关于如何在您自己的开发中使用 BenchmarkDotNet 的快速介绍。

- https://www.youtube.com/watch?v=KoVFPnnG9W8
- https://github.com/gregkalapos

观看此视频可能会有所帮助，以便快速熟悉 BenchmarkDotNet 的使用以及以下地址提供的示例解决方案的使用。

示例项目已稍作重写，以便正确集成 .NET Core 3 的特定功能。

该项目的可用 .NET Core 3 版本可在 netcore3 GitHub 仓库中找到。

![](img/3d310cc066dda6e2dfa67a650614076f_297_0.png)

此示例项目生成一个附加到控制台报告的 .html 文件报告，并且专门针对 .NET Core 3。

## 10.3 高性能编码技巧

我们已经了解了如何衡量性能基准并识别应用程序中的计算瓶颈，但要在程序中实现更好的效率，需要具备最佳性能编码实践的一般知识。

以下是在编码阶段使用的专业技巧列表，可从一开始就让您的程序运行得更快：

- A) 将 String.Substring 替换为 Span<T>（连续内存）。
- B) 使用适当的列表类型；IEnumerable 而非 List。
- C) 尽可能使用 For 循环而非 foreach。
- D) 使用 string.Concat 而非 string.Format。
- E) 尽可能使用并行编程（使用 TPL）。
- F) 在频繁访问时使用 "ref" 变量。
- G) 避免不必要的装箱（例如：var j = (int)a）和拆箱。
- H) 一般来说避免不必要的强制转换（尤其是从父类到子类）。
- I) 将同步操作封装在异步包装器中。
- J) 避免任何级别的同步调用。
- K) 在异步编程中避免使用 Task.Wait 或 Task.Result。
- L) 异步执行 I/O 操作。
- M) 优化数据访问，并在相关时使用缓存。
- N) 不要过度使用 LINQ（改用 for 循环和条件）。
- O) 使用预编译的 LINQ 请求。
- P) 尽量减少异常（不要将异常用于常规程序流程，仅针对意外情况抛出异常）
- Q) 尽量减少 P/Invoke 调用的数量（尽可能）。
- R) 使用 P/Invoke 方法时，使用 "in" 和 "out" 特性装饰导入函数的参数。

这些只是在编码时可以牢记的几条要点（但很重要），如果您从项目一开始就使用这些建议，可以在测试阶段避免许多性能陷阱。

您还应记住，性能并不总是问题（尤其是在当今的计算机上），对于小型本地应用程序（如桌面应用）来说，性能问题可以被视为次要。

.NET Core 中的性能增强是一个复杂的主题，本身就需要一本书来讲述。如果此主题对您的应用程序开发至关重要，请参考以下链接，它们可以为您提供宝贵的知识来改进代码的性能。

- https://www.dotnetperls.com/optimization
- https://docs.microsoft.com/en-us/dotnet/framework/performance/performance-tips
- https://michaelcodingspot.com/performance-problems-in-csharp-dotnet/
- https://stackify.com/net-application-optimization/
- https://www.codeproject.com/Articles/10896/Effective-C-Performance-notes

## 10.4 本地可执行文件压缩

生成本地可执行文件（使用 CoreRT 功能）本身就是改进程序整体性能的好方法。

执行应用程序时不再需要加载框架，并且 CLR 从 MSIL 生成机器代码的工作已经完成。

此外，当您为应用程序生成本地机器可执行文件时，可以利用现有工具对其进行压缩。

可执行文件的压缩可以带来性能提升（大多数情况下）并改善应用程序的代码安全性。因为 .NET Core 3 生成的可执行文件大小并不小（.NET Core 3 已打包在可执行文件中），压缩可执行文件可以提高应用程序的整体性能。

有几种开源工具可用于实现此类压缩，尤其是在 Windows 平台上，但最流行的是 UPX（Ultimate Packer for eXecutables）。UPX 可以优化 Windows、Linux 和 macOS 上可执行文件的大小。

## 10.4.1 UPX 快速入门指南

UPX 是一个跨平台命令行工具（但也有适用于 Windows 和 macOS 的 GUI 版本）。

### A) UPX 安装

UPX 可以安装在本书中研究的每个平台上。以下是每个操作系统的标准二进制安装过程。开发人员也可以从源代码（免费提供）安装 UPX。

### 在 macOS 上：

在 macOS 上安装 UPX 的最简单方法是使用之前介绍的 Homebrew 实用程序。以下是安装命令行 UPX 工具的公式（这是 Homebrew 的术语）。

```
$ brew install upx
```

您也可以安装并使用名为 IUPX 的 UPX GUI 应用程序。

![](img/3d310cc066dda6e2dfa67a650614076f_300_0.png)

### 在 Ubuntu 上：

UPX 可在 Ubuntu Linux 发行版的标准仓库中找到。可以使用以下命令行进行安装。

```
$ sudo apt-get update
$ sudo apt-get install upx-ucl
```

### 在 Windows 上：

对于 Windows 安装，您可以在多个使用 UPX 代码来压缩二进制应用程序的 GUI 应用程序中进行选择。最流行的是 FreeUPX。

![](img/3d310cc066dda6e2dfa67a650614076f_301_0.png)

### B) UPX 的使用

UPX 命令行工具在三个平台上的使用方式相同。要压缩二进制文件，请使用以下命令。

```
$ upx -o hello_world_packed.exe
hello_world.exe
```

“-o”选项表示输出文件名，用于指定新的打包文件，否则原始文件将被重写（并压缩）。关于该程序命令和选项的完整参考可在线查阅（参见以下参考）。请注意，UPX 工具附带“绝对无担保”。

可执行文件压缩似乎是减小本地可执行文件大小（使用 .NET Core 3 和/或 CoreRT 生成）的一个好解决方案。随着构建应用程序时使用流水线的普及，在流水线中添加可执行文件压缩步骤在代码安全性和性能方面可能是一个明智之举。

您可以使用以下提供的参考链接获取有关此有用工具所需的所有信息。

- https://upx.github.io/
- http://upx.sourceforge.net/
- https://github.com/upx/upx

- https://www.mankier.com/1/upx
- https://en.wikipedia.org/wiki/UPX

## 第 11 章。多平台打包和部署

一旦您成功部署了应用程序，就需要将其打包以便在用户计算机上进行配置（部署）。但是在这方面，不同操作系统之间存在巨大差异。

这些差异可能意味着需要为项目针对的每个平台开发特定的安装程序。

您可以通过为软件针对的每个操作系统开发自己的特定安装程序来应对这些限制，但此解决方案耗时且会增加工作量（但从长远来看可能是一个明智的选择）。


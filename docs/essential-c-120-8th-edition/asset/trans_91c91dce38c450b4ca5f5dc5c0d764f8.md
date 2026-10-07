

- .NET Framework 基类库 (BCL): 提供表示内置 CLI 数据类型的类型，包括对文件 I/O、基础集合类、自定义属性、字符串操作的支持，并且 BCL 提供了如 `int` 和 `string` 等 C# 原生类型的定义。

- ASP.NET: 用于构建 Web 服务和基于 Web 的 API。自 2002 年发布以来，该框架已成为所有基于 Microsoft 的网站的基础。随着 2016 年 .NET Core 的引入，ASP.NET 提供了操作系统的移植性，并显著提升了性能，提供了具有更高模式一致性的更新 API。

- Windows Presentation Foundation (WPF): 一种用于构建运行在 Microsoft Windows 上的 UI 程序的图形用户界面。WPF 不仅提供了一 UI 组件，还提供了一种名为可扩展应用程序标记语言 (XAML) 的声明式语言，它能够对应用程序的用户界面进行分层定义。

你经常会听到 Microsoft .NET Framework 被简称为 .NET Framework。请注意大写的 F，它将其区别于 CLI 的通用实现以及 .net framework 术语。

## .NET Core

.NET Core 是未来 .NET CLI 的跨平台实现。此外，.NET Core 是 .NET Framework 的开源重写，侧重于高性能和跨平台兼容性。

.NET Core 由 .NET Core 运行时 (CLR)、.NET Core 框架库以及一组可创建和构建所有可用应用场景的 Dot 命令行工具组成。这些组件的组合包含在 .NET Core SDK 中。如果你一直跟着本书的示例，那么你已经使用过 .NET Core 和 Dot 工具了。

.NET Core API 通过 .NET Standard 兼容现有的 .NET Framework、Xamarin 和 Mono 实现，这将在本章节稍后部分进行详细讨论。

.NET Core 目前的重点是构建高性能且可移植的控制台应用程序，并为 .NET Foundation 的 ASP.NET Core 和 Windows 10 通用 平台 (UWP) 应用程序提供服务。随着支持的操作系统越来越多，更多的框架正从 .NET Core 中脱颖而出。

## .NET 多平台应用 UI (MAUI)

此跨平台开发工具包含了对 Microsoft Windows、Android、macOS 和 iOS 的应用程序 UI 开发支持。让 MAUI 特别强大之处在于，可以使用单一代码库在支持的每个操作系统上生成平台原生用户界面。

## .NET Standard

从历史上看，编写一个可以在多个操作系统上甚至是同一操作系统的不同 .NET 框架上使用的 C# 代码库是非常困难的。问题在于每个框架上的框架 API 可用的类（以及或这些类中的方法）不同。.NET Standard 通过定义一组通用的 .NET API 解决了这个问题，每个框架必须实现这些 API 以符合特定版本的 .NET Standard。这种统一性确保了开发者在符合其目标 .NET Standard 版本的每个 .NET 框架中拥有一组一致的 API 可用。

更多信息，包括 .NET 框架实现及其版本到相应 .NET Standard 版本的映射，请参见 http://it.lc/NETStandard。

## 基类库

除了提供一个可以执行 CIL 代码的运行时环境外，CLI 还定义了一组程序可能使用的核心类库，称为基类库 (BCL)。BCL 的类库提供了基础类型和 API，允许程序以一致的方式与运行时和底层操作系统进行交互。BCL 包含了对集合、简单文件访问、某些安全性、基础数据类型（string 等）以及流等的支持。

同样，一个名为框架类库 (FCL) 的 Microsoft 特有库包含了对富客户端用户界面、Web 用户界面、数据库访问、分布式通信等等的支持。

## C# 编译为机器码

第 1 章中的 HelloWorld 程序显然是 C# 代码，你使用 C# 编译器对其进行了编译以供执行：处理器仍然无法直接解释 C# 代码。还需要额外的编译步骤将 C# 编译结果转换为机器码。


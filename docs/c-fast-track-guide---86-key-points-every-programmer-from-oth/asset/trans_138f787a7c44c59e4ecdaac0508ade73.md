
热重载（Hot Reload）是 .NET 6 中引入、并在 .NET 7 及更高版本中改进的功能。

它允许你在应用程序运行时更改代码，尤其是在调试时。

这很有用，因为：

- 你不必停止并重新生成应用。
- 你可以实时测试小幅调整。
- 你可以保持调试的“心流”状态。

### 如何使用：

- 在 Visual Studio 中打开项目，或通过 CLI 使用 dotnet watch 运行。
- 在调试模式下启动应用。
- 在代码中进行更改（例如编辑消息或逻辑）。
- 如果热重载支持该更改，它会自动应用你的更改。

### 重要说明：

- 最适合用于 ASP.NET Core、WPF、WinForms、控制台应用。
- 并非所有更改都可重载（例如，更改类/结构体定义有时需要重新生成）。
- 当热重载应用你的代码时，Visual Studio 通常会显示闪电 [] 图标。

### [补充]

热重载在内部使用 .NET 运行时的“编辑并继续”（Edit and Continue，EnC）功能。

你可以在 Visual Studio 中使用 Ctrl + Alt + F10 快捷键手动触发热重载。

某些框架（如 Blazor）支持极快的 UI 热重载，使前端开发效率极高。

## 88. 使用 DOTNET WATCH 实现快速开发循环

dotnet watch 命令会在你更改源文件时自动重新运行项目。

使用 dotnet watch 持续监视代码，并在编辑后立即重新运行应用。非常适合快速反馈循环。

### [代码示例]

```text
# Open a terminal in your project directory and run:
dotnet watch run
// Example: Program.cs
Console.WriteLine("This is the initial version.");
// After saving changes while dotnet watch is running:
Console.WriteLine("Code updated! dotnet watch reloaded the app.");
```

### [执行结果]

```text
Terminal output:
dotnet watch □ started
watch : Started
This is the initial version.
watch : File changed: Program.cs
watch : Restarting
Code updated! dotnet watch reloaded the app.
```

dotnet watch 是 .NET CLI 工具集的一部分，像项目的实时观察器一样工作。

### 为什么有用：

- 保存更改时，它会自动重新编译并重新运行项目。
- 非常适合控制台应用、API 或 Blazor 开发。
- 节省时间，避免枯燥的手动停止-运行循环。

### 工作原理：

- 监视 .cs 文件（以及其他相关文件）的更改。
- 触发重新生成并重新启动应用。
- 可与 run、test、build 等配合使用。例如：

dotnet watch test 会在每次文件更改时重新运行测试。

### 何时使用：

- 在开发需要即时反馈的应用期间。
- 当频繁微调少量逻辑时。

### [补充]

可以在项目的 .csproj 文件中使用 watch 节来配置 dotnet watch，以忽略或包含某些文件。

它在内部使用文件系统监视器来高效检测更改。

你也可以传递参数：

```text
dotnet watch run --my-arg value
```

## 第 4 章 请求评价

非常感谢你读到最后。

这本书是为像你这样的开发者精心打造的——那些已经会写代码、已经在其他语言中与逻辑和结构打过交道、不需要别人告诉其什么是变量的人。

相反，我们纯粹聚焦于 C# 的独特之处：那些习语、特性、生态系统以及细微差别，否则即使是经验丰富的程序员也可能被绊倒。

目标是清晰而不妥协——快速、专注且高度相关。

无论你是从 Java、Python、JavaScript 还是任何其他背景转过来，我希望本指南能帮助你剔除噪音，聚焦于让 C# 与众不同的核心知识。

如果你是一位资深 C# 开发者，只是想跟上最近版本中的变化，我真心希望它充当了一次简短而有力的复习。

现在，我想请你帮个小忙。

如果这本书帮助了你，哪怕只是一点点——也许它为你节省了几个小时，澄清了一个棘手的概念，或者在其他资源显得臃肿或过时时给了你一个清晰的概览——请考虑留下评价。

不必很长。

事实上，如果你时间紧张，只需快速点一下星级评分，对我来说就意义重大。

但如果你确实有几分钟时间分享一个想法、一个见解，甚至一条批评，我向你保证：我会阅读每一个字。

你的反馈不仅值得感激——而且至关重要。它帮助我塑造下一个版本、改进重要之处，甚至可能选择下一个主题。

什么让你困惑？什么对你帮助最大？有遗漏吗？你想要更多代码示例、图表、与其他语言的现实世界比较，甚至小练习吗？或者也许你只是想告诉我，书中哪里让你发出“啊，现在我懂了”的感叹。所有这些都很有价值。

你的声音对这一过程的引导作用远超你的想象。

真的——如果时间很紧，哪怕一句评价或只是点些星星也极其有帮助。

再次感谢你的阅读，我真心希望我们能在另一本书、另一次深入探索中，或在你学习旅程所到之处再次相遇。

永远万事如意。


7. 将 Main 过程更改为以下内容（只需足以让 Excel 运行起来）：

```
static void Main(string[] args)
{
    Microsoft.Office.Interop.Excel.Application xl = new Application();
    xl.Quit();
}
```

- 8. 右键单击解决方案，然后选择“添加”->“新建项目”。
- 9. 添加一个新的安装项目。
- 10. 右键单击该安装项目，然后选择“添加”->“项目输出”。
- 11. 选择“主输出”。
- 12. 单击“确定”。

安装项目将自动确定随应用程序部署的内容。在 Visual Studio 2012 中，使用 C# 3.0 时，它将部署主互操作程序集，如图 7-1 所示。

![](img/80ff26f06fc9ab951e1cd4257b867366_521_0.png)

图 7-1：
在 C# 3.0 中部署 PIA。

在 Visual Studio 2012 中，安装程序不部署 PIA。正在使用的特定部分会直接编译到应用程序的 EXE 中。图 7-2 演示了这一点。

![](img/80ff26f06fc9ab951e1cd4257b867366_522_0.png)

**图 7-2：** 在 C# 4.0 中不部署 PIA。

## 跳过 ref 语句

由于编程模型不同，许多 COM API 包含大量引用参数。与 C# 中的 ref 不同，这些参数通常不是为了改变传入的参数以便调用方后续使用，而只是传递值参数的另一种方式。

因此，C# 程序员必须为所有此类 ref 参数创建临时变量并按引用传递它们，这似乎不合理。所以让我们删除它们。

相反，专门针对 COM 方法，C# 编译器允许你按值向此类方法传递参数，并自动生成临时变量来保存传入的值，然后在调用返回时丢弃这些变量。这样，调用方看到的是值语义，不会经历任何副作用，但被调用的方法仍然获得引用。

你可以在第 2 章经典的可选参数示例中看到这一点。在 Microsoft Word 通常的 SaveAs 中，一切都是引用参数。

```csharp
object filename = "test.docx";
object missing = System.Reflection.Missing.Value;

doc.SaveAs(ref filename,
    ref missing, ref missing, ref missing,
    ref missing, ref missing, ref missing,
    ref missing, ref missing, ref missing,
    ref missing, ref missing, ref missing,
    ref missing, ref missing, ref missing);
```

在 C# 4.0 中，你可以同时跳过“missing”可选参数和 ref 语句。

```
object filename = "test.docx";
doc.SaveAs(filename);
```

## 第 IV 部分

## Visual Studio 之旅

![](img/80ff26f06fc9ab951e1cd4257b867366_524_0.png)

> > “我所寻找的是动态软件应用程序和内容，而不是软件的含沙射影和意图。”

## 内容速览

- 第 1 章：Visual Studio 入门 ..................501
- 第 2 章：使用界面 ................................517
- 第 3 章：自定义 Visual Studio ............................541
- 第 4 章：转换文本模板 ..........................557

## 第 1 章：Visual Studio 入门

### 本章内容

- 概览可用版本
- 设置 Visual Studio
- 了解项目和解决方案
- 探索不同类型的项目

你很可能已经发现的许多 C# 内容都可以使用命令提示符和 `csc.exe` 来运行。事实是，这并不是一种很好的编程方式。它不宽容、缓慢，而且很难记住语言的具体细节。集成开发环境（IDE）是一个为开发提供平台的程序。它有助于让开发更容易。

习惯从空白屏幕和命令行开始的程序员常常认为 IDE 缓慢、拖沓、浪费时间。然而，我从未见过这些程序员中的任何一个在 Visual Studio 中工作后不改变看法。它快速、易用、敏捷且智能。

确实，你不必使用 IDE 来编程，但如果你要使用一个 IDE，那就应该是 Visual Studio。它是专门为编写 C# 代码而构建的，也是为构建 Windows 程序而设计的。（推销结束——微软，现在给我 20 美元吧。）

然而，还有其他选择。MonoDevelop 是为 Linux 用户编写 .NET 代码而构建的工具，但也可在 Windows 中运行。SharpDevelop 是另一个 IDE，作为测试平台具有一些极佳的潜力。这两个工具都是免费的。

说真的，自从我深入钻研并撰写 *《Visual Studio .NET 高效编程》* 以来，我就不是 Visual Studio 的粉丝。它确实让编写软件更容易。它不能替代对语言、面向对象编程或 .NET Framework 的了解，但它确实让生活稍微轻松了一些。

本章向你介绍 Visual Studio 的各种版本，并讨论你可用的 C# 项目。

## 版本划分

Visual Studio 有许多不同的版本（多得数不清——甚至有一大堆）。

原因在于其著名的许可问题。如果微软只按整套软件的价值出售整个包，只有《财富》50 强企业才买得起，这会排除约 99% 的受众。如果微软制作许多不同版本，并试图纳入不同人群使用的功能，它就能覆盖近 100% 的受众。

![](img/80ff26f06fc9ab951e1cd4257b867366_527_0.png)

本书重点介绍 Professional 版，正如我在引言中提到的。然而，许多示例代码可在任何版本中运行——尽管步骤列表有所不同。

在本章中，我将逐一介绍所有主要版本的功能和优势。在本节末尾，有一个表格显示主要功能以及每个版本包含的内容。

### Express 版

Express 是 Visual Studio 的免费版本。

是的，我说的是*免费*，也就是“不花钱”。

Express 是为爱好者而设计的，但我认识的许多专业程序员将其用作“家庭”版，用于小型个人项目或从事开源项目。

尽管 Express 的功能比 Professional 版少得多，但你可以在 Express 中编译本书中几乎所有的代码示例。它拥有 .NET Framework 的强大功能，而 .NET Framework 也是免费的，并为你提供学习 C# 的重要途径。

Express 版并非为制作生产软件而设计。它缺少几种项目类型以及许多团队开发工具。尽管如此，它运行 C# 和其他任何东西一样好——请记住，C# 只是一种语言。

Express 有许多不同的子版本。Express 的细分将微软开发生态划分为技术领域：每个主要平台一个版本。这样，爱好者开发者就可以专注于自己的兴趣所在。

- **用于 Windows 8 的 Visual Studio Express：** Windows 应用商店及其应用程序将彻底改变 Windows 世界。用于 Windows 8 的 Express 使你能够免费开发 Windows 应用商店风格的应用，只需承担使用商店相关的部署成本。你可以使用此版本开发 C#、C++ 和 JavaScript Windows 8 应用以及相关组件。不过，此版本非常适合学习语言和参与开源应用程序项目。开源项目（你只需贡献代码，而不是为报酬贡献整个项目）是 Express 版本的良好用途。如果你没有其他选择，我建议你从这里开始。

- **用于 Windows 桌面的 Visual Studio Express 2012：** 与 Windows 8 版一样，Visual Studio 的 Windows 桌面版允许你用多种语言编写在 Windows 7 或 8（或服务器版）的 Windows 桌面上运行的应用程序。你无法像在大公司中那样拥有大型多层应用程序，但可以编写相当可靠的 WPF 或 Windows Forms 程序作为组件。

- **用于 Web 的 Visual Studio Express 2012：** Web 版是 Visual Studio 一个有趣的免费版本。它围绕使用 ASP.NET、ASP.NET MVC 或 Silverlight 创建网页而设计。由于这些语言不进行编译，你可以免费编写生产软件。这对你我来说都更好。

撰写本文时，VB 和 C# 都受支持，并且 Visual Studio 中 Web 项目的大部分功能都可用。要了解更多信息，请访问 www.microsoft.com/express。

- **用于 Windows Phone 的 Visual Studio Express 版本：** 撰写本文时，Visual Studio 的 Windows Phone 版仍然是 2010 版，但我敢打赌，当你读到本文时，它将是 2012 版。WP 版是最早创建的特定平台版本之一，显然也是这批 Express 版本的模板。此包为你提供使用 XAML 和 C# 或 VB.NET 构建、调试和部署 Windows Phone 应用所需的一切。

### Professional 版

Professional 版是为专业程序员设计的。这个 Visual Studio 版本是我每天使用的版本。它旨在生成解决特定问题的独立程序。

微软很在行，其 Professional 版有三个目标：

- 支持新兴趋势
- 激发开发者的愉悦感
- 驾驭下一代平台浪潮

这真是一针见血。这是整本书所基于的版本，也是我推荐用于大多数程序生产的版本，尽管它需要花钱。

![](img/80ff26f06fc9ab951e1cd4257b867366_528_0.png)


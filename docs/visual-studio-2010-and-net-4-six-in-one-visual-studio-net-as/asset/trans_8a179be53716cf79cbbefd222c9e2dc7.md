
这个程序非常简单，即使它大约有70行代码。`Main` 方法创建一个 Excel 表格，并设置了一个包含名称和内存使用情况的双列表格。通过对 `Process.GetProcesses()` 进行 LINQ 查询，它根据内存消耗获取顶级进程。该方法将进程信息放入 Excel 表格，通过 `Charts.Add` 方法创建一个精美的三维柱状图，并将其复制到剪贴板。最后，它创建一个新文档并将图表粘贴到文档正文中。

此时，你已经准备好通过 Ctrl+F5 来构建并运行此应用程序。你会看到 Excel 和 Word 闪烁几秒钟，然后 Word 将显示与图 24-2 中的图表类似的结果。

![](img/b5597c749e848b27b0d305153ae16106_1110_0.png)

**图 24-2：** 在 Microsoft Office 中显示图表

## 令人沮丧的问题

尽管与其提供的价值相比，上面的代码看起来简单又简洁，但它充满了语法噪音。如果你恰好在 Visual Basic 中创建此应用程序，它会更短且没有这些噪音。

第一个且引人注目的是，代码大量使用了 `Type.Missing` 实例。它们作为 COM 方法可选参数的占位符存在。在这段短代码中，你可以数出它们出现了 17 次，意味着总共有 204 个不必要的字符。`ChartWizard` 方法的调用包含 11 个参数，其中只有 2 个使用了非默认值。你必须传递 `Type.Missing` 实例才能让代码编译。

另一个设置 Excel 单元格值的代码片段如下：

```csharp
((Excel.Range)excel.Cells(i, 1)).Value = p.ProcessName;
((Excel.Range)excel.Cells(i, 2)).Value = p.WorkingSet64;
```

这个简单的操作应该是“有噪音”的？首先，你必须将对象单元格转换为 `Excel.Range`，然后通过 `Value2` 属性设置值。如果你从未在 C# 中用过 Excel，可能需要一点时间才能熟悉这种风格。它可以被称为任何东西，但不是“直观”。

看看调用 `Document.Add` 方法的代码。它接受的四个参数必须通过 `ref` 传递：

```csharp
object template = Type.Missing;
object newTemplate = Type.Missing;
object docType = Type.Missing;
object visible = Type.Missing;
word.Documents.Add(
ref template,
ref newTemplate,
ref docType,
ref visible);
```

调用该方法是为了修改它们（`Type.Missing` 是不可变的）。`Add` 方法已经实现，你的选择是原样使用它。为了调用此方法，你必须创建四个 `System.Object` 临时变量并将 `Type.Missing` 赋值给它们。整个努力都是为了通过引用传递。

## 消除痛苦

托管语言团队找到了解决这些沮丧问题的办法。该解决方案是 C# 4.0 语言规范的一部分，由本章后面介绍的几个特性组成。

创建一个新的控制台应用程序并将其命名为 `PaneWithOfficeRemoved`。将 `Program.cs` 文件更改为列表 24-2 所示的内容。生成并运行项目。

> 列表 24-2：Program.cs 中移除了语法噪音

```csharp
using System;
using System.Linq;
using System.Diagnostics;
using Excel = Microsoft.Office.Interop.Excel;
using Word = Microsoft.Office.Interop.Word;
namespace PaneWithOfficeRemoved
{
class Program
{
    static void Main(string[] args)
    {
        var excel = new Excel.Application();
        excel.Visible = true;
        excel.Workbooks.Add();
        excel.Cells[1, 1].Value = "Process Name";
        excel.Cells[1, 2].Value = "Memory Usage";

        var processes = Process.GetProcesses()
            .OrderByDescending(p => p.WorkingSet64)
            .Take(10);
        int i = 2;
        foreach (var p in processes)
        {
            excel.Cells[i, 1].Value = p.ProcessName;
            excel.Cells[i, 2].Value = p.WorkingSet64;
            i++;
        }

        var range = excel.Cells[1, 1];
        var chart = excel.ActiveWorkbook.Charts.Add(After: excel.ActiveSheet);
        chart.ChartWizard();
        Source = range.CurrentRegion;
        Title = "Memory Usage " + Environment.MachineName;
        chart.ChartType = Excel.XChartType.xl3DColumn;
        chart.Copy(Excel.XlAppearance.xlScreen);
        Excel.XlCopyPictureFormat = xlBitmap;
        Excel.XlPictureAppearance = xlScreen;

        var word = new Word.Application();
        word.Visible = true;
        word.Documents.Add();
        word.Selection.Paste();
    }
}
}
```

代码文件 [Program.cs] 可在 Wrox.com 下载。

你可以看到，它的工作方式与列表 24-1 完全相同。然而，这个版本没有了烦人的语法噪音。

从列表 24-2 中你可以立即识别出没有任何 `Type.Missing` 实例！查看 `Charts.Add` 和 `ChartWizard` 方法。你可以看到参数是通过名称传递的。在 24-2 中，使用了显式类型声明。现在，让我们看看背后，并检查使这一切成为可能的改进。

## 动态查找

C# 开发者熟悉类型和操作在编译过程中会被严格检查这一事实。在编程语言的宇宙中还有另一个星系：动态语言。编译器对类型进行一些检查；其中大部分被推迟到执行阶段。

除了动态语言外，还有脚本语言和对象模型（例如来自 Microsoft Office 的 COM 对象、Visual Studio 中的 DTE 对象、Internet Explorer 中的 HTML DOM 等），它们在运行时也会检查操作。

在这个复杂的世界里，这些工具和语言的运行方式应该是提高开发者的效率。像 JavaScript、PowerShell 等许多脚本工具和语言，以及像 Python 或 Ruby 等动态语言在今天非常流行。它们为对象提供了统一的方法，无论对象源自何处、后台如何运作，都能独立运行。这些工具关注最重要的事情：提供最简单、最直观的方法来使用对象的功能。

长期以来，C# 无法与这些语言和工具的灵活性竞争。但现在情况不再如此。

## 动态绑定

C# 4.0 新版本提供了动态绑定作为一种选择和执行操作的统一方法。操作可以在各种对象上执行，无论特定对象来自 COM（通过互操作性）、IronRuby、IronPython、HTML DOM 还是任何其他动态上下文。运行时接管了开发者的责任，并由它决定给定操作对特定对象的含义。

动态绑定在 C# 4.0 中实现为一种显式机制，你可以根据需要选择是否使用这种行为。然而，当你迁移你的代码并运行 C# 3.0 代码时


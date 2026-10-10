
是的，我也是这么这么的。我甚至不想尝试去分解这段代码——幸运的是，我并不需要这样做。这正是编译器要做的工作，不是吗？

# 使用动态语言运行时运行

动态语言不仅仅是动态类型。你可以做一些强大的事情。就像所有的力量一样，你必须小心不要误用。

动态运行时——如图 6-1 所示——是添加到 .NET Framework 的一个库，专门用于向 Visual Studio 体系（如 IronRuby）添加动态语言（如 Ruby），或者为现有的静态语言添加动态语言特征（如 C# 4.0）。

![](img/6df7bb88e9302e98442acc219cfbd7fc_513_0.png)

动态语言运行时帮助编译器在编译后的程序集中构建代码，这些代码将进行许多动态选择。前一节末尾的代码块是最简单的一种示例。

`DLR` 辅助了 `IRONRuby` 的创建，使得在 Visual Studio 中直接使用 Ruby（当前的动态语言）进行编程成为可能。当然，由于 `DLR` 让 C# 具备动态语言特征，你在 Ruby 中可以的操作现在可以在 C# 中完成。

## 动态 Ruby

Ruby 在实现 Trabb Pardo-Knuth 算法时利用了它的动态根。不要被名字吓跑——这只是一个可以通过计算机代码解决的简单问题。

程序需要从输入设备读取 11 个数字——在这种情况下是控制台的 `ReadLine` 方法。它将它们存储在数组中。然后，它使用递归反向处理数组——从最后一个输入值开始。如果值不超过某个任意阈值，它就会打印结果。

该程序在 Ruby 中看起来如下：

```ruby
class TPK
def f( x )
  return Math.sqrt(x.abs) + 5*x ** 3
end
def main
  Array.new(11) { gets.to_i }.reverse.each do |x|
    y = f(x)
    puts "#{x} #{y > 400 ? 'TOO LARGE' : y}"
  end
end
```
这不是一本 Ruby 教程，这一点我很清楚。尽管如此，这是我能用来示例的最好的动态语言——绝无仅此。

定义了两个函数：`f` 和 `main`。`main` 从控制台接受 11 个数字并将它们移动到整数数组（这就是 `gets.to_i` 所做的）。对于数组中的每个值，它将 `y` 设置为 `f(x)` 并检查它是否高于这个任意值。如果是，它打印“TOO LARGE”；否则它打印该数字。

为什么动态化对这个算法很重要？其实并不重要。你可以完全使用静态类型来完成。不过，动态部分确实有影响。

第三卷
第六章

## 动态 C#

当然，C# 现在也有类似的特征，对吧？你应该能够做同样的事情！事实上，你确实可以。代码如下：

```csharp
static dynamic f(dynamic x)
{
    return (Math.Sqrt(x) + 5.0 * Math.Pow(x, 3.0));
}
static void Main(string[] args)
{
    dynamic[] array = new Array[11];
    for (int i = 0; i < 11; i++)
    {
        array[i] = Console.ReadLine();
    }
    for (int i = 10; i>=0; i--)
    {
        dynamic y = array[i];
        if (y > 400.0)
        {
            Console.WriteLine(String.Format("{0} TOO LARGE", i));
        }else
        {
            Console.WriteLine(String.Format("{0}: {1}", i, array[i]));
        }
    }
    Console.ReadKey();
}
```

逐行来看，该应用程序的功能与 Ruby 代码相同，尽管代码更长。我保持了相同的名称以便于查找。因为我必须使用循环来处理积分器，这使得正文的。

# 使用动态语言运行时

图 6-2: TPK

![](img/6df7bb88e9302e98442acc219cfbd7fc_516_0.png)

为什么动态化对这个算法很重要？其实并不重要。你可以完全使用静态类型来完成。不过，动态部分确实有影响。

# 使用动态导入

如果你计划针对 Microsoft Office 编写代码，相信我——这是你需要的信息。

## 使用动态导入

许多 COM 方法接受并返回变体类型（variant types），这些类型由主互操作程序集（primary Interop assemblies）作为对象表示。在大多数情况下，调用这些方法的程序员已经根据上下文知道返回对象的静态类型，但必须显式地对返回值进行类型转换（cast）以利用这些知识。这些类型转换在日常开发中非常常见，以至于变成了一个巨大的麻烦。

为了获得更顺畅的体验，你可以以这种方式导入这些 COM API，使变体使用 `dynamic` 类型表示。换句话说，从你的角度来看，COM 签名中出现的是 `dynamic` 而不是 `object`。

这意味着你可以轻松地访问返回对象的成员，或者将对象赋值给强类型局部变量而无需进行类型转换。为了说明，你可以写：

```csharp
excel.Cells[1, 1].Value = "Hello";
```

而不是：

```csharp
{Excel.Range}excel.Cells[1, 1].Value2 = "Hello";
```

以及

```csharp
Excel.Range range = excel.Cells[1, 1];
```

而不是

```csharp
Excel.Range range = {Excel.Range}excel.Cells[1, 1];
```

为什么这很重要？首先，它简化了程序员的工作。Microsoft Office 的代码极其难读。看看这段我为《Visio 入门》（Vis For Dummies）一书编写的 Office 应用程序代码：

```csharp
Office.CommandBars commandBars = default(Office.CommandBars);
Office.CommandBar commandBar = default(Office.CommandBar);
Office.CommandButton runReport = default(Office.CommandButton);
commandBars = (Microsoft.Office.Core.CommandBars).Application.CommandBars;
commandBar = commandBars.Add("Toolbar", Office.MsoPosition.msoTop);
commandBar.Context = Visio.VisObjSheet.VisioObj.commandBar.Controls += *;
runReport = (Microsoft.Office.Core.CommandButton).Controls.Add(null, null, null, msoControlButton);
runReport.Tag = "Start Report";
runReport.Click += Visio.VisibleSheets;
```

- 注意

## 在不使用主互操作程序集的情况下

以下是 C# 4.0 中该代码块的样子：

```csharp
Office.CommandBars commandBars = Office.CommandBars;
Office.CommandBar commandBar = Office.CommandBar;
Office.CommandButton runStoreReport = Office.CommandButton;
commandBars = Application.CommandBars;
commandBar = commandBars.Add("Toolbar", msoBarTop, , true);
commandBar.Context = Vis.VisUIB., visUIB.Drawing = ***;
runStoreReport = commandBar.Controls.Add(msoControlButton);
runStoreReport.Tag = "Store Report";
runStoreReport.Click += Visualie;
```

有很多内容要读。请记住，所有这些类型转换仍然存在——它们由编译器处理。Microsoft 并没有将 Office 组件重写为 .NET；公司只是让编译器的通信变得更好。编译器仍然构建与原有的主互操作程序集进行通信的代码。

## 在不使用主互操作程序集的情况下

提到 `PIAs`（原谅它与另一个著名的缩写相似），它们在 .NET 4.0 中处理得好得多。

`PIAs` 是从 COM 接口生成的大型 .NET 程序集，用于促进强类型互操作性。它们在设计时提供了很好的支持，此时你对互操作的体验就像类型真的定义在 .NET 中一样。然而，在运行时，这些大型程序集很容易构建你的程序，并导致版本问题，因为它们是独立于你的应用程序分发的。

`no-PIA` 功能允许你在设计时继续使用 `PIAs`，而不需要在运行时包含它们。C# 4.0 编译器将程序实际使用的 `PIA` 的小部分直接转到它的程序集中。`PIA` 不需要在运行时加载。

要查看 Visual Studio 2012 和 Visual Studio 2010（如果你有）中如何操作这些步骤：

1. 通过选择“文件: 新建项目”并选择“C# - 控制台应用程序”，并将你的项目命名为 `PIAs`。
2. 项目加载后，右键点击“引用”。
3. 点击“添加引用”。
4. 如果你有，选择 `Microsoft.Office.Interop.Excel`，版本 12，或者你已加载的最新版本。
5. 点击“确定”。
6. 在文件头添加 `using Microsoft.Office.Interop.Excel;`。

## 在不使用主互操作程序集的情况下

7. 将 `Main` 过程更改如下（仅足以让 Excel 运行起来）：

```csharp
static void Main(string[] args)
{
    Microsoft.Office.Interop.Excel.Application xl = new Application();
    xl.Quit();
}
```



3. 你可以创建一个新的 .css 文件并向其中添加样式，也可以先创建样式然后选择创建新的 .css 文件的选项。可以通过使用应用样式窗口来应用样式。

## Feedback 7.3
- 1. 在你的文档中添加一个 RequiredFieldValidator 和 RangeValidator。
- 2. 将所有三个验证器的 ControlToValidate 属性设置为 QuantityTextBox。
- 3. 将 RequiredFieldValidator 的 Enabled 属性设置为 true。
- 4. 将 RangeValidator 的 MinimumValue 属性设置为 1，其 MaximumValue 设置为 100。
- 5. 最后，将 RangeValidator 的 Type 属性设置为数值类型（Integer 或 Double）。

## Feedback 7.4
```
1. Session("Email") = EmailTextBox.Text
2. EmailLabel.Text = Session("Email").ToString()
3. With Response.Cookies("Email")
   .Value = Session("Email").ToString()
   .Expires = Today.AddYears(3)
End With
```
- 4. 使用 Session 对象或将状态值存储在客户端机器上的 cookie 中。
- 5. 使用 ViewState 属性允许你仅为当前页面维护值。
- 6. Page_Load 事件在每次往返服务器时都会发生。初始化步骤应仅在页面的首次显示时执行（Not IsPostBack），检索会话变量应仅在回发时发生（IsPostBack）。

## Feedback 8.1
- 1. FormView 和 DetailsView 都一次显示一条记录，但通过设计模板，使用 FormView 控件可以更好地控制布局。
- 2. 当需要过滤时需要多个数据源控件。当你有一个列表框时，一个数据源控件用所有记录填充列表，而另一个数据源控件用于过滤数据集。
- 3. 当没有更新时，数据读取器是最好的选择。

## Feedback 10.2
- 1. `PersonsHashTable.Item(KeyString)`
- 2. 集合的 Item 属性通常是默认属性。
- 3. `PersonsHashTable.RemoveAt(KeyString)`
- 4. `APerson = CType(PersonsHashTable.Item(KeyString), Person)`

## Feedback 10.3
- 1. 由该对象 ToString 方法返回的内容。
- 2. 你可以编写自己的 ToString 方法，该方法必须重写基类 ToString 方法。

## Feedback 10.4
- 1. a. 对于数据类型使用 GenericType。
  
  ```vb
  Public Sub Swap(Of GenericType)(ByRef Item1Type As GenericType, _
      ByRef Item2Type As GenericType)
      Dim TempType As GenericType
  ```
  
  b.
  ```vb
  Public Class GenericCollection (Of GenericType)
      Inherits CollectionBase
  ```
- 2. 任何类型的对象都可以用泛型类使用，但单个集合中的所有对象必须是同一类型。
- 3. List, Dictionary, LinkedList, Queue, ReadOnlyCollection, Stack, Sorted-Dictionary, SortedList。

## Feedback 11.1
- 1. `Event WillSoundAlarm()`—必须出现在模块级别（在 Declarations 部分）。
      `RaiseEvent WillSoundAlarm()`—出现在程序逻辑中。
- 2. Alarm 控件的一个实例包含一个 WillSoundAlarm 事件；像为其他任何对象编码事件一样对其进行编码。

## Feedback 11.2
- 1. 使用 ASP.NET Web Site 模板并向项目添加一个 WebUserControl。
- 2. 创建你的控件；然后从 Solution Explorer 将控件文件拖到 Web 表单上。

## Feedback 12.1
- 1. a. .hhx 是一个索引文件，用于保存可搜索索引的条目。
  b. .hhc 是目录文件，用于存储内容选项卡的标题和组织结构。
  c. .chm 是一个编译帮助文件，用于保存编译的帮助项目。
  d. .jpeg 是一个图形文件，用于保存图像。
  e. .avi 是一个多媒体文件，用于存储电影。
  f. .htm 是一个主题文件，用于保存在帮助内容窗格中显示的屏幕。
- 2. 上下文相关帮助
- 弹出帮助
- ToolTips
- 状态栏
- 帮助菜单

## Feedback 13.1
Smart Device 应用程序在运行 Windows 操作系统的设备上运行。

## Feedback 13.2
- 1. Content 属性。
- 2. 属性窗口在标题区域包含一个文本框用于输入对象名称。
- 3. ElementHost 控件提供了将 WPF 控件添加到 Windows Form 应用程序的能力。

## Feedback 13.3
- 1. 语言集成查询（LINQ）是一种用于查询数据的标准语言。
- 2. LINQ 通常用于数据集合，例如数组、XML，以及使用 LINQ to SQL 模板转换为对象的 SQL 数据集。
- 3. 使用类型推断，字段的数据类型由字段的使用方式决定。
- 4. Child <fieldname> Attribute ./fieldname Descendant ...<fieldname>

## Feedback 13.4
- 1. My.Application.ChangeUICulture("fr-FR")
- 2. 该语句应放置在 Sub New() 过程中。

## Feedback 13.5
- 1. 后台处理代码可以放置在任何过程中。
- 2. BackgroundWorker1.RunWorkerAsync()
- 3. 在 DoWork 事件处理程序中使用 BackgroundWorker.CancellationPending 方法。在取消按钮的事件处理程序中调用 CancelAsync 方法以取消操作。在 RunWorkerCompleted 事件处理程序中检查 e.Cancelled。

## APPENDIX

## B

## Review of Introductory
VB Concepts

本附录旨在作为对在入门课程中通常涵盖的 VB 主题的回顾。你应始终将 MSDN 帮助文件作为主要参考，并在需要对这些主题中的任何一个进行更多解释时查阅。

## Microsoft’s Visual Studio

微软的最新 Visual Studio 版本，称为 Visual Studio 2008，包含 Visual Basic、Visual C++、C#（C sharp）和 .NET Framework 版本 3.5。Visual Studio 2008 有时被称为 Visual Studio 版本 9。

## The .NET framework

Visual Studio 中的编程语言在 .NET Framework 中运行。该框架提供了更轻松地开发基于 Web 和基于 Windows 的应用程序的功能，允许不同语言的对象协同工作，并标准化语言引用数据和对象的方式。许多第三方厂商已为在 .NET Framework 中运行而制作了其他语言的版本，包括 FORTRAN、COBOL 和 Java。

.NET 语言都编译为一种通用的机器语言，称为 Microsoft Intermediate Language（MSIL）。MSIL 代码，称为托管代码，在 Common Language Runtime（CLR）中运行，CLR 是 .NET Framework 的一部分。

微软将 .NET Framework 作为 Windows 操作系统的一部分包含在内。当某人安装其操作系统的任何可用更新时，.NET Framework 也包含在内。

## Visual Studio

Visual Studio（VS）是微软的一组产品。该软件包附带 Visual Studio 集成开发环境（IDE）和 Visual Basic、C++ 和 C# 编程语言。所有语言共享相同的 IDE，因此程序员从一种语言切换到另一种语言应该相对容易。Visual Studio 有多个版本，具有不同的功能和价格。在帮助中可以看到显示 Express Edition、Professional Edition 和 Team Developer Edition 功能的矩阵。

Visual Studio 运行在 Windows XP 和 Windows Vista 上。

## Namespaces

命名空间用于在 .NET Framework 中组织和引用类组。在命名空间内，两个类不能具有相同的名称。框架中的类组织在诸如
- System
- System.Data
System.Drawing
System.Windows.Forms

的命名空间中

多个文件可以位于同一命名空间中，一个文件可以包含多个命名空间。一些企业使用命名空间按应用领域组织其类。

默认情况下，新的 VB 项目包含某些命名空间的引用。如果你想使用其他命名空间中的类，可以添加 Imports 语句。例如，要在 StreamWriter 中写入数据（它取代了 VB 的顺序文件），你必须声明 StreamWriter 数据类型的对象，该对象位于 System.IO 命名空间中（未包含在默认引用中）。你可以使用以下两种方法之一：
- 1. 使用 Imports 语句：

```
' 此语句出现在文件的顶部，在 Class 语句之前：
Imports System.IO
```

```
' 此语句出现在类内部，在模块级别或在过程中：
Dim BooksStreamWriter As StreamWriter
```
- 2. 不使用 Imports 语句但通过包含命名空间来限定每个引用：

```
' 此语句出现在类内部，在模块级别或在过程中：
Dim BooksStreamWriter As System.IO.StreamWriter
```

如果你检查设计器自动生成的代码，你会看到每个引用都是完全限定的。

## Visual Basic Solutions and Projects

VB 解决方案由一个或多个项目组成，而项目由多个文件组成。Visual Studio IDE 会自动为新解决方案创建一个文件夹；解决方案中的所有文件都应存储在该文件夹中。

## The Solution File

VB 解决方案文件是一个文本文件，存储项目的名称和解决方案的配置信息。该文件可以用文本编辑器编辑，并具有 .sln 扩展名。伴随的 .suo 文件存储环境屏幕布局的信息，不是文本文件，因此无法编辑。但是，你可以删除 .suo 文件；下次打开解决方案时，.suo 文件将被重建。

默认情况下，VS 2008 不会自动在 Solution Explorer 中显示解决方案文件。选择 Tools / Options / Projects and Solutions / Always show solution 以显示解决方案文件。你需要显示解决方案文件以重命名它或向解决方案添加另一个项目。


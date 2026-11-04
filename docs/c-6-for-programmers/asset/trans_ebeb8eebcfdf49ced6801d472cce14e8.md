
| 自定义控件技术和 PaintEventArgs 属性 | 说明 |
|---|---|
| *自定义控件技术* | |
| **从 Windows 窗体控件继承** | 可以这样做来为现有控件添加功能。如果重写方法 `OnPaint`，请调用基类的 `OnPaint` 方法。只能为原始控件的外观增补内容，不能重新设计它。 |
| **创建 UserControl** | 可以创建由多个现有控件组成的 `UserControl`（例如，组合它们的功能）。将绘制代码放在 Paint 事件处理程序中，或放在重写的 `OnPaint` 方法中。 |
| **从 Control 类继承** | 定义全新的控件。重写方法 `OnPaint`，然后调用基类方法 `OnPaint` 并添加绘制控件的代码。使用此方法，可以同时自定义控件的外观和功能。 |
| *PaintEventArgs 属性* | |
| **Graphics** | 控件的图形对象，用于在控件上绘制。 |
| **ClipRectangle** | 指定表示控件边界的矩形。 |

**图 15.49** | 自定义控件的创建。

## 时钟控件

我们在图 15.50 中创建一个“时钟”控件。这是一个由 Label 和 Timer 组成的 `UserControl`——每当 Timer 引发事件（本示例中每秒一次），Label 就会更新以反映当前时间。

```csharp
// Fig. 15.50: ClockUserControl.cs
// User-defined control with a Timer and a Label.
using System;
using System.Windows.Forms;

namespace ClockExample
{
    // UserControl that displays the time on a Label
    public partial class ClockUserControl : UserControl
    {
        // constructor
        public ClockUserControl()
        {
            InitializeComponent();
        }
    }
}
```

**图 15.50** | 带 Timer 和 Label 的用户定义控件。（第 1 部分，共 2 部分。）

```csharp
// update Label at every tick
private void clockTimer_Tick(object sender, EventArgs e)
{
    // get current time (Now); convert to string
    displayLabel.Text = DateTime.Now.ToLongTimeString();
}
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_534_0.png)

**图 15.50** | 带 Timer 和 Label 的用户定义控件。（第 2 部分，共 2 部分。）

## 计时器

**计时器**（System.Windows.Forms 命名空间）是非可视组件，按设定间隔生成 Tick 事件。该间隔由 Timer 的 **Interval** 属性设置，它定义事件之间相隔的毫秒数（千分之一秒）。默认情况下，计时器处于禁用状态，不生成事件。

## 添加用户控件

此应用包含一个用户控件（ClockUserControl1）和一个显示该用户控件的 Form。创建一个 Windows 应用，然后选择 **项目 > 添加用户控件...** 创建 UserControl 类。此时会显示一个对话框，可从中选择要添加的项类型——用户控件已被选中。然后，我们将文件（和类）命名为 ClockUserControl。空白的 ClockUserControl 显示为灰色矩形。

## 设计用户控件

可以像 Windows 窗体一样处理此控件，也就是说，可以使用“工具箱”添加控件，并使用“属性”窗口设置属性。不过，这里不是创建应用，而只是创建一个由其他控件组成的新控件。向 UserControl1 添加一个 Label（displayLabel）和一个 Timer（clockTimer）。将 Timer 的间隔设置为 1000 毫秒，并在每个 Tick 事件（第 18–22 行；默认事件）中设置 displayLabel 的文本。要生成事件，必须在“属性”窗口中将属性 Enabled 设置为 true，以启用 clockTimer。

结构 **DateTime**（System 命名空间）包含属性 **Now**，它返回当前时间。方法 **ToLongTimeString** 将 Now 转换为包含当前小时、分钟和秒的字符串（以及 AM 或 PM，具体取决于区域设置）。我们使用它在第 21 行设置 displayLabel 中的时间。

创建后，我们的时钟控件会作为一项出现在“工具箱”中标题为 *项目名组件* 的部分，其中 *项目名* 是项目名称。在该项出现在“工具箱”中之前，可能需要切换到应用的 Form。要使用该控件，只需将其拖到 Form 上并运行 Windows 应用。我们为 ClockUserControl1 对象设置了白色背景，使其在 Form 中更醒目。图 15.50 显示了 Clock 的输出，其中包含我们的 ClockUserControl。Clock 中没有事件处理程序，因此只展示 ClockUserControl 的代码。

### 与其他开发者共享自定义控件

Visual Studio 允许你与其他开发者共享自定义控件。要创建可导出到其他解决方案的 UserControl，请执行以下操作：

- 1. 创建新的类库项目。
- 2. 删除最初随应用提供的 Class1.cs。
- 3. 在“解决方案资源管理器”中右键单击项目，然后选择“添加”>“用户控件...”。在出现的对话框中，命名用户控件文件并单击“添加”。
- 4. 在项目中，向 UserControl 添加控件和功能（图 15.51）。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_535_0.png)

图 15.51 | 自定义控件的创建。

- 5. 生成项目。Visual Studio 会在输出目录（bin/Debug 或 bin/Release）中为 UserControl 创建 .dll 文件。该文件不可执行；类库用于定义可在其他可执行应用中重复使用的类。你可以将 .dll 文件交给其他开发者，他们可以按照步骤 6 和 7 操作。
- 6. 创建新的 Windows 应用。
- 7. 在新的 Windows 应用中，右键单击“工具箱”，然后选择“选择项...”。在出现的“选择工具箱项”对话框中，单击“浏览...”。浏览到步骤 1–5 中创建的类库中的 .dll 文件。该项随后会出现在“选择工具箱项”对话框的“.NET Framework 组件”选项卡中。如果尚未勾选，请勾选该项。单击“确定”将该控件添加到“工具箱”。现在可以将此控件像任何其他控件一样添加到 Form。

### 15.15 小结

当今许多商业应用都提供易于使用和操作的 GUI。由于对用户友好 GUI 的需求，设计复杂 GUI 的能力已成为一项必不可少的编程技能。Visual Studio 的 IDE 使 GUI 开发快速而简单。第 14 章和第 15 章介绍了基本的 Windows 窗体 GUI 开发技术。第 15 章演示了如何创建菜单，菜单使用户可以方便地访问应用的功能。你学习了 DateTimePicker 和 MonthCalendar 控件，它们允许用户输入日期和时间值。我们演示了 LinkLabels，它们用于将用户链接到应用或网页。你使用了多个向用户提供数据列表的控件——ListBoxes、CheckedListBoxes 和 ListViews。我们使用 ComboBox 控件创建下拉列表，并使用 TreeView 控件以分层形式显示数据。随后介绍了使用选项卡窗口和多文档界面的复杂 GUI。本章最后演示了可视继承和创建自定义控件。第 16 章将介绍字符串和字符处理。

## 16
## 字符串和字符：深入探讨

## 目标

在本章中，你将：

- - 创建和操作 `string` 类的不可变字符串对象以及 `StringBuilder` 类的可变字符串对象。
- - 使用 `string` 和 `StringBuilder` 类的各种方法。
- - 操作 `Char` 结构的字符对象。
- - 使用正则表达式类 `Regex` 和 `Match`。

**大纲**

- 16.1 简介
- 16.2 字符和字符串基础
- 16.3 string 构造函数
- 16.4 string 索引器、Length 属性和 CopyTo 方法
- 16.5 比较字符串
- 16.6 在字符串中定位字符和子字符串
- 16.7 从字符串中提取子字符串
- 16.8 连接字符串
- 16.9 其他 string 方法
- 16.10 StringBuilder 类
- 16.11 StringBuilder 类的 Length 和 Capacity 属性、EnsureCapacity 方法和索引器
- 16.12 StringBuilder 类的 Append 和 AppendFormat 方法
- 16.13 StringBuilder 类的 Insert、Remove 和 Replace 方法
- 16.14 Char 方法
- 16.15 正则表达式简介（在线）
- 16.16 小结

## 16.1 简介

本章介绍 .NET Framework 类库的字符串和字符处理功能，并演示如何使用正则表达式在文本中搜索模式。本章介绍的技术可用于大多数类型的应用，尤其是文本编辑器、文字处理器、页面排版软件、计算机排版系统和其他类型的文本处理软件。前面几章介绍了一些基本的字符串处理功能。现在，我们将详细讨论 System 命名空间中的 string 类和 char 类型以及 System.Text 命名空间中的 StringBuilder 类的文本处理功能。

我们首先概述字符和字符串的基础知识，其中讨论*字符常量*和*字符串字面量*。然后提供 string 类的许多构造函数和方法的示例。这些示例演示如何确定字符串的*长度*、*复制字符串*、*访问字符串中的单个字符*、*搜索字符串*、从较大的字符串中获取*子字符串*、*比较字符串*、*连接字符串*、*替换字符串中的字符*，以及将字符串转换为*大写或小写*字母。

接下来，我们介绍 StringBuilder 类，它用于动态组合字符串。我们演示 StringBuilder 在确定和指定 StringBuilder 大小方面的功能，以及在 StringBuilder 对象中*追加*、*插入*、*删除*和*替换*字符的功能。然后介绍 Char 结构的字符测试方法，这些方法使程序能够确定字符是数字、字母、小写字母、大写字母、标点符号，还是标点符号以外的符号。此类方法可用于验证用户输入中的单个字符。此外，Char 类型提供将字符转换为*大写或小写*的方法。

我们在 http://www.deitel.com/books/CSharpFP 提供一个在线章节，讨论正则表达式。我们介绍 System.Text.RegularExpressions 命名空间中的 Regex 和 Match 类，以及用于构成正则表达式的符号。然后演示如何*查找字符串中的模式*、*将整个字符串与模式匹配*、*替换字符串中与模式匹配的字符*，以及在正则表达式中指定为模式的分隔符处*拆分字符串*。


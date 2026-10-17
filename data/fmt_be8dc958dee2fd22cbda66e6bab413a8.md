
```csharp
TimeSpan instanceName = new TimeSpan(Hours, Minutes, Seconds);
TimeSpan instanceName = new TimeSpan(Days, Hours, Minutes, Seconds);
TimeSpan instanceName = new TimeSpan(Days, Hours, Minutes, Milliseconds);
```

在通用格式中，`Days`、`Hours`、`Minutes`、`Seconds` 和 `Milliseconds` 的值均为整数。

# 对 DateTime 和 TimeSpan 对象进行数学运算

你可以通过以下方式对 `DateTime` 和 `TimeSpan` 对象进行数学运算：

- 你可以将一个 `TimeSpan` 加到 `DateTime` 对象，以获得比第一个对象更后的 `DateTime` 对象。例如，假设我们有一个设置为 4 月 5 日的 `DateTime` 对象，并且有一个设置为 10 天的 `TimeSpan` 对象。如果我们将 `TimeSpan` 对象加上 `DateTime` 对象，将得到另一个设置为 4 月 15 日的 `DateTime` 对象。

- 你可以从一个 `DateTime` 对象减去另一个，以得到表示两个 `DateTime` 对象之间间隔时间的 `TimeSpan` 对象。例如，假设我们有一个设置为 1 月 20 日的 `DateTime` 对象，减去另一个设置为 1 月 15 日的 `DateTime` 对象。结果将是一个设置为 5 天的 `TimeSpan` 对象。

这是一个如何创建一个表示 10 天的 `TimeSpan` 对象，然后将该对象加到 `DateTime` 对象中的示例：

```csharp
// Create a DateTime object for August 15, 2019.
DateTime dt = new DateTime(2019, 8, 15);

// Create a TimeSpan object for 10 days.
TimeSpan timespan = new TimeSpan(10, 0, 0, 0);

// Add the TimeSpan object to the DateTime object.
DateTime futureDate = dt + timespan;
```

执行此代码后，`futureDate` 对象将设置为 2019 年 8 月 25 日。

下面的代码示例展示了如何从一个 `DateTime` 对象减去另一个 `DateTime` 对象。结果是一个表示两个 `DateTime` 对象之间间隔时间的 `TimeSpan` 对象：

```csharp
// Create two DateTime objects.
DateTime date1 = new DateTime(2019, 8, 15);
DateTime date2 = new DateTime(2019, 8, 30);

// Get the amount of time.
TimeSpan tspan = date2 - date1;
```

执行此代码后，`tspan` 对象将设置为 15 天。

下面的方法展示了如何通过数学方式调整 `DateTime` 对象：

| 方法 | 说明 |
| :--- | :--- |
| `Add(TimeSpan)` | 返回表示当前 `DateTime` 加上指定 `TimeSpan` 的 `DateTime` 对象。 |
| `Subtract(DateTime)` | 返回表示当前 `DateTime` 与指定 `DateTime` 之间差值的 `TimeSpan` 对象。 |
| `Add(DateTime)` | 返回表示当前 `DateTime` 加上指定的 `DateTime` 的 `DateTime` 对象。 |
| `AddDays(int)` | 返回表示当前 `DateTime` 加上指定天数的 `DateTime` 对象。 |
| `AddHours(int)` | 返回表示当前 `DateTime` 加上指定小时数的 `DateTime` 对象。 |
| `AddMinutes(int)` | 返回表示当前 `DateTime` 加上指定分钟数的 `DateTime` 对象。 |
| `AddSeconds(int)` | 返回表示当前 `DateTime` 加上指定秒数的 `DateTime` 对象。 |
| `AddMilliseconds(int)` | 返回表示当前 `DateTime` 加上指定毫秒数的 `DateTime` 对象。 |

# 知识点检查

- **9.9** 如果在不初始化的情况下创建 `DateTime` 对象，它将持有什么默认日期和时间？

- **9.10** 给出一个示例，实例化名为 `dt` 的 `DateTime` 对象，并初始化为 1965 年 3 月 22 日。

- **9.11** 给出一个示例，说明如何在消息框中以短日期格式显示名为 `dt` 的 `DateTime` 对象。

- **9.12** 给出一个示例，实例化名为 `dt` 的 `DateTime` 对象，并初始化为系统当前日期和时间。

- **9.13** 给出一个示例，实例化名为 `dt` 的 `DateTime` 对象，并初始化为系统当前日期但不包含时间。

- **9.14** 给定以下声明，表达式 `date1 > date2` 是真还是假？

```
DateTime date1 = new DateTime(1977, 3, 22);
DateTime date2 = new DateTime(1978, 3, 22);
```

**9.15** `TimeSpan` 对象包含什么内容？

**9.16** 在执行以下代码后，`date2` 对象中将存储什么日期？

```
DateTime date1 = new DateTime(1977, 3, 22);
TimeSpan ts = new TimeSpan(3, 0, 0, 0);
DateTime date2 = date1 + ts;
```

# 9.4 枚举类型 (Enumerated Types)

> 概念

枚举数据类型是一种由程序员人员定义的数据类型。它由预定义的常量（称为枚举员）组成，这些常量表示整数值。

有时，在程序中，你需要一种方法来表示无法以直接方式存储在内存中的值。例如，假设你正在编写一个处理星期（周日、周一、周二等）的程序，你需要某种方式在内存中表示每周的每一天。一种解决方案是让整数 0 到 6 代表每周的每一天；0 可以代表周日，1 可以代表周一，以此此类推。虽然这种方法可行，但它也有一些缺点。

例如，对于阅读代码的人来说，可能并不清楚值 0 到 6 代表每周的每一天。此外，你可能认为周日是每周的第一天，而另一个人可能认为周一是每周的第一天。当那个人看到值 0 时，他或她可能认为它代表的是周一。

处理此类数据的更好方法是创建一个枚举数据类型。枚举数据类型是可以自己创建的数据类型。当你创建一个枚举数据类型时，你指定一组属于该数据类型的符号值。以下是一个枚举数据类型的声明示例：

```
enum Day { Sunday, Monday, Tuesday, Wednesday,
Thursday, Friday, Saturday }
```

枚举数据类型的声明以关键字 `enum` 开始，后面跟着类型名称，然后是大括号内的标识符列表。示例声明创建了一个名为 `Day` 的枚举数据类型。括号内列出的标识符 Sunday、Monday、Tuesday、Wednesday、Thursday、Friday 和 Saturday 被**枚举员**。它们表示属于 `Day` 数据类型的值。

> 注意

注意枚举员没有包含在引号中；因此，它们不是字符串。枚举员必须是有效的 C# 标识符。

枚举员是表示整数值的常量。当你声明一个枚举类型时，枚举员会被分配整数值，从 0 开始。例如，在 `Day` 数据类型中，`Day.Sunday` 枚举员被分配值为 0，`Day.Monday` 枚举员被分配值为 1，以此此类推。

`enum` 声明出现在以下任何位置：

- 应用程序命名空间（namespace）外部

- 应用程序命名空间内部

- 类（class）内部

在本书中我们始终在编写结构声明的相同区域编写 enum 声明：在应用程序的命名空间内部，但在类内部。

一旦你在程序中创建了枚举数据类型，你就可以声明该类型的变量。例如，以下语句将 `workDay` 声明为 `Day` 类型的变量：

```
Day workDay;
```

我们称之为 **enum 变量**。因为 `workDay` 是 `Day` 类型的变量，所以我们可以赋值给它的值是 `Day` 类型的枚举员。例如，以下语句将值 `Day.Wednesday` 赋值给 `workDay` 变量：

```
workDay = Day.Wednesday;
```

注意，我们赋值的是 `Day.Wednesday` 而不仅仅是 `Wednesday`。`Day.Wednesday` 是 `Day` 类型中 `Wednesday` 枚举员的完全限定名称。你必须使用枚举员的完全限定名称，因为同一个枚举员可能出现在多个枚举类型中。这是另一个示例：

```
Day weekendDay = Day.Saturday;
```

该语句声明了一个名为 `weekendDay` 的 `Day` 变量，并用值 `Day.Saturday` 初始化它。

以下代码显示另一个示例。（假设应用程序表单有一个名为 `mondayRadioButton` 的单选按钮控件。）

```csharp
Day selectedDay;
if (mondayRadioButton.Checked)
{
    selectedDay = Day.Monday;
}
```

在代码中，第 1 行声明了一个名为 `selectedDay` 的 Day 变量。第 2 行的 if 语句判断 `mondayRadioButton` 控件是否被选中。如果是，第 4 行的语句将 `Day.Monday` 赋值给 `selectedDay` 变量。

你可以对 enum 变量和枚举员进行比较。以下代码显示了一个示例。（假设 `selectedDay` 是一个 Day 变量。）

```csharp
if (selectedDay == Day.Wednesday)
{
    MessageBox.Show("Halfway through the week!");
}
```

第 1 行的 if 语句判断 `selectedDay` 变量是否等于 `Day.Wednesday`。如果是，第 3 行显示一个消息框。

以下代码显示了如何在 switch 语句中测试 enum 变量。（假设 `selectedDay` 是一个 Day 变量。）

```csharp
switch (selectedDay)
{
    case Day.Sunday:
        MessageBox.Show("Rest.");
        break;
    case Day.Monday:
        MessageBox.Show("Back to work.");
        break;
    case Day.Tuesday:
        MessageBox.Show("Going.");
        break;
    case Day.Wednesday:
        MessageBox.Show("Halfway through the week!");
        break;
    case Day.Thursday:
        MessageBox.Show("Almost there.");
        break;
    case Day.Friday:
        MessageBox.Show("Just day.");
        break;
    case Day.Saturday:
        MessageBox.Show("Weekend today!");
        break;
}
```

## 使用枚举员或 enum 变量的 ToString 方法

枚举员和 enum 变量都有一个 `ToString` 方法。当你调用枚举员的 `ToString` 方法时，它返回枚举员的。例如，以下代码将显示 "Sunday"：

```csharp
MessageBox.Show(Day.Sunday.ToString());
```

当你调用 enum 变量的 `ToString` 方法时，它返回该变量所包含的名字。例如，以下代码将显示 "Thursday"：

```csharp
Day today = Day.Thursday;
MessageBox.Show(today.ToString());
```

当你对字符串和 enum 变量使用 `+` 运算符时，会调用 enum 变量的 `ToString` 方法。（对 int 使用 `+` 运算符时也会发生相同的情况。会调用 int 变量的 `ToString` 方法。）这是一个示例：

```csharp
Day today = Day.Thursday;
MessageBox.Show("Today is " + today);
```

# 教程 9-2：完成颜色应用程序

> 教程 9-2：完成颜色应用程序

ROY GIV 记忆法常用于帮助记住以下可见光谱的颜色：红、橙、黄、绿、蓝、靛和紫。在本教程中，你将完成颜色应用程序，该程序显示这些颜色。当你点击时，应用程序将显示颜色的名称。

应用程序的表单已经为你创建，如图 9-14 所示。颜色实际上是一组 Label 控件，它们的 BackColor 属性被设置为相应的颜色。

图 9-14 应用程序的表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fba28_1224_0.png)

**步骤 1**：启动 Visual Studio。打开学生示例中 Chap8 文件夹下的 Color Spectrum 项目。

**步骤 2**：在代码编辑器中打开 Form1 代码。编写 *Spectrum* 枚举类型的声明。确保将声明写在 `Color_Spectrum` 命名空间内部，如下所示。注意 *Spectrum* 类型中的枚举员表示你将要使用的颜色。

**步骤 3**：为 `DisplayColor` 方法编写注释和代码。注意第 28 行，此方法有一个 *Spectrum* 类型的参数变量。当我们调用此方法时，枚举员的名字将显示在 `colorLabel` 控件中。

**步骤 4**：接下来，为 Label 控件创建 Click 事件处理程序。切换回设计器（Designer）并双击 `redLabel` 控件。这将打开代码编辑器，你会看到一个名为 `redLabel_Click` 的空事件处理程序。通过输入语句完成事件处理程序。该语句调用 `DisplayColor` 方法，将 `Spectrum.Red` 作为参数传递。

**步骤 5：** 对其余的 Label 控制重复此过程，编写程序 9-4 所示的剩余 Click 事件处理程序。

**步骤 6：** 保存项目。然后，按下键盘上的 F5 键，或点击工具栏上的“开始调试”按钮 (*) 来编译并运行应用程序。当应用程序运行时，点击表单上显示的颜色以确认应用程序运行正常。完成后，点击“退出”按钮退出应用程序。

# 程序 9-4 色彩应用程序中 Form1 的完整代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Color_Spectrum
{
enum Spectrum
{
Red, Orange, Yellow, Green,
Blue, Indigo, Violet
}

public partial class Form1 : Form
{
public Form1()
{
InitializeComponent();
}
```
```csharp
}
// DisplayColor 方法
显示了
// 颜色的名称。
private void
DisplayColor(Spectrum color)
{
colorLabel.Text =
color.ToString();
}

private void
redLabel_Click(object sender, EventArgs
e)
{
DisplayColor(Spectrum.Red);
}

private void
orange_Label_Click(object sender,
EventArgs e)
{
DisplayColor(Spectrum.Orange);
}

private void
yellowLabel_Click(object sender,
EventArgs e)
{
DisplayColor(Spectrum.Yellow);
}

private void
```

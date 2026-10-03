
```cs
private void btnEquals_Click(object sender, EventArgs e)
{
    if (lblFirstValue.Text.Equals(String.Empty) ||
        lblMathFunction.Text.Equals(String.Empty) ||
        lblValue.Text.Equals(String.Empty) || lblValue.Text.Equals(noValue))
        return;

    var endsWithDecimalSign = lblFirstValue.Text.EndsWith(decimalSign);
    int length = Convert.ToInt32(lblFirstValue.Text.Length);
    if (endsWithDecimalSign)
        lblFirstValue.Text = lblFirstValue.Text.Substring(0, length - 1);

    length = Convert.ToInt32(lblValue.Text.Length);
    endsWithDecimalSign = lblValue.Text.EndsWith(decimalSign);
    if (endsWithDecimalSign)
        lblValue.Text = lblValue.Text.Substring(0, length - 1);

    var value1 = Convert.ToDouble(lblFirstValue.Text);
    var value2 = Convert.ToDouble(lblValue.Text);
    var mathFunction = lblMathFunction.Text;
    var result = 0d; // decimal = 0m, double = 0d
    if (mathFunction.Equals(plusSign))
        result = value1 + value2;
    else if (mathFunction.Equals(minusSign))
        result = value1 - value2;
    else if (mathFunction.Equals(divisionSign))
        result = value1 / value2;
    else if (mathFunction.Equals(multiplicationSign))
        result = value1 * value2;

    lblMathFunction.Text = String.Empty;
    lblFirstValue.Text = String.Empty;

    lblValue.Text = result.ToString("F3");
}
```

# 4. 循环与迭代

## 简介

迭代是多次执行代码块的一种方法；例如，它可以是一个数组或值的集合。本章中的示例将使用下面的数组来提供数据。

```cs
string[] animals = { "Cat", "Dog", "Bird", "Fish", "Lizard" };
```

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_132_0.png)

## For

`for` 循环是一种遍历一组值的方法，直到给定的表达式求值为假为止。一个 `for` 循环包含三个部分：循环的起始值、控制循环停止的表达式以及计数器。

`int i = 0` 是起始值，`i < 5` 是让循环停止的条件，`i++` 是迭代器。

```cs
for (int i = 0; i < 5; i++)
{
    lstResult.Add(animals[i]);
}
```

另一种动态确定循环何时停止的方法是使用数组的 `Length` 属性或集合的 `Count` 方法来确定它有多少项。

```cs
for (int i = 0; i < animals.Length; i++)
{
    lstResult.Add(animals[i]);
}
```

## Foreach

使用 `foreach` 循环，你不需要知道元素的数量，因为它会遍历数组中的所有元素，除非你使用 `break` 命令显式结束循环。

```cs
foreach (string animal in animals)
{
    if (animal.Equals("Fish")) break;
    lstResult.Add(animal);
}
```

## While

`while` 循环是在条件为真时执行代码块的循环。需要注意的是，如果初始条件为假，`while` 循环将不会执行。

```cs
int counter = 0;
while (!animals[counter].Equals("Bird"))
{
    lstResult.Add(animals[counter]);
    counter++;
}
```

## Do

`do` 循环与 `while` 循环相反，至少执行一次。

```cs
int counter = 0;
do
{
    lstResult.Add(animals[counter]);
    counter++;
} while (!animals[counter].Equals("Bird"));
```

## 练习：循环

在本次练习中，你将使用 `foreach` 循环将数组值添加到列表框中，当用户点击 **Move (For)** 或 **Move (While)** 按钮时，选中的值将移动到第二个列表框。

可以通过调用 `Items.Clear` 方法清除显示选中值的列表框。

```cs
1stSelected.Items.Clear();
```

# C# 初学者

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_135_0.png)

## 添加控件

1. 在 Visual Studio 中创建一个 Windows Forms 并命名为 Loops。
2. 在表单添加一个文本为 Cars 的标签。
3. 在标签下方添加一个列表框并命名为 `ItCars`。
4. 在列表下方添加一个文本为 Move (For) 的按钮并命名为 `btnMoveCars-For`。
5. 将列表的 `SelectionMode` 属性设置为 `MultiExtended`，以便在按住 Ctrl 或 Shift 键时选择多个项。
6. 在表单添加一个文本为 Selected Cars 的标签。
7. 在标签下方添加一个列表框并命名为 `ItSelectedCars`。
8. 在列表下方添加一个文本为 Move (While) 的按钮并命名为 `btnMove-CarsWhile`。

## 向 ItCars 列表框添加值

1. 双击表面区域（而不是控件）以添加 `Form_Load` 事件。
2. 定位 `Form1` 类的开头添加一个名为 `cars` 的字符串数组，其中包含汽车列表。

```cs
public partial class Form1 : Form
{
    string[] cars = {
        "Volvo", "Saab", "Corvette", "Mustang", "Honda" };
}
```

# C# 初学者

3. 找到 `Form_Load` 事件并使用 `for` 循环将 `cars` 数组中的项添加到 `LstCars` 列表框。使用 `cars` 数组的 `Length` 属性来确定所需的迭代次数。

```cs
for (int i = 0; i < cars.Length; i++)
{
    LstCars.Items.Add(cars[i]);
}
```

`Form_Load` 事件的完整代码如下：

```cs
private void Form1_Load(object sender, EventArgs e)
{
    for (int i = 0; i < cars.Length; i++)
    {
        LstSelectedCars.Items.Add(cars[i]);
    }
}
```

## 使用 foreach 循环将选中值移动到 LstSelectedCars 列表框

1. 在表单设计器中双击 `btnMoveCars` ，这将创建并带你进入按钮的 `Click` 事件。
2. 清空 `LstSelectedCars` 列表框。

```cs
SelectedCars.Items.Clear();
```

3. 使用 `foreach` 循环将选中项从 `LstCars` 列表框移动到 `LstSelectedCars` 列表框。你可以在列表的 `SelectedItems` 属性中找到选中项。

```cs
foreach (string car in LstSelectedCars.SelectedItems)
{
    LstSelectedCars.Items.Add(car);
}
```

4. 运行并在列表中选择一个或多辆汽车，点击列表框时按住 Ctrl 或 Shift 键选择多项。
5. 点击 Move (For) 按钮将选中项移动到 `LstSelectedCars` 列表。
6. 关闭应用程序。

# C# 初学者

`btnnMoveCarsFor_Click` 事件的完整代码如下：

```cs
private void btnnMoveCarsFor_Click(object sender, EventArgs e)
{
    lstSelectedCars.Items.Clear();
    foreach (string car in lstSelectedCars.SelectedItems)
    {
        lstSelectedCars.Items.Add(car);
    }
}
```

## 使用 while 循环将选中值移动到 lstSelectedCars 列表框

1. 在表单设计器中双击 `btnMoveWhile` 按钮，这将创建并带你进入按钮的 `Click` 事件。
2. 清空 `lstSelectedCars` 列表框。

```cs
lstSelectedCars.Items.Clear();
```

3. 使用 `while` 循环将选中项从 `lstCars` 列表框移动到 `lstSelectedCars` 列表框。你可以在列表框的 `SelectedItems` 属性中找到选中项。

```cs
int index = 0;
while (index < lstCars.SelectedItems.Count)
{
    lstSelectedCars.Items.Add(lstCars.SelectedItems[index]);
    index++;
}
```

4. 运行并在列表中选择一个或多辆汽车，点击列表框时按住 Ctrl 或 Shift 键选择多项。
5. 点击 Move (While) 按钮将选中项移动到 `lstSelectedCars` 列表。
6. 关闭应用程序。

`btnMoveCarsWhile_Click` 事件的完整代码如下：

```cs
private void btnMoveCarsWhile_Click(object sender, EventArgs e)
{
    lstSelectedCars.Items.Clear();
    int index = 0;
    while (index < lstSelectedCars.SelectedItems.Count)
    {
        lstSelectedCars.Items.Add(lstCars.SelectedItems[index]);
        index++;
    }
}
```

# 5. 调试

## 简介

调试是你必须采用并学习的技能，用于监控程序流中的运行情况，它通常用于发现和修复错误。在特定点进行调试时，你可以通过在代码中插入所谓的“断点”来查看变量和控制属性的当前值。当命中断点时，执行将停止，这样你就可以切换到开发环境并弄清楚应用程序在该阶段发生了什么。

调试时你可以利用许多窗口，你将在这里熟悉其中一些。

在调试模式下，命中断点后，你可以逐步执行代码，这简化了查找需要修复的问题所在的任务。要调试应用程序，它必须处于 Debug 模式；你可以从主菜单栏下方的标准工具栏设置该模式。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_140_0.png)

## 断点和窗口

如果你大致知道想要调试的问题所在，你可以在想要停止执行的行上放置断点。这允许你使用可用于调试的各种窗口和工具。

要设置或删除断点，请点击所需的代码行并从 Debug 菜单中选择“切换断点”、按下键盘上的 `F9` 键，或点击目标代码行左侧的灰色区域。断点显示为代码窗口左侧灰色区域上的实心红圈，代码背景将变为深红色。

# C# 初学者

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_141_0.png)

```cs
public Form1()
{
    InitializeComponent();
}
```

要以调试模式启动应用程序，请按键盘上的 `F5` 键，在主菜单中选择调试-开始调试，或点击标准工具栏上的播放按钮。如果你想在禁用调试的情况下启动应用程序，可以按键盘上的 `Ctrl+F5` 或在主菜单中选择调试-无调试启动。

当执行遇到断点时，执行将在该断点处停止，使你能够使用下表描述按钮或键盘键逐步执行代码。注意，设置断点的代码行将高亮显示；这种高亮效果将在逐步执行时显示下一行执行的行。逐步执行代码时，使用 `F11` 逐行执行代码，并在方法被调用时进入方法内部；并使用 `F10` 逐行执行，但在方法被调用时完整执行方法，而不进入方法内部。

# C# 初学者

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_141_1.png)

```cs
public Form1()
{
    InitializeComponent();
}
```

| 调试菜单 | 键盘键 | 描述 |
| :--- | :--- | :--- |
| 开始调试 | `F5` | 启动应用程序 |
| 全部中断 | `Ctrl+Break` | 中断应用程序 |
| 停止调试 | `Ctrl+F5` | 停止调试 |
| 重启 | `Ctrl+Shift+F5` | 重启应用程序 |
| 单步进入 | `F11` | 进入方法 |
| 单步跳过 | `F10` | 执行方法而不进入 |
| 单步跳出 | `Shift+F11` | 退出方法 |

（注：原文后续部分存在大量重复描述，此处已根据核心内容进行整合翻译）

6. 打开“监视”窗口并为其添加一个变量，在单步执行代码时观察窗口中的变化。
7. 打开“本地”窗口，在单步执行代码时观察窗口中的变化。
8. 打开“自动显示”窗口，在单步执行代码时观察窗口中的变化。
9. 关闭应用程序。

## 练习：调试订单表单

在此练习中，你将打开之前创建的订单表单项目。你希望在点击产品单元控件中的向上/向下按钮时，向“输出”窗口打印调试信息。请在一行中打印产品名称、价格和行总额，并在不同的列中打印这些值。为这些值添加描述性文本（见下图）。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_144_0.png)
![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_144_1.png)

1. 打开你在之前的练习中创建的订单表单。
2. 找到 `numUnits1_ValueChanged` 事件，当点击 `NumericUpDown` 控件中的向上/向下按钮时会触发该事件。
3. 在事件的最后一行代码之后添加代码：

```cs
Debug.WriteLine(String.Format("{0}\tPrice: {1}\tUnits: {2}\tlineTotal: {3}", txtProduct1.Text, price, units, lineTotal));
```

4. 对其他 `ValueChanged` 事件重复步骤 2-3。
5. 打开“输出”窗口。
6. 运行应用程序，向表单添加数据并点击向上/向下箭头。点击按钮时，数据应写入输出窗口（见上图）。
7. 关闭应用程序。

# 6. 简单类型

## 引言

简单类型是用户定义的类型，你可以使用 `struct`（结构体）或 `enum`（枚举）关键字来创建自己的数据类型。在某些情况下，如果不涉及多个变量，单个值不足以表示你正在处理的数据；与其声明多个变量，你可以将它们封装在一个赋予适当名称的 `struct` 块中。从结构体声明的变量可以用于访问存储在其中的多个相关值。

枚举基本上是一组相互相关的常量值列表。

### 枚举

如果你想创建一个具有固定值集的变量，例如星期几的名称或月份，那么 `enum` 是一个很好的选择。枚举始终在名称级别或类级别声明。

虽然理论上你可以使用多个文本或数值变量来实现类似的结果，但不建议这样做，因为代码将难以维护得多。使用枚举有几个优点：

- **提高可管理性**
  使用枚举时遇到无效参数和拼写错误的名称概率较低。枚举由于有一组固定的值，因此限制了可以使用哪些值。
- **提高开发者体验**
  枚举中的可用值将通过 IntelliSense 显示。
- **提高代码可读性**
  使用枚举使代码更容易阅读和理解。
- **提高可重用性**
  你可以轻松在不同场景中重用同一个枚举。

# C# 初学者教程

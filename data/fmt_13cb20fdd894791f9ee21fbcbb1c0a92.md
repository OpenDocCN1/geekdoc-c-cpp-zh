
```csharp
private void firstButtonClick_Click(object sender, EventArgs e) {
    // 声明一个字符串变量。
    string myName;

    // 将 nameTextBox 的 Text 属性
    // 赋值给 myName 变量。
    myName = nameTextBox.Text;
}

private void secondButtonClick_Click(object sender, EventArgs e) {
    // 将 myName 变量赋值给 outputLabel
    outputLabel.Text = myName; // ERROR!
}
```

# 处理数据

这条语句位于 `secondButton_Click` 事件处理程序中，尝试将 `myname` 变量赋值给 `outputLabel` 控件的 `Text` 属性。这条语句无法运行，因为 `myname` 变量是 `firstButton_Click` 事件处理程序的局部变量，`secondButton_Click` 中的语句无法访问它。

# 变量的作用域

程序员使用“作用域”一词来描述程序中可以访问变量的部分。变量仅对其作用域内的语句可见。

局部变量的作用域从变量声明开始，到其声明的方法结束结束。正如你在上一个示例中看到的，局部变量无法被方法外部的语句访问。此外，局部变量无法被方法内部但在变量声明之前的代码访问。

### 变量的生命周期

变量的生命周期是程序执行期间变量存在内存中的时间。当声明变量的方法开始执行时，局部变量在内存中创建。当方法结束时，所有方法的局部变量都会被销毁。因此，局部变量的生命周期是声明它的方法执行期间。

### 重名变量

你不能在同一个作用域内声明两个同名的变量。例如，如果你在事件处理程序中声明了一个名为 `productDescription` 的变量，你不能在同一个事件处理程序中声明另一个同名的变量。但是，你可以在不同的方法中使用同名的变量。

# 赋值兼容性

只有当值与数据类型兼容时，你才能给变量赋值。只有字符串与字符串数据类型兼容，因此在以下代码示例中的所有赋值：

```
// 声明并初始化一个字符串变量。
string productDescription = "Chocolate Truffle";
// 声明另一个字符串变量。
string myFavoriteProduct;

// 给字符串变量赋值。
myFavoriteProduct = productDescription;

// 将 TextBox 的值赋值给字符串变量。
productDescription = userInputBox.Text;
```

以下注释解释了这些代码行：

- 在第 2 行中，我们用字符串字面量初始化了一个字符串变量。这是可以的，因为字符串字面量与字符串变量是兼容。

- 在第 8 行中，我们将一个变量赋值给另一个字符串变量。这样做的原因显而易见，字符串变量与其他字符串变量是兼容。

# 处理数据

- 假设应用程序有一个名为 `userInputTextBox` 的 TextBox 控件。在第 11 行中，我们将 TextBox 控件的 `Text` 属性值赋值给字符串变量。这是可以的，因为控件的 `Text` 属性值始终是一个字符串。

然而，以下代码将无法运行，因为它尝试将一个非字符串值赋值给字符串变量。

```
// 声明一个字符串变量。
string employeeID;

// 给变量赋值。这可行吗？
employeeID = 125;  <- ERROR!
```

在第 5 行中，我们尝试将数字 125 赋值给字符串变量。数字与字符串变量不具有赋值性，因此这条语句在代码编译时会导致错误。

> 注意：虽然你可以存储字符串 `"125"`，但你不能存储数字 125。

# 变量一次只保存一个值

变量在程序运行时可以持有不同的值，但它们一次只能持有一个值。当你给变量赋值时，该值将替换变量中原有的值。例如，查看以下代码：

```
// 声明一个字符串变量。
string productDescription;

// 给变量赋值。
productDescription = "Large-Roast Coffee";

// 显示变量的值。
MessageBox.Show(productDescription);

// 给变量赋一个不同的值。
productDescription = "Chocolate Truffle";

// 显示变量的值。
MessageBox.Show(productDescription);
```

以下注释解释了我们做了什么：

- 第 2 行声明了一个名为 `productDescription` 的字符串变量。

- 第 5 行将 `"Large-Roast Coffee"` 赋值给 `productDescription` 变量。

- 第 8 行在消息框中显示 `productDescription` 变量的值。（消息框将显示 Large-Roast Coffee。）

- 第 11 行将 `"Chocolate Truffle"` 赋值给 `productDescription` 变量。执行此语句后，`productDescription` 变量将持有 `"Chocolate Truffle"`。

- 第 14 行在消息框中显示 `productDescription` 变量的值。（消息框将显示 Chocolate Truffle。）

# 处理数据

代码示例说明了变量的两个重要特性：

- 变量一次只能持有一个值。

- 当你在变量中存储值时，它将替换原来的值。

教程 1 为你提供了使用变量练习。你将创建一个使用 TextBox 控件存储这些值的应用程序，并在操作中使用这些变量。

#### 教程 1：出生日期应用程序

在本教程中，你将创建一个应用程序，允许用户输入有关出生日的信息：

* 星期（周一、周二等）

* 月份（一月、二月等）

* 月的日期

* 年份

图 9 显示了你的应用程序表单，并带有所有控件的名称。当应用程序运行时，用户将每个数据输入到单独 TextBox 中。当用户点击 Show Date 按钮时，应用程序会将 TextBox 内容拼接成类似“Friday, June 1, 1990”的字符串。该字符串显示在 `dateOutputLabel` 中。当用户点击 Clear 按钮时，TextBox 和 `dateOutputLabel` 的内容将被清除。Exit 按钮将关闭应用程序。

图 9 出生日期字符串

![](img/9467d25da5679b16515c9401daaae36c_134_0.png)

步骤 1：启动 Visual Studio（或 Visual # Express）并开始创建一个名为 Birth Date 的 Windows Forms 应用程序。

步骤 2：如图 9 所示设置应用程序表单，注意表单的 Text 属性设置为 Birth Date String。图中显示了控件的名称。当你在表单上放置每个控件时，请参考表 1 的相关属性设置。

步骤 3：一旦设置好表单及其控件，你就可以为按钮控件创建 Click 事件处理程序。在本文教程结束时，程序 1 显示了表单的完整代码。将被指示参考程序 1

## 表 1 控制属性设置

| 控制名称 | 控制类型 | 属性设置 |
| --- | --- | --- |
| dayOfWeekPromptLabel | Label | Text: 输入星期 |
| monthPromptLabel | Label | Text: 输入月份名称 |
| dayOfMonthPromptLabel | Label | Text: 输入月份的数字 |
| yearPromptLabel | Label | Text: 输入年份 |
| dayOfWeekTextBox | TextBox | 属性未更改 |
| monthTextBox | TextBox | 属性未更改 |
| dayOfMonthTextBox | TextBox | 属性未更改 |
| yearTextBox | TextBox | 属性未更改 |
| dateOutputLabel | Label | AutoSize: False, BorderStyle: FixedSingle, Text: (Text 属性的内容已清除。), TextAlign: MiddleCenter |
| showDateButton | Button | Text: 显示日期 |
| cancelButton | Button | Text: 清除 |
| exitButton | Button | Text: 退出 |

正如我们使用事件处理程序一样。（请记住，程序 1 中的数字不是程序的一部分。它们仅供参考。）

在设计器中，双击 `showDateButton` 。在代码编辑器中，你会看到一个名为 `showDateButton_Click` 的空事件处理程序。通过在程序 1 的第 21–31 行中输入代码，完成 `showDateButton_Click` 事件处理程序。

让我们仔细查看代码：

第 22 行：此语句声明了一个名为 `output` 的字符串变量。

第 25–28 行：这些行实际上是一条很长的语句，被分成了多行。该语句将 `TextBox` 控制的属性连接起来，并带有适当的逗号和空格，创建一个日期字符串。生成的字符串被赋值给 `output` 变量。

例如，用户输入了以下内容：

- 在 `dayOfWeekTextBox` 控制中输入 Friday（周五）。

- 在 `monthTextBox` 控制中输入 June。

- 在 `dayOfMonthTextBox` 控制中输入 1。

- 在 `yearTextBox` 控制中输入 1990。

此语句中的拼接产生了字符串 `"June 1, 1990"`；它被赋值给 `output` 变量。

第 31 行：此语句将 `output` 赋值给 `dateOutputLabel` 控制的 `Text` 属性。当此语句执行时，`output` 变量的内容将显示在 `dateOutputLabel` 控制中。

步骤 4：切换回设计器视图并双击 `cancelButton` 控制。在代码编辑器中，你会看到一个名为 `clearButton_click` 的空事件处理程序。通过输入程序 1 中第 36–43 行所示的代码，完成 `clearButton_click` 事件处理程序。

让我们看一眼代码：

第 37–40 行：每个语句都将空字符串 (`""`) 赋值给其中一个 `TextBox` 控制的 `Text` 属性。当这些语句执行完毕后，`TextBox` 控制将显示为空白。

第 43 行：此语句将空字符串 (`""`) 赋值给 `dateoutputlabel` 的 `Text` 属性。在语句执行执行后，标签将显示为空白。

步骤 5：切换到设计器视图并双击 `exitButton` 控制。在代码编辑器中，你会看到一个名为 `exitButton_click` 的事件处理程序。通过输入程序 1 中第 48–49 行所示的代码，完成 `clearButton_click`（此处原文可能有误，应为 exitButton_click）事件处理程序。

步骤 6：保存项目。然后，按下键盘上的 F5 键，或点击工具栏上的调试按钮 (()) 来编译并运行应用程序。表单将如图 10 左侧所示所示出现。通过向 `TextBoxes` 中输入值并点击“Show Date”按钮来测试应用程序。日期应该显示出来，类似于图中右侧所示。点击“Clear”按钮，或点击“Exit”按钮，表单应该关闭。

**图 10** 生日字符串应用程序

![](img/9467d25da5679b16515c9401daaae36c_136c_1)

### 数据处理

7 对于以下每一项，确定其数据类型应该是整数（integer）、字符串（string）还是实数（real number）。

- a. 宠物名称

- b. 销售税

- c. 邮寄地址

- d. 游戏分数

8 说明下列哪些是合法的变量名。如果不是，请解释原因。

- a. pay_Rate

- b. speed of sound

- c. totalCost

- d. 2ndPlaceName

9 执行以下语句后，`message` 变量将存储什么内容？

```
string message = "He" + "11" + "o!";
```

10 为点击事件处理程序声明的数据类型是什么？

11 假设变量 `greeting` 尚未赋值，以下语句的结果将是什么？

`MessageBox.Show(greeting);`

12 下述语句会导致错误吗？为什么或为什么不会。

`string luckyNumber = 7;`

13 为变量 `name`、`city` 和 `state` 编写一条单一的声明语句。

## 数值型数据类型与变量

> 概念：如果你需要在变量中存储一个数字并在数学运算中使用该数字，则该变量必须是数值类型。请根据你需要存储的数字类型选择合适的数值数据类型。

在上一节中，你学习了关于字符串变量的内容。字符串类型的变量可以用于存储文本，但它们不能为了执行数学运算而存储数值数据。如果你需要存储数字并对其进行数学运算，则必须使用数值数据类型。

C# 语言提供了几种基本数据类型。C# 提供的许多数据类型用于超出本文范围的特殊用途。当涉及数值数据时，你通常会使用表 2 中描述的三数值数据类型。

以下是声明各种数据类型变量的示例：

```
int speed;
double distance;
decimal grossPay;
```

第一条语句声明了一个名为 `speed` 的 `int` 变量。第二个示例声明了一个名为 `distance` 的 `double` 变量。第三条语句声明了一个名为 `grossPay` 的 `decimal` 变量。

## 表 2 最常用的基本数值类型

| 数据类型 | 说明 |
| --- | --- |
| int | `int` 数据类型的变量只能包含数字。例如，一个 `int` 变量可以存储值如 42、0 和 -99。`int` 变量不能包含带有小数部分的数字，如 22.1 或 -4.9。 |
| double | `int` 类型是存储整数的主要数据类型。在本文中，我们需要存储和处理整数时使用它。`int` 变量使用 32 位内存，可以存储 -2,147,483,648 到 2,147,483,647 范围内的整数。`double` 数据类型的变量可以存储实数，如 3.5、-87.5 或 3.0。存储在 `double` 变量中的数字会被保留到 15 位精度。我们使用 `double` 类型来存储任何可能带有小数部分的数字。`double` 类型对于存储极大或极小的数字特别有用。在内存中，`double` 变量使用 64 位内存。它以程序员称为*浮点表示法*（floating-point notation）的格式存储。`double` 数据类型的变量可以存储 ±5.0 × 10⁻³²⁴ 到 ±1.7 × 10³⁰⁸ 范围内的数字。 |
| decimal | `decimal` 数据类型的变量可以存储比 `double` 类型精度更高的实数。存储在 `decimal` 变量中的数字会被保留到 28 位精度。由于 `decimal` 变量存储的是高精度的实数，它们最常用于金融应用程序。在本文中，我们存储金额时通常使用 `decimal` 类型。在内存中，`decimal` 变量使用 128 位内存。它以程序员称为*小数表示法*（decimal notation）的格式存储。`decimal` 数据类型的变量可以存储 ±1.0 × 10⁻²⁸ 范围内的数字。 |

## 数值字面量

字面量（Literal）是写入程序代码中的数据。当你在编写程序代码时知道想在变量中存储一个特定值时，可以将该值赋值为字面量。

数值字面量是写入程序代码中的数字。例如，以下语句声明了一个名为 `hoursWorked` 的 `int` 变量，并将其初始化为 40：

```
int hoursWorked = 40;
```

在这条语句中，数字 40 是一个数值字面量。下面显示了另一个示例：

```
double temperature = 87.6;
```

这条语句声明了一个名为 `temperature` 的 `double` 变量，并将其初始化为 87.6。数字 87.6 是一个数值字面量。

### 数据处理

当你在程序代码中编写数值字面量时，该字面量会被分配一个数据类型。在 C# 中，如果数值字面量是一个整数（没有写小数点）且它在 `int` 的范围内，则它被视为 `int`。如果它带有小数点，则被视为 `double`。如果它带有 `m` 后缀，则被视为 `decimal`。如果它带有 `f` 后缀，则被视为 `float`。

# 处理数据

答案是肯定的，有一种方法。你可以使用强制转换运算符将值从一种数值数据类型显式转换为另一种数值数据类型，即使这种转换可能会导致数据丢失。强制转换运算符所需的所需的类型名称，写在括号内，并放置在你想要转换的值左侧。以下代码示例演示了：

```
// 定义一个 int 变量。
int wholeNumber;

// 定义一个 double 变量。
double realNumber = 3.0;

// 将 double 赋值给 int。
wholeNumber = (int)realNumber;
```

以下点描述了该代码：

- 第 2 行声明了一个名为 wholeNumber 的 int 变量。

- 第 5 行声明了一个名为 realNumber 的 double 变量，并用值 3 初始化。

- 第 8 行使用强制转换运算符将 realNumber 的值转换为 int，并将转换后的值赋值给 wholeNumber。在此语句执行后，wholeNumber 变量被赋值为值 3。

表 3 显示了涉及不同类型强制转换运算符的其他代码示例。

# 表 3 强制转换运算符使用的示例

| 代码示例 | 描述 |
|---|---|

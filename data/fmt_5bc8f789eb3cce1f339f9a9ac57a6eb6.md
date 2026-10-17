
假设一家零售企业计划进行批发销售活动，所有商品的价格都将按指定的百分比降低。在本教程中，你将创建一个应用程序来计算减去折扣后的商品销售价格。以下是伪代码表示的算法：

- 1. 获取商品的原始价格。
- 2. 获取折扣百分比。（例如，输入 20 表示 20%。）
- 3. 将百分比除以 100，将小数点移动到正确的位置。
- 4. 将百分比乘以原始价格。这就是折扣金额。
- 5. 从原始价格中减去折扣。这就是销售价格。
- 6. 显示销售价格。

图 3-20 显示了应用程序的表单以及控件的名称。当应用程序运行时，用户在 `originalPriceTextBox` 中输入原始价格，并在 `discountTextBox` 控件中输入折扣百分比。当用户点击 `calculateButton` 时，应用程序计算商品的销售价格并在 `salePriceLabel` 控件中显示结果。`exitButton` 控制应用程序的表单。

## 图 3-20 销售价格计算器表单

![](img/8a88e1d8c69a687988c05f162ce3cac_170_0.png)

## 3.6 使用 ToString 方法格式化数字

**步骤 1:** 启动 Visual Studio（或 Visual Studio Express）并开始创建一个名为“Sale Price Calculator”的 Windows Forms 应用程序。

**步骤 2:** 如图 3-20 所示设置应用程序的表单。注意表单的 `Text` 属性已设置为“Sale Price Calculator”。控件的名称如图所示。在将每个控件放置在表单上时，请参考表 3-13 的相关属性设置。

## 表 3-13 控件属性设置

| 控件名称 | 控件类型 | 属性设置 |
|---|---|---|
| `originalPriceLabel` | Label | Text: 输入商品的原始价格: |
| `discountPercentageLabel` | Label | Text: 输入折扣百分比: |
| `outputDescriptionLabel` | Label | Text: 销售价格: |
| `originalPriceTextBox` | TextBox | 属性未更改 |
| `discountPercentageTextBox` | TextBox | 属性未更改 |
| `salePriceLabel` | Label | AutoSize: False BorderStyle: Fixed (Text 属性的内容已清除。) TextAlign: 居中中间 |
| `calculateButton` | Button | Text: 计算销售价格 |
| `exitButton` | Button | Text: 退出 |

**步骤 3:** 一旦你设置好了带有控件的表单，你就可以点击 Button 控件的事件处理程序。在本教程结束时，程序 3-3 将显示表单的完整代码。在编写处理程序时，你会被指示要求参考程序 3-3。（记住，程序 3-3 中的数字不是程序的一部分。它们仅供参考。）

在设计器（Designer）中，双击 `calculateButton` 控件。这将打开代码编辑器，你将看到一个名为 `calculateButton_Click` 的事件处理程序。通过输入程序 3-5 中第 22-43 行所示的代码来完成 `calculateButton_click` 处理程序。

让我们来看代码：

**第 22 行:** 该语句声明了一个 `decimal` 型变量 `originalPrice`。该变量将存储商品的原始价格。

**第 23 行:** 该语句声明了一个 `decimal` 型变量 `discountPercentage`。该变量将存储折扣百分比。

**第 24 行:** 该语句声明了一个 `decimal` 型变量 `discountAmount`。该变量将存储从商品原始价格中减去的折扣金额。该金额将通过计算。

**第 25 行:** 该语句声明了一个 `decimal` 型变量 `salePrice`。该变量将存储商品的销售价格。该金额将通过计算。

**第 28 行:** 该语句将 `originalPriceTextBox` 控件的 `Text` 属性转换为 `decimal`，并将结果赋值给 `originalPrice` 变量。

第 31 行: 该语句将 `discountPercentageTextBox` 控件的 `Text` 属性转换为 `decimal`，并将结果赋值给 `discountPercentage` 变量。

第 34 行: 该语句将 `discountPercentage` 除以 100，并将结果存回 `discountPercentage` 中。这会将 `discountPercentage` 变量的小数点向左移动两位。

第 37 行: 该语句计算折扣金额。它将 `originalPrice` 乘以 `discountPercentage`并将结果赋值给 `discountAmount`。

第 40 行: 该语句计算商品的销售价格。它从 `originalPrice` 变量中减去 `discountAmount`并将结果赋值给 `salePrice`。

第 43 行: 该语句显示商品的销售价格。它将 `salePrice` 转换为字符串并将结果赋值给 `salePriceLabel` 的 `Text` 属性。注意，格式字符串 "c" 被传递给 `salePrice.ToString` 方法。

**步骤 4:** 将视图切换回设计器并双击 `exitButton`。在编辑器中，你将看到一个名为 `exitButton_Click` 的事件处理程序。

**步骤 5:** 保存项目。然后，按键盘上的 `F5` 键或点击工具栏上的调试来运行应用程序。通过在 TextBoxes 中输入值并点击“计算”来测试应用程序。显示销售价格，类似于图 3-21。点击“退出”按钮，表单关闭。

## 图 3-21 销售价格计算器应用程序

![](img/8a88e1d8c69a687988c05f162cecac_172_0.png)

## 程序 3-3 销售价格应用程序的完整表单

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

namespace Sale_Calculator
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void calculateButtonClick(object sender, EventArgs e)
        {
            decimal originalPrice; // 商品的原始价格
            decimal discountPercentage; // 折扣百分比
            decimal discountAmount; // 折扣金额
            decimal salePrice; // 商品的销售价格

            // 获取商品的原始价格。
            originalPrice = decimal.Parse(originalPriceTextBox.Text);

            // 获取折扣百分比。
            discountPercentage = decimal.Parse(discountPercentageTextBox.Text);

            // 将百分比的小数点左移两位。
            discountPercentage = discountPercentage / 100;

            // 计算折扣金额。
            discountAmount = originalPrice * discountPercentage;

            // 计算销售价格。
            salePrice = originalPrice - discountAmount;

            // 显示销售价格。
            salePriceLabel.Text = salePrice.ToString("c");
        }

        private void exitButton_Click(object sender, EventArgs e)
        {
            // 关闭表单。
            this.Close();
        }
    }
}
```

3.30 编写一条编程语句，使用货币格式在消息框中显示名为 `salary` 的变量的字符串值。

3.31 以下变量名指示了它们所存储的数据。对于每个变量，请格式化你认为最合适的字符串。

- a. `discountPercentage`
- b. `atomicWeight`
- c. `retailPrice`
- d. `quantityPurchased`
- e. `degreesFahrenheit`

# 第3章

## 数据处理

3.32 当执行以下代码段时，消息框中将显示什么值？

```csharp
double apples = 12.0;

MessageBox.Show(apples.ToString("n0"));
```

3.33 检查整数变量并使用 `d` 或 `D` 格式字符串指定前导零的个数 `wxyz`。

```csharp
int valueA = 234, valueB = 56, valueC = 7, valueD = 89123;
```

3.34 编写一条程序语句，使用名为 `millimeters` 的变量的 `ToString` 方法，使其能够以定点科学格式显示小数点后四位数的精度。

## 简单异常处理

> 概念：异常是程序在运行时发生的意外错误。如果程序没有处理异常，程序将异常停止。

异常是程序在运行时发生的意外错误，如果该错误没有通过通常由程序员控制的各种情况得到妥善处理，就会导致程序停止。例如，假设用户在 `TextBox` 中输入了一个值，且该值预计应是一个数字。程序使用其中一个 `Parse` 方法将字符串的 `Text` 转换为数值数据类型，但该字符串包含无效字符且无法转换。`Parse` 方法无法继续执行，因此发生了异常。（使用专业术语来说，当发生意外错误且方法无法继续操作时，我们称该方法“抛出”异常。）

让我们来看一个例子。如果你打开了教程 3-2 中的“燃油经济”项目，然后点击“启动调试”按钮或按 `F5` 运行应用程序，在行驶英里处输入数字，然后在燃油量处输入非数字字符序列。图 3-22 显示了一个示例，用户输入了 `wxyz`，然后点击“计算 MPG”。由于你为燃油量输入的字符串无法转换为 `double`，因此抛出了异常。应用程序停止运行，Visual Studio 进入到一种被称为“断点模式”的特殊模式。显示如图 3-23 所示的窗口，异常发生时正在执行的代码行是

# 图 3-22 输入的燃油量无效

![](img/8a88e1d8c69a687988c05f162ce32cac_174_0.png)

## 3.7 简单异常处理

# 图 3-23 异常报告并赋值给

```csharp
// 获取燃油量并赋值给
// gallons 变量；
gallons = double.Parse(gallons);
// 捕获异常
FormatException ex = new FormatException();
// 在 UI 中显示错误
Console.WriteLine(ex.Message);
```

![](img/8a88e1d8c69a687988c05f162ce32cac_175_0.png)

图 3-23 中的异常窗口显示了大量信息，但如果你查看标题栏下方的行，你会看到“输入格式不正确”的消息。那里有关于导致异常发生的事件描述。要退出断点模式，请点击“停止调试”按钮 ()，或按 `Shift+F5`。Visual Studio 将返回到正常模式。

## 异常

C# 与大多数现代编程语言一样，允许你编写在异常被抛出时做出响应的代码，以防止程序突然崩溃。这种代码被称为异常处理器，使用 `try-catch` 语句编写。有多种方法编写 `try-catch` 语句，但以下通用格式是最简单的：

```csharp
try {
    statement;
    statement;
    etc.
}
catch {
    statement;
    statement;
    etc.
}
```

第一个关键字出现后，紧接着是一组在大括号内的一个或多个语句。这组语句被称为 `try` 块。`try` 块中的一个或多个语句都可能抛出异常。

在 `try` 块之后会出现 `catch` 块。`catch` 子句后面是一组包含在大括号内的一个或多个语句。这组语句被称为 `catch` 块。

当执行 `try-catch` 语句时，`try` 块中的语句按照它们出现的顺序执行。如果 `try` 块中的语句抛出了异常，程序将立即跳转到 `catch` 子句并执行 `catch` 子句。

第 26 行的语句只是将异常对象的 `Message` 属性传递给 `MessageBox.show` 方法。这会导致在消息框中显示默认错误消息。3-25 显示了当用户为 `milesTextBox` 或 `gallonsTextBox` 输入无效输入后显示的消息示例。

**图 3-25** 显示异常默认错误消息控制的消息框。

![](img/8a88e1d8c69a687988c05f162ce32cac_178_0.png)

在教程 3-4 中，你将创建一个使用 `try-catch` 语句的应用程序，用于处理用户向 TextBox 控制输入无效数据时抛出的异常。

# 教程 3-4:

## 创建带有异常处理的应用程序

确定一组值的平均值是一个简单的计算：将所有值相加，然后和除以值的个数。虽然这是一个直接计算，但在编写计算平均值的程序时很容易出错。例如，假设变量 `a`、`b` 和 `c` 分别持有一个值，我们想要计算这些值的平均值。如果我们不粗心，可能会写出类似下面的语句来执行计算：

```
average = a + b + c / 3.0;
```

你能看出这条语句中的错误吗？当它执行时，将先进行除法。`b` 的值会被除以 3，然后结果加到 `a + b` 上。这不是计算平均值的正确方法。为了纠正这个错误，我们需要在 `a + b + c` 周围使用括号，如下：

```
average = (a + b + c) / 3.0;
```

在本教程中，你将创建一个计算三次测试平均值的应用程序。图 3-26 显示了该应用程序的表单，以及所有控件的名称。

**图 3-26** 测试平均值表单

![](img/8a88e1d8c69a687988c05f162ce32cac_178_1.png)

## 3.7 简单异常处理

应用程序运行时，用户将测试分输入 TextBox TextBox中。当用户点击 `calculateButton` 控制时，应用程序将计算平均测试分并将结果显示在 `averageLabel` 控制中。`clearButton` 控制将清除 TextBoxes 的内容和 `averageLabel` 控制。`exitButton` 控制应用程序的表单。

- 步骤 1：启动 Visual Studio（或 Visual Studio Express）并开始创建一个名为 `Test Average` 的新 Windows Forms Application。
- 步骤 2：如图 3-26 所示设置应用程序的表单。注意表单的属性设置为 `Test Average`。控件的名称在图中。当你将每个控件放在表单上时，请参考表 3-14 进行相关的属性设置。

## 表 3-14 控件属性设置

| 控件名称 | 控件类型 | 属性设置 |
| :--- | :--- | :--- |
| `testPromptLabel` | Label | Text: 1: |
| `testPromptLabel` | Label | Text: 2: |
| `testPromptLabel` | Label | Text: 3: |
| `outputDescriptionLabel` | Label | Text: Average Test Score: |
| `testTextBox` | TextBox | 属性未更改 |
| `testTextBox` | TextBox | 属性未更改 |
| `testTextBox` | TextBox | 属性未更改 |
| `averageLabel` | Label | AutoSize: False BorderStyle:FixedSingle Text: (Text 属性的内容已清除。) TextAlign:MiddleCenter |
| `calculateButton` | Button | Text: Calculate Sale |
| `clearButton` | Button | Text: Clear |
| `exitButton` | Button | Text: Exit |

- 步骤 3：一旦你设置好了带有控件的表单，就可以为 Button 控件创建 `Click` 事件处理程序。在教程结束时，Program 3-4 显示了表单的完整代码。在编写事件处理程序时，将被指示参考 Program 3-4。（记住，Program 3-4 中的行号不是程序的一部分。它们仅供参考。）

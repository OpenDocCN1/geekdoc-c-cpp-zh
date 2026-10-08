
- `yearsOnJob`，一个用于存储当前工作年限的 `int` 变量。

**第 32-33 行：** 这些语句从文本控件获取薪水和当前工作年限，并将这些值赋值给 `salary` 和 `yearsOnJob` 变量。

**第 36 行：** 如果此语句判断 `salary` 是否大于或等于 `MINIMUM_SALARY`，则程序继续到第 38 行。否则，程序跳转到第 50 行的 `else` 子句，并在第 53-54 行将字符串“未达到最低薪水要求”赋值给 `decisionLabel` 的 `Text` 属性。

**第 38 行：** 如果此语句判断 `yearsOnJob` 是否大于或等于 `MINIMUM_YEARS_ON`。如果是，继续到第 41 行，将字符串“您符合贷款”赋值给 `decisionLabel.Text`。否则，程序跳转到第 43 行的 `else` 子句，并在第 46-47 行将字符串“当前工作年限不符”赋值给 `decisionLabel.Text`。

# 决策

第 5 ：切换到设计视图（Designer）并双击 `exitButton` 控件。

在代码编辑器中，你会看到一个名为 `exitButton_Click` 的空事件处理程序。

通过在程序 3 的第 77–89 行输入代码来完成 `exitButton_Click` 事件处理程序。

第 6 ：保存项目并运行应用程序。首先，输入工资为 45000，当前工作年限为1。点击 `Check Qualifications`（检查资质）按钮，应用程序应显示消息“未达到当前工作年限（Minimum years at current job not met）”。

点击 `Clear`（清除）按钮。输入工资 35000，当前工作年限 5。点击 `Check Qualifications` 按钮，应用程序应显示消息“未达到最低要求（Minimum salary requirement not met）”。

点击 `Clear` 按钮。输入工资 45000，当前工作年限 5。点击 `Check Qualifications` 按钮，应用程序应显示消息“符合贷款条件（You qualify for the loan）”。

根据你的需要继续测试应用程序。完成后，点击 `Exit`（退出）按钮，表单应该关闭。

## 贷款资格应用程序的程序 3 Form1 代码

```sharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace Loan_Qualifier
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void checkButton_Click(object sender, EventArgs e)
        {
            try
            {
                // 常量定义
                const decimal MINIMUM_SALARY = 40000m;
                const int MINIMUM_YEARS_ON_JOB = 2;

                // 局部变量
                decimal salary;
                int yearsOnJob;

                // 获取工资和工作年限。
                salary = decimal.Parse(salaryTextBox.Text);
                yearsOnJob = int.Parse(yearsTextBox.Text);

                // 判断用户是否符合条件。
                if (salary >= MINIMUM_SALARY
                if (yearsOnJob >= MINIMUM_YEARS_ON_JOB)
                {
                    // 用户符合条件。
                    decisionLabel.Text = "You qualify for the loan.";
                }
                else
                {
                    // 用户不符合条件。
                    decisionLabel.Text = "Minimum years at current " +
                        "job not met.";
                }
            }
            else
            {
                // 用户不符合条件。
                decisionLabel.Text = "Minimum salary requirement " +
                    "not met.";
            }
            catch (Exception ex)
            {
                // 显示错误消息。
                MessageBox.Show(ex.Message);
            }
        }

        private void clearTextBox_Click(object sender, EventArgs e)
        {
            // 清空文本框和决策Label。
            salaryTextBox.Text = "";
            yearsTextBox.Text = "";
            decisionLabel.Text = "";

            // 重置焦点。
            salaryTextBox.Focus();
        }

        private void exitButton_Click(object sender, EventArgs e)
        {
            // 关闭表单。
            this.Close();
        }
    }
}
```

# 嵌套决策结构中的缩进和对齐

为了调试，在嵌套语句中使用正确的对齐和缩进非常重要。这有助于查看结构的每个部分执行了哪些操作。例如，以下代码在功能上与程序 3 的第 36–55 行等效。虽然这段代码在逻辑上是正确的，但由于没有正确缩进，调试将非常困难。

## 决策

```sharp
if (salary >= MINIMUM_SALARY)
{
  if (yearsOnJob >= MINIMUM_YEARS_ON_JOB)
  {
    // 用户符合条件，
    decisionLabel.Text = "You qualify for the loan";
  }
  else
  {
    // 用户不符合条件。
    decisionLabel.Text = "Minimum years at current " +
      "job not met";
  }
}
else
{
  // 用户不符合条件。
  decisionLabel.Text = "Minimum salary requirement " +
    "not met";
}
```

幸运的是，Visual Studio 会自动对决策结构中的语句进行缩进和对齐。如图 14 所示，正确的缩进和对齐让我们更容易判断 `if` 和 `else` 子句是否关联在一起。

### 图 14 if 和 else 子句的对齐

![](img/9467d25da5679b16515c9401daaae36c_226_0.png)

### 测试一系列条件

在教程 3 中，你看到了程序如何使用嵌套结构来测试多个布尔表达式。程序拥有一系列需要测试的布尔表达式，然后根据哪个表达式为真来执行操作，这并不罕见。实现这一点的一种方法是让一个决策结构内部嵌套许多个决策结构。例如，查看 Student Samples Programs 中第 4 文件夹下的 Grader 应用程序。

图 15 显示了应用程序的表单，带有几个控件的名称。当你运行应用程序时，在 `testTextBox` 中输入一个数字测试分并点击 `determineGrade` 按钮；随后会在 `gradeLabel` 中显示一个成绩。

## 决策

### 图 15 Grader 应用程序的表单

![](img/9467d25da5679b16515c9401daaae36c_226_0.png)

以下 10 分制的评分标准用于确定成绩：

| 分数 | 成绩 |
| :--- | :--- |
| 90及以上 | A |
| 80–89 | B |
| 70–79 | C |
| 60–69 | D |
| 60以下 | F |

确定成绩的逻辑可以如下：

- 如果分数低于 60，则为“D”。
- 否则，如果分数低于 70，则为“C”。
- 否则，如果分数低于 80，则为“B”。
- 否则，如果分数低于 90，则为“A”。

这种逻辑需要多个决策结构，如图 16 所示。

### 图 16 使用嵌套决策结构确定成绩

![](img/9467d25da5679b16515c9401daaae36c_226_0.png)

## 决策

打开代码编辑器并查看所示的 `checkButton_Click` 事件处理程序，它位于第 12–41 行。

```sharp
1 private void checkButton_Click(object sender, EventArgs e)
2 {
3 try
4 {
5 // 命名常量
6 ... (省略部分代码)
7
8 // 获取工资和工作年限。
9 salary = decimal.Parse(salaryTextBox.Text);
10 yearsOnJob = int.Parse(yearsTextBox.Text);
11
12 // 判断用户是否符合条件。
13 if (salary >= MINIMUM_SALARY
14
15 if (yearsOnJob >= MINIMUM_YEARS_ON_JOB)
16 {
17 // 用户符合条件。
18 decisionLabel.Text = "You qualify for the loan.";
19 }
20 else
21 {
22 // 用户不符合条件。
23 decisionLabel.Text = "Minimum years at current " +
24 "job not met.";
25 }
26 }
27 else
28 {
29 // 用户不符合条件。
30 decisionLabel.Text = "Minimum salary requirement " +
31 "not met.";
32 }
33 } catch (Exception ex) {
34 // 显示错误消息。
35 MessageBox.Show(ex.Message);
36 }
37 }
```

### if-else 语句

尽管之前显示的 Grader 应用程序是一个示例，但嵌套决策结构的逻辑非常复杂。C# 提供了一种特殊的决策结构，称为 **if-else 语句**，它让这种逻辑的编写变得简单。使用以下通用格式编写 if-else 语句：

```sharp
if (BooleanExpression_1) {
    语句; // 如果 BooleanExpression_1 为真，则执行此语句。
} else if (BooleanExpression_2) {
    语句; // 如果 BooleanExpression_2 为真，则执行此语句。
}
// 根据需要插入多个 else if 子句...
else {
    语句; // 如果没有任何布尔表达式为真，则执行此语句。
}
```

当语句执行时，会测试 `BooleanExpression_1`。如果 `BooleanExpression_1` 为真，则执行随后的语句，并跳过其余部分。如果 `BooleanExpression_1` 为假，程序将跳转到下一个 `else if` 并测试 `BooleanExpression_2`。如果为真，则执行随后的语句；结构继续执行，直到找到为真的布尔表达式，或者没有更多的 `else` 子句。如果布尔表达式都为假，则执行 `else` 子句的语句。

例如，查看 Student Samples Programs 第 4 文件夹中的 Grader 应用程序。该应用程序与之前讨论的 Grader 应用程序类似。用户输入数字分数，应用程序将显示成绩。这与图 15 所示的表单完美匹配。然而，Grader2 应用程序使用 if-else 语句来确定成绩，而不是嵌套的 if-else 语句。

## 决策

```csharp
{
  gradeLabel.Text = "A";
}
catch (Exception ex)
{
  // 显示一条错误消息。
  MessageBox.Show(ex.Message);
}
```

注意 if-else 语句中使用的对齐和缩进：`if`、`else if` 和 `else` 子句都是对齐的，而条件执行的语句则被缩进。

你永远不需要使用 if-else-if 语句，因为它的逻辑可以通过嵌套的 if-else 语句来实现。然而，在调试时，长系列嵌套的 if-else 语句有两个特别的缺点：

- *代码可能会变得复杂且难以理解。*
- 因为缩进在嵌套语句中非常重要，长系列嵌套的 if-else 语句可能会变得太长无法在不进行水平滚动的情况下显示在计算机屏幕上。此外，长语句在纸打印时通常会换行，使得代码更难以阅读。

if-else-if 语句的逻辑通常比长系列嵌套的 if-else 语句更容易遵循。而且由于 if-else-if 语句中的所有子句都是对齐的，该语句中的行长度往往更短。

### 检查点

- 1. 将以下嵌套的 if-else if 语句转换为 if-else-if 语句：

```csharp
if (number == 1)
{
  MessageBox.Show("One");
}
else
  if (number == 2)
  {
    MessageBox.Show("Two");
  }
else
  if (number == 3)
  {
    MessageBox.Show("Three");
  }
else
  {
    MessageBox.Show("Unknown");
  }
```

### 逻辑运算符

**概念：** 逻辑与运算符 (`&&`) 和逻辑或运算符 (`||`) 允许你连接多个布尔表达式以创建一个复合表达式。逻辑非运算符 (`!`) 会反转布尔表达式的真值。

C# 语言提供了一组被称为逻辑运算符的运算符，你可以使用它们来创建复杂的布尔表达式。表 3 描述了这些运算符。

#### 表 3 逻辑运算符

| 运算符 | 含义 |
|---|---|
| &&& | 这是逻辑与运算符。它将两个布尔表达式连接为一个复合表达式。只有当两个子表达式都为真时，复合表达式才为真。 |
| \|\| | 这是逻辑或运算符。它将两个布尔表达式连接为一个复合表达式。其中一个或两个子表达式为真，复合表达式就为真。其中一个子表达式为真是必要的，无论哪一个都无所谓。 |
| ! | 这是逻辑非运算符。它是一个元运算符，意味着它作用于一个操作数。操作数必须是一个布尔表达式。非运算符反转其操作数的真值。如果它应用于一个真的表达式，运算符返回假。如果它应用于一个假的的表达式，运算符返回真。 |

表 4 显示了使用逻辑运算符的几个复合布尔表达式的示例。

#### 表 4 使用逻辑运算符的复合布尔表达式

| 表达式 | 含义 |
|---|---|
| x > y && a < b | x 是否大于 y 且 a 是否小于 b？ |
| x == y \|\| x == z | x 是否等于 y 或 x 是否等于 z？ |
| ! (x > y) | 表达式 x > y 是否为真？ |

## &&& 运算符

**&& 运算符**是逻辑与运算符。它接受两个布尔表达式作为操作数，并创建一个仅当两个子表达式都为真时为真的布尔表达式。以下使用 && 运算符的 if 语句示例：

```csharp
if (temperature < 20 && minutes > 12)
{
    MessageBox.Show("温度处于危险区域。");
}
```

在该语句中，两个布尔表达式 `temperature < 20` 和 `minutes > 12` 被组合为一个复合表达式。只有当 `temperature` 小于 20 且大于 12 时，才会执行 `MessageBox.Show`。如果任一个布尔子表达式为假，复合表达式为假，就不会显示消息。

## 决策

#### 表 5 AND 运算符的真值表

| 表达式 | 表达式的值 |
| :--- | :--- |
| true && false | false |
| false && true | false |
| false && false | false |
| true && true | true |

如所示，`&&` 运算符的两侧都必须为真，运算符才会返回真值。

### || 运算符

`||` 运算符是逻辑或运算符。它接受两个布尔表达式作为操作数，并创建一个当其中一个子表达式为真时为真的复合布尔表达式。以下使用 `||` 运算符的 if 语句示例：


```c
private void determineGradeButton_Click(object sender, EventArgs args)
{
    try
    {
        // 用于存储测试分数的变量。
        double testScore;
        // 获取测试分数。
        testScore = double.Parse(testScoreTextBox.Text);
        // 确定等级。
        if (testScore < 60)
        {
            gradeLabel.Text = "F";
        }
        else
        {
            if (testScore < 70)
            {
                gradeLabel.Text = "D";
            }
            else
            {
                if (testScore < 80)
                {
                    gradeLabel.Text = "C";
                }
                else
                {
                    if (testScore < 90)
                    {
                        gradeLabel.Text = "B";
                    }
                    else
                    {
                        gradeLabel.Text = "A";
                    }
                }
            }
        }
    }
    catch (Exception ex)
    {
        // 显示错误消息。
        MessageBox.Show(ex.Message);
    }
}
```

# if-else-if 语句

尽管之前显示的 Grader 应用程序是一个简单的示例，但嵌套决策结构的逻辑相当复杂。C# 提供了一种决策结构的特殊版本，称为 `if-else-if` 语句，它使得编写这种逻辑变得更加简单。你使用以下通用格式编写 `if-else-if` 语句：

```csharp
if (BooleanExpression_1) {
    statement;
    statement;
    etc;
} else if (BooleanExpression_2) {
    statement;
    statement;
    etc;
}
根据需要插入尽可能多的 else if...
else {
    statement;
    statement;
    etc;
}
```

当执行执行时，会测试 `BooleanExpression_1`。如果 `BooleanExpression_1` 为真，则执行紧随其后的语句set，并跳过结构的其余部分。如果 `BooleanExpression_1` 为假，程序跳转到下一个 `else if` 子句并测试 `BooleanExpression_2`。如果它为真，则执行结构的其余部分。此过程一直持续到发现某个布尔表达式为真，或者没有更多的 `else if` 子句剩余。如果没有一个布尔表达式为真，则执行最后一个 `else` 子句之后的语句set。

例如，参考本书示例程序中 *Chap04* 的 *Grader2* 应用程序。该应用程序的工作原理与之前过的 *Grader* 应用程序完全相同。用户输入数字测试分数，应用程序显示等级。它的表单与图 4-15 中的表单完全一致。Grader2 应用程序使用 *else-if-else* 来确定等级，而不是 `else-if` 语句。这里显示了 *Grader2* 应用程序的 `determineGradeButton_Click` 事件处理程序：

```csharp
private void determineGradeButton_Click(object sender, EventArgs e) {
    try {
        // 用于存储测试分数的变量。
        double testScore = double.Parse(testScoreTextBox.Text);
        // 确定等级。
        if (testScore < 60) {
            gradeLabel.Text = "F";
        } else if (testScore < 70) {
            gradeLabel.Text = "D";
        } else if (testScore < 80) {
            gradeLabel.Text = "C";
        } else if (testScore < 90) {
            gradeLabel.Text = "B";
        } else {
            gradeLabel.Text = "A";
        }
    } catch (Exception ex) {
        // 显示错误消息。
        MessageBox.Show(ex.Message);
    }
}
```

## 4.3 嵌套结构

## 检查点

4.1 将以下嵌套嵌套 `if` 语句转换为 `if-else` 语句：

```csharp
if (number == 1) {
    MessageBox.Show("One");
} else if (number == 2) {
    MessageBox.Show("Two");
} else if (number == 3) {
    MessageBox.Show("Three");
} else {
    MessageBox.Show("Unknown");
}
```

## 4.4 逻辑运算符

概念：逻辑与运算符 `&&` 和逻辑或运算符 `||` 允许你连接多个表达式。逻辑非运算符 `!` 则反转布尔表达式的真值。

C# 语言提供一组称为逻辑运算符的运算符，可以使用它们来创建布尔表达式。表 4-3 描述了这些运算符。

### 表 4-3 逻辑运算符

| 运算符 |  |

|---|---|

| `&&` | 逻辑与运算符。它将两个布尔表达式连接成一个复合表达式。只有当两个子表达式都为真时，复合表达式为真。 |

| `||` | 逻辑或运算符。它将两个布尔表达式连接成一个复合表达式。一个或两个子表达式为真时，复合表达式为真。只需其中一个子表达式为真即可。 |

| `!` | 逻辑非运算符。它是一个元运算符，意味着它只作用于一个操作数。运算符反转其操作数的真值。如果它应用于一个真的表达式，运算符返回假；如果它应用于一个假的表达式，运算符返回真。 | |

表 4-4 显示了使用逻辑运算符的若干复合布尔表达式示例。

### 表 4-4 使用逻辑运算符的复合布尔表达式

| 表达式 | 含义 |

|---|---|

| `x > y && a < b` | `x` 是否大于 `y` 且小于 `b`？ |

| `x == y || x == z` | `x` 是否等于 `y` 或等于 `z`？ |

| `! (x)` | 表达式 `x > y` 是否不真？ |

### && 运算符

`&&` 运算符是逻辑与运算符。它接受两个布尔表达式作为操作数，并创建一个仅当两个子表达式都为真时为真的复合布尔表达式。以下是一个使用 `&&` 运算符的 `if` 语句示例：

```csharp
if (temperature < 20 && minutes > 12)
    MessageBox.Show("温度处于危险区域。");
```

表 4-5 显示了 `&&` 运算符的真表。真表列出了显示所有与 `&&` 运算符连接的真与假组合的表达式。同时也显示了表达式的结果值。

### 表 4-5 AND 运算符的真表

| 表达式 | 表达式的值 |

|---|---|

| true && false | false |

| false && true | false |

| false && false | false |

| true && true | true |

如下表所示，`||` 运算符的两侧都必须为真，运算符才会返回真值。

### || 运算符

`||` 运算符是逻辑或运算符。它接受两个布尔表达式作为操作数，并创建一个复合表达式，当其中一个子表达式为真时，该表达式为真。以下是一个使用 `||` 运算符的 `if` 语句示例：

```
if (temperature < 20 || temperature > 100)
{
    MessageBox.Show("The temperature is in the danger zone.");
}
```

只有当 `temperature` 小于 20 或 `temperature` 大于 100 时，`MessageBox.Show` 语句才会执行。如果任一子表达式为假，复合表达式为真。表 4-6 显示了 `||` 运算符的真表。

### 表 4-6 || 运算符的真表

| 表达式 | 表达式的值 |

|---|---|

| true || false | true |

| false || true | true |

| false || false | false |

| true || true | true |

一个 `||` 表达式要为真，只需要 `||` 运算符的一侧为真。另一侧是假还是真并不重要。

### 短路求值

`&&` 和 `||` 运算符都执行短路求值。`&&` 运算符的工作原理如下：如果 `&&` 运算符左侧的表达式为假，则不检查右侧的表达式。因为只要有一个子表达式为假，复合表达式为假，检查剩余的表达式将浪费 CPU 时间。因此，当 `&&` 运算符发现其左侧表达式为假时，它会发生短路，不再评估右侧的表达式。

`||` 运算符的短路求值原理如下：如果 `||` 运算符左侧的表达式为真，则不检查右侧的表达式。因为只需要其中一个表达式为真即可，检查剩余的表达式将浪费 CPU 时间。

## 4.4 逻辑运算符

### ! 运算符

该运算符是逻辑非运算符。它是一个元运算符，接受布尔表达式作为输入并反转其逻辑值。换句话说，如果表达式为真，`!` 运算符返回假；如果表达式为假，`!` 运算符返回真。

以下是使用逻辑非运算符的 `if` 语句：

```
if (!temperature > 100) {
    MessageBox.Show("This is below the maximum temperature.");
}
```

首先，测试表达式 `(temperature > 100)` 并得到一个真或假的结果值。然后，将 `!` 运算符应用到该值上。如果表达式 `(temperature > 100)` 为真，`!` 运算符返回假。如果表达式 `(temperature > 100)` 为假，`!` 运算符返回真。之前的代码等同于询问“温度是否大于 100？”。

注意，在这个示例中，我们给表达式 `temperature > 100` 加上了括号。这是必要的，因为 `!` 运算符的优先级高于关系运算符。如果我们不给表达式 `temperature > 100` 加上括号，`!` 运算符将仅作用于 `temperature` 变量。

表 4-7 显示了 `!` 运算符的真表

| 表达式 | 表达式的值 |

|---|---|

| ! true | false |

| ! false | true |

### 逻辑运算符的优先级

我们之前提到过，`&&` 和 `||` 逻辑运算符的优先级高于关系运算符。例如，看以下表达式：

```
creditScore > 700 || accountBalance > 9000
```

当评估此表达式时，`>` 运算符先作用，然后是 `||` 运算符作用。该表达式与以下内容相同：

```
(creditScore > 700) || (accountBalance > 9000)
```

许多程序员选择用括号将逻辑运算符左右的表达式括起来，如此处所示。尽管在很多情况下并不强制要求使用括号，但使用括号可以让复合表达式更容易理解。

### 使用逻辑运算符检查数值范围

有时，你需要编写代码来确定一个数值是否在特定的值范围内或在特定范围之外。在判断一个数字是否在范围内，最好是使用 `&&` 运算符。例如，以下语句检查 `x` 的值以确定其是否在 20 到 40 的范围之内：

```
if (x > 20 && x < 40) {
    MessageBox.Show("The value is in the acceptable range.");
}
```

### 第 4 章 决策

此语句所测试的复合布尔表达式仅当 `x` 大于 20 且小于 40 时才为真。`x` 的值必须在 20 和 40 之间，该复合表达式才为真。

在判断一个数字是否在范围之外时，最好是使用 `||` 运算符。以下语句确定 `x` 是否在 20 到 40 的范围之外：

```
if (x < 20 || x > 40)
    MessageBox.Show("The value is in the acceptable range.");
```

在测试范围时，不要混淆逻辑运算符的逻辑是非常重要的。例如，`x` 不可能同时小于 20 又大于 40：

```
if (x < 20 && x > 40)
```

显然，这个复合表达式永远不会为真。让我们来看一个显示范围的示例。当你在 TextBox 中输入数字并点击 `checkButton` 时，会弹出一个消息框告诉你该数字是可以接受的。

```
private void checkButton_Click(object sender, EventArgs e)
{
    try
    {
        // 声明一个变量并用用户输入初始化。
        int number = int.Parse(inputText.Text);
        // 检查数字范围。
        if (number >= 1 && number <= 10)
        {
            MessageBox.Show("That number is acceptable.");
        }
        else
        {
            MessageBox.Show("That number is NOT acceptable.");
        }
    }
    catch (Exception ex)
    {
        // 显示错误。
        MessageBox.Show(ex.Message);
    }
}
```

## 测试

4.12 什么是复合布尔表达式？

4.13 下表显示了通过逻辑运算符连接的真假值的组合。通过圈选 T 或 F 完成表格，以指示此类组合的结果是真还是假。

| 逻辑表达式 | 结果（圈出 T 或 F） |

|---|---|

| true && false | T F |

| true && true | T F |

| false && true | T F |

| false && false | T F |

| true || false | T F |

| true || true | T F |

| false || true | T F |

| false || false | T F |

4.14 假设变量 `a = 2`, `b = 4`, `c = 6`。对于以下每个条件，圈出 T 或 F 以指示它是真还是假。

| | | 结果（圈出 T 或 F） |

|---|---|

| `a == 4 && b > 2` | T F |

| `c < 6 && a > 3` | T F |

| `1 == -1 && c == 3` | T F |

| `a >= -1 && a <= b` | T F |

| `!(a > 2)` | T F |

4.15 解释 `&&` 和 `||` 运算符如何进行短路求值。

4.16 写一个 `if` 语句，如果变量 `speed` 在 0 到 200 的范围内，则在消息框中显示“The number is valid”。

4.17 写一个 `if` 语句，如果变量 `speed` 在 0 到 200 的范围之外，则在消息框中显示“The number is not valid”。

# 变量与标志

> **概念：** 你可以在 `bool` 变量中存储 true 和 false 的值，这些变量通常用作标志。

C# 语言提供了 `bool` 数据类型，你可以用它来创建存储 true 或 false 值的变量。下面是一个变量定义的示例：

```csharp
bool grandMaster;
```

这声明了一个名为 `grandMaster` 的 `bool` 变量。在程序中，我们可以为该变量赋值 true 或 false，如下所示：

```csharp
if (points > 5000)
{
    grandMaster = true;
}
else{
    grandMaster = false;
}
```

`bool` 数据类型的变量通常用作标志。标志是一个表示程序中是否存在某个条件的变量。当标志变量被设置为 `false` 时，表示该条件尚存在。当标志变量被设置为 `true` 时，意味着该条件存在。例如，之前的代码可能用于游戏以判断用户是否为“特大师”。如果他或她获得的积分超过了 5,000 分，我们将 `grandMaster` 变量设置为 `true`。否则，我们将变量设置为 `false`。在程序的稍后部分，我们可以这样测试 `grandMaster` 变量：

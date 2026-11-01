
```csharp
double input1 = Convert.ToDouble(input1TextBox.Text);
double input2 = Convert.ToDouble(input2TextBox.Text);
bool result = input1 < input2;
resultLabel.Text = "Is the first one lower? " + result.ToString();
```

### 代码 8.6

为方便起见，下面也给出了完整的最终事件处理程序：

```csharp
private void equalsButton_Click(object sender, EventArgs e)
{
    double input1 = Convert.ToDouble(input1TextBox.Text);
    double input2 = Convert.ToDouble(input2TextBox.Text);
    bool result = input1 == input2;
    resultLabel.Text = "Are they equal? " + result.ToString();
}
private void greaterButton_Click(object sender, EventArgs e)
{
    double input1 = Convert.ToDouble(input1TextBox.Text);
    double input2 = Convert.ToDouble(input2TextBox.Text);
    bool result = input1 > input2;
    resultLabel.Text = "Is the first one greater? " + result.ToString();
}
private void lowerButton_Click(object sender, EventArgs e)
{
    double input1 = Convert.ToDouble(input1TextBox.Text);
    double input2 = Convert.ToDouble(input2TextBox.Text);
    bool result = input1 < input2;
    resultLabel.Text = "Is the first one lower? " + result.ToString();
}
```

### 代码 8.7

10. 生成并运行项目。我输入了以下数字，当点击比较按钮时，比较结果会显示出来，如图 8.2、图 8.3 和图 8.4 所示。

请注意，相等和不相等比较也可以应用于字符串类型变量，而其余的比较运算符则不能。

## 第 8 章 条件语句

![](img/41d82527c4e41cdb7e56259564306ddc_212_0.png)

图 8.2. 相等比较结果

![](img/41d82527c4e41cdb7e56259564306ddc_212_1.png)

图 8.3. 第一个数更大？比较结果

![](img/41d82527c4e41cdb7e56259564306ddc_212_2.png)

图 8.4. 第一个数更小？比较结果

### 8.1.2. 算术运算符

算术运算符对数值操作数进行运算并生成数值结果。以下是 C# 中常用的算术运算符：

表 8.2. 算术运算符

| 运算符 | 操作 |
|---|---|
| + | 将操作数相加 |
| - | 从第一个操作数中减去第二个操作数 |
| * | 将操作数相乘 |
| / | 将第一个操作数除以第二个操作数 |
| % | 取模运算符：返回第一个操作数除以第二个操作数后的余数 |

> 通常的数学运算优先级规则适用：* 和 / 是优先执行的操作，而 + 和 - 其次执行。我们可以像在普通算术运算中一样，使用括号轻松改变运算顺序。

让我们构建一个简单的计算器来展示这些运算符在项目中的使用：

- 1. 创建一个 C# 项目。
- 2. 添加两个 TextBox，用户将在其中输入数字。将它们的 Name 属性设置为 **input1TextBox** 和 **input2TextBox**。
- 3. 添加五个按钮，单击它们时将执行算术运算。将它们的 Text 属性分别设置为 +、-、*、/ 和 %。将它们的 Name 属性分别设置为 **addButton**、**subtractButton**、**multiplyButton**、**divideButton** 和 **modButton**。
- 4. 添加另一个用于显示结果的 TextBox。将它的 Name 属性设置为 **resultTextBox**。窗体布局可能类似于图 8.5 所示的布局。
- 5. 双击按钮以创建它们的事件处理程序。
- 6. 我们首先编写 addButton 的 Click 事件处理程序代码。首先，我们将 **input1TextBox** 和 **input2TextBox** 的 Text 输入转换为 double 类型变量，就像我们在上一个示例中所做的那样，并将这些变量相加得到加法结果。然后通过 **toString()** 方法转换为字符串后，在 **resultTextBox** 中显示该结果。这些代码行显示在代码 8.8 所示的事件处理程序中。

![](img/41d82527c4e41cdb7e56259564306ddc_214_0.png)

图 8.5. 窗体布局

```csharp
private void addButton_Click(object sender, EventArgs e)
{
    double input1 = Convert.ToDouble(input1TextBox.Text);
    double input2 = Convert.ToDouble(input2TextBox.Text);
    double result = input1 + input2;
    resultTextBox.Text = result.ToString();
}
```

### 代码 8.8

7. 我们如下所示，在其按钮的 Click 事件处理程序中使用相应的运算符执行剩余操作：

```csharp
private void subtractButton_Click(object sender, EventArgs e)
{
    double input1 = Convert.ToDouble(input1TextBox.Text);
    double input2 = Convert.ToDouble(input2TextBox.Text);
    double result = input1 - input2;
    resultTextBox.Text = result.ToString();
}
private void multiplyButton_Click(object sender, EventArgs e)
{
    double input1 = Convert.ToDouble(input1TextBox.Text);
    double input2 = Convert.ToDouble(input2TextBox.Text);
    double result = input1 * input2;
    resultTextBox.Text = result.ToString();
}
private void divideButton_Click(object sender, EventArgs e)
{
    double input1 = Convert.ToDouble(input1TextBox.Text);
    double input2 = Convert.ToDouble(input2TextBox.Text);
    double result = input1 / input2;
    resultTextBox.Text = result.ToString();
}
private void modButton_Click(object sender, EventArgs e)
{
    double input1 = Convert.ToDouble(input1TextBox.Text);
    double input2 = Convert.ToDouble(input2TextBox.Text);
    double result = input1 % input2;
    resultTextBox.Text = result.ToString();
}
```

### 代码 8.9（续）

请注意，这些事件处理程序中唯一变化的是算术运算符。

8. 生成并运行项目。在输入 TextBox 中输入任意数字，然后点击相应的按钮执行算术运算。我们的计算器按预期运行，如下图所示：

![](img/41d82527c4e41cdb7e56259564306ddc_215_0.png)

图 8.6. 加法运算

- - 当算术运算使用 `int` 类型变量和 `float/double` 类型变量执行时，结果将为 `double` 类型。
- - 当算术运算使用 `double` 类型变量和 `float` 类型变量执行时，结果将为 `double` 类型。

![](img/41d82527c4e41cdb7e56259564306ddc_216_0.png)

图 8.7. 减法运算

![](img/41d82527c4e41cdb7e56259564306ddc_216_1.png)

图 8.8. 乘法运算

![](img/41d82527c4e41cdb7e56259564306ddc_216_2.png)

图 8.9. 除法运算

- 3. 为四个递增/递减运算符添加四个按钮。将它们的 Name 属性分别设置为 **incrementButton**、**decrementButton**、**addButton** 和 **subtractButton**。将它们的 Text 属性分别设置为 ++、--、+= 和 -=。

- 4. 在此项目中，我们将不添加用于显示结果的 Label 或 TextBox。而是使用结果更新输入 TextBox。窗体布局如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_218_0.png)

图 8.11. 窗体布局

- 5. 单击按钮以创建它们的 Click 事件处理程序。在这些事件处理程序中，我们需要读取这些 TextBox 的最新值。我们像往常一样执行此操作：

```csharp
double number1 = Convert.ToDouble(number1TextBox.Text);
double number2 = Convert.ToDouble(number2TextBox.Text);
```

### 代码 8.10

我们通过这些代码行获得了输入的数值。对于 ++ 按钮，让我们使用关联的 ++ 运算符将每个数字加 1，如下所示：

```csharp
number1++;
number2++;
```

### 代码 8.11

然后，使用最新值更新 TextBox：

```csharp
number1TextBox.Text = number1.ToString();
number2TextBox.Text = number2.ToString();
```

### 代码 8.12

6. 我们对其余按钮执行类似的操作。这些操作之后，我们将得到以下事件处理程序方法：

```csharp
private void incrementButton_Click(object sender, EventArgs e)
{
    double number1 = Convert.ToDouble(number1TextBox.Text);
    double number2 = Convert.ToDouble(number2TextBox.Text);
    number1++;
    number2++;
    number1TextBox.Text = number1.ToString();
    number2TextBox.Text = number2.ToString();
}
private void decrementButton_Click(object sender, EventArgs e)
{
    double number1 = Convert.ToDouble(number1TextBox.Text);
    double number2 = Convert.ToDouble(number2TextBox.Text);
    number1--;
    number2--;
    number1TextBox.Text = number1.ToString();
    number2TextBox.Text = number2.ToString();
}
private void addButton_Click(object sender, EventArgs e)
{
    double number1 = Convert.ToDouble(number1TextBox.Text);
    double number2 = Convert.ToDouble(number2TextBox.Text);
    number1 += number2;
    number1TextBox.Text = number1.ToString();
    number2TextBox.Text = number2.ToString();
}
private void subtractButton_Click(object sender, EventArgs e)
{
    double number1 = Convert.ToDouble(number1TextBox.Text);
    double number2 = Convert.ToDouble(number2TextBox.Text);
    number1 -= number2;
    number1TextBox.Text = number1.ToString();
    number2TextBox.Text = number2.ToString();
}
```

### 代码 8.13

> 请注意，在本例中，应用运算符 += 和 -= 后，第二个操作数 number2 不会改变。结果只写入 number1。我们在这里更新 number2 的 TextBox 只是为了演示。


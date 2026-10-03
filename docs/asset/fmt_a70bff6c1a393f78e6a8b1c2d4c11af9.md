
# C# 入门教程

## 清除按钮

4. 给 `lblFirstValue` 和 `lblMathFunction` 标签分配空字符串以清除它们。

5. 运行应用程序并确保清除按钮工作正常。

6. 关闭应用程序。

以下是清除按钮的完整代码：

```csharp
private void btnClear_Click(object sender, EventArgs e)
{
    lblValue.Text = noValue;
    lblFirstValue.Text = String.Empty;
    lblMathFunction.Text = String.Empty;
}
```

## 记忆按钮

**记忆 (M)** 按钮的作用是将标签 `lblValue` 中的当前值存储在表单级别名为 `memory` 的 `string` 变量中。然后用户应该可以通过点击**记忆读取 (MR)** 按钮来恢复该值。

1. 将按钮命名为 `btnMemory`。

2. 在表单上双击记忆按钮以创建其 Click 事件。

3. 在表单级别声明名为 `memory` 的字符串变量并给它分配一个空字符串。

```csharp
string memory = String.Empty;
```

4. 滚动到 `btnMemory_Click` 事件。

5. 将 `lblValue` 标签的值赋值给 `memory` 变量。

6. 将 `lblValue` 标签的值重置为 `noValue` 常量。

以下是记忆按钮的完整代码：

```csharp
private void btnMemory_Click(object sender, EventArgs e)
{
    memory = lblValue.Text;
    lblValue.Text = noValue;
}
```

## 记忆读取按钮

记忆读取 (MR) 按钮的作用是读取存储在记忆变量中的值并显示在 `lblValue` 标签中。

1. 将按钮命名为 `btnMemoryRecall`。

2. 在表单上双击记忆读取按钮以创建其 Click 事件。

3. 将表单级别创建的 `memory` 值赋值给 `lblValue` 标签。

4. 运行应用程序测试记忆和记忆读取按钮：输入一个值然后点击记忆按钮。点击清除按钮清除标签，然后点击记忆读取按钮获取记忆变量中的值并显示在 `lblValue` 标签中。

5. 关闭应用程序。

以下是记忆读取按钮的完整代码：

```csharp
private void btnMemoryRecall_Click(object sender, EventArgs e)
{
    lblValue.Text = memory;
}
```

## 小数按钮

小数点按钮的作用是在 `lblValue` 标签的值末尾添加小数点字符。为了符合用例规范，你必须根据 Windows 操作系统的区域设置创建另一个小数点字符串（逗号或点），将常量命名为 `decimalSign` 并根据你国家使用的符号为其赋值。

1. 将按钮命名为 `btnDecimal`。

2. 在表单上双击小数点按钮以创建其 Click 事件。

3. 滚动到表单开头，添加一个名为 `decimalSign` 的字符串常量，并分配相应的小数点。

```csharp
const string decimalSign = ",";
```

4. 回到 `btnDecimal_Click` 事件。

5. 在事件方法中添加名为 `hasDecimal` 的 `bool` 变量，并根据 `lblValue` 是否包含 `decimalSign` 常量中的小数点分配 `true` 或 `false`。

```csharp
bool hasDecimal = lblValue.Text.Contains(decimalSign);
```

6. 添加一个 `if` 语句检查 `hasDecimal` 变量是否为 `false`，或者是否未向标签添加小数点。

```csharp
if (!hasDecimal) lblValue.Text += decimalSign;
```

7. 运行应用程序并输入小数值。尝试添加多个小数点，这不应该是可能的。

8. 关闭应用程序。

以下是小数点按钮的完整代码：

```csharp
private void btnDecimal_Click(object sender, EventArgs e)
{
    bool hasDecimal = lblValue.Text.Contains(decimalSign);
    if (!hasDecimal) lblValue.Text += decimalSign;
}
```

## 算术按钮

**算术 (+, -, x, /)** 按钮的目的是点击计算 (=) 按钮时确定如何计算结果。当点击其中一个按钮时，该按钮的算术符号应显示在 `lblMathFunction` 标签中，`lblValue` 中的值应移动到 `lblFirstValue` 标签（数值标签上方的小标签），并将 `noValue` 常量的值赋值给 `lblValue` 标签。将 `sender` 参数强制转换为 `Button`，以获取点击按钮的 `Text` 属性，并将其显示在 `lblMathFunction` 标签中。

1. 选择一个**算术**按钮，并在**属性**窗口的**事件**部分中为其 **Click** 事件字段添加名称 `btnCalculate_Click`。

2. 如果你没有跳转到事件方法，请点击表单上的按钮进入其 **Click** 事件，将参数转换为 `Button` 变量 `btn`。

3. 将 `sender` 参数强制转换为名为 `btn` 的 `Button` 变量。

```csharp
Button btn = (Button)sender;
```

4. 将 `btn` 变量（实际上是点击的按钮）的 `Text` 属性分配给 `lblMathFunction` 标签。将在蓝色标签中显示按钮文本。稍后将使用此值决定如何执行计算。

```csharp
lblMathFunction.Text = btn.Text;
```

5. 将 `lblValue` 标签的值分配给 `lblFirstValue` 标签。

```csharp
lblFirstValue.Text = lblValue.Text;
```

6. 将 `lblValue` 标签的值设置为 `noValue` 常量的值。

```csharp
lblValue.Text = noValue;
```

7. 运行应用程序，确保算术符号显示在蓝色标签中，并且值已从 `lblValue` 标签移动到 `lblFirstValue` 标签。

8. 关闭应用程序。

以下是**计算**按钮的完整代码：

```csharp
private void btnCalculate_Click(object sender, EventArgs e)
{
    Button btn = (Button)sender;
    lblMathFunction.Text = btn.Text;
    lblFirstValue.Text = lblValue.Text;
    lblValue.Text = noValue;
}
```

## 符号按钮

符号 (±) 按钮的目的是在 `lblValue` 标签中显示负号（使数值变为负数）或在值为负数时移除负号。由于用例规定代码中除了表单开头的常量外不应存在硬编码值，因此必须添加一个名为 `minusSign` 的字符串常量，其中包含一个负号。

1. 将按钮命名为 `btnSign`。

2. 双击表单上的符号按钮以创建其 **Click** 事件。

3. 滚动到表单开头，添加常量 `minusSign` 并为其赋值一个负号。

```csharp
const string minusSign = "-";
```

4. 回到 `btnSign_Click` 事件方法。

5. 添加一个布尔（`bool`）变量 `hasSign`，通过使用 `Contains` 属性检查 `lblValue` 标签的 `Text` 属性是否存在负号，以此检查是否为负值。

```csharp
bool hasSign = lblValue.Text.Contains(minusSign);
```

6. 添加 `if` 语句检查 `hasSign` 值是否为 `true`，这意味着它是一个负数，应该移除负号。你可以对 `lblValue` 标签的 `Text` 属性使用 `Replace` 方法，将负号替换为空字符串。

```csharp
if (hasSign) lblValue.Text = lblValue.Text.Replace(minusSign, String.Empty);
```

7. 添加 `else` 语句检查值是否不等于存储在 `noValue` 常量中的值；即值不为零。如果是这样，在 `lblValue` 的 `Text` 属性开头插入负号，使数值变为负数。你可以使用 `Text` 属性的 `Insert` 方法在字符串开头添加负号。

```csharp
else if (lblValue.Text != noValue) lblValue.Text = lblValue.Text.Insert(0, minusSign);
```

8. 运行应用程序并添加正负数切换功能。

9. 关闭应用程序。

以下是符号按钮的完整代码：

```csharp
private void btnSign_Click(object sender, EventArgs e)
{
    bool hasSign = lblValue.Text.Contains(minusSign);
    if (hasSign)
        lblValue.Text = lblValue.Text.Replace(minusSign, String.Empty);
    else if (lblValue.Text != noValue)
        lblValue.Text = lblValue.Text.Insert(0, minusSign);
}
```

## 平方根按钮

平方根 (√) 按钮的目的是计算 `lblValue` 标签中值的平方根并在同一标签中显示结果。在计算平方根时可以使用 `Math` 类的 `Sqrt` 方法。在调用 `Sqrt` 方法之前，你必须检查值是否为正数，因为无法计算负数的平方根。如果值为负数，请显示带有适当消息的消息框。

1. 将按钮命名为 `btnSqrt`。

2. 双击表单上的平方根按钮创建其 **Click** 事件。

3. 添加布尔（`bool`）变量 `hasSign`，通过使用 `Contains` 属性检查 `lblValue` 标签的 `Text` 属性是否存在负号，以此检查是否为负值。

```csharp
bool hasSign = lblValue.Text.Contains(minusSign);
```

4. 添加 `if` 语句检查 `hasSign` 值是否为 `true`，这意味着它是一个负数，应该移除负号。你可以对 `lblValue` 标签的 `Text` 属性使用 `Replace` 方法，将负号替换为空字符串。

```csharp
if (hasSign)
{
    MessageBox.Show("Cannot calculate the square root of a negative number");
    return;
}
```

5. 接下来你需要检查 `lblValue` 是否以小数点结尾，如果是，则将其移除。

```csharp
var endsWithDecimalSign = lblValue.Text.EndsWith(decimalSign);
int length = lblValue.Text.Length;
if (endsWithDecimalSign) lblValue.Text = lblValue.Text.Substring(0, length - 1);
```

6. 使用 `Math` 类的 `Sqrt` 方法计算平方根。

```csharp
// 平方根计算逻辑
var value = Convert.ToDouble(lblValue.Text);
var result = Math.Sqrt(value);
lblValue.Text = result.ToString();
```

## 等于按钮

等 (=) 按钮的目的是根据点击的算术值，使用相应的算术运算计算两个值的结果。由于用例规定代码中除了表单开头的常量外不应存在硬编码值，你必须为剩余的三个算术运算符 `plusSign`、`divisionSign` 和 `multiplicationSign` 添加字符串常量。

1. 将按钮命名为 `btnEquals`。

2. 双击表单上的等按钮创建其 **Click** 事件。

3. 滚动到表单开头，添加三个常量 `plusSign`、`divisionSign` 和 `multiplicationSign`。

```csharp
const string plusSign = "+";
const string divisionSign = "/";
const string multiplicationSign = "x";
```

4. 你首先需要检查是否任何标签为空，或者 `lblValue` 的值是否为 0，如果是，则提前退出事件。

```csharp
var endsWithDecimalSign = lblFirstValue.Text.EndsWith(decimalSign);
int length = Convert.ToInt32(lblFirstValue.Text.Length);
if (endsWithDecimalSign)
    lblFirstValue.Text = lblFirstValue.Text.Substring(0, length - 1);
```

5. 你需要检查 `lblValue` 的值是否以小数点字符结尾并将其删除。

```csharp
length = Convert.ToInt32(lblFirstValue.Text.Length);
endsWithDecimalSign = lblValue.Text.EndsWith(decimalSign);
if (endsWithDecimalSign)
    lblFirstValue.Text = lblFirstValue.Text.Substring(0, length - 1);
```

6. 声明两个名为 `value1` 和 `value2` 的变量，并将两个标签转换后的 `double` 类型存储在它们中（`lblValue` 和 `lblFirstValue`）。

```csharp
var value1 = Convert.ToDouble(lblFirstValue.Text);
var value2 = Convert.ToDouble(lblValue.Text);
```

7. 获取存储在 `lblMathFunction` 标签中的值并将其赋值给名为 `mathFunction` 的字符串变量。

```csharp
var mathFunction = lblMathFunction.Text;
```

8. 添加一个名为 `result` 的小数值并将其赋值为 0。你可以显式地使用 `double` 数据类型清除变量，也可以隐式地使用 `var` 关键字并赋值为 `0d`；在 0 之后的 `d` 指定了编译器该值应被视为一个 `double` 值。

```csharp
var result = 0d; // decimal = 0m, double = 0d
```

9. 如果 `mathFunction` 中存储的符号等于常量 `plusSign`，则计算结果为 `value1 + value2` 并将结果存储在 `result` 变量中。

```csharp
if (mathFunction.Equals(plusSign))
    result = value1 + value2;
```

10. 如果符号等于常量 `minusSign`，计算结果为 `value1 - value2` 并将结果存储在 `result` 变量中。

```csharp
else if (mathFunction.Equals(minusSign))
    result = value1 - value2;
```

11. 如果符号等于常量 `divisionSign`，则计算结果为 `value1 / value2` 并结果存储在 `result` 变量中。

```csharp
else if (mathFunction.Equals(divisionSign))
    result = value1 / value2;
```

12. 否则，如果符号等于常量 `multiplicationSign`，则计算结果为 `value1 * value2` 并结果存储在 `result` 变量中。

```csharp
else if (mathFunction.Equals(multiplicationSign))
    result = value1 * value2;
```

13. 接下来清空两个 `lblMathFunction` 和 `lblFirstValue`。

```csharp
lblMathFunction.Text = String.Empty;
lblFirstValue.Text = String.Empty;
```

14. 使用 `ToString` 方法的格式选项，将 `result` 变量的结果格式化为 3 位小数的输出。

```csharp
lblValue.Text = result.ToString("F3");
```

15. 运行应用程序并进行几次涉及 `+`, `-`, `x` 和 `/` 的计算。

16. 关闭应用程序。

这里是 Equals 按钮的完整代码：

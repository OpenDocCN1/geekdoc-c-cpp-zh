
首先，如果应用程序要求用户在文本框中输入一个值，你可以检查文本框的 `Text` 属性，以确保用户输入了一个或多个字符。其次，如果应用程序要求用户在文本框中输入数字，你可以在 `try-catch` 语句中使用 `Convert` 类的适当方法，来检查文本框的 `Text` 属性是否可以转换为相应的数值数据类型。第三，如果应用程序要求用户在指定范围内在文本框中输入数字，你可以使用 `if-else` 语句来检查数字是否在该范围内。这被称为范围检查。

虽然此图只显示了如何检查用户输入到文本框的数据，但相同的原理适用于其他类型的控件。在控件 10 中，你将学习更多关于验证其他类型控件中输入内容的知识。此外，虽然此图只显示了如何检查数字的范围，你也可以检查字符串和日期，以确保它们落在某些范围内。你将在第 9 章中学习更多关于处理数据和字符串的知识。

通常，执行数据验证的代码会防止异常的抛出。例如，如果用户没有在“每月投资”文本框中输入值，此图中的代码将显示对话框并将焦点移动到“每月投资”文本框。如果你没有包含这段代码，当应用程序尝试将空字符串转换为数值数据类型时就会发生异常。

由于不使用异常处理来验证数据的代码比使用异常处理的代码运行更快，因此你应该尽可能避免使用异常来验证数据。当然，这并不总是可行或可能的。例如，解析一个字符串以检查它是否包含有效的数值格式是很困难的。如果不使用异常处理来验证数据，代码将无法处理这些错误。你将在第 9 章中学习更多关于处理数据和字符串的知识。

# 第 7 章 如何处理异常和验证数据 203

## 检查必填字段的方法

```csharp
public bool IsPresent(TextBox textbox, string name)
{
    if (textBox.Text == "")
    {
        MessageBox.Show(name + " is a required field.", "Entry Error");
        textBox.Focus();
        return false;
    }
    return true;
}
```

## 检查有效数字格式的方法

```csharp
public bool IsDecimal(TextBox textbox, string name)
{
    try
    {
        Convert.ToDecimal(textBox.Text);
        return true;
    } catch (FormatException)
    {
        MessageBox.Show(name + " must be a decimal value.", "Entry Error");
        textBox.Focus();
        return false;
    }
}
```

## 检查有效数值范围的方法

```csharp
public bool IsWithinRange(TextBox textbox, string name, decimal min, decimal max)
{
    decimal number = Convert.ToDecimal(textBox.Text);
    if (number < min || number > max)
    {
        MessageBox.Show(name + " must be between " + min.ToString() + " and " + max.ToString() + ".", "Entry Error");
        textBox.Focus();
        return false;
    }
    return true;
}
```

## 代码使用这些方法检查一个条目的有效性

```csharp
if (IsPresent(txtMonthlyInvestment, "Monthly Investment") &&
    IsDecimal(txtMonthlyInvestment, "Monthly Investment") &&
    IsWithinRange(txtMonthlyInvestment, "Monthly Investment", 1, 1000))
{
    MessageBox.Show("Monthly Investment is valid.", "Test");
}
```

## 描述

- 由于检查文本框的有效数据很常见，因此创建像这样的通用方法通常是有意义的。

图 7-9 如何使用通用方法来验证条目

### 如何验证多个条目

图 7-10 展示了两种编写 `IsValidData` 方法的方法来验证表单上的多个条目。这里显示的方法使用图 7-9 中的方法验证月投资和利率文本框。虽然这些方法只检查了两个文本框，但你可以使用此类方法检查表单上的每一个条目。这样，整个表单的数据验证都集中在一个位置，使得代码易于阅读和维护。

图中的第一个方法使用一系列 `if` 语句来检查三个条件。在每个 `if` 语句中，使用非 `!` 运算符来反转方法返回的布尔值。例如，如果月投资项不存在，`IsPresent` 方法将显示对话框并返回 `false`。结果是剩余的 `if` 语句不会执行。

第二个方法使用单个 `return` 语句来检查所有验证条件。为了实现这一点，它使用逻辑与运算符 `&&` 返回所有条件的结果。由于该运算符是短路的，只有在前一个条件返回 `true` 时才会评估下一个条件。结果是，验证方法将一直调用直到其中一个返回 `false`。然后该方法将显示对话框，整个 `IsValidData` 方法将返回 `false` 值。

注意这两个方法都首先调用 `IsPresent` 方法，然后是 `IsDecimal` 方法，最后是 `IsWithinRange` 方法。在这种情况下，`IsDecimal` 必须在 `IsWithinRange` 之前调用，因为 `IsWithinRange` 假设传递它的文本框包含有效的数值。如果你传递一个包含无效数值的文本框，该方法将抛出 `FormatException`。然而，如果你使用 `IsDecimal` 方法首先检查文本框的数值，则 `IsWithinRange` 方法永远不会抛出 `FormatException`。

![](img/3148667e42d4db35b3d08576aaa1fa01_223_0.png)

### 使用系列简单 if 语句的代码

```csharp
public bool isValidData()
{
    // 验证月投资文本框
    if (!IsPresent(txtMonthlyInvestment
```

### 在单个 return 语句中使用复合条件的代码

```csharp
public bool isValidData()
{
    return
        // 验证月投资文本框
        IsPresent(txtMonthlyInvestment, "Monthly Investment") &&
        IsDecimal(txtMonthlyInvestment, "Monthly Investment") &&
        IsWithinRange(txtMonthlyInvestment, "Monthly Investment",
        1, 1000) &&

        // 验证利率文本框
        IsPresent(txtInterestRate, "Yearly Interest Rate") &&
        IsDecimal(txtInterestRate, "Yearly Interest Rate") &&
        IsWithinRange(txtInterestRate, "Yearly Interest Rate", 1, 20);
}
```

## 描述

- 这两个方法都使用图中显示的方法来检查表单上的条目。像这样的方法将整个表单的数据验证代码在一个位置。

### 带有数据验证的未来价值应用

在 7-7 中，你看到了一个使用结构化异常处理来捕获可能抛出的所有异常的未来价值应用版本。现在，你将看到一个包含验证用户输入代码改进版本。这段代码防止抛出格式异常，并向用户提供更具描述性的信息。

### 对话框

图 7-11 显示了当用户输入无效数据时显示的对话框。例如，如果用户没有输入必填字段，会显示第一个对话框。如果用户输入的月投资或年利率不是有效的小数格式，会显示第二个对话框。如果用户输入的数字不在应用程序指定的范围内，会显示第三个对话框。

### 代码

图 7-12 显示了此版本未来价值应用的代码。首先，`btnCalculate_Click` 方法包含一个异常处理器，用于捕获任何意外异常。在此块中，如果 `IsValidData` 方法返回 `true` 值，则计算并显示未来价值。否则，检测到错误的验证方法将显示对话框并将焦点移动到相应的框。

`IsValidData` 方法检查表单上的三个框，确保它们包含有效的数值条目。在此，调用了一个名为 `IsDecimal` 的方法来检查用户是否在“年份”框中输入了有效的整数。该方法的工作原理与 `IsDecimal` 方法相似。

此应用程序中的每个方法都执行特定的任务。例如，`btnCalculate_Click` 方法从表单获取值并在表单上显示。`IsValidData`、`IsPresent`、`IsDecimal` 和 `IsWithinRange` 方法包含了验证用户输入的代码。

然而，这段代码可以更高效。例如，如果用户在月投资框中输入有效的小数，`ToDecimal` 被调用三次：一次通过 `IsDecimal` 方法，一次通过 `IsWithinRange` 方法，另一次通过 `btnCalculate_Click` 方法。对于大多数应用程序，能够复用和易于维护此代码带来的收益远大于任何性能问题。

### 带有必填字段对话框的未来价值表单

![](img/3148667e42d4db35b3d08576aaa1fa01_226_0.png)

### 无效小数的对话框

![](img/3148667e42d4db35b3d08576aaa1fa01_226_1.png)

### 无效范围的对话框

![](img/3148667e42d4db35b3d08576aaa1fa01_226_2.png)

### 意外异常的对话框

![](img/3148667e42d4db35b3d08576aaa1fa01_226_3.png)

## 描述

* 如果用户没有输入必填字段，会显示第一个对话框。
* 如果用户输入的月投资或年利率不是有效的小数格式，会显示第二个对话框。
* 如果用户输入的数字不在应用程序指定的范围内，会显示第三个对话框。
* 如果发生了任何其他类型的异常，将显示第四个对话框。

图 7-11 未来价值应用的对话框

# 未来价值应用程序的代码

`private void btnFutureValue.Click(object sender, System.EventArgs e)`

{

```csharp
try {
    if (IsValidData()) {
        decimal monthlyInvestment =
            Convert.ToDecimal(txtMonthlyInvestment.Text);
        decimal yearlyInterestRate =
            Convert.ToDecimal(txtInterestRate.Text);
        int years = Convert.ToInt32(txtYears.Text);

        int months = years * 12;
        decimal monthlyInterestRate = yearlyInterestRate / 12 / 100;
        decimal futureValue = CalculateFutureValue(
            monthlyInvestment, monthlyInterestRate, months);

        txtFutureValue.Text = futureValue.ToString("c");
        txtMonthlyInvestment.Focus();
    }
} catch (Exception ex) {
    MessageBox.Show(ex.Message + "\n\n" +
        ex.GetType().ToString() + "\n" + 
        ex.StackTrace, "Exception");
}
```

`public bool IsValidData()`

{

```csharp
return
    IsPresent(txtMonthlyInvestment, "Monthly Investment") &&
    IsDecimal(txtMonthlyInvestment, "Monthly Investment") &&
    IsWithinRange(txtMonthlyInvestment, "Monthly Investment", 1, 1000) &&

    IsPresent(txtInterestRate, "Yearly Interest Rate") &&
    IsDecimal(txtInterestRate, "Yearly Interest Rate") &&
    IsWithinRange(txtInterestRate, "Yearly Interest Rate", 1, 20) &&

    IsPresent(txtYears, "Number of Years") &&
    IsInt32(txtYears, "Number of Years") &&
    IsWithinRange(txtYears, "Number of Years", 1, 40);
```

`public bool IsPresent(TextBox textbox, string name)`

{

```csharp
if (textbox.Text == "") {
    MessageBox.Show(name + " is a required field.", "Entry Error");
    textbox.Focus();
    return false;
}
return true;
```

7-12 未来价值应用程序的代码（部分 1，共2 部分）

# 未来价值应用程序的代码

`public bool IsDecimal(TextBox textBox, string name)`

{

```csharp
  try {
    Convert.ToDecimal(textBox.Text);
    return true;
  }
  catch (FormatException ex) {
    MessageBox.Show(name + " must be a decimal value.", "Entry Error");
    textBox.Focus();
    return false;
  }
}
```

`public bool IsInt32(TextBox textBox, string name)`

{

```csharp
  try {
    Convert.ToInt32(textBox.Text);
    return true;
  }
  catch (FormatException ex) {
    MessageBox.Show(name + " must be an integer.", "Entry Error");
    textBox.Focus();
    return false;
  }
}
```

`public bool IsWithinRange(TextBox textBox, string name, decimal min, decimal max)`

{

```csharp
  decimal number = Convert.ToDecimal(textBox.Text);
  if (number < min || number > max) {
    MessageBox.Show(name + " must be between " + min + " and " + max + ".", "Entry Error");
    textBox.Focus();
    return false;
  }
  return true;
}
```

`private decimal CalculateFutureValue(decimal monthlyInvestment, decimal monthlyInterestRate, int months)`

{

```csharp
  decimal futureValue = 0;
  for (int i = 0; i < months; i++) {
    futureValue = (futureValue + monthlyInvestment) * (1 + monthlyInterestRate);
  }
  return futureValue;
}
```

图 7-12 未来价值应用程序的代码（部分 2，共2 部分）

# 观点

在本章中，你学习了如何处理异常和验证数据，以便能够编写“无懈可击”的应用程序。这意味着无论用户输入什么数据或用户如何与用户界面交互，你的应用程序都不会抛出未处理的异常。这是任何专业应用程序的基本功能。

但 C# 语言还有很多你需要的学习的内容。因此在第 8 章中，你将学习如何使用数组和集合。在第 9 章中，你将学习如何处理日期，并学习更多字符串的操作。在第 10 章中，你将学习如何开发使用其他类型控件表单。完成这些章节后，你将能够开发出相当复杂的应用程序。

## 术语

- 异常 `exception`

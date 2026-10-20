

# 具有三个无效字段的未来价值表单

![](img/844f608d10a44654833ea5efc8a2e7a7_240_0.png)

# 显示错误的对话框

![](img/844f608d10a44654833ea5efc8a2e7a7_240_1.png)

# 未预期异常的对话框

![](img/844f608d10a44654833ea5efc8a2e7a7_240_2.png)

# 描述

- 如果用户输入无效数据，例如无效的小数或整数值，或超出应用程序指定范围的值，则会显示第一个对话框。
- 如果发生未预期的异常，则会显示第二个对话框。

# 未来价值应用程序的代码

```
private void btnCalculate_Click(object sender, EventArgs e)
{
    try
    {
        if (IsValidData())
        {
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
    }
    catch(Exception ex)
    {
        MessageBox.Show(ex.Message + "\n\n" +
            ex.GetType().ToString() + "\n" +
            ex.StackTrace, "Exception");
    }
}

private bool IsValidData()
{
    bool success = true;
    string errorMessage = "";

    errorMessage += IsDecimal(txtMonthlyInvestment.Text,
        txtMonthlyInvestment.Tag.ToString());
    errorMessage += IsWithinRange(txtMonthlyInvestment.Text,
        txtMonthlyInvestment.Tag.ToString(),
        1, 1000);

    errorMessage += IsDecimal(txtInterestRate.Text,
        txtInterestRate.Tag.ToString());
    errorMessage += IsWithinRange(txtInterestRate.Text,
        txtInterestRate.Tag.ToString(), 1, 20);

    errorMessage += IsInt32(txtYears.Text, txtYears.Tag.ToString());
    errorMessage += IsWithinRange(txtYears.Text, txtYears.Tag.ToString(),
        1, 40);

    if (errorMessage != "")
    {
        success = false;
        MessageBox.Show(errorMessage, "Entry Error");
    }
    return success;
}
```

图 7-12    未来价值应用程序的代码（第 1 部分，共 2 部分）

# 未来价值应用程序的代码

```csharp
private string IsDecimal(string value, string name)
{
    string msg = "";
    if (!Decimal.TryParse(value, out _))
    {
        msg += name + " must be a valid decimal value.\n";
    }
    return msg;
}

private string IsInt32(string value, string name)
{
    string msg = "";
    if (!Int32.TryParse(value, out _))
    {
        msg += name + " must be a valid integer value.\n";
    }
    return msg;
}

private string IsWithinRange(string value, string name, decimal min, decimal max)
{
    string msg = "";
    if (Decimal.TryParse(value, out decimal number))
    {
        if (number < min || number > max)
        {
            msg += name + " must be between " + min + " and " + max + ".\n";
        }
    }
    return msg;
}

private decimal CalculateFutureValue(decimal monthlyInvestment, decimal monthlyInterestRate, int months)
{
    decimal futureValue = 0m;
    for (int i = 0; i < months; i++)
    {
        futureValue = (futureValue + monthlyInvestment) * (1 + monthlyInterestRate);
    }
    return futureValue;
}
```

# 展望

在本章中，你学习了如何处理异常并验证数据，以便编写“防弹”的应用程序。这意味着无论用户输入什么数据或如何使用用户界面，你的应用程序都不会抛出未处理的异常。这是任何专业应用程序的基本功能。

但你对 C# 语言还有很多东西需要学习。因此，在第 8 章中，你将学习如何使用数组和集合。在第 9 章中，你将学习如何使用日期，并将学习更多关于使用字符串的知识。而在第 10 章中，你将学习如何开发使用其他类型控件的窗体。当你完成这些章节后，你将能够开发相当复杂的应用程序。

# 术语

- exception
- throw an exception
- catch an exception
- exception handling
- subclass
- structured exception handling
- try-catch statement
- exception handler
- try block
- catch block
- stack trace
- finally block
- throw statement
- data validation
- range checking

# 练习 7-1 增强 Invoice Total 应用程序

本练习指导你完成增强 Invoice Total 应用程序的过程，使其捕获任何运行时错误并验证 Subtotal 输入。

- 1. 打开位于 C:\C#\Chapter 07\InvoiceTotal 目录中的应用程序。这是你在第 4 章中工作的版本。
- 2. 向 btnCalculate_Click() 方法添加一个 try-catch 语句，以便捕获 Convert 类的 ToDecimal() 方法可能抛出的任何异常。catch 块应显示如图 7-2 所示的对话框。然后，测试应用程序以确保其正确工作。
- 3. 在 try 块中添加代码以检查用户是否在 Subtotal 文本框中输入了值。如果未输入值，则应显示一个对话框，其中包含一条消息，指出 Subtotal 是必填字段。然后，测试此增强功能。
- 4. 在 try 块中添加代码以对用户输入进行范围检查，使其大于零且小于 10,000。如果不是，则应显示一个对话框，指定可接受的范围。然后，测试此增强功能。当你确信应用程序工作正确时，关闭它。

# 练习 7-2 增强 Future Value 应用程序

本练习指导你完成增强你在第 6 章中工作的 Future Value 应用程序的过程。

- 1. 打开位于 C:\C#Chapter 07\FutureValue 目录中的应用程序。
- 2. 向 btnCalculate_Click() 方法添加一个 try-catch 语句以捕获和处理可能发生的任何 FormatException 或 OverflowException。这些 catch 块应显示适当的对话框消息。然后，测试这些增强功能。
- 3. 向 try-catch 语句添加另一个 catch 块以捕获可能发生的任何其他异常。此 catch 块应显示一个对话框，其中显示异常对象中包含的消息，以及异常类型和堆栈跟踪。
- 4. 在 CalculateFutureValue() 方法的 return 语句之前添加一个 throw 语句，无论计算结果如何，都抛出 Exception 类的新异常。此语句将用于测试步骤 3 的增强功能，并且应指定一条通用消息，指出未知错误。然后，通过在三个文本框中输入有效值并单击 Calculate 按钮来测试应用程序。如果抛出异常并且最后一个 catch 块正常工作，则结束应用程序并注释掉 throw 语句。
- 5. 编写三个名为 IsDecimal()、IsInt32() 和 IsWithinRange() 的通用验证方法，以测试文本框是否包含有效的小数值、有效的 int 值以及在给定范围内的值。如果验证不成功，每个方法都应返回一条错误消息，其中包含正在验证的文本框的名称。如果你在编写这些方法时需要帮助，可以参考图 7-9。
- 6. 编写一个 IsValidData() 方法，该方法调用你在步骤 5 中创建的三个通用方法来验证用户输入到三个文本框中的数据。每个文本框应测试两种类型的无效数据：（1）无效格式和（2）无效范围。如果发生任何错误，应显示一个对话框，其中包含这些错误。另请确保此方法返回一个布尔值，指示验证是否成功。
- 7. 修改 Calculate 按钮事件处理程序中的代码，以便在处理数据之前使用 IsValidData() 方法验证数据。然后，测试应用程序以确保其正常工作。如果正常工作，则结束应用程序并注释掉 FormatException 和 OverflowException catch 块，因为这些异常现在已通过数据验证防止。
- 8. 对应用程序进行最终测试，然后关闭它。


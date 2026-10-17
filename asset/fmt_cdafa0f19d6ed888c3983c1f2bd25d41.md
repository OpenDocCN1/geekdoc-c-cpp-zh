
此图中的 `try-catch` 语句显示了你可能如何捕获 `Invoice Total` 应用程序中四个语句之一抛出的任何异常。例如，如果用户在 `Subtotal` 文本框中输入非数字值，`Convert` 类的 `Decimal` 方法将抛出异常。然后，应用程序将跳转到 `catch` 块，跳过 `try` 块中所有剩余语句。在这种情况下，`catch` 块只需显示一个对话框通知用户该问题。然后，用户可以点击 OK 按钮并输入有效数字。

# 第 7 章 如何处理异常和验证数据 191

## 简单 try-catch 语句的语法

```
try {
    statements }
catch {
    statements
}
```

## 一个 try-catch 语句

```
try {
    decimal subtotal = Convert.ToDecimal(txtSubtotal.Text);
    decimal discountPercent = .2m;
    decimal discountAmount = subtotal * discountPercent;
    decimal invoiceTotal = subtotal - discountAmount;
}
```

## 发生异常时显示的对话框

![](img/3148667e42d4db35b3d08576aaa1fa01_210_0.png)

### 描述

- 你可以使用 `try-catch` 语句编写一个异常处理器，用以捕获并处理抛出的任何异常。
- 你可以在任何可能抛出异常的语句周围编写一个 `try` 块。然后，你可以编写一个 `catch` 块，其中包含当 `try` 块中发生异常时执行的语句。

图 7-3 如何捕获异常

# 如何使用异常的属性和方法

由于异常是一个对象，因此它具有属性和方法。如果你想在捕获异常的 `catch` 块中使用异常的属性或方法，你必须为异常提供一个名称，如图 7-4 所示。为了实现这一点，你在 `catch` 关键字后面编写一组括号。在这些括号内，你编写异常类的名称，然后是异常的名称。

如果你在事件处理器中编写 `try-catch` 语句，你不能使用 `e` 作为异常的名称。默认情况下，事件处理器已将此名称用于其 `EventArgs` 参数。因此，你必须指定另一个名称，如 `x` 或 `e`。或者，你必须将 `EventArgs` 参数的名称从 `e` 改为其他。

一旦为异常指定了名称，就可以使用 `Message` 属性获取错误的简短描述。你还可以使用 `GetType` 方法获取创建异常对象的类型。然后，为了获取类型的名称，可以使用 `ToString` 方法，如此图示例所示。最后，你可以使用 `StackTrace` 属性获取一个表示堆栈跟踪的字符串。

堆栈跟踪是异常发生之前被调用的方法列表。这些方法按照调用顺序的反序进行列出。因此，第一个调用的方法最后显示。例如，此图中的对话框显示 `Invoice Total` 方法中的 `btnCalculate_Click` 方法的第 24 行调用了 `Decimal` 类的 `Parse` 方法。以此此类推。

当你使用异常的属性和方法获取有关异常的信息时，可以将这些信息显示在对话框中。这样，如果抛出了异常，你的用户就能为你提供有关问题的信息。或者，如果发生了阻止程序继续的严重异常，你可以将异常信息写入日志文件，以便监控和审查这些异常。你将在第 21 章中学习如何向文件写入数据。

# 第 7 章 如何处理异常和验证数据 193

## 访问异常的 try-catch 语句语法

```
try { statements }
catch (Exception) { statements }
```

## 所有异常的两个常用属性

| 属性 | 描述 |
| :--- | :--- |
| `Message` | 简要描述异常的消息。 |
| `StackTrace` | 列出异常发生之前的调用方法的字符串。 |

## 所有异常的通用方法

| 方法 | 描述 |
| :--- | :--- |
| `GetType()` | 获取异常的类型。 |

## 访问异常的 try-catch 语句

## 发生异常时显示的对话框

![](img/3148667e42d4db35b3d08576aaa1fa01_212_0.png)

### 描述

- 如果你想在 `catch` 块中使用异常的属性或方法，你必须为异常提供一个名称。
- 堆栈跟踪是异常发生之前被调用的方法列表。列表按反序排列，从最后一次调用到第一次。

### 注意

- 如果在事件处理器中编写 `try-catch` 语句，你不能使用 `e` 作为异常的名称，因为它已用于参数。

图 7-4 如何使用异常的属性和方法

# 如何捕获特定类型的异常

在某些情况下，`try-catch` 语句的 `try` 块中的语句可能会抛出多种异常。这时，你可能希望以不同的方式处理每种异常。你可以像图 7-5 所示编写 catch 块。在这里，第一个 `catch` 块捕获 `FormatException`，第二个 `catch` 块捕获 `OverflowException`，第三个 `catch` 块捕获任何其他。

当你捕获异常时，应该意识到必须先编写最具体的异常的 `catch` 块，再编写不具体的异常的 `catch` 块。例如在此图中，`FormatException` 类型和 `OverflowException` 类型都比 `Exception` 类型更具体。因此，你的 `catch` 块必须在 `Exception` 类型的 `catch` 块之前。如果将它们写在 `Exception` 类型的 `catch` 块之后，编译项目时将得到生成错误。这是因为 `catch` 块按顺序求值，这意味着 `Exception` 的 `catch` 块将捕获发生的任何异常。

虽然你必须在 `Exception` 类型的 `catch` 块之前编写 `FormatException` 和 `OverflowException` 的 `catch` 块，但你不需要在 `FormatException` 类型之前编写 `OverflowException` 类型的 `catch` 块。这是因为 `OverflowException` 类是 `ArithmeticException` 类的子类，而不是 `FormatException` 类。换言之，从不具体到具体的异常规则仅适用于基于同一类的子类之间。

## try-catch 语句的完整语法

```
try { statements }
  catch(MostSpecificException [exceptionName]) { statements }...
  catch(NextMostSpecificException [exceptionName]) { statements }...
  catch(LeastSpecificException [exceptionName]) { statements }
  finally { statements }
```

## 捕获特定异常的 try-catch 语句

```cs
try {
  decimal monthlyInvestment =
    Convert.ToDecimal(txtMonthlyInvestment.Text);
  decimal yearlyInterestRate =
    Convert.ToDecimal(txtInterestRate.Text);
  int years = Convert.ToInt32(txtYears.Text);
} catch (FormatException) // 特定异常 {
  MessageBox.Show(
    "发生了格式异常。请检查所有条目。",
    "输入错误");
} catch (OverflowException) // 另一个特定异常 {
  MessageBox.Show(
    "发生了溢出异常。请输入较小的值。",
    "输入错误");
} catch (Exception ex) // 所有其他异常 {
  MessageBox.Show(ex.Message, ex.GetType().ToString());
} finally // 无论是否发生异常，此代码都会执行 {
  PerformCleanup();
}
```

### 描述

- 你可以为 `try` 块中可能发生的每种异常编写一个代码块。如果你编写了多个 `catch` 块，则必须先编写针对特定类型异常的 `catch` 块。
- 由于所有异常都是 `Exception` 类的子类，因此 `Exception` 类的 `catch` 块可以捕获所有类型的异常。
- 你可以在所有 `catch` 块之后编写一个 `finally` 块。该块中的代码无论是否发生异常都会被执行。它通常用于释放任何系统资源。

图 7-5 如何捕获特定类型的异常

# 如何抛出异常

现在你已经学习了如何捕获异常，准备好学习如何从你编写的方法抛出异常了。要做到这一点，可以使用如图 7-6 所示的 `throw` 语句。如你所示，可以使用该语句抛出一个新异常或抛出一个现有异常。

要抛出一个新异常，你需要编写 `throw` 关键字，后面跟着 `new` 关键字以及想要创建异常的异常类名。（正如你将在本书的后后部分看到的，`new` 关键字是从类创建对象的关键字。）当你这样做时，还可以提供一个字符串来提供异常的简要描述。该参数被赋值给异常的 `Message` 属性。

`throw` 语句的使用在第一个示例中说明。在这里，`CalculateFutureValue` 方法在执行计算之前会检查计算中使用的值是否小于或等于零。如果是，则会抛出一个异常。通常情况下，只有在发生真正的异常情况时才抛出异常。在第一个示例中，`CalculateFutureValue` 方法接收到负数时无法执行计算。处理这种情况的另一种方法是返回一个负值（如 -1）来指示无法计算。然而，抛出异常允许你提供异常情况的描述，这对于可能想要使用此项的程序员通常非常有帮助。

你还可以使用 `throw` 语句来测试异常处理程序，如图2所示。在这里，`throw` 语句被编写在 `try-catch` 语句的 `try` 块中。然后当执行该语句时，就会执行 `catch` 块中的代码，这样你可以确保它工作正常。

如果你需要捕获现有异常，第三个示例将很有用。这种技术执行部分处理异常的操作，然后再次抛出异常，以便另一个异常处理程序可以完成异常的处理。在这种情况下，用户输入了一个不是有效小数的值，会抛出 `FormatException`。然后，`catch` 块捕获异常，将焦点移到文本框并重新抛出异常。这样，调用方法也可以捕获异常并执行某些处理。

## 如何处理异常和验证数据

### 抛出新异常的语法

```cs
throw new Exception([message]);
```

### 抛出现有异常的语法

```cs
throw exceptionName;
```

### 当发生条件时抛出异常的方法

```cs
private decimal CalculateFutureValue(decimal monthlyInvestment, decimal monthlyInterestRate, int months)
{
    if (monthlyInvestment <= 0)
        throw new Exception("每月投资额必须大于 0.");
    if (monthlyInterestRate <= 0)
        throw new Exception("利率必须大于 0.");
}
```

### 用于测试目的的抛出异常的代码

```cs
try {
    decimal subtotal = Convert.ToDecimal(txtSubtotal.Text);
    throw new Exception("发生了未知异常。");
} catch (Exception ex) {
    MessageBox.Show(ex.Message + "\n\n"
        + ex.GetType().ToString() + "\n"
        + ex.StackTrace, "异常");
}
```

### 重新抛出异常的代码

```cs
try {
    Convert.ToDecimal(txtSubtotal.Text);
} catch (FormatException fe) {
    txtSubtotal.Focus();
    throw fe;
}
```

## 何时抛出异常

- 当方法遇到无法完成任务的情况时。
- 当你想生成异常来测试异常处理程序时。
- 当你想捕获异常、执行某些处理，然后再次抛出异常时。

### 描述

- 你可以使用该语句抛出新异常或现有异常。当你创建一个新异常时，可以指定一个赋值给 `Message` 属性的字符串。

图 7-6 如何抛出异常

# 带有异常的未来价值应用程序

图 7-7 展示了你在上一章看到的未来价值应用程序的改进版本。如你所示，此版本使用结构化异常处理来捕获用户点击表单上的“计算”按钮时可能抛出的任何异常。

为了捕获异常，`btnCalculate_Click` 方法的所有语句都编写在 `try` 块中。然后，第一个 `catch` 块处理用户在其中一个文本框中输入无效数字格式数据时抛出的任何异常。接下来，第二个 `catch` 块处理用户输入过大数字时抛出的任何溢出异常。如果抛出了其中任何一个异常，`catch` 块中的代码将显示一个描述异常并指示用户可以采取的纠正措施的对话框。

虽然前两个 `catch` 块捕获特定异常，但第三个 `catch` 块捕获所有其他异常。由于由于这些异常的原因，应用程序使用异常的属性和方法在对话框中显示有关异常的信息。在这种情况下，异常类的名称显示在对话框的标题栏中，异常的简要描述显示在正文中。这样用户就可以向修复此漏洞的人提供有关异常的信息。

注意，此第三个 `catch` 块不能使用 `e` 作为异常名称，因为 `e` 用于 `System.EventArgs` 参数。相反，此 `catch` 块使用 `ex` 作为异常对象的名称。

同样注意，如果在 `CalculateFutureValue` 方法中发生异常，该异常不会被该方法捕获。结果是异常被传递回调用方法，在本例中为 `btnCalculate_Click`。然后，该方法中的相应 `catch` 块将处理该异常。

## 带异常处理的 Future值应用代码

```csharp
private void btnCalculate_Click(object sender, System.EventArgs e)
{
    try
    {
        decimal monthlyInvestment =
            Convert.ToDecimal(txtMonthlyInvestment.Text);
        decimal yearlyInterestRate =
            Convert.ToDecimal(txtInterestRate.Text);
        int years = Convert.ToInt32(txtYears.Text);

        decimal monthlyInterestRate = yearlyInterestRate / 12 / 100;
        int months = years * 12;

        decimal futureValue = this.CalculateFutureValue(
            monthlyInvestment, monthlyInterestRate, months);
        txtFutureValue.Text = futureValue.ToString("c");

        txtMonthlyInvestment.Focus();
    }
    catch (FormatException)
    {
        MessageBox.Show(
            "Invalid numeric format. Please check all entries.",
            "Entry Error");
    }
    catch (OverflowException)
    {
        MessageBox.Show(
            "Overflow error. Please enter smaller values.",
            "Entry Error");
    }
    catch (Exception ex)
    {
        MessageBox.Show(
            ex.Message,
            ex.GetType().ToString());
    }
}
```

```csharp
private decimal CalculateFutureValue(decimal monthlyInvestment,
    decimal monthlyInterestRate, int months)
{
    decimal futureValue = 0;
    for (int i = 0; i < months; i++)
    {
        futureValue = (futureValue + monthlyInvestment
            * (1 + monthlyInterestRate));
    }
    return futureValue;
}
```

# 如何验证数据

每当用户输入数据时，通常需要对这些数据进行检查以确保其有效性。这被称为数据验证。当某个输入无效时，应用程序需要显示错误消息并给用户另一个输入有效数据的机会。这需要一直进行，直到表单上的所有输入都有效为止。

## 如何验证单条输入

当用户向文本框中输入文本时，你可能想要执行几种类型数据验证。特别是，执行图 7-8 所示的三种类型的数据验证是常见的。

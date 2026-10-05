

# try-catch 语句的完整语法

```
try { statements }
  catch(MostSpecificException [exceptionName]) { statements }...
  catch(NextMostSpecificException [exceptionName]) { statements }...
  catch(LeastSpecificException [exceptionName]) { statements }
  finally { statements }
```

# 捕获特定异常的 try-catch 语句

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

# 描述

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

# 如何处理异常和验证数据

## 抛出新异常的语法

```cs
throw new Exception([message]);
```

## 抛出现有异常的语法

```cs
throw exceptionName;
```

## 当发生条件时抛出异常的方法

```cs
private decimal CalculateFutureValue(decimal monthlyInvestment, decimal monthlyInterestRate, int months)
{
    if (monthlyInvestment <= 0)
        throw new Exception("每月投资额必须大于 0.");
    if (monthlyInterestRate <= 0)
        throw new Exception("利率必须大于 0.");
}
```

## 用于测试目的的抛出异常的代码

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

## 重新抛出异常的代码

```cs
try {
    Convert.ToDecimal(txtSubtotal.Text);
} catch (FormatException fe) {
    txtSubtotal.Focus();
    throw fe;
}
```

# 何时抛出异常

- 当方法遇到无法完成任务的情况时。
- 当你想生成异常来测试异常处理程序时。
- 当你想捕获异常、执行某些处理，然后再次抛出异常时。

# 描述

- 你可以使用该语句抛出新异常或现有异常。当你创建一个新异常时，可以指定一个赋值给 `Message` 属性的字符串。

图 7-6 如何抛出异常

# 带有异常的未来价值应用程序

图 7-7 展示了你在上一章看到的未来价值应用程序的改进版本。如你所示，此版本使用结构化异常处理来捕获用户点击表单上的“计算”按钮时可能抛出的任何异常。

为了捕获异常，`btnCalculate_Click` 方法的所有语句都编写在 `try` 块中。然后，第一个 `catch` 块处理用户在其中一个文本框中输入无效数字格式数据时抛出的任何异常。接下来，第二个 `catch` 块处理用户输入过大数字时抛出的任何溢出异常。如果抛出了其中任何一个异常，`catch` 块中的代码将显示一个描述异常并指示用户可以采取的纠正措施的对话框。

虽然前两个 `catch` 块捕获特定异常，但第三个 `catch` 块捕获所有其他异常。由于由于这些异常的原因，应用程序使用异常的属性和方法在对话框中显示有关异常的信息。在这种情况下，异常类的名称显示在对话框的标题栏中，异常的简要描述显示在正文中。这样用户就可以向修复此漏洞的人提供有关异常的信息。

注意，此第三个 `catch` 块不能使用 `e` 作为异常名称，因为 `e` 用于 `System.EventArgs` 参数。相反，此 `catch` 块使用 `ex` 作为异常对象的名称。

同样注意，如果在 `CalculateFutureValue` 方法中发生异常，该异常不会被该方法捕获。结果是异常被传递回调用方法，在本例中为 `btnCalculate_Click`。然后，该方法中的相应 `catch` 块将处理该异常。


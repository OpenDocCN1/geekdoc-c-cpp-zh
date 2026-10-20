

## 访问异常的 try-catch 语句语法

```
try { statements }
catch(ExceptionClass exceptionName) { statements }
```

## 所有异常的两个常见属性

| 属性 | 描述 |
|---|---|
| Message | 获取简要描述当前异常的消息。 |
| StackTrace | 获取一个字符串，其中列出了在异常发生前所调用的方法。 |

## 所有异常的一个常见方法

| 方法 | 描述 |
|---|---|
| GetType() | 获取当前异常的类型。 |

## 访问异常的 try-catch 语句

```
try
{
    decimal subtotal = Convert.ToDecimal(txtSubtotal.Text);
}
catch(Exception ex)
{
    MessageBox.Show(ex.Message + "\n\n" + ex.GetType().ToString() + "\n" + ex.StackTrace, "Exception");
}
```

## 如果发生异常时显示的对话框

![](img/844f608d10a44654833ea5efc8a2e7a7_226_0.png)

## 描述

- 如果你想在 catch 块中使用异常的属性或方法，你必须为异常提供一个名称。
- 堆栈跟踪是异常发生前所调用的方法列表。该列表按相反顺序显示，从最后调用的方法到第一个调用的方法。

## 注意

- 如果你正在事件处理程序内编写 try-catch 语句，你不能使用 e 作为异常的名称，因为它被用作处理程序参数的名称。

## 如何捕获特定类型的异常

在某些情况下，try-catch 语句的 try 块中的语句可能会抛出不止一种类型的异常。然后，你可能希望对每种异常进行不同的处理。为此，你可以像图 7-5 所示那样编写 catch 块。在这里，第一个 catch 块捕获 FormatException，第二个 catch 块捕获 OverflowException，第三个 catch 块捕获任何其他异常。

当你捕获特定异常时，你应该意识到你必须首先为类层次结构中最具体的异常编写 catch 块，并且必须最后为最不具体的异常编写 catch 块。例如，在此图中，FormatException 类型和 OverflowException 类型都比 Exception 类型更具体。因此，它们的 catch 块必须在 Exception 类型的 catch 块之前编写。如果它们在 Exception 类型之后编写，你在尝试编译项目时会收到构建错误。这是因为 catch 块按顺序进行评估，这意味着 Exception 类型的 catch 块会捕获发生的任何异常。换句话说，其他 catch 块永远不会被执行。

尽管你必须在 Exception 类型的 catch 块之前为 FormatException 和 OverflowException 类型编写 catch 块，但你不必在 OverflowException 类型之前编写 FormatException 类型的 catch 块。这是因为 OverflowException 类是 ArithmeticException 类的子类，而不是 FormatException 类。换句话说，最不具体到最具体异常的规则仅适用于基于同一类的子类。

当你编写 try-catch 语句时，你可能会发现你有一些无论是否抛出异常或抛出何种类型的异常都应运行的代码。例如，如果你的应用程序使用数据库连接等系统资源，通常会执行一些清理代码以在不再需要时释放这些资源。不要将此代码包含在 try 块和每个 catch 块中，你可以将其编写在 finally 块中。然后，此代码在 try 块中的所有语句执行后执行。或者，如果抛出异常，则在 catch 块中的语句执行后执行。这允许你将清理代码存储在一个位置而不是多个位置，从而使代码更易于阅读和维护。

## 捕获特定类型异常的 try-catch 语句语法

```
```csharp
try { statements }
[catch(MostSpecificException [exceptionName]) { statements } ]...
[catch(NextMostSpecificException [exceptionName]) { statements } ]...
[catch([LeastSpecificException [exceptionName]]) { statements }]
[finally { statements }]
```
```

## 捕获两种特定异常的 try-catch 语句

```
```csharp
try
{
    decimal monthlyInvestment =
        Convert.ToDecimal(txtMonthlyInvestment.Text);
    decimal yearlyInterestRate =
        Convert.ToDecimal(txtInterestRate.Text);
    int years = Convert.ToInt32(txtYears.Text);
}
catch(FormatException)        // a specific exception
{
    MessageBox.Show(
        "A format exception has occurred. Please check all entries.",
        "Entry Error");
}
catch(OverflowException)      // another specific exception
{
    MessageBox.Show(
        "An overflow exception has occurred. Please enter smaller values.",
        "Entry Error");
}
catch(Exception ex)           // all other exceptions
{
    MessageBox.Show(ex.Message, ex.GetType().ToString());
}
finally      // this code runs whether or not an exception occurs
{
    PerformCleanup();
}
```
```

## 描述

- 你可以为 try 块中可能发生的每种异常类型编写一个 catch 块。如果你编写多个 catch 块，你必须首先为最具体的异常类型编写 catch 块。
- 由于所有异常都是 Exception 类的子类，因此 Exception 类的 catch 块会捕获所有类型的异常。
- 你可以在所有 catch 块之后编写一个 *finally* 块。此块中的代码无论是否发生异常都会被执行。它通常用于释放任何系统资源。

![](img/844f608d10a44654833ea5efc8a2e7a7_228_0.png)

## 如何抛出异常

现在你已经学会了如何捕获异常，你就可以学习如何从你编写的方法中抛出异常。为此，你可以使用图 7-6 所示的 throw 语句。正如你所见，你可以使用此语句抛出新异常或抛出现有异常。

要抛出新异常，你编写 throw 关键字，后跟 new 关键字和你想要从中创建异常的异常类名。（正如你将在本书后面看到的那样，new 关键字是用于从类创建对象的关键字。）这样做时，你还可以提供一个字符串参数，提供异常的简要描述。此参数分配给异常的 Message 属性。然后，当你处理异常时，你可以使用 Message 属性获取此字符串。

throw 语句的这种用法在该图的第一个示例中进行了说明。在这里，在执行计算之前，CalculateFutureValue() 方法会检查用于计算的值是否小于或等于零。如果是，则从 Exception 类创建的异常将被抛出。这里显示的两个 throw 语句都包含一个简要描述异常原因的字符串。

通常，你只有在真正出现异常情况时才应抛出异常。在第一个示例中，当 CalculateFutureValue() 方法接收到负数时，无法执行计算。因此，这是一个异常情况，抛出异常是有意义的。处理这种情况的另一种方法是返回一个负小数（例如 -1.0m）来指示无法执行计算。然而，抛出异常允许你提供异常情况的描述，这通常对可能想要使用此方法的其他程序员有帮助。

你也可以使用 throw 语句来测试异常处理例程，如第二个示例所示。在这里，throw 语句在 try-catch 语句的 try 块内编写。然后，当执行此语句时，catch 块内的代码将被执行，以便你可以确保其正常工作。

该图的第三个示例展示了如何抛出现有异常。如果需要捕获异常、执行部分处理异常的处理，然后再次抛出异常以便另一个异常处理程序可以完成处理异常，则此技术很有用。在这种情况下，ToDecimal() 方法在 try 块内使用，将用户输入到文本框中的值转换为十进制。如果用户输入的值不是有效的十进制数，则会抛出 FormatException。然后，catch 块捕获此异常，将焦点移至文本框，并重新抛出异常。这样，调用方法也可以捕获异常并执行一些额外的处理。

使用 C# 7.0，你还可以使用 throw 表达式抛出异常。throw 表达式与 throw 语句的写法相同，但可以在 throw 语句无法使用的某些上下文中使用。例如，它们可以在空合并表达式中使用，如该图的最后一个示例所示。它们也可以在你学过的条件表达式中使用


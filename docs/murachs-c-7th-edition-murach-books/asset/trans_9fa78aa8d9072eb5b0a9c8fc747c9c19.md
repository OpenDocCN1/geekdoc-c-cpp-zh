

## 增强的发票总额表单

![](img/844f608d10a44654833ea5efc8a2e7a7_170_0.png)

### Calculate 按钮的 Click 事件处理程序

```
private void btnCalculate_Click(object sender, EventArgs e)
{
    string customerType = txtCustomerType.Text;
    decimal subtotal = Convert.ToDecimal(txtSubtotal.Text);
    decimal discountPercent = .0m;

    if (customerType == "R")
    {
        if (subtotal < 100)
            discountPercent = .0m;
        else if (subtotal >= 100 && subtotal < 250)
            discountPercent = .1m;
        else if (subtotal >= 250)
            discountPercent = .25m;
    }
    else if (customerType == "C")
    {
        if (subtotal < 250)
            discountPercent = .2m;
        else
            discountPercent = .3m;
    }
    else
    {
        discountPercent = .4m;
    }

    decimal discountAmount = subtotal * discountPercent;
    decimal invoiceTotal = subtotal - discountAmount;

    txtDiscountPercent.Text = discountPercent.ToString("p1");
    txtDiscountAmount.Text = discountAmount.ToString("c");
    txtTotal.Text = invoiceTotal.ToString("c");

    txtCustomerType.Focus();
}
```

## 如何编写循环

C# 提供了三种不同的语句来控制循环的执行。这些语句提供了迭代结构的 C# 实现。

### 如何编写 while 和 do-while 循环

图 5-8 显示了如何使用 while 语句和 do-while 语句来编写 while 循环和 do-while 循环。这两种循环的区别在于，布尔表达式是在 while 循环开始时求值，而在 do-while 循环结束时求值。因此，while 循环中的语句执行零次或多次，而 do-while 循环中的语句至少执行一次。

编写 while 循环时，通常使用计数器变量来使循环中的语句执行特定次数。这在该图的第一个示例中有所说明。这里，计数器变量是一个名为 i 的 int 类型，该计数器被初始化为 1。请注意，循环中的最后一行语句在每次循环迭代时递增计数器。因此，只要计数器变量小于 5，该循环中的第一条语句就会被执行。顺便说一下，将计数器变量命名为 i、j 和 k 等单个字母是一种常见的编码实践。

大多数情况下，你可以使用这两种类型的循环来完成相同的任务。例如，该图的第二个示例使用 while 循环来计算一系列按月付款在指定利率下的未来价值，而第三个示例使用 do-while 循环执行相同的计算。

编写循环时，重要的是要记住，在循环内声明的任何变量都具有块作用域，因此不能在循环外使用。这就是为什么这里显示的所有循环中使用的变量都在循环外部声明的原因。这样，在循环执行完毕后，你就可以使用这些变量。

编写循环时，可能会编写无限循环，即永远不会结束的循环。例如，如果你忘记编写递增计数器变量的语句，那么 while 或 do-while 循环中的条件永远不会变为 false，就会发生这种情况。然后，你可以切换到 Visual Studio 并单击 Debug 工具栏上的 Break All 按钮进入中断模式并调试程序，如本章后面所示。或者，你可以单击 Stop Debugging 按钮来结束应用程序。

### while 语句的语法

```
while (booleanExpression)
{
    statements
}
```

一个将 1 到 4 的数字相加的 while 循环

```
int i = 1, sum = 0;
while (i < 5)
{
    sum += i;
    i++;
}
```

一个计算未来值的 while 循环

```
int i = 1;
while (i <= months)
{
    futureValue = (futureValue + monthlyPayment) * (1 + monthlyInterestRate);
    i++;
}
```

### do-while 语句的语法

```
do
{
    statements
}
while (booleanExpression);
```

一个计算未来值的 do-while 循环

```
int i = 1;
do
{
    futureValue = (futureValue + monthlyPayment) * (1 + monthlyInterestRate);
    i++;
}
while (i <= months);
```

### 描述

- 当你使用 while 语句时，条件会在 while 循环执行之前进行测试。当你使用 do-while 语句时，条件会在 do-while 循环执行之后进行测试。
- while 或 do-while 循环只要其布尔表达式为 true，就会执行其大括号内的语句块。
- 如果循环需要多条语句，你必须用大括号将语句括起来。然后，在块中声明的任何变量或常量都具有块作用域。如果循环只需要一条语句，则不必用大括号括住该语句。
- 如果条件表达式永远不会变为 false，循环就永远不会结束。然后，程序进入无限循环，你可以通过 Debug 工具栏上的 Break All 或 Stop Debugging 命令来取消该循环。

![](img/844f608d10a44654833ea5efc8a2e7a7_172_0.png)

### 如何编写 for 循环

图 5-9 显示了如何使用 for 语句编写 for 循环。当你需要递增或递减决定循环执行次数的计数器变量时，此类循环很有用。

要编写 for 循环，你首先编写 for 关键字，然后编写用括号括起来并用分号分隔的三个表达式。第一个表达式是初始化表达式，通常声明一个计数器变量并为其分配一个起始值。第二个表达式是布尔表达式，指定循环执行的条件。第三个表达式是递增表达式，确定每次执行循环时计数器变量如何递增或递减。

该图的第一个示例说明了如何使用这些表达式。这里，初始化表达式声明了一个名为 i 的计数器变量，其类型为 int，并为其分配初始值 0。接下来，布尔表达式指定只要计数器小于 5，循环就会重复。然后，递增表达式在每次循环重复结束时将 1 加到计数器上。执行此循环时，数字 0 到 4 将像这样存储为字符串变量：

```
0 1 2 3 4
```

该图显示了如何使用单条语句或语句块编写此循环。如果在循环内编写多条语句，则必须用大括号将语句括起来。但如果只编写单条语句，则大括号是可选的。

下一个示例计算数字 8、6、4 和 2 的总和。在此示例中，sum 变量在循环之前声明，以便在循环执行的语句块之外可用。然后，初始化表达式将计数器变量初始化为 8，布尔表达式指定只要计数器大于零，循环就会执行，并且递增表达式使用赋值运算符在每次循环重复时从计数器变量中减去 2。在循环内，计数器变量的值会加到已存储在 sum 变量中的值上。因此，sum 变量的最终值为 20。

最后一个示例显示了如何编写计算一系列按月付款未来值的 for 循环。这里，循环每个月执行一次。如果你将此示例与图 5-8 中的最后一个示例进行比较，你可以看到当需要计数器变量时，for 循环如何改进了 while 循环。

尽管本图中未显示，但可以在 for 循环之前声明计数器变量。然后，可以在循环之外访问此变量。但是，如果需要在循环之外访问计数器变量，通常使用图 5-8 中描述的 while 或 do-while 循环会更容易。

你也可以在 for 循环内声明计数器变量而不指定类型。要做到这一点，你用 var 关键字代替类型。然后，类型会根据分配给变量的值推断出来。但在大多数情况下，你会指定类型而不是使用 var 关键字。


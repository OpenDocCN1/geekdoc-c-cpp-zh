
# 发票总额（Invoice Total）应用程序的增强版本

为了让你更好地理解如何使用 if-else 语句，图 5-5 展示了第 3 章介绍的发票总额应用程序的增强版本。这次，应用程序的表单提供了两个用户输入项：客户类型和小计金额。

如果你查看图中的事件处理程序，你会发现折扣是通过嵌套语句确定的。例如，如果客户类型为 R 且小计金额大于等于 250，则折扣百分比为 .25。如果客户类型为 C 且小计金额小于 250，则折扣百分比为 .20。

编写此类语句时，按照逻辑顺序编写条件是一个良好的习惯。例如，针对客户类型 R 的嵌套 if 语句中的表达式范围从：小计小于 100，到小计大于等于 100 且小于 250，再到小计大于等于 250。这涵盖了从最小到最大所有可能的小计金额（subtotal）。虽然你也可以按照其他顺序编写这些条件，但这会让你更难判断是否已经涵盖了所有可能性。

为了效率考虑，从发生频率最高到最低的顺序编写条件也是好的。例如，如果大多数客户都是 R 类型，那么该条件应该被考虑，以便最先处理。不过，在某些情况下，高效的顺序并不符合逻辑，因此你必须决定是否为了效率而牺牲代码的可读性。通常情况下，性能的提升并不显著，因此你大可以按照最符合逻辑的顺序编写语句。

如果你愿意，可以使用 `switch` 语句，其中包含的语句可以获得与图中嵌套 if 语句相同的结果。这甚至可能让代码更易读。另一方面，如果你正确地使用了缩进，大量的嵌套语句也应该是易于阅读和理解的。

在代码编辑器中输入 `if` 和 `switch` 语句时，记住你可以使用代码片段（code snippets）输入所需的各种 `if`、`else` 和 `switch` 结构，包括代码块所需的大括号。如果你想复习如何使用代码片段，可以查阅图 3-11。

## # 增强的发票总额表单

![](img/3148667e42d4db35b3d08576aaa1fa01_164_0.png)

Click(object sender, System.EventArgs e) 的事件处理程序

```csharp
private void btnCalculate_Click(object sender, System.EventArgs e) {
    string customerType = txtCustomerType.Text;
    decimal subtotal = Convert.ToDecimal(txtSubtotal.Text);
    decimal discountPercent = .0m;

    if (subtotal < 100) {
        discountPercent = .0m;
    } else if (subtotal >= 100 && subtotal < 250) {
        discountPercent = .1m;
    } else if (subtotal >= 250) {
        discountPercent = .25m;
    } else if (customerType == "C") {
        if (subtotal < 250) {
            discountPercent = .2m;
        } else {
            discountPercent = .3m;
        }
    } else {
        discountPercent = .4m;
    }

    decimal discountAmount = subtotal * discountPercent;
    decimal invoiceTotal = subtotal - discountAmount;

    txtDiscountPercent.Text = discountPercent.ToString("P");
    txtDiscountAmount.Text = discountAmount.ToString("c");
    txtTotal.Text = invoiceTotal.ToString("c");

    txtCustomerType.Focus();
}
```

图 5-5 增强版的发票总额应用程序

## 如何编写循环

C# 提供了三种不同的语句来控制循环的执行。这些语句提供了迭代结构的 C# 实现。

### 如何编写 while 和 do-while 循环

图 5-6 展示了如何使用 `while` 语句和 `do-while` 语句来编写 `while` 循环和 `do-while` 循环。这两种循环的区别在于：布尔表达式在 `while` 循环开始时评估，而在 `do-while` 循环结束时评估。结果是，`while` 循环中的语句执行零次或多次，而 `do-while` 循环中的语句始终至少执行一次。

在编写循环时，通常使用计数器变量来执行特定次数的循环语句。这在第一个示例中得到了。。这里计数器变量是 `int` 类型，并初始化为 1。注意，循环中的最后一条语句每次迭代时都会增加计数器。顺便说，使用 `i`、`j` 和 `k` 等单字母命名计数器变量是一种常见做法。大多数情况下，你可以使用任何类型的循环完成相同的任务。例如，图中的第二个示例使用 `while` 循环计算指定利率下系列每月付款的未来价值，而第三个示例使用 `do-while` 循环执行相同的计算。（注意：OCR 文本包含重复和碎片化的句子，此处已进行清理）。

### while 语句的语法

```csharp
while (booleanExpression) {
    statements
}
```

### 累加 1 到 4 的数字的 while 循环

```csharp
int i = 1, sum = 0;
while (i < 5) {
    sum += i;
    i++;
}
```

### 计算 1 到 4 数字的 while 循环

```csharp
int i = 1;
while (i < 5) {
    // 假设此处有累加逻辑
    i++;
}
```

### do-while 语句的语法

```csharp
do {
    statements
} while (booleanExpression);
```

### 计算未来值的 do-while 循环

```csharp
int i = 1;
do {
    // 假设此处有计算逻辑
    i++;
} while (i <= 4);
```

### 说明

- 当你使用 `while` 语句时，在循环执行前测试条件。当你使用 `do-while` 语句时，在循环执行后测试条件。
- `while` 循环在布尔表达式为真时执行块；`do-while` 循环在布尔表达式为真时执行块。
- 如果循环需要多条语句，必须用大括号包裹。如果循环只需要一条语句，则不需要大括号。
- 如果条件表达式变为为假，循环将停止。你可以通过调试工具来查看。

![](img/3148667e42d4db35b3d08576aaa1fa01_164_0.png)

## 如何编写 for 循环

图 5-7 展示了如何使用 `for` 语句来编写循环。这种类型的循环在你需要增加或递减计数器变量时非常有用。

要编写 `for` 循环，首先编写 `for` 关键字，后面跟着由分号隔的括号。第一个表达式是初始化表达式，通常声明变量并为其赋值。第二个表达式是布尔表达式，指定循环执行的条件。第三个表达式是增量表达式，决定计数器每次如何变化。

图中的第一个示例说明了如何使用这些表达式。初始化表达式声明了变量 `i` 并赋予其初始值 0。接下来，布尔表达式指定只要 `i` 小于 5 就会重复。然后，增量表达式在每次循环结束时给 `i` 加 1。当此循环执行时，0 到 4 的数字将存储在变量中：

```
0 1 2 3 4
```

图中展示了如何使用单个语句或语句块编写此循环。如果你在循环中编写多条语句，必须使用大括号。但如果你只编写单个语句，大括号是可选的。

下一个示例计算 8、6、4 和 2 的和。在这个示例中，变量在循环之前声明，因此在循环的语句块外部可用。然后，初始化表达式将计数器初始化为 8，布尔表达式指定只要计数器大于 0 就会执行循环，增量表达式在每次循环时从计数器中减 2。在循环内部，计数器变量的值被加到存储在变量中的值。结果是 `sum` 变量的最终值为 20。

最后一个示例展示了如何编写计算系列每月付款未来值的 `for` 循环。在这里，循环每月执行一次。如果你将此示例与图 5-6 中的最后一个示例进行比较，就可以看到在需要计数器变量时 `for` 循环是如何改进 `while` 循环的。

虽然图中没有显示，可以在 `for` 循环之前声明计数器。这样，该变量就可以在循环外部访问。

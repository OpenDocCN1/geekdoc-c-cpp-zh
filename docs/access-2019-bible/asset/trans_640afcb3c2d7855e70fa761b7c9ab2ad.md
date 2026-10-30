

## 第六部分：Microsoft Access 编程基础

### If 关键字

If 关键字可以用几种不同的方式使用，但它们都会检查一个条件，并根据求值结果执行操作。条件必须求值为布尔值（True 或 False）。如果条件为真，程序会移动到 If 语句之后的下一行。如果条件为假，程序会跳到 Else 语句之后的语句，如果存在 Else，则跳到 Else 语句之后的语句；如果没有 Else 子句，则跳到 End If 语句。

### If...Then 结构

If 语句可以采用几种不同的形式。第一种形式是 If...Then 结构。它是一个单行语句，条件和操作都在同一语句中。在下面的示例中，如果 sCity 变量包含某些数据，则会设置 sState 变量：

```
If sCity = "Dallas" Then sState = "Texas"
```

VBA 首先求值 sCity = "Dallas" 并判断条件是否为真或假。如果为真（即 sCity 已被赋值为 Dallas），则执行 Then 关键字之后语句的部分。在本例中，sState 变量被赋值为 Texas。如果条件为假，程序会继续执行过程中的下一行，sState 变量不会改变。

### If...End If 结构

下一个形式是 If...End If 结构。此结构以及后面的结构通常称为 If 块，因为它们可以包含多行代码（代码块），而与只能执行一行的 If...Then 结构不同。之前的示例可以重写为 If...End If：

```
If sCity = "Dallas" Then
    sState = "Texas"
End If
```

此示例与之前的示例完全相同。如果条件语句为真，则会执行 If 块中的单行。不同之处在于条件为假时。在这种情况下，程序会分支到 End If 语句之后的下一行，并继续执行程序。

If...End If 结构的优点是，当条件为真时可以执行多个语句。在下一个示例中，当条件为真时，会为两个变量赋值：

```
If sCity = "Dallas" Then
    sState = "Texas"
    dTaxRate = 0.075
End If
```

如果条件为真，则会执行两个语句。否则，程序会分支到 End If 下方的行并继续执行。

### If...Else...End If 结构

在之前的示例中，当条件为真时会执行一个或多个语句，而当条件为假时什么也不发生。Else 关键字可以包含在 If 块中，以标识当条件为假时应运行的语句：

```
If sCity = "Dallas" Then
    sState = "Texas"
    dTaxRate = 0.075
Else
    sState = "Michigan"
    dTaxRate = 0.05
End If
```

当条件为真时，会执行前两个语句（将 sState 设置为 Texas 并将 dTaxRate 设置为 0.075）。然后程序会分支到 End If 下方的行并继续执行。Else 和 End If 之间的两个语句不会被执行。

如果条件为假，则程序会分支到 Else 语句下方的语句并跳过前两个语句。看到这种结构执行条件满足时的某些代码行以及条件不满足时的其他代码行是很常见的。

你必须使用 If 块才能使用 Else 语句。Else 语句与第一种结构（If...Then 结构）不兼容。

### If...ElseIf...End If 结构

最后一个 If 结构是另一种 If 块类型的结构。不是只有一个条件，而是存在多个条件。ElseIf 语句定义了你需要的任意多个其他条件：

```
If sCity = "Dallas" Then
    sState = "Texas"
    dTaxRate = 0.075
ElseIf sCity = "Detroit" Then
    sState = "Michigan"
    dTaxRate = 0.05
Else
    sState = "Oregon"
    dTaxRate = 0.0625
End If
```

程序通过 If...ElseIf...EndIf 结构的方式与通过其他结构的方式类似。如果第一个条件为真，则执行第一部分中的语句，程序分支到 End If 正下方的一行。如果第一个条件为假，程序会分支到第二个条件（第一个 ElseIf）并测试该条件。如果没有任何条件为真，则执行 Else 部分中的语句。使用 ElseIf 时，Else 语句是可选的。如果省略 Else 语句且没有任何条件为真，则 If 块中不会执行任何语句。

### 嵌套 If 语句

嵌套语句是指将语句放在其他语句的块内。对于 If 来说，嵌套意味着一个 If 块位于另一个 If 块内部：

```
If sState = "Michigan" Then
    If sCity = "Detroit" Then
        dTaxRate = 0.05
    ElseIf sCity = "Kalamazoo" Then
        dTaxRate = 0.045
    Else
        dTaxRate = 0
    End If
End If
```

外部 If 块测试 sState 变量。如果该条件为真，则执行内部 If 块，并测试 sCity 变量。如果外部 If 块中的条件为假，程序会分支到与正在求值的 If 语句匹配的 End If 语句下方的行。适当的缩进虽然不是必需的，但有助于查看哪个 Else 和 End If 语句与哪个 If 语句对应。

### 布尔值和条件

If 语句非常棒，你会在编写的几乎每一段代码中看到它们。然而，有两种情况它们被误用。考虑以下代码片段：

```
If blsBuyer = True Then
    blsInPurchasing = True
Else
    blsInPurchasing = False
End If
```

这是一个简单的 If...Else...End If 结构，其中条件检查布尔变量 blsBuyer 是否为 True。根据该条件的结果，另一个布尔变量被设置为 True 或 False。代码本身没有问题——它可以编译并正常运行——但有一种方法可以简化代码并使其更易读。首先，将布尔变量与 True 或 False 进行比较是不必要的，因为该变量本身就是真或假。第一行可以简化为：

```
If blsBuyer Then
```

假设 blsBuyer 为 True，则在第一个示例中，编译器会求值 blsBuyer = True，这简化为 True = True，当然返回 True。在更简单的示例中，blsBuyer 被求值并返回 True。由于 blsBuyer 是一个布尔变量，将其与布尔值进行比较是多余的。

第二个简化步骤是完全删除 If 语句。每当你在 If 块中设置布尔值时，都应考虑是否可以直接设置该布尔值：

```
blsInPurchasing = blsBuyer
```

这一行代码与我们最初的五行代码做同样的事情。如果 `blsBuyer` 为 True，`blsInPurchasing` 也将为 True。如果 `blsBuyer` 为 False，`blsInPurchasing` 也将为 False。也可能存在需要将一个变量设置为另一个变量相反值的情况。VBA 提供了 Not 关键字来将布尔值从 True 转换为 False，反之亦然：

```
blsInPurchasing = Not blsTruckDriver
```

变量 `blsTruckDriver` 被求值为真或假，Not 关键字返回相反值。如果 `blsTruckDriver` 为 True，`blsInPurchasing` 将被赋值为 False。

当你有许多条件需要测试时，`If...Then...ElseIf...Else` 条件可能会变得相当笨重。更好的方法是使用 Select Case...End Select 结构。

### Select Case...End Select 语句

VBA 提供了 Select Case 语句来检查多个条件。以下是 Select Case 语句的一般语法：

```
Select Case Expression

    Case Value1
        [Action to take when Expression = Value1]

    Case Value2
        [Action to take when Expression = Value2]

    Case ...

    Case Else
        [Default action when no value matches Expression]

End Select
```

请注意，该语法与 `If...Then` 语句的语法类似。不是布尔条件，Select Case 语句在最顶部使用一个表达式。然后，每个 Case 子句将其值与表达式的值进行测试。当 Case 值与表达式匹配时，程序会执行代码块，直到遇到另一个 Case 语句或 End Select 语句。VBA 只会执行一个匹配的 Case 语句的代码。

> **NOTE**
> 
> 如果多个 Case 语句与测试表达式的值匹配，则只有第一个匹配的代码会执行。如果在第一个匹配之后出现其他匹配的 Case 语句，VBA 会忽略它们。


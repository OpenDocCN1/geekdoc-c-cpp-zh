
则求值为 **true**。借助短路求值，计算机一旦知道表达式的值就能停止求值。

C# 还包含 `&` 和 `|` 运算符。它们都会计算操作数的逻辑与或逻辑或，正如 `&&` 和 `||` 所做的那样。它们之间的区别在于：`&&` 和 `||` 进行短路求值，而 `&` 和 `|` 不进行短路求值。它们适用于涉及复合或复杂表达式的情况，在这种情况下，你希望执行整个表达式，而不管条件表达式的结果是否返回 **true**。考虑以下代码：

```csharp
((aValue > bValue) & (count++ < 100))
```

使用逻辑与（`&`）始终会使 count 加 1，无论 aValue 是否大于 bValue。将 `&` 替换为 `&&` 会对整个表达式产生相同的结果；但是，递增 count 的副作用可能不会发生。使用 `&&` 并执行短路求值时，只有当表达式第一部分 `(aValue > bValue)` 求值为 **true** 时，才可能将 count 加 1。使用 `&&` 时，如果 `(aValue > bValue)` 求值为 `false`，则第二个表达式不会执行。

![](img/e33ae760e23d89eac66541252ad65de8_279_0.png)

由于这些符号（`&`、`&&` 和 `||`）在视觉上相似，使用它们可能导致代码难以调试。你可能需要添加注释来解释条件表达式。

考虑示例 5-6 中所示的代码：

### 示例 5-6

```csharp
int    x = 0;
       y = 0;
       z = 0;

if (x > 1 && ++y > 0)
    z += 1;
Console.WriteLine("Y is {0}, Z is {1}", y, z);
```

示例 5-6 的输出为

```text
Y is 0, Z is 0
```

如果将 `&&` 替换为单个与号（`&`），如示例 5-7 所示：

### 示例 5-7

```csharp
if (x > 1 & ++y > 0)
```

变量 `y` 会递增 1，产生如下输出：

```text
Y is 1, Z is 0
```

## 布尔数据类型

声明为 `bool` 类型的变量保存 `true` 或 `false` 值。当在条件表达式中使用 `bool` 变量时，你不必添加符号来将该变量与某个值进行比较。你只需将 `bool` 变量名作为表达式写入即可。例如，以下代码片段声明了一个布尔变量：

```csharp
bool salariedEmployee;
```

声明之后，可以使用条件表达式来确定 `salariedEmployee` 保存的是 `true` 还是 `false` 值。该条件表达式可写为：

```csharp
if (salariedEmployee)
```

不必写成 `if (salariedEmployee == true)`，因为 `salariedEmployee` 被定义为 `bool` 类型。

![](img/e33ae760e23d89eac66541252ad65de8_280_0.png)

测试该标识符是否为 `true` 是可以的。这是有效的，甚至可能更具可读性，尤其是在变量标识符描述性不强的情况下。

### 布尔标志

布尔数据类型通常用作标志，用于在条件存在或条件发生变化时发出信号。要创建标志情形，请声明一个 `bool` 数据类型变量，并将其初始化为 `true` 或 `false`。然后使用该变量控制处理过程。只要布尔变量的值保持不变，处理就继续。当某个计划中的条件发生变化时，更改布尔数据类型的值，处理就会停止。例如，moreData 被声明为布尔变量，初始化为 `true`，但在所有数据处理完毕后可以改为 `false`。

```csharp
bool moreData = true;
:
:
if (moreData)              // Other statement(s) that might change
                           // value of moreData to false.
                           // Execute statement(s) following the if
                           // when moreData is true.
```

到目前为止，你看到的表达式都使用与英文等价的词来表示条件表达式。在接下来的几节中，你将学习用于条件表达式的运算符，并了解如何在 C# 中实现选择语句。

## if...else 选择语句

`if` 选择语句分为单向、双向或嵌套，并与条件表达式结合使用。`if` 语句有助于根据条件表达式的结果指定备用路径。这些表达式可能涉及运行时输入的值或使用数据进行的计算。接下来的几节将说明如何在程序中包含这些类型的选择语句。

### 单向 if 语句

当需要测试某个表达式时，使用**单向选择语句**。当表达式的结果为 **true** 时，执行额外的处理。单向 `if` 语句的一般格式为：

```csharp
if (conditional_expression)
    statement;    // Actions to be performed when the expression
                  // evaluates to true.
```

在 C# 中，表达式必须括在圆括号中。请注意，包含该表达式的那一行末尾没有分号。表达式在求值时必须产生布尔结果——该结果可求值为 `true` 或 `false`。因此，表达式可以是布尔变量，也可以是涉及两个或更多操作数的条件表达式。对于单向 `if` 语句，当表达式求值为 `false` 时，紧跟在条件表达式之后的语句会被跳过或绕过。对于 `false` 结果，不会包含任何特殊语句。执行将继续进行 `if` 语句之后的代码段。

如果表达式求值为 `true`，则执行该语句，然后执行将继续进行 `if` 语句之后的同一代码段，与表达式求值为 `false` 时一样。

在上述语法说明中，`statement` 表示当表达式求值为 `true` 时发生的动作。要将多个语句与 `true` 结果关联起来，请将这些语句括在花括号内。这些语句称为 `true` 语句。通过将 `true` 语句括在花括号内，你标记了当表达式求值为 `true` 时要执行的语句的开始和结束。

考虑示例 5-8。

### 示例 5-8

```csharp
if (examScore > 89)
{
    grade = 'A';
    Console.WriteLine("Congratulations - Great job!");
}
Console.WriteLine("I am displayed, whether the expression "
                + "evaluates true or false");
```

当 `examScore` 等于 89 或任何更小的值时，表达式求值为 `false`，花括号内的 `true` 语句被跳过。执行右花括号之后的 `WriteLine()` 方法。当 `examScore` 等于 95 时，执行 `true` 语句，并执行右花括号之后的 `WriteLine()`。

考虑对示例 5-8 的以下修改：

```csharp
if (examScore > 89)
    grade = 'A';                          // Missing opening curly brace '{'
    Console.WriteLine("Congratulations - Great job!");
                                             // Missing closing curly brace '}'
    Console.WriteLine("I am displayed, whether the expression "
                      + "evaluates true or false");
```

在这里，`Console.WriteLine("Congratulations - Great job!");` 始终会执行。缩进仅为了可读性。如果省略花括号，不会产生语法错误或警告。对于 `examScore` 的所有值（甚至 `examScore` 为零），都会显示祝贺消息。

> **注意** 一些程序员会将与 `if` 语句关联的所有语句都括在花括号中。这包括单行的 `true` 语句。这样，他们就不会忘记用 `{}` 包围主体。作为初学者，鼓励你遵循这一准则。

单向 `if` 语句中的执行流程如图 5-1 所示。当表达式求值为 `true` 时，执行 `true` 语句。如图所示，无论表达式求值为 `true` 还是 `false`，执行都会在同一位置继续。

![](img/e33ae760e23d89eac66541252ad65de8_282_0.png)

**图 5-1** 单向 if 语句

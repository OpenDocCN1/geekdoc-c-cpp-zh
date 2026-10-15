
```
if (Number1>Number2) // condition
{
Console.WriteLine("Number1 is greater than Number2"); //statement
... //statements
}
else
{
Console.WriteLine("Number2 is greater than Number1"); //statement
... //statements
}
```

在前面的代码片段中，当条件（`Number1>Number2`）未得到满足时，程序控制转移到 `else` 块并执行其中的代码块。为了逐一评估多个条件，可以对 `if else` 语句进行嵌套。以下代码片段展示了一个示例以理解嵌套 `if else` 语句的语法：

```
if (Number1 > Number2 && Number1 > Number3) //condition
{
Console.WriteLine("Number1 is greatest"); //statement
... //statements
}
else
if (Number2 > Number3) //condition
{
Console.WriteLine("Number2 is greatest"); //statement
...//statements
}
else
{
Console.WriteLine("Number3 is greatest"); //statement
... //statements
}
```

在前面的代码片段中，首先在 `if` 块中检查一个条件（`Number1 > Number2 && Number1 > Number3`）。如果满足，则执行 `if` 块内的语句；否则，程序控制转移到 `else if` 块并检查另一个条件（`Number2 > Number3`）。如果此条件（`Number2 > Number3`）得到满足，则 `else if` 块内的语句将被执行；否则，程序控制转移到 `else` 块。

## The switch Statement

`switch` 语句是另一种类型的选择语句。`switch` 语句的主要目的是允许变量或表达式的值控制程序执行的流程。变量或表达式通常被称为 `switch` 语句的控制变量。`switch` 语句分为两个主要部分，`switch` 和 `case`。在 `switch` 语句中，`switch` 块内变量的值会与不同的 `case` 表达式进行检查。如果变量的值与其中任何一个 `case` 表达式匹配，则该 `case` 语句内的语句会被执行。

以下代码片段展示了 `switch` 语句的示例：

```
switch (Marks) // test expression
{
case 1: //expression
{
    Console.Write("Your marks are very low");
}
break;
case 2: //expression
{
    Console.Write("Your marks are low");
}
break;
case 3: //expression
{
    Console.Write("Your marks are average");
}
break;
case 4: //expression
{
    Console.Write("Your marks are good");
}
break;
case 5: //expression
{
    Console.Write("Your marks are very good");
}
break;
default:
break;
}
```

前述代码片段中使用的关键字如下：

- `switch` — 表示 `switch` 语句开始的关键字，并在括号内包含测试表达式
- `test expression` — 表示需要与 `case` 表达式进行比较的任何整数表达式，例如 `int` 和 `char`
- `case` — 表示包含冒号（`:`）后跟表达式的关键字
- `expression` — 表示与测试表达式的值进行比较的任何常量值
- `break` — 表示更改 `switch` 语句流程的关键字
- `default` — 表示当其他 `case` 表达式都不与测试表达式匹配时使 `default` 块内的代码执行的关键字

`switch` 语句包含一个测试表达式，例如 `int`、`char` 和 `string`，并将 `case` 与该测试表达式的值进行匹配。程序控制从一个 `case` 流向另一个 `case`。如果 `case` 与指定的测试表达式匹配，程序控制将被转移到该特定 `case` 语句并执行该 `case` 语句内的语句。`switch` 语句中还存在一个可选块，即 `default` case。它不指定任何表达式，而是用 `default` 关键字代替 `case` 关键字表示。如果没有任何 `case` 表达式与测试表达式匹配，程序执行将被转移到 `default` 关键字之后的语句。

## Iteration Statements or Loops

假设你想在程序中执行一组语句 50 次。无需将代码写 50 次，你可以将代码写在循环内并指定一个条件以使循环执行 50 次；从而节省编码中涉及的复杂性和时间。迭代语句或循环以重复的方式执行语句或一组语句。在 C# 中，有以下四种迭代语句：

- `while` loop — 在执行循环之前评估条件。只要指定的条件为真，循环就会继续执行。
- `do...while` loop — 在评估条件之前至少执行一次循环体。
- `for` loop — 直到循环中指定的条件变为 `false`，循环体就会继续执行。
- `foreach` loop — 对数组或对象集合中的每个元素继续执行循环体。

让我们详细讨论这些迭代语句或循环。

### The while Loop

`while` 循环只要布尔表达式（条件）求值为 `true`，就会执行语句或一组语句。`while` 循环主要用于你事先不知道循环将执行多少次的情况。`while` 循环中指定的条件在开始循环之前进行检查，只要指定的条件为真，循环内的语句就会执行。当布尔表达式求值为 `false` 时，循环终止。以下代码片段展示了 `while` 循环的示例：

```
int Number= 51;
while (Number <= 50)    //condition
{
    Console.WriteLine("I will be executed 50 times");    //statement
    Number = Number + 1; //increment or decrement
}
```

在前面的代码片段中，条件是一个布尔表达式，语句可以是任何 C# 语句。在执行 `while` 循环内的任何语句之前，会评估条件。如果条件求值为 `true`，则会执行语句，否则不会。一旦执行了 `while` 循环内的语句，程序控制就会转移到 `while` 循环的起点以再次检查条件以进行下一次迭代。

### The do...while Loop

`do...while` 循环的工作方式与 `while` 循环相同，只是 `do...while` 循环在每次迭代后在循环末尾检查条件。这意味着即使条件为 `false`，`do...while` 循环也肯定至少执行一次。与 `while` 循环不同，在 `do...while` 循环中，必须在 `while` 表达式后放置一个分号；否则，循环将不会执行。

以下代码片段展示了 `do...while` 循环的语法：

```
int Number = 51;
do {
    Console.WriteLine("I will be executed 50 times "); //statement
    Number = Number + 1; //increment or decrement
}
while (Number <= 50) ; //condition
```

在前面的代码片段中，你可以看到 `while` 块内的布尔表达式不是 `true`，但循环执行了一次，因为在 `do...while` 循环中，`while` 块中指定的条件是在执行循环一次后才检查的。

### The for Loop

`for` 循环可能是所有循环中最重要的。它与 `while` 循环类似，只是 `for` 循环的语法还包括一个初始化器，用于初始化变量，以及一个循环表达式，用于递增或递减变量的值。与 `while` 循环不同，`for` 循环适用于你确切知道要执行语句多少次的情况。`for` 循环的语法如下：

```
for ( initializer; condition; loop expression) {
    ...    //statements
}
```

前述语法中使用的术语说明如下：

- `initializer` — 指定循环内使用的变量的初始值。它是在第一次执行循环之前求值的表达式。它通常是对用作循环计数器的局部变量的初始化。
- `condition` — 指定在开始循环的每次新迭代之前检查的表达式。它必须求值为 `true` 才能执行另一次迭代。
- `loop expression` — 指定在结束循环的每次迭代后求值的表达式。你可以用它来递增或递减循环计数器。

以下代码片段展示了 `for` 循环的使用：

```
for (int Number = 1; Number <= 50; Number++) {
    Console.WriteLine("I will be executed 50 times");
}
```

在前面的代码片段中，`Number` 变量被初始化为 1。只要 `Number` 变量的值小于或等于 50，循环就会迭代。每次迭代后，`Number` 变量的值递增 1，并且只要 `for` 循环中指定的条件为 `true`，`for` 循环内部的语句就会执行。

### The foreach Loop

`foreach` 循环遍历列表中的所有项目。列表可以是数组或对象集合。`foreach` 循环的工作方式与 `for` 循环相同。`foreach` 循环的语法如下：

```
foreach(<data_type> <variable_name> in <array_name>) {
    ...       //statements
}
```

语法中使用的术语说明如下：

- `data_type` — 指定变量的数据类型。变量和数组的数据类型必须相同。
- `variable_name` — 表示作为 `array_name` 数组中每个项目值的代表的变量名。
- `in` — 表示在 `variable_name` 变量之后应用的关键字。
- `array_name` — 表示你正在访问的数组或对象集合的名称。

以下代码片段展示了 `foreach` 循环的使用：

```
string[] bookTitles = new string[] { "Alice in Wonderland",
"Pelican Brief",
"Ignited Minds" };
foreach (string i in bookTitles)
{
    ...       //statements
}
```

在前面的代码片段中，定义了一个名为 `bookTitles` 的字符串类型数组，并使用 `foreach` 循环来迭代 `bookTitles` 数组的项目。

如果在一个循环内部存在一个或多个循环，则称为嵌套循环。例如，如果一个 `for` 循环位于另一个 `for` 循环或 `do...while` 循环内部，则称为嵌套循环。你也可以创建一个无限循环，如果你不想终止循环的话。在无限循环中，给出了一个不切实际的终止条件，该条件永远不会满足。

## Jump Statements

跳转语句是允许你在程序执行期间的任何特定时刻将程序控制从一个点移动到另一个点的语句。在 C# 中，有五种类型的跳转语句，分别是：

- `goto` statement — 直接将程序控制转移到带标签的语句。已被赋予某个名称或标签的语句或语句块称为带标签语句。
- `break` statement — 终止其出现的循环。因此，程序控制被转移到 `break` 语句之后的语句。
- `continue` statement — 将程序控制转移到 `continue` 关键字出现的循环的下一次迭代。
- `return` statement — 终止其出现的方法的执行并将控制返回给调用方法。
- `throw` statement — 指定程序执行期间发生异常。

让我们详细讨论重要的跳转语句。

### The goto Statement

`goto` 语句用于将程序控制转移到与 `goto` 语句具有相同标签的语句。具有相同标签的语句称为带标签语句。一个以上的 `goto` 语句可以将程序控制转移到同一个带标签语句。`goto` 语句可以将程序控制转移到控制语句之外；然而，它不能将程序控制转移到控制语句内部，例如 `while` 循环、`do...while` 循环和 `for` 循环。一般来说，不建议使用 `goto` 语句，因为它增加了程序执行的复杂性。然而，它们可以在 `switch` 语句中使用，或者当你想将程序控制转移到嵌套循环之外时使用。以下代码片段展示了 `goto` 语句的示例：

```
if(Number1>Number2)
{
    if(Number1>Number3)
    {
        goto MyLabel; // label
    }
}
MyLabel: //labeled statement
{
    Console.WriteLine("Number1 is greater than Number2");
    ...//Statements
}
```

在前面的代码片段中，你可以看到嵌套 `if` 语句内部的 `goto` 语句（`goto MyLabel;`）将程序控制转移到带标签语句（`MyLabel:`）。

### The break Statement

`break` 语句终止其存在的循环。它还可以改变循环的流程。退出循环后，程序控制被转移到循环之后的下一个语句块。你可以使用 `break` 语句从 `switch` 语句中的 `case` 退出或控制语句，例如 `for`、`foreach`、`while` 或 `do...while` 循环。以下代码片段展示了 `break` 语句的使用：

```
{
    int number;
    for (number = 1; number <= 10; number++)
    {
        Console.WriteLine(number);
        if (number>=5)
            break; //break statement
    }
    Console.WriteLine("Press ENTER to quit...");
    Console.ReadLine();
}
```

在前面的代码片段中，你可以看到 `number` 变量的值需要打印到 `for` 循环中指定的条件 `number<=10` 为 `true` 为止。然而，在 `for` 循环中，我们使用了 `if` 语句，其中我们指定了条件，即当 `number` 变量的值变得大于或等于 5 时，则应终止循环。这是通过在 `if` 语句中使用 `break` 语句完成的。

前述代码片段的输出如下所示：

![](img/e073a4882197be4ab61103cbe0bcb394_156_0.png)

Figure 3.1: Showing the Output of the break Statement

### The continue Statement

`continue` 语句开始其存在的封闭循环的新一次迭代。此语句可以存在于不同种类的循环语句中，例如 `while`、`do...while`、`for` 或 `foreach` 循环。`continue` 语句在特定条件未满足时执行其后的语句。此语句必须包含在循环中；否则，会发生编译时错误。以下代码片段展示了如何使用 `continue` 语句：

```
{
    int number;
    for (number = 1; number <= 10; number++)
    {
        if (number<=5)
            continue;
        Console.WriteLine(number);
    }
    Console.WriteLine("Press ENTER to quit...");
    Console.ReadLine();
}
```

在前面的代码片段中，`if` 语句内部的 `continue` 语句将程序控制转移到 `for` 循环的开头，并且只要 `number` 变量的值小于或等于 5，就不会执行下一个语句。每当 `number` 变量的值变得大于 5 时，就会执行 `continue` 语句之后的下一个语句。

前述代码片段的输出如下：

![](img/e073a4882197be4ab61103cbe0bcb394_157_0.png)

在学习了控制流语句之后，让我们学习异常处理。

## Exception Handling

异常是由于某些异常条件而产生的运行时错误，例如将数字除以零、将字符串传递给保存整数值的变量。捕获和处理运行时错误是任何程序员的重要且关键的任务；但在讨论运行时错误之前，让我们先看看编译时错误。编译时错误是在编译程序期间发生的错误。它可能由于糟糕的编码或错误的语法而发生。你可以在查看编译器生成的错误消息后纠正这些编译时错误。另一方面，运行时错误是在程序执行期间发生的错误，因此在那时它们无法被纠正。因此，需要事先采取必要的措施来防止此类错误。为此，你应该首先确定以下两个方面：

- 找出程序中可能导致运行时错误的部分
- 当它们发生时如何处理这些错误

表 3.1 描述了一些常见的异常类：

| Exception Class | Description |
|---|---|
| `SystemException` | Represents a base class for other exception classes |
| `AccessException` | Occurs when a type member, such as a variable, cannot be accessed |

### 表 3.1：值得注意的异常类

| 异常类 | 描述 |
|---|---|
| `ArgumentException` | 定义了方法的一个无效参数 |

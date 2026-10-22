

7. 编写一个程序，要求用户输入一个 `double` 类型的数字，并输出该数字的立方值。使用你自行设计的函数计算并输出该值。`main()` 程序应将输入的值传递给该函数。

8. 编写一个程序，显示执行取模运算的结果。用户应首先输入一个整数作为第二个操作数，该操作数之后保持不变。然后，用户输入要计算取模的数字；当输入 0 或更小的数字时，终止该过程。示例运行如下：

```
This program computes moduli.
Enter an integer to serve as the second operand: 256
Now enter the first operand: 438
438 % 256 is 182

Enter next number for first operand (<= 0 to quit): 1234567
1234567 % 256 is 135
Enter next number for first operand (<= 0 to quit): 0
Done
```

9. 编写一个程序，要求用户输入华氏温度。程序应将温度读取为 `double` 类型的数字，并将其作为参数传递给一个名为 `Temperatures()` 的用户自定义函数。该函数应计算对应的摄氏温度和开尔文温度，并以小数点右侧两位的精度显示这三个温度。每个值都应标明其所代表的温标。以下是将华氏温度转换为摄氏温度的公式：

`Celsius = 5.0 / 9.0 * (Fahrenheit - 32.0)`

开尔文温标通常用于科学领域，它将 0 定义为绝对零度，即可能达到的最低温度。以下是将摄氏温度转换为开尔文温度的公式：

`Kelvin = Celsius + 273.16`

`Temperatures()` 函数应使用 `const` 创建转换公式中出现的三个常量的符号表示。`main()` 函数应使用循环允许用户反复输入温度；当输入 `q` 或其他非数字值时停止。请利用 `scanf()` 返回所读取项目数量这一事实：如果读取到一个数字，它将返回 1；但如果用户输入 `q`，则不会返回 1。`==` 运算符用于测试相等性，因此可以使用它将 `scanf()` 的返回值与 1 进行比较。

## C 控制语句：循环

本章将学习以下内容：

- 关键字：
  - `for`
  - `while`
  - `do while`
- 运算符：
  - `< > >=`
  - `<= != == +=`
  - `*= -= /= %=`
- 函数：
  - `fabs()`
- C 的三种循环结构——`while`、`for` 和 `do while`
- 使用关系运算符构造表达式，以控制这些循环
- 其他几种运算符
- 数组，它们通常与循环一起使用
- 编写具有返回值的函数

强大、智能、灵活且实用！我们大多数人都不会介意被这样形容。使用 C，至少有机会让我们的程序获得这样的评价。关键在于控制程序的流程。根据计算机科学（它是研究计算机的科学，而不是由计算机进行的科学……至少目前还不是），一门优秀的语言应该提供以下三种程序流程形式：

- 执行一系列语句
- 重复执行一系列语句，直到满足某个条件（循环）
- 使用测试在不同的语句序列之间做出选择（分支）

第一种形式你已经很熟悉了；之前的所有程序都由一系列语句组成。`while` 循环是第二种形式的一个例子。本章将更深入地介绍 `while` 循环，以及另外两种循环结构——`for` 和 `do while`。最后一种形式，即在不同的可能行动方案之间进行选择，会使程序更加“智能”，并极大地提高计算机的实用性。遗憾的是，在获得这种能力之前，你还需要再等一章。本章还将介绍数组，因为数组能让你运用新学到的循环知识。此外，本章还会继续讲解函数。现在，让我们先复习一下 `while` 循环。

### 再访 `while` 循环

你已经对 `while` 循环有了一定了解，不过让我们通过一个对从键盘输入的整数求和的程序来复习它（见程序清单 6.1）。这个示例利用 `scanf()` 的返回值来终止输入。

**程序清单 6.1 summing.c 程序**

```
/* summing.c -- sums integers entered interactively */
#include <stdio.h>
int main(void)
{
    long num;
    long sum = 0L;      /* initialize sum to zero  */
    int status;

    printf("Please enter an integer to be summed ");
    printf("(q to quit): ");
    status = scanf("%ld", &num);
    while (status == 1) /* == means "is equal to"  */
    {
        sum = sum + num;
        printf("Please enter next integer (q to quit): ");
        status = scanf("%ld", &num);
    }
    printf("Those integers sum to %ld.\n", sum);

    return 0;
}
```

程序清单 6.1 使用 `long` 类型，以便容纳更大的数字。为了保持一致，程序将 `sum` 初始化为 `0L`（`long` 类型的 0），而不是 `0`（`int` 类型的 0）；尽管 C 的自动转换机制允许你直接使用普通的 `0`。

下面是一次示例运行：

```
Please enter an integer to be summed (q to quit): 44
Please enter next integer (q to quit): 33
Please enter next integer (q to quit): 88
Please enter next integer (q to quit): 121
Please enter next integer (q to quit): q
Those integers sum to 286.
```

### 程序注释

我们先来看看 `while` 循环。该循环的测试条件是下面这个表达式：

```
status == 1
```

`==` 运算符是 C 的相等运算符；也就是说，该表达式用于测试 `status` 是否等于 1。不要将它与 `status = 1` 混淆，后者是将 1 赋值给 `status`。在 `status == 1` 这一测试条件下，只要 `status` 的值为 1，循环就会继续执行。每次循环中，程序都会将 `num` 的当前值加到 `sum` 上，因此 `sum` 始终保存一个不断更新的总和。当 `status` 获得非 1 的值时，循环终止，程序输出 `sum` 的最终值。

为了使程序正常工作，它应在每次循环中为 `num` 获取一个新值，并在每次循环中更新 `status`。程序通过使用 `scanf()` 的两个不同特性来实现这一点。首先，它使用 `scanf()` 尝试读取 `num` 的新值。其次，它利用 `scanf()` 的返回值报告这次尝试是否成功。回顾第 4 章“字符字符串与格式化输入/输出”中的内容，`scanf()` 返回成功读取的项目数量。如果 `scanf()` 成功读取一个整数，它会将该整数放入 `num`，并返回值 1；这个值随后被赋给 `status`。（注意，输入值会被放入 `num`，而不是 `status`。）这同时更新了 `num` 和 `status` 的值，于是 `while` 循环进入下一轮。如果你输入非数字内容，例如 `q`，`scanf()` 找不到可读取的整数，因此其返回值以及 `status` 都将为 0。这会终止循环。输入字符 `q` 由于不是数字，会被放回输入队列；它不会被读取。（实际上，不只是 `q`，任何非数字输入都会终止循环；但要求用户输入 `q`，比要求用户输入非数字内容更简单。）

如果 `scanf()` 在尝试转换值之前遇到问题（例如检测到文件结尾或遇到硬件问题），它会返回特殊值 `EOF`，该值通常被定义为 -1。这个值同样会导致循环终止。

`scanf()` 的这种双重用途解决了循环交互式输入中的一个棘手问题：如何告诉循环何时停止？例如，假设 `scanf()` 没有返回值。那么，每次循环中唯一会发生变化的就是 `num` 的值。你可以利用 `num` 的值终止循环，例如使用 `num > 0`（`num` 大于 0）或 `num != 0`（`num` 不等于 0）作为测试条件，但这样会阻止你输入某些值。可以将循环替换为下面的形式：

```
while (scanf("%ld", &num) == 1)
{
    /* loop actions */
}
```

第二种形式同时以两种不同的方式使用 `scanf()`。首先，如果函数调用成功，它会将一个值放入 `num`。其次，函数的返回值（它是 1 或 0，而不是 `num` 的值）控制着循环。由于循环条件会在每次迭代时进行测试，因此每次迭代都会调用 `scanf()`，从而获取新的 `num` 和新的测试结果。换句话说，C 的语法特性允许你用下面这种简化形式替代标准循环格式：

```
while getting and testing the value succeeds
    process the value
```

现在，让我们更加正式地了解一下 `while` 语句。

### `while` 语句

这是 `while` 循环的一般形式：

```
while (expression)
    statement
```

`statement` 部分可以是一个以分号结尾的简单语句，也可以是一个用花括号括起来的复合语句。

到目前为止，示例中的 `expression` 部分都使用了关系表达式；也就是说，`expression` 是对值进行比较。更一般地说，你可以使用任意表达式。如果 `expression` 为真（或者更准确地说，非零），则执行一次 `statement`，然后再次测试 `expression`。这种测试和执行的循环会一直重复，直到 `expression` 变为假（零）。每次循环都称为一次迭代（见图 6.1）。

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_221_0.png)

图 6.1 `while` 循环的结构。


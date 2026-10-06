

# 第 2 章 使用数据

当你想要实现的仅仅是将一个变量的值加 1 时，使用前缀递增和后置递增运算符没有明显的区别。然而，这些运算符的功能有所不同。当你使用前缀 `++` 时，结果会先被计算并存储，然后使用该变量。例如，在下面的代码中，b 和 c 最终都持有 5。`WriteLine()` 语句显示 5 和 5。在这个示例中，4 被赋值给 b，然后 b 变为 5，然后 5 被赋值给 c。

```csharp
b = 4;
c = ++b;
WriteLine("{0} and {1}", b, c);
```

相反，当你使用后置 `++` 时，会先使用变量，然后才计算并存储结果。例如，在下面代码的第二行中，4 被赋值给 c；赋值赋值之后，b 增加并取值为 5。

```csharp
b = 4;
c = b++;
WriteLine("{0} and {1}", b, c);
```

最后这个 `WriteLine()` 语句显示 5 和 4。换句话说，如果 b = 4，那么 b++ 的值也是 4，在上面的第二个语句中，该值赋值给 c。然而，在 4 被赋值给 c 之后，b 增加到了 5。

> 当你需要在独立语句中给变量加 1 时，结果取决于你使用前缀还是后置递增运算符。许多程序员都使用其中任一个运算符。这可能是一个错误，因为前缀运算符更高效。我们将在“循环”部分看到一个展示前缀运算符优越性的示例。

前缀或后置递减运算符（`--`）会使变量的值减少 1。例如，如果 s 和 t 都被赋值为 34，那么表达式 `--s` 的值为 33，而表达式 `t--` 的值为 34，但 t 变为 33。

观看视频《使用快捷算术运算符》。

# 两个真值一假
使用算术运算符

- 1. 26 % 4 * 3 的值是 18。
- 2. 4 / 3 + 2 的值是 3。
- 3. 如果 price 为 4 且 tax 为 5，那么 price --tax 的值是 -1。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_92_0.png)

Copyright 2018 Cengage Learning. 版权所有。任何部分均不得复制、扫描或复制。WCN 02-200-022

# 你来做

执行算术运算

在接下来的步骤中，你向程序添加一些算术语句。

- 1. 打开一个名为 DemoVariables2 的新 C# 程序文件，并输入以下语句以启动一个演示算术操作的程序：
```csharp
using static System.Console;
class DemoVariables2
{
    static void Main()
{
}
``````
- 2. 编写一个声明七个整数变量的语句。为其中两个变量分配初始值；另外五个变量的值将被计算。由于所有这些变量都是相同类型，你可以使用单个语句声明所有七个整数。记住，要这样做，你需要在变量名之间插入逗号，并在末尾放置单个分号。你可以为了可读性在任何需要的地方换行。（或者，你也可以使用多个单独声明。）
```csharp
int value1 = 10,
sum, diff, product, quotient, remainder;
```
- 3. 编写算术语句来计算两个赋值变量之和、差、乘积以及余数。
```csharp
sum = value1 + value2;
diff = value1 - value2;
product = value1 * value2;
quotient = value1 / value2;
remainder = value1 % value2;
```

与其声明变量 sum, diff, product, quotient 和 remainder 稍后赋值，不如一次性为所有赋值，如 `int sum = value1 + value2;`。唯一的要求是在计算中使用 value1 和 value2 之前必须已经对其进行赋值。

- 4. 包含五个 `WriteLine` 语句来显示结果。
```csharp
WriteLine("The sum of {0} and {1} is {2}", value1, value2, sum);
WriteLine("The difference between {0} and {1}" + " is {2}", value1, value2, diff);
WriteLine("The product of {0} and {1} is {2}", value1, value2, product);
WriteLine("{0} divided by {1} is {2}", value2, quotient);
WriteLine("and the remainder is {0}", remainder);
```

（继续）

- 5. 添加两个右括号——一个用于 Main(C) 方法，另一个用于 DemoVariables2 类。
- 6. 保存文件，编译程序并执行它。输出应该像图 2-11。

```
The sum of 43 and 10 is 53
The difference between 43 and 10 is 33
the product of 43 and 10 is 430
divided by 10 is 4
and the remainder is 3
```

**图 2-11** 将 value1 和 value2 变量输出到你选择的任何值，保存程序，编译并再次运行它。重复几次。在每次执行后，通过输出结果分析 value1 和 value2 变量的值，确保你理解算术运算的结果。

- 7. 将 value1 和 value2 的值改为任何值，保存程序，编译并运行它。重复几次。在每次执行后，通过输出结果确保你理解算术运算的结果。

# 使用 bool 类型

布尔逻辑基于真或假的比较。`int` 变量可以持有两个值，但 `bool` 变量只能持有真或假。使用 `bool` 类型。以下语句使用 `bool` 类型来声明并赋值值：

```csharp
bool isItMonday = false;
bool areTired = true;
```

> 当你需要在独立语句中给变量加 1 时，结果取决于你使用前缀还是后置递增运算符。许多程序员都使用其中任一个运算符。这可能是一个错误，因为前缀运算符更高效。我们将在“循环”部分看到一个展示前缀运算符优越性的示例。

布尔逻辑通常以大写的 B 开始，因为是以乔治·布尔（George Boole，1815-1864）命名的。然而，C# 的数据类型 `bool` 以小写的 b 开始。

你也可以根据比较的结果为布尔变量赋值。比较运算符比较两个项目；包含运算符运算符的具有布尔值。表 2-4 描述了 C# 支持的六种比较运算符。

| 运算符 | 描述 | 真示例 | 假示例 |
| --- | --- | --- | --- |
| < | 小于 | 3 < 8 | 8 < 3 |
| > | 大于 | 4 > 2 | 2 > 4 |
| == | 等于 | 7 == 7 | 3 == 9 |
| <= | 小于等于 | 5 <= 5 | 8 <= 6 |
| >= | 大于等于 | 7 >= 3 | 1 >= 2 |
| != | 不等于 | 5 != 6 | 3 != 3 |

表 2-4 比较运算符

在使用任何需要两个键的运算符（==, <=, >=, !=）时，两个符号之间不能放置任何空格。

新程序员常见的错误是尝试使用单个符号创建布尔表达式。相等运算符使用两个符号，例如，以下语句将真或假赋值给 isDiscountProvided：
isDiscountProvided = custStatus ==;

语句中的第二个运算符 ( == ) 将 custStatus 与 1 进行比较。然后使用赋值运算符 ( = ) 将结果赋值给左侧的变量。

合法的（但有些无用的）声明语句可能包含以下内容，它们比较两个值：

```csharp
bool isBigger = 6 > 5; // 存储值为真
bool isSmallerOrEqual = 7 <= 4; // 存储值为假
```

在比较中使用变量（已赋值的）而不是常量使用布尔值更有意义，例如：
bool doesEmployeeReceiveOvertime = hoursWorked > 40;
bool isHighTaxBracket = annualIncome > 100000;

在第一个语句中，hoursWorked 与常量值 40 进行比较。如果 hoursWorked 变量持有小于或等于 40 的值，则该表达式求值为为


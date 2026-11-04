

## 6.4 应用：偶数整数求和

现在考虑一个示例应用，它演示 for 的简单用法。图 6.5 中的应用使用 for 语句对 2 到 20 的偶数整数求和，并将结果存储在名为 total 的 int 变量中。循环的每次迭代（第 12–15 行）将控制变量 number 的值加到变量 total 中。

```
1  // Fig. 6.5: Sum.cs
2  // Summing integers with the for statement.
3  using System;
4  
5  class Sum
6  {
7     static void Main()
8     {
9        int total = 0; // initialize total
10
11       // sum even integers from 2 through 20
12       for (int number = 2; number <= 20; number += 2)
13       {
14          total += number;
15       }
16
17       Console.WriteLine($"Sum is {total}"); // display results
18    }
19 }
```

```
Sum is 110
```

*初始化*和*增量*表达式可以是逗号分隔的列表，使您能够使用多个初始化表达式或多个增量表达式。例如，尽管不鼓励这样做，您也可以通过使用逗号，将 `for` 的主体语句（第 14 行）合并到 `for` 头部的增量部分，如下所示：

```
total += number, number += 2
```

## 6.5 应用：复利计算

下一个应用使用 `for` 语句计算复利。考虑以下问题：

> 一个人在储蓄账户中投资 $1,000，年利率为 5%。假设所有利息都留在存款中，计算并打印 10 年中每年年末账户中的金额。使用以下公式确定金额：

*a* = *p* (1 + *r*)^n

其中

- *p* 是原始投资金额（即本金）
- *r* 是年利率（例如，5% 使用 0.05）
- *n* 是年数
- *a* 是第 *n* 年末的存款金额。

该问题的解决方案（图 6.6）涉及一个循环，它对资金留在存款中的 10 年中的每一年执行指定的计算。

```csharp
 1  // Fig. 6.6: Interest.cs
 2  // Compound-interest calculations with for.
 3  using System;
 4
 5  class Interest
 6  {
 7     static void Main()
 8     {
 9        decimal principal = 1000; // initial amount before interest
10        double rate = 0.05; // interest rate
11
12        // display headers
13        Console.WriteLine("Year  Amount on deposit");
14
15        // calculate amount on deposit for each of ten years
16        for (int year = 1; year <= 10; ++year)
17        {
18           // calculate new amount for specified year
19           decimal amount = principal *
20              ((decimal) Math.Pow(1.0 + rate, year));
21
22           // display the year and the amount
23           Console.WriteLine($"{year,4}{amount,20:C}");
24        }
25     }
26  }
```

**图 6.6** | 使用 `for` 的复利计算。（第 1 部分，共 2 部分。）

| 年份 | 存款金额 |
| ---- | ---------------- |
| 1 | $1,050.00 |
| 2 | $1,102.50 |
| 3 | $1,157.63 |
| 4 | $1,215.51 |
| 5 | $1,276.28 |
| 6 | $1,340.10 |
| 7 | $1,407.10 |
| 8 | $1,477.46 |
| 9 | $1,551.33 |
| 10 | $1,628.89 |

图 6.6 | 使用 for 的复利计算。（第 2 部分，共 2 部分。）

第 9 行和第 19 行声明 decimal 变量 principal 和 amount，第 10 行声明 double 变量 rate。第 9–10 行还将 principal 初始化为 1000（即 $1,000.00），并将 rate 初始化为 0.05。C# 将像 0.05 这样的数字字面量视为 double 类型。类似地，C# 将像 7 和 1000 这样的整数字面量视为 int 类型——与 double 值不同，int 值可以赋给 decimal 变量。当 principal 初始化为 1000 时，int 值 1000 会隐式提升为 decimal 类型——不需要强制转换。第 13 行输出应用两列输出的标题。第一列显示年份，第二列显示该年末的存款金额。

### 6.5.1 使用 Math 方法 pow 执行利息计算

类提供对对象执行常见任务的方法。大多数方法必须在特定对象上调用。例如，为了向图 4.12 中的银行账户存款，我们在 Account 对象 account1 和 account2 上调用了方法 Deposit。许多类还提供执行不需要特定对象的常见任务的方法——这些方法必须使用类名调用。此类方法称为静态方法。您已经使用过 Console 类的几个静态方法——方法 Write、WriteLine 和 ReadLine。调用静态方法时，需要指定类名，后跟成员访问运算符（.）和方法名，如下所示：

```
ClassName.MethodName(arguments)
```

C# 不包含求幂运算符，因此我们使用 Math 类的静态方法 Pow 来执行复利计算。表达式

```
Math.Pow(x, y)
```

计算 x 的 y 次方的值。该方法接收两个 double 实参并返回一个 double 值。图 6.6 中的第 19–20 行执行以下计算

```
a = p (1 + r)^n
```

其中 a 是金额，p 是本金，r 是利率，n 是年份。在此计算中，我们需要将 decimal 值 principal 乘以一个 double 值（调用 Math.Pow 返回的值）。由于任一种转换都可能丢失信息，C# 不会将 double 隐式转换为 decimal 类型，反之亦然，因此第 20 行包含一个 (decimal) 强制转换运算符，将 Math.Pow 的 double 返回值显式转换为 decimal。

for 语句的主体包含计算 1.0 + rate，它作为 Math.Pow 方法的实参出现。事实上，该计算在每次循环中都会产生相同结果，因此在循环的每次迭代中重复该计算是浪费的。

### 性能提示 6.1

在循环中，避免进行结果永远不会改变的计算——此类计算通常应放在循环之前。优化编译器通常会为您执行此操作。

### 6.5.2 使用字段宽度和对齐进行格式化

在每次计算后，第 23 行

```
Console.WriteLine($"{year,4}{amount,20:C}");
```

显示年份以及该年末的存款金额。以下内插表达式格式化年份：

```
{year,4}
```

逗号后的整数 4 表示年份值应显示在宽度为 4 的字段中——也就是说，WriteLine 显示该值时至少占四个字符位置。如果要输出的值宽度少于四个字符位置（本例中为一或两个字符），默认情况下该值在字段中右对齐——在这种情况下，根据年份值的不同，该值前面会有两个或三个空格。如果要输出的值宽度超过四个字符位置，字段宽度将向右扩展以容纳整个值——这会将金额列向右推，破坏表格输出中整齐的列。类似地，内插表达式

```
{amount,20:C}
```

将金额格式化为货币（C），在至少 20 个字符的字段中右对齐。要将值左对齐，只需使用负的字段宽度。

### 6.5.3 注意：不要将 float 或 double 用于货币金额

第 4.9 节介绍了用于精确货币表示和计算的简单类型 decimal。您可能想使用浮点类型 float 或 double 进行此类计算。然而，对于某些值，float 或 double 类型会出现我们所说的表示误差。例如，浮点数常常作为计算的结果出现——当我们用 10 除以 3 时，结果是 3.333333...，其中数字 3 的序列无限重复。计算机只分配固定大小的空间来保存这样的值，因此显然存储的浮点值只能是一个近似值。

### 常见编程错误 6.2

以假定浮点数会被精确表示的方式使用它们（例如，在相等比较中使用它们）可能导致错误结果。浮点数只能近似表示。

### 错误预防提示 6.2

不要使用 double（或 float）类型的变量执行精确的货币计算——而应使用 decimal 类型。浮点数的不精确性可能导致错误，从而产生不正确的货币值。


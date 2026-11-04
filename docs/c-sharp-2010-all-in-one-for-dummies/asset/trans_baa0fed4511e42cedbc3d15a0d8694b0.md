
and reassigns the uppercased character to sb[0]. Finally, it extracts the improved string "Jones" from the StringBuilder.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_96_0.png)

本章前面介绍的 BuildASentence 示例可以从使用 StringBuilder 中受益。我经常使用 StringBuilder。

本书网站上的 StringCaseChanging 和 VariousStringTechniques 示例展示了 StringBuilder 的实际应用。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_96_1.png)

Book II 介绍了 C# 中称为 extension methods 的特性。那里的示例向 String 类添加了几个方便的方法。稍后在该迷你书中，我们将描述如何在字符串、char 数组和 byte 数组之间进行转换。这些是你可能需要经常执行的操作（并且在本书网站上的 StringCaseChanging 示例中有所展示）。

## 第 4 章：流畅的操作符

### 本章内容

- ✔ 进行一点算术运算
- ✔ 进行一些逻辑算术运算
- ✔ 用复合逻辑运算符使事情复杂化

**M**数学家创建变量并以各种方式操作它们，将它们相加、相乘，甚至——这有点难——对它们进行积分。本迷你书的第 2 章描述了如何声明和定义变量。然而，它几乎没有提到在声明变量后如何使用变量来完成工作。本章探讨了可以在变量上执行的操作以完成工作。操作需要 *运算符*，例如 `+`、`-`、`=`、`<` 和 `&`。本章将介绍算术、逻辑和其他类型的运算符。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_98_0.png)

编写能完成任务的程序是好的。如果你编写的程序什么都不做，你永远成不了 C# 程序员——当然，除非你是顾问。

## 执行算术运算

算术运算符的集合可以分为几个组：简单算术运算符、赋值运算符以及编程特有的特殊运算符集合。在消化完这些之后，你还需要消化另一组逻辑运算符。*Bon appétit!*

### 简单运算符

你很可能在小学就学会了如何使用大多数简单运算符。表 4-1 列出了它们。**注意：** 计算机使用星号 (\*)，而不是乘号 (×)，来进行乘法。

**表 4-1** 简单运算符

| 运算符 | 其含义 |
|---|---|
| - (一元) | 取负值 |
| * | 乘法 |
| / | 除法 |
| + | 加法 |
| - (二元) | 减法 |
| % | 取模 |

表中大多数运算符是 *二元* 运算符，因为它们操作两个值：一个在运算符左侧，一个在右侧。唯一的例外是一元负号。然而，它与其它运算符一样简单，如以下示例所示：

```
int n1 = 5;
int n2 = -n1;   // n2 now has the value -5.
```

`-n` 的值是 `n` 值的负值。

取模运算符可能不如其它运算符那么熟悉。取模类似于除法后的余数。因此，5 % 3 是 2（5 / 3 = 1，余数 2），25 % 3 是 1（25 / 3 = 8，余数 1）。读作“五 modulo 三”或简单地“五 mod 三”。偶数 mod 2 为 0：6 % 2 = 0（6/2 = 3，余数 0）。

除取模外的算术运算符对所有数值类型都有定义。取模运算符未定义浮点数，因为浮点值相除后没有余数。

### 操作顺序

某些表达式的值可能不明确。例如，考虑以下表达式：

```
int n = 5 * 3 + 2;
```

程序员的意思是“先将 5 乘以 3 再加 2”，结果为 17，还是“将 5 乘以 3 与 2 的和”，结果为 25？

C# 通常从左到右执行常见运算符。因此，前面的示例将值 17 分配给变量 `n`。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_99_0.png)

逻辑比较对所有数值类型都有定义，包括 float、double、decimal 和 char。以下所有语句都是合法的：

```csharp
bool b;
b = 3 > 2;        // true
b = 3.0 > 2.0;    // true
b = 'a' > 'b';    // false -- Alphabetically, later is greater.
b = 'A' < 'a';    // true -- Upper A is less than lower a.
b = 'A' < 'b';    // true -- All upper are less than all lower.
b = 10M > 12M;    // false
```

比较运算符始终产生类型为 bool 的结果。除了 == 之外的比较运算符对 string 类型的变量无效。（不用担心：C# 提供了其他比较字符串的方法。）

## 比较浮点数：你的浮点数比我的大吗？

比较两个浮点值可能会很棘手，你需要小心这些比较。考虑以下比较：

```csharp
float f1;
float f2;
f1 = 10;
f2 = f1 / 3;
bool b1 = (3 * f2) == f1; // b1 is true if (3 * f2) equals f1.
f1 = 9;
f2 = f1 / 3;
bool b2 = (3 * f2) == f1;
```

请注意，前一个示例中的第五行和第八行都首先包含赋值运算符 (=)，然后是逻辑比较 (==)。它们是不同的东西，所以不要在想写 == 时写 =。C# 先执行逻辑比较，然后将结果赋给左侧的变量。

b1 和 b2 计算之间的唯一区别是 f1 的初始值。那么 b1 和 b2 的值是多少？b2 的值显然为 true：9 / 3 是 3；3 * 3 是 9；9 等于 9。瞧！

b1 的值并不明显：10 / 3 是 3.333 . . . 而 3.333 . . . * 3 是 9.999 . . . ，9.999 . . . 等于 10 吗？这取决于你的处理器和编译器的聪明程度。在 Pentium 或更新的处理器上，如果将计算移离比较，C# 不够聪明，无法意识到 b1 应该是 true。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_103_0.png)

你可以使用系统绝对值方法来比较 f1 和 f2：

```csharp
Math.Abs(f1 - 3.0 * f2) < .00001; // Use whatever level of accuracy.
```

此计算在两种情况下都返回 true。你可以使用常量 Double.Epsilon 代替 .00001 以获得最大精度。Epsilon 是两个非零 double 变量之间可能存在的最小差异。

在这种情况下，C# 会计算 boolExpression1 和 boolExpression2。然后它会查看两者是否都为 true 才能决定 b 的值。然而，这可能是浪费精力。如果一个表达式为 false，就没有理由执行另一个。无论第二个表达式的值如何，结果都将为 false。尽管如此，& 仍会继续计算两个表达式。

&& 运算符避免不必要地计算两个表达式，如以下示例所示：

```
bool b = (boolExpression1) && (boolExpression2);
```

在这种情况下，C# 会计算 boolExpression1。如果它为 false，则 b 被设为 false，程序继续执行。另一方面，如果 boolExpression1 为 true，则 C# 会计算 boolExpression2 并将结果存储在 b 中。&& 运算符使用这种短路求值，因为如果需要，它会绕过第二个布尔表达式。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_105_0.png)

大多数程序员大部分时间都使用双重形式。

|| 运算符的工作方式相同，如以下表达式所示：

```
bool b = (boolExpression1) || (boolExpression2);
```

如果 boolExpression1 为 true，则没有必要计算 boolExpression2，因为结果始终为 true。

你可以将这些运算符读作 "short-circuit and" 和 "short-circuit or."

## 在 TrackDownAMate.com 上匹配表达式类型

在计算中，表达式的类型与它的值一样重要。考虑以下表达式：

```
int n;
n = (5 * 5) + 7;
```

我的计算器说 n 的结果值为 32。然而，该表达式还有一个基于其各部分类型的整体类型。

用 "type language" 写出来，前面的表达式变为

```
int [=] (int * int) + int;
```

要计算表达式的类型，请遵循与计算表达式值相同的模式。乘法优先于加法

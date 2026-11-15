

System.Console.Write("Enter the denominator: ");
denominator = int.Parse(System.Console.ReadLine());

quotient = numerator / denominator;
remainder = numerator % denominator;

System.Console.WriteLine(
    "{0} / {1} = {2} with remainder {3}",
    numerator, denominator, quotient, remainder);
}

输出 3.1 显示了清单 3.3 的结果。

### 输出 3.1：

```
Enter the numerator: 23
Enter the denominator: 3
23 / 3 = 7 with remainder 2.
```

使用二元运算符时要注意结合性的顺序。二元运算符的顺序是从左到右。相比之下，赋值运算符的顺序是从右到左。然而，仅凭结合性本身并不指定除法是在赋值之前还是之后进行。运算符优先级定义了这一点。目前为止所使用的运算符优先级如下：

- 1. *, /, 和 %
- 2. + 和 -
- 3. =

因此，你可以假设语句的行为符合预期，即除法和余数运算符在赋值之前发生。

如果你忘记为这些二元运算符之一的结果赋值，将会收到输出 3.2 中所示的编译错误。

### 输出 3.2：

```
... error CS0201: Only assignment, call, increment, decrement,
and new object expressions can be used as a statement
```

## 结合性和运算符优先级

与数学一样，编程语言支持结合性的概念。结合性是指操作数的分组方式，因此也是运算符求值的顺序。给定一个在表达式中出现多次的单个运算符，该运算符先结合第一个双元组，然后结合下一个操作数，直到所有运算符都被求值。例如，a-b-c 结合为 (a-b)-c，而不是 a-(b-c)。

结合性仅在所有运算符相同时才适用。当语句中出现不同的运算符时，这些运算符的优先级决定了哪些运算符首先被求值。例如，运算符优先级表示在表达式 a+b*c 中，乘法运算符应在加法运算符之前求值。

## 将加法运算符用于字符串

运算符也可以用于非数值类型。例如，可以使用加法运算符连接两个或多个字符串，如清单 3.4 所示。

### 清单 3.4：将二元运算符用于非数值类型

```
class FortyTwo
{
    static void Main()
    {
        short windSpeed = 42;
        System.Console.WriteLine(
            "The original Tacoma Bridge in Washington\\was"
            + "brought down by a "
            + windSpeed + " mile/hour wind.");
    }
}
```

输出 3.3 显示了清单 3.4 的结果。

### 输出 3.3：

```
The original Tacoma Bridge in Washington
was brought down by a 42 mile/hour wind.
```

由于不同文化中语言的句子结构各不相同，开发者应谨慎不要将加法运算符用于需要本地化的字符串。更推荐使用复合格式化（请参阅第 1 章）。

## 在算术运算中使用字符

在前一章介绍 char 类型时，我提到过，尽管它存储的是字符而不是数字，但 char 类型是整数类型（“整数”意味着它基于整数）。它可以与其他整数类型一起参与算术运算。然而，char 类型值的解释并非基于其存储的字符，而是基于其底层值。例如，数字 3 包含 Unicode 值 0x33（十六进制），在十进制中为 51。另一方面，数字 4 包含 Unicode 值 0x34，即十进制中的 52。在清单 3.5 中将 3 和 4 相加，结果为十六进制值 0x67，即十进制中的 103，相当于字母 g。

### 清单 3.5：将加法运算符用于 char 数据类型

```
int n = '3' + '4';
char c = (char)n;
System.Console.WriteLine(c); // Writes out g.
```

输出 3.4 显示了清单 3.5 的结果。

### 输出 3.4：

g

你可以利用字符类型的这一特性来确定两个字符相距多远。例如，字母 f 比字母 c 远三个字符。你可以通过用字母 f 减去字母 c 来确定这个值，如清单 3.6 所示。

### 清单 3.6：确定两个字符之间的字符差值

```
int distance = 'f' - 'c';
System.Console.WriteLine(distance);
```

输出 3.5 显示了清单 3.6 的结果。

### 输出 3.5：

3

## 特殊浮点特性

浮点类型 float 和 double 具有一些特殊特性，例如它们处理精度的方式。本节将探讨一些具体示例，以及一些独特的浮点类型特性。

float 具有七位精度，可以存储值 1,234,567 和值 0.1234567。但是，如果将这两个 float 相加，结果将被舍入为 1234567，因为数字的小数部分超过了 float 所能容纳的七位有效数字。这种舍入可能变得很重要，尤其是在重复计算或相等性检查时（请参阅即将介绍的高级主题，浮点类型的意外不等性）。

请注意，简单的赋值也可能出现不准确，例如 double number = 140.6f。由于 double 能够存储比 float 更精确的值，C# 编译器实际上会将此表达式求值为 double number = 140.600006103516；140.600006103516 作为 float 是 140.6，但作为 double 表示时并不完全是 140.6。

### 高级主题

### 浮点类型的意外不等性

浮点数的不准确性在比较值是否相等时可能非常令人困惑，因为它们可能会意外地不相等。请考虑清单 3.7。

### 清单 3.7：由于浮点不准确性导致的意外不等性

```
decimal decimalNumber = 4.2M;
double doubleNumber1 = 0.1F * 42F;
double doubleNumber2 = 0.1D * 42D;
float floatNumber = 0.1F * 42F;

Trace.Assert(decimalNumber == (decimal)doubleNumber1);
// Displays: 4.2 != 4.200000000000000025488
System.Console.WriteLine(
    "{0} != {1}", decimalNumber, (decimal)doubleNumber1);

Trace.Assert((double)decimalNumber == doubleNumber1);
// Displays: 4.2 != 4.2000006258488
System.Console.WriteLine(
    "{0} == {1}", (double)decimalNumber, doubleNumber1);

Trace.Assert((float)decimalNumber == floatNumber);
// Displays: 4.2M != 4.2F
System.Console.WriteLine(
    "{0} != {1}",
    (float)decimalNumber, floatNumber);

Trace.Assert(decimalNumber == (double)floatNumber);
// Displays: 4.2000006258488 == 4.20000028610229
System.Console.WriteLine(
    "{0} == {1}", decimalNumber, (double)floatNumber);

Trace.Assert(doubleNumber1 == doubleNumber2);
// Displays: 4.2000006258488 != 4.2
System.Console.WriteLine(
    "{0} == {1}", doubleNumber1, doubleNumber2);

Trace.Assert(floatNumber == doubleNumber2);
// Displays: 4.2F != 4.20;
System.Console.WriteLine(
    "{0}F != {1}D", floatNumber, doubleNumber2);

Trace.Assert((double)4.2F == 4.2D);
// Displays: 4.2F == 4.2D;
System.Console.WriteLine(
    "{0} == {1}", (double)4.2F, 4.2D);

Trace.Assert(4.2F == 4.2D);
// Displays: 4.2F != 4.2D
System.Console.WriteLine(
    "{0}F != {1}D", 4.2F, 4.2D);
```

输出 3.6 显示了清单 3.7 的结果。

### 输出 3.6：

```
4.2 != 4.2000006258488
4.2F != 4.20000028610229
(float)4.2M == 4.2F
4.2000006258488 == 4.20000028610229
4.2000006258488 != 4.2
4.2F != 4.2D
4.19999980926514 == 4.2
4.2F != 4.2D
```

Assert() 方法旨在每当参数求值为 false 时显示调试对话框。然而，此代码清单中的所有 Assert() 语句都将求值为 true。因此，尽管代码清单中的值看起来相等，但由于浮点数的不准确性，它们实际上并不等价。此外，这并非某种累积的舍入误差。C# 编译器执行计算，而不是运行时。即使你只是直接赋值 4.2F 而不是进行计算，比较结果也将保持不相等。

为了避免由浮点类型不准确性引起的意外结果，开发者应避免将这些类型用于相等条件判断。相反，相等性评估应包含容差。实现此目的的一个简单方法是用一个值（操作数）减去另一个值，然后评估结果的绝对值是否小于最大容差。更好的做法是使用 decimal 类型来替代 float 类型。

你还应了解一些其他独特的浮点特性。例如，你可能会预期将整数除以零会导致错误，对于 int 和 decimal 等原始数据类型确实如此。然而，float 和 double 允许某些特殊值。请考虑清单 3.8 及其生成的输出，输出 3.7。

### 清单 3.8：将浮点数除以零，显示 NaN

```
float n = 0;
// Displays: NaN
System.Console.WriteLine(n / 0);
```

### 输出 3.7：

```
NaN
```

在数学中，某些数学运算是未定义的。在 C# 中，将 0F 除以值 0 的结果是“不是数字”，所有尝试打印此类数字输出的操作都将导致 NaN。同样，对负数求平方根（System.Math.Sqrt(-1））也会导致 NaN。


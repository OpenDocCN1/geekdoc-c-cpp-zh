
```csharp
public static bool AlmostEqualRelative2(float x, float y, float maxRelativeError)
{
  if (x == Double.NaN || y == Double.NaN)
    return false; // 根据 IEEE规范
  if (x == y)
    return true;
  float relativeError;
  if (Math.Abs(x) > Math.Abs(y))
    relativeError = Math.Abs(x - y) / y;
  else
    relativeError = Math.Abs(x - y) / x;
  if (relativeError <= maxRelativeError)
    return true;
  return false;
}
```

遗憾的是，这个新函数对于零附近的数字仍然表现不佳。例如，最接近零的正数和最接近零的负彼此极其接近，但此函数会正确计算出它们具有很大的相对误差。因此，需要对最大绝对误差增加额外的检查，以正确计算靠近零但符号相反的数字。如果绝对误差或相对误差任一小于输入的最大值，则新函数将返回 `true`。在 C# 中实现此附加功能的方法是编写类似如下的代码：

```csharp
public static bool AlmostEqualRelativeAbsolute(float x, float y, float maxAbsoluteError)
{
  if (x == Double.NaN || y == Double.NaN)
    return false; // 根据 IEEE规范
  if (Math.Abs(x - y) < maxAbsoluteError)
    return true;
  float relativeError=0.0;
  if (Math.Abs(y) > Math.Abs(x))
    relativeError = Math.Abs((x - y) / y);
  else
    relativeError = Math.Abs((x - y) / x;
  if (relativeError <= maxRelativeError)
    return true;
  return false;
}
```

然而，这个新的函数仍然存在缺陷。总结来说，Dawson [14] 的方法（由 Ruegg [15] 扩展）是在位级上进行浮点比较，而不是在数值上。与其选择任意的容差因子进行数值比较，他们的技术围绕着位级比较，这不仅更准确，还很好地利用了硬件限制。

# C# 中的数值方法、算法与工具

# 引言

.NET Framework `Math` 类提供了用于计算常用函数的常量和静态方法。因此，在开始本书关于 C# 数值方法的介绍时，逻辑做法是回顾该库中所有的数学例程，并包含一些实际示例以更好地说明这些例程如何在实际应用中使用。关于复数的数学方法将在后面的章节中讨论。

## .NET Framework Math 类

## 2.2 .NET Framework Math 类 - 字段

### 2.2.1 Math.PI 和 Math.E 字段

`Math.PI` 和 `Math.E` 字段在内部声明为：

```csharp
public const double PI;
public const double E;
```

## 2.3 .NET Framework Math 类 - 方法

### 2.3.1 Minimum 和 Maximum 方法

.NET Framework `Math` 类库提供了两个方法用于比较数字的相对大小。`Math.Min` 方法返回两个数中较小的一个；`Math.Max` 方法返回两个数中较大的一个。这些方法的声明如下：

```csharp
public static [type] Min([type] x, [type] y);
public static [type] Max([type] x, [type] y);
```

两个输入参数 `x` 和 `y` 以及由标签 `[type]` 指定的相同类型输出表明，这些方法可以使用以下数据类型进行重载：`byte`, `sbyte`, `int16`, `int64`, `decimal`, `double`, `single`, `uint16`, `uint32` 和 `uint64`。下面的代码段演示了如何使用 `Min` 和 `Max` 方法返回输出，并按指示显示两个变量的较小或较大值。

```csharp
public static void MinMax_Example()
{
    double x = 5.0, y = 10.0;
    Console.WriteLine("The smaller of {0} and {1} is {2}.", x, Math.Min(x,y));
    Console.WriteLine("The greater of {0} and {1} is {2}.", x, Math.Max(x,y));
}
```

### 2.3.2 Power, Exponential 和 Logarithmic 方法

具有固定实数底 $b > 1$ 和实数幂 $x$ 的通用指数函数是用公式 $f(x)=b^x$ 表示的函数。数字 $x$ 称为指数，表达式 $b^x$ 正式称为 b 的 x 次幂，或以 b 为底的 x 的数幂。更常见的表达方式是“b 的 x 次方”、“b 的 x 次幂”或“b 的幂 x”。常用的底是自然数底 $e$ 和底 10。如果底等于 $e$，则该指数函数称为自然指数函数，并用 $f(x)=exp(x)$ 表示。

任何指数函数的逆函数（在定义良好的情况下）被称为 $\log_b$。因此 $\log_bb^x=x$。给定的正实数底的对数是底为了产生该数字而提升的幂或指数。根据定义，底为 $b$ 的 $x$ 的对数写为 $\log_b(x)$，如果底是隐式的，则写为 $\log(x)$。因此，对于数字 $x$、底 $b$ 和指数 $y$，如果 $x=b^y$ 则 $y=\log_b(x)$。

.NET Framework `Math` 类提供了一套完整的方法用于计算实数的幂、指数和对数。能够处理复数的类似方法将在后面的章节中讨论。

Power 方法 `Math.Pow(b,x)` 用于计算 $b^x$，其中 $b$ 和 $x$ 是实数。这两个输入变量以及结果的输出都是 `double` 类型。该方法在内部声明为：

```csharp
public static double Pow(double b, double x);
```

特别是，当指数 $x = 1/2 = 0.5$ 时，$b^x = b^{1/2} = \sqrt{b}$。Power 方法的这种特殊情况在应用程序中发生频率足够，以至于 .NET Framework 类库了自己的内部方法 `Math.Sqrt(x)`，通过输入参数 $x$ 对实数求平方根。该方法在内部声明为：

```csharp
public static double Sqrt(double x);
```

输入参数 $x$ 和该方法返回的值都是 `double` 类型。如果 $x \geq 0$，则该方法返回 $x$ 的正平方根。如果 $x < 0$，则该方法返回 NaN。如果 $x = NaN$ 或 $x = PositiveInfinity$，则返回该对应值。

当底 $b$ 是自然底 $e$ 时，表达式 $e^x$ 称为指数函数。方法 `Math.Exp(x)` 通过输入参数 $x$ 将 $e$ 升特定的幂。该方法在内部声明为：

```csharp
public static double Exp(double x);
```

注意输入参数 $x$ 和 `Math.Exp(x)` 产生的输出都是 `double`。如果输入 $x = NaN$ 或 $x = PositiveInfinity$，返回该值而不抛出异常。然而，如果 $x = NegativeInfinity$，则返回 0。

指数函数 $e^x$ 的逆函数是自然对数，或底为 $e$ 的对数，通常写为 $ln(x)$ 或 $log(x)$。方法 `Math.Log(x)` 用于通过输入参数 $x$ 计算底为 $e$ 的自然对数，在内部声明为：

```csharp
public static double Log(double x);
```

如果 $x > 0$，`Math.Log(x)` 返回 $x$ 的自然对数，即 $ln(x)$。如果 $x = 0$，`Math.Log(x)` 返回 $NegativeInfinity$。如果 $x < 0$，`Math.Log(x)` 返回 NaN。

方法 `Math.Log(x)` 还可以重载以返回输入参数 $x$ 和 `newBase` 分别指定的底的对数。该方法在内部声明为：

```csharp
public static double Log(double x, double newBase);
```

如果 $x > 0$ 且 `newBase >= 0`，`Log(x, newBase)` 返回底为 `newBase` 的 $x$ 的对数，即 $log_{newBase}(x)$。如果 `newBase < 0`，`Log(x, newBase)` 返回 NaN。如果 $x = 0$，`Log(x, newBase)` 返回 $NegativeInfinity$。如果 $x < 0$，`Log(x, newBase)` 返回 NaN。底 10 对数在应用程序中发生频率足够，以至于 .NET Framework Math 类库提供了自己的内部方法来取实数的底10对数。方法 `Math.Log10(x)` 用于计算输入参数 $x$ 指定的底10对数。该方法在内部声明为：

```csharp
public static double Log10(double x);
```

如果 $x > 0$，`Math.Log10(x)` 返回 $x$ 的底10对数，即 $log_{10}(x)$。如果 $x = 0$，`Math.Log10(x)` 返回 $NegativeInfinity$。如果 $x < 0$，`Math.Log10(x)` 返回 NaN。

下面的代码段说明了我们讨论的幂、指数和对数方法的使用。

```csharp
public static void PowerExpLog_Example()
{
    double b = 2.75, x = 3.25, newBase = 8.0;
    Console.WriteLine("Exp({0}) = {1}", x, Math.Exp(x));
    Console.WriteLine("Log({0}) = {1}\n", Math.Log(Math.Exp(x)));

    Console.WriteLine("Pow({0}, {1}) = {2}", b, x, Math.Pow(b, x));
    Console.WriteLine("Log10({0})/Log10({1}) = {2}\n", Math.Pow(b, x), Math.Log10(b));

    Console.WriteLine("Log({0}) = {1}", newBase, x); // 注意：此处 OCR 有错误，逻辑建议为 Math.Log(x, newBase)
    // 根据变量上下文假设 Math.Log10(x) 或类似
    Console.WriteLine("Pow({0}, {1}) = {2}", x, newBase);
    Math.Log10(x, newBase); Math.Pow(newBase, Math.Log(x, newBase));
}
```

### 2.3.3 特殊乘法、除法和余数方法

有时当两个32位整数相乘时，最终乘积将大于32位整数数据类型所允许的最大值。虽然可以返回并将变量切换为能够接收大数字的其他数据类型，但可能有理由让变量在相乘时保留原始数据类型。因此，.NET Framework 类库提供了一个名为 `Math.BigMul(x,y)` 的特殊方法，它可以计算两个32位整数的乘积，并产生一个64位整数的输出。该方法在内部声明为：

```csharp
public static long BigMul(int x, int y);
```

同样，.NET Framework 类库提供了一个特殊方法 `Math.DivRem` 用于计算两个整数的商，并将任何余数返回在输出参数中。`DivRem` 方法可以被重载并用于32位和64位整数，其在内部声明声明为：

```csharp
public static int DivRem(int x, int y, out int remainder);
public static long DivRem(long x, long y, out long remainder);
```

最后，方法 `Math.IEERemainder(x,y)` 返回从两个 `double` 类型整数除中得到的余数。其返回值也是 `double` 类型。该方法在内部声明为：

```csharp
public static double IEERemainder(double x, double y);
```

其中 $x$ 是被除数，$y$ 是除数。该方法实际上计算 $x-yQ$，其中 $Q=x/y$ 被舍入到整数。如果 $Q$ 落在两个整数之间，则返回偶整数。如果表达式 $x-yQ$ 为零，则 $x>0$ 时返回 $+0$，$x<0$ 时返回 $-0$。如果 $y=0$，则返回 NaN。

下面的示例演示了 `BigMul`、`DivRem` 和 `IEERemainder` 的使用：

```csharp
public static void MultDivRemExample()
{
    int int1 = Int32.MaxValue;
    int int2 = Int32.MaxValue;
    int intResult;
    long longResult;

    longResult=Math.BigMul(int1,int2);
    Console.WriteLine("{0}*{1}={2}\n", int1,int2,longResult);

    intResult=Math.DivRem(int1,int2,intResult);
    Console.WriteLine("{0}/{1}={2}, with a remainder of ({3}).*", int1,int2,intResult);

    String str="The IEE remainder of {0:f} is ({2:e})";
    divisor=2.0; // (2:e)
    doubleResult=Math.IEERemainder(Double.MaxValue,divisor);
    Console.WriteLine(str,Double.MaxValue,divisor,doubleResult);

    divisor=3.0;
    doubleResult=Math.IEERemainder(Double.MaxValue,divisor);
    Console.WriteLine(str,Double.MaxValue,divisor,doubleResult);
}
```

### 2.3.4 绝对值方法

对于任何实数 $x$，$x$ 的绝对值或模由 $|x|$ 定义，并定义如下：

> |x| = { x if x >= 0 

             -x if x < 0 }

从上面的定义可以看出，$x$ 的绝对值总是正数或零，而不会是负数。.NET Framework 类库提供了方法 `Math.Abs(x)`，用于根据输入参数 $x$ 返回数字的绝对值。该方法在内部声明为：

```csharp
public static [type] Abs([type] x);
```

输入参数 `x` 和返回值具有由 `[type]` 提供的相同数据类型，这意味着该方法可以使用以下数据类型进行重载：`decimal`, `double`, `int32`, `int64`, `sbyte`, `single`。如果输入参数 `x` 等于负无穷 `NegativeInfinity` 或正无穷 `PositiveInfinity`，则返回值为正无穷 `PositiveInfinity`。如果输入参数 `x` 等于 NaN，则返回值为 NaN。下面的代码段说明了 `Math.Abs(x)` 的用法。

```
double x = -2.0;
Console.WriteLine("Before: (0,-5) After: (1,-5)",x,Math.Abs(x));
```

将在显示器屏幕上显示输出输出：

Before: -2.0      After: 2.0

### 2.3.5 符号方法 (Sign Method)

符号函数是一个提取实数符号的数学函数。为了避免与三角正弦函数混淆，该函数通常根据单词“sign”的拉丁语形式称为符号函数（signum function）。实数 `x` 的符号函数如下。该方法的声明如下：

> $$sng(x) = \begin{cases} -1 & \text{如果 } x < 0 \\ 0 & \text{如果 } x = 0 \\ 1 & \text{如果 } x > 0 \end{cases}$$

方法 `Math.Sign(x)` 返回一个指示输入参数 `x` 指定的数字符号的值。该方法在内部声明为：

```csharp
public static int Sign([type] x);
```

输入参数 `x` 是由标签 `[type]` 指定的数据类型，这意味着该方法可以使用以下数据类型进行重载：`int16`, `int32`, `int64`, `sbyte`, `single`, `decimal`, `double`。下面的代码段说明了 `Math.Sign(x)` 的用法：

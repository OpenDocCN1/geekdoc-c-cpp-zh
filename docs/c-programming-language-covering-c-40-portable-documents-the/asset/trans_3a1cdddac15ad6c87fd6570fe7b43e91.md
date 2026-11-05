
|  | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | -z | +0 | -0 | +∞ | -∞ | NaN |
| -x | -z | +z | -0 | +0 | -∞ | +∞ | NaN |
| +0 | +0 | -0 | +0 | -0 | NaN | NaN | NaN |
| -0 | -0 | +0 | -0 | +0 | NaN | NaN | NaN |
| +∞ | +∞ | -∞ | NaN | NaN | +∞ | -∞ | NaN |
| -∞ | -∞ | +∞ | NaN | NaN | -∞ | +∞ | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制乘法：

```
decimal operator *(decimal x, decimal y);
```

如果结果值太大而无法以十进制格式表示，则会抛出 System.OverflowException。如果结果值太小而无法以十进制格式表示，则结果为零。结果的精度，在任何舍入之前，是两个操作数精度的总和。

十进制乘法等价于使用类型 System.Decimal 的乘法运算符。

> PETER SESTOFT 文本在此处以及本章其他地方提到“IEEE 754 浮点”时，更精确的说法应为“IEEE 754 二进制浮点”，因为该 IEEE 标准的 2008 版本描述了二进制和十进制浮点，而这两者是非常不同的东西！
> 
> 此外，以下规则由 IEEE 754 二进制浮点标准规定，并被当前 Microsoft 和 Mono C# 实现所遵守：每当一个或多个操作数为 NaN 时，结果为 NaN，且结果的 NaN 有效载荷等于其中一个 NaN 操作数的有效载荷。64 位 double 的 NaN 有效载荷由其 51 个最低有效位组成（因此 double 可以表示 2^51——大约 2*10^15——个不同的 NaN）。32 位 float 的 NaN 有效载荷由其 22 个最低有效位组成（因此 float 可以表示 2^22——大约 4*10^6——个不同的 NaN）。

NaN 有效载荷的保留对于高效的科学计算非常重要。为了使这种方法真正有效，除了算术运算符之外，System.Math 中的数学函数也应遵守 IEEE 二进制浮点。在当前实现中，它们大多如此。

.NET 库提供方法 System.Double.IsNaN(d) 来测试一个 double 是否为 NaN。

对于类型 double，它还提供了 DoubleToInt64Bits 和 Int64BitsToDouble 方法，可用于获取和设置 NaN 有效载荷位：

```
public static long GetNanPayload(double d) {
    return System.BitConverter.DoubleToInt64Bits(d) & 0x0007FFFFFFFFFFFF;
}
```

```
public static double MakeNanPayload(long nanbits) {
    nanbits &= 0x0007FFFFFFFFFFFF;
    nanbits |= System.BitConverter.DoubleToInt64Bits(Double.NaN);
    return System.BitConverter.Int64BitsToDouble(nanbits);
}
```

奇怪的是，.NET 库没有为类型 float 提供相应的方法，但可以使用不安全指针转换来实现相同的效果。有关详细内容，请参阅对 §18.4 的注释。

## 7.8.2 除法运算符

对于形式为 x / y 的操作，将应用二进制运算符重载解析 (§7.3.4) 来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。

下面列出了预定义的除法运算符。运算符都计算 x 和 y 的商。

- 整数除法：
```
int operator /(int x, int y);
uint operator /(uint x, uint y);
long operator /(long x, long y);
ulong operator /(ulong x, ulong y);
```

如果右操作数的值为零，则会抛出 System.DivideByZeroException。

除法向零舍入。因此结果的绝对值是小于或等于两个操作数商的绝对值的最大可能整数。结果为零或正数，当两个操作数符号相同时；结果为零或负数，当两个操作数符号相反时。

如果左操作数是最小的可表示 int 或 long 值且右操作数为 -1，则会发生溢出。在 checked 上下文中，这会导致抛出 System.OverflowException（或其子类）。在 unchecked 上下文中，是否抛出 System.OverflowException（或其子类）或溢出未报告且结果值为左操作数的值，是实现定义的。

- 浮点除法：

```
float operator /(float x, float y);
double operator /(double x, double y);
```

商是根据 IEEE 754 算术规则计算的。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。在表中，x 和 y 为正有限值；z 是 x / y 的结果。如果结果对于目标类型来说太大，则 z 为无穷大。如果结果对于目标类型来说太小，则 z 为零。

|  | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | -z | +∞ | -∞ | +0 | -0 | NaN |
| -x | -z | +z | -∞ | +∞ | -0 | +0 | NaN |
| +0 | +0 | -0 | NaN | NaN | +0 | -0 | NaN |
| -0 | -0 | +0 | NaN | NaN | -0 | +0 | NaN |
| +∞ | +∞ | -∞ | +∞ | -∞ | NaN | NaN | NaN |
| -∞ | -∞ | +∞ | -∞ | +∞ | NaN | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制除法：

```
decimal operator /(decimal x, decimal y);
```

如果右操作数的值为零，则会抛出 System.DivideByZeroException。如果结果值太大而无法以十进制格式表示，则会抛出 System.OverflowException。如果结果值太小而无法以十进制格式表示，则结果为零。结果的精度是能保留等于真实数学结果最近可表示十进制值的最小精度。

十进制除法等价于使用类型 System.Decimal 的除法运算符。

## 7.8.3 余数运算符

对于形式为 x % y 的操作，将应用二进制运算符重载解析 (§7.3.4) 来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。

下面列出了预定义的余数运算符。运算符都计算 x 和 y 之间除法的余数。

- 整数余数：
```
int operator %(int x, int y);
uint operator %(uint x, uint y);
long operator %(long x, long y);
ulong operator %(ulong x, ulong y);
```

x % y 的结果是由 x - (x / y) * y 产生的值。如果 y 为零，则会抛出 System.DivideByZeroException。

> ERIC LIPPERT 请考虑以下代码：
> 
> ```csharp
> static bool IsOdd(int x) { return x%2 == 1; }
> ```
> 它正确吗？不正确！根据上面的句子，这等同于
> 
> ```csharp
> static bool IsOdd(int x) { return x-(x/2)*2 == 1; }
> ```
> 当 x 为 -1 时为假。正确的代码是
> 
> ```csharp
> static bool IsOdd(int x) { return x%2 != 0; }
> ```

如果左操作数是最小的 int 或 long 值且右操作数为 -1，则会抛出 System.OverflowException。在任何情况下，x % y 抛出异常时，x / y 也会抛出异常。

- 浮点余数：
```
float operator %(float x, float y);
double operator %(double x, double y);
```

下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。在表中，x 和 y 为正有限值；z 是 x % y 的结果，计算为 x - n * y，其中 n 是小于或等于 x / y 的最大可能整数。这种计算余数的方法类似于对整数操作数使用的方法，但与 IEEE 754 定义不同（其中 n 是最接近 x / y 的整数）。

|  | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | +z | NaN | NaN | x | x | NaN |
| -x | -z | -z | NaN | NaN | -x | -x | NaN |
| +0 | +0 | +0 | NaN | NaN | +0 | +0 | NaN |
| -0 | -0 | -0 | NaN | NaN | -0 | -0 | NaN |
| +∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| -∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制余数：
`decimal operator %(decimal x, decimal y);`

如果右操作数的值为零，则会抛出 System.DivideByZeroException。结果的精度，在任何舍入之前，是两个操作数精度中的较大者，且结果的符号，如果非零，则与 x 相同。

十进制余数等价于使用类型 System.Decimal 的余数运算符。

> > CHRIS SELLS “余数”运算符在其他计算机语言中也称为“modulo”，有时表示为“mod”。如果你真是个极客，你会发现自己在（松散地）人类句子中使用“modulo”来代替短语“除……之外”，例如“Modulo 测试、调试和文档，我们准备好发布了！”

## 7.8.4 加法运算符

对于形式为 x + y 的操作，将应用二进制运算符重载解析 (§7.3.4) 来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。

下面列出了预定义的加法运算符。对于数值类型和枚举类型，预定义的加法运算符计算两个操作数的和。当其中一个或

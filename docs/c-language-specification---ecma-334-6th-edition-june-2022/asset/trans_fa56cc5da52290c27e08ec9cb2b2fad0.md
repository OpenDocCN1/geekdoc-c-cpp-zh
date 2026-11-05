

- 整数除法：
`int operator /(int x, int y);`
`uint operator /(uint x, uint y);`
`long operator /(long x, long y);`
`ulong operator /(ulong x, ulong y);`
如果右操作数的值为零，则会抛出 `System.DivideByZeroException`。
除法将结果向零舍入。因此结果的绝对值是两个操作数商的绝对值的最大可能整数，且小于或等于该商。结果为零或正数，当两个操作数符号相同时；结果为零或负数，当两个操作数符号相反时。
如果左操作数是最小的可表示 `int` 或 `long` 值且右操作数为 -1，则会发生溢出。在检查上下文中，这会导致抛出 `System.ArithmeticException`（或其子类）。在未检查上下文中，是否抛出 `System.ArithmeticException`（或其子类）或溢出未报告且结果值为左操作数的值，由实现定义。

- 浮点除法：
`float operator /(float x, float y);`
`double operator /(double x, double y);`
商是根据 IEC 60559 算术规则计算的。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。在表中，x 和 y 为正有限值。z 是 x / y 的结果，四舍五入到最接近的可表示值。

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
`decimal operator /(decimal x, decimal y);`
如果右操作数的值为零，则会抛出 `System.DivideByZeroException`。如果结果值的大小太大而无法以十进制格式表示，则会抛出 `System.OverflowException`。由于舍入，即使第一个操作数不为零，结果也可能为零。在舍入之前，结果的精度是与首选精度最接近且能保持等于精确结果的精度。首选精度是 x 的精度减去 y 的精度。
十进制除法等价于使用类型 `System.Decimal` 的除法运算符。
上面定义的未提升预定义除法运算符的提升形式（§11.4.8）也是预定义的。

## 11.9.4 余数运算符

对于形式为 x % y 的操作，将应用二进制运算符重载解析（§11.4.5）来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型是运算符的返回类型。

下面列出了预定义的余数运算符。这些运算符都计算 x 和 y 之间除法的余数。

- 整数余数：
```
int operator %(int x, int y);
uint operator %(uint x, uint y);
long operator %(long x, long y);
ulong operator %(ulong x, ulong y);
```
x % y 的结果是 x - (x / y) * y 的值。如果 y 为零，则会抛出 System.DivideByZeroException。

如果左操作数是最小的 int 或 long 值且右操作数为 -1，则仅当 x / y 会抛出异常时，才会抛出 System.OverflowException。

- 浮点余数：
```
float operator %(float x, float y);
double operator %(double x, double y);
```
下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。在表中，x 和 y 为正有限值。z 是 x % y 的结果，计算方式为 x - n * y，其中 n 是小于或等于 x / y 的最大可能整数。这种计算余数的方法与用于整数操作数的方法类似，但与 IEC 60559 定义不同（其中 n 是最接近 x / y 的整数）。

|  | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | +z | NaN | NaN | +x | +x | NaN |
| -x | -z | -z | NaN | NaN | -x | -x | NaN |
| +0 | +0 | +0 | NaN | NaN | +0 | +0 | NaN |
| -0 | -0 | -0 | NaN | NaN | -0 | -0 | NaN |
| +∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| -∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制余数：
```
decimal operator %(decimal x, decimal y);
```
如果右操作数的值为零，则会抛出 System.DivideByZeroException。是否抛出 System.ArithmeticException（或其子类）由实现定义。符合规范的实现不得在 x / y 不会抛出异常的任何情况下为 x % y 抛出异常。在舍入之前，结果的精度是两个操作数精度中的较大者，且结果的符号（如果非零）与 x 相同。

十进制余数等价于使用类型 System.Decimal 的余数运算符。

> *注意：这些规则确保对于所有类型，结果永远不会与左操作数符号相反。结束注释*

上面定义的未提升预定义余数运算符的提升形式（§11.4.8）也是预定义的。

## 11.9.5 加法运算符

对于形式为 x + y 的操作，将应用二进制运算符重载解析（§11.4.5）来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型是运算符的返回类型。

下面列出了预定义的加法运算符。对于数值类型和枚举类型，预定义的加法运算符计算两个操作数的和。当一个或两个操作数为 string 类型时，预定义的加法运算符连接操作数的字符串表示形式。

- 整数加法：
```
int operator +(int x, int y);
uint operator +(uint x, uint y);
long operator +(long x, long y);
ulong operator +(ulong x, ulong y);
```
在检查上下文中，如果和超出结果类型的范围，则会抛出 System.OverflowException。在未检查上下文中，溢出不会被报告，超出结果类型范围的任何重要高位都被丢弃。

- 浮点加法：
```
float operator +(float x, float y);
double operator +(double x, double y);
```
和是根据 IEC 60559 算术规则计算的。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。在表中，x 和 y 为非零有限值，z 是 x + y 的结果。如果 x 和 y 具有相同大小但符号相反，则 z 为正零。如果 x + y 太大而无法在目标类型中表示，则 z 为与 x + y 具有相同符号的无穷大。

| | y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|
| x | z | x | x | +∞ | -∞ | NaN |
| +0 | y | +0 | +0 | +∞ | -∞ | NaN |
| -0 | y | +0 | -0 | +∞ | -∞ | NaN |
| +∞ | +∞ | +∞ | +∞ | +∞ | NaN | NaN |
| -∞ | -∞ | -∞ | -∞ | NaN | -∞ | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制加法：
```
decimal operator +(decimal x, decimal y);
```
如果结果值的大小太大而无法以十进制格式表示，则会抛出 System.OverflowException。在舍入之前，结果的精度是两个操作数精度中的较大者。

十进制加法等价于使用类型 System.Decimal 的加法运算符。

- 枚举加法。每个枚举类型隐式提供以下预定义运算符，其中 E 是枚举类型，U 是 E 的基础类型：
  
  `E operator +(E x, U y);`
  `E operator +(U x, E y);`

在运行时，这些运算符的求值方式与 (E)((U)x + (U)y) 完全相同。

- 字符串连接：
  
  `string operator +(string x, string y);`
  `string operator +(string x, object y);`
  `string operator +(object x, string y);`

这些二进制 + 运算符的重载执行字符串连接。如果字符串连接的操作数为 null，则替换为空字符串。否则，任何非字符串操作数都通过调用从 object 类型继承的虚拟 ToString 方法转换为其字符串表示形式。如果 ToString 返回 null，则替换为空字符串。

示例：
```
using System;
class Test
{
    static void Main()
    {
        string s = null;
        Console.WriteLine("s = >" + s + "<");  // Displays s = ><

        int i = 1;
        Console.WriteLine("i = " + i);          // Displays i = 1

        float f = 1.2300E+15F;
        Console.WriteLine("f = " + f);          // Displays f = 1.23E+15

        decimal d = 2.900m;
        Console.WriteLine("d = " + d);          // Displays d = 2.900
    }
}
```
注释中显示的输出是在美式英语系统上的典型结果。精确的输出可能取决于执行环境的区域设置。字符串连接运算符本身在每种情况下的行为都相同，但执行期间隐式调用的 ToString 方法可能会受到区域设置的影响。

结束示例

字符串连接运算符的结果是一个字符串，由左操作数的字符后跟右操作数的字符组成。字符串连接运算符永远不会返回 null 值。如果没有足够的内存来分配结果字符串，则可能会抛出 System.OutOfMemoryException。

- 委托组合。每个委托类型隐式提供以下预定义运算符，其中 D 是委托类型：
  
  `D operator +(D x, D y);`
  
  如果第一个操作数为 null，则操作的结果是第二个操作数的值（即使它也是 null）。否则，如果第二个操作数为 null，则操作的结果是


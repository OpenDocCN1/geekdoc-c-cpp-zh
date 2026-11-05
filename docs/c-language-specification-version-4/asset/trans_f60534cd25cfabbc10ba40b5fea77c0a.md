
| | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +X | +Z | +Z | NaN | NaN | X | X | NaN |
| -X | -Z | -Z | NaN | NaN | -X | -X | NaN |
| +0 | +0 | +0 | NaN | NaN | +0 | +0 | NaN |
| -0 | -0 | -0 | NaN | NaN | -0 | -0 | NaN |
| +∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| -∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制余数：

    ```
    decimal operator %(decimal x, decimal y);
    ```

    如果右操作数的值为零，则引发 System.DivideByZeroException。在进行任何舍入之前，结果的小数位数是两个操作数中小数位数较大者；如果结果非零，则其符号与 x 的符号相同。

    decimal 余数等效于使用 System.Decimal 类型的余数运算符。

### 7.8.4 加法运算符

对于形如 x + y 的运算，应用二元运算符重载决策（§7.3.4）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型是该运算符的返回类型。

下面列出预定义的加法运算符。对于数值类型和枚举类型，预定义的加法运算符计算两个操作数之和。当一个或两个操作数为 string 类型时，预定义的加法运算符将操作数的字符串表示形式串联起来。

- 整数加法：

    ```
    int operator +(int x, int y);
    uint operator +(uint x, uint y);
    long operator +(long x, long y);
    ulong operator +(ulong x, ulong y);
    ```

    在 checked 上下文中，如果和超出结果类型的范围，则引发 System.OverflowException。在 unchecked 上下文中，不报告溢出，并且丢弃结果类型范围之外的任何有效高阶位。

- 浮点加法：

    ```
    float operator +(float x, float y);
    double operator +(double x, double y);
    ```

    和根据 IEEE 754 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是非零有限值，z 是 x + y 的结果。如果 x 和 y 具有相同量值但符号相反，则 z 为正零。如果 x + y 太大而无法在目标类型中表示，则 z 是与 x + y 符号相同的无穷大。

    | | y | +0 | -0 | +∞ | -∞ | NaN |
    |---|---|---|---|---|---|---|
    | x | z | x | x | +∞ | -∞ | NaN |
    | +0 | y | +0 | +0 | +∞ | -∞ | NaN |
    | -0 | y | +0 | -0 | +∞ | -∞ | NaN |
    | +∞ | +∞ | +∞ | +∞ | +∞ | NaN | NaN |
    | -∞ | -∞ | -∞ | -∞ | NaN | -∞ | NaN |
    | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- decimal 加法：

    ```csharp
    decimal operator +(decimal x, decimal y);
    ```

    如果结果值太大而无法用 decimal 格式表示，则引发 System.OverflowException。在进行任何舍入之前，结果的小数位数是两个操作数中小数位数较大者。

    decimal 加法等效于使用 System.Decimal 类型的加法运算符。

- 枚举加法。每个枚举类型都隐式提供以下预定义运算符，其中 E 是枚举类型，U 是 E 的基础类型：

    ```csharp
    E operator +(E x, U y);
    E operator +(U x, E y);
    ```

    在运行时，这些运算符完全按照 (E)((U)x + (U)y) 求值。

- 字符串串联：

    ```csharp
    string operator +(string x, string y);
    string operator +(string x, object y);
    string operator +(object x, string y);
    ```

    二元 + 运算符的这些重载执行字符串串联。如果字符串串联的操作数为 null，则替换为空字符串。否则，任何非字符串参数都通过调用从 object 类型继承的虚拟 ToString 方法转换为字符串表示形式。如果 ToString 返回 null，则替换为空字符串。

    ```
    using System;
    class Test
    {
        static void Main() {
            string s = null;
            Console.WriteLine("s = >" + s + "<");    // displays s = ><
            int i = 1;
            Console.WriteLine("i = " + i);           // displays i = 1
            float f = 1.2300E+15F;
            Console.WriteLine("f = " + f);           // displays f = 1.23E+15
            decimal d = 2.900m;
            Console.WriteLine("d = " + d);           // displays d = 2.900
        }
    }
    ```

    字符串串联运算符的结果是一个字符串，它由左操作数的字符后跟右操作数的字符组成。字符串串联运算符从不返回 null 值。如果没有足够内存来分配结果字符串，则可能引发 System.OutOfMemoryException。

- 委托组合。每个委托类型都隐式提供以下预定义运算符，其中 D 是委托类型：

    ```
    D operator +(D x, D y);
    ```

    当两个操作数都是某个委托类型 D 时，二元 + 运算符执行委托组合。（如果操作数具有不同的委托类型，则发生绑定期错误。）如果第一个操作数为 null，则运算结果是第二个操作数的值（即使该值也为 null）。否则，如果第二个操作数为 null，则运算结果是第一个操作数的值。否则，运算结果是一个新的委托实例，调用该实例时，先调用第一个操作数，再调用第二个操作数。有关委托组合的示例，请参见 §7.8.5 和 §15.4。由于 System.Delegate 不是委托类型，因此未为其定义运算符 +。

### 7.8.5 减法运算符

对于形如 x - y 的运算，应用二元运算符重载决策（§7.3.4）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型是该运算符的返回类型。

下面列出预定义的减法运算符。这些运算符都从 x 中减去 y。

- 整数减法：

    ```
    int operator -(int x, int y);
    uint operator -(uint x, uint y);
    long operator -(long x, long y);
    ulong operator -(ulong x, ulong y);
    ```

    在 checked 上下文中，如果差超出结果类型的范围，则引发 System.OverflowException。在 unchecked 上下文中，不报告溢出，并且丢弃结果类型范围之外的任何有效高阶位。

- 浮点减法：

    ```
    float operator -(float x, float y);
    double operator -(double x, double y);
    ```

    差根据 IEEE 754 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是非零有限值，z 是 x - y 的结果。如果 x 和 y 相等，则 z 为正零。如果 x - y 太大而无法在目标类型中表示，则 z 是与 x - y 符号相同的无穷大。

    | | y | +0 | -0 | +∞ | -∞ | NaN |
    |---|---|---|---|---|---|---|
    | x | z | x | x | -∞ | +∞ | NaN |
    | +0 | -y | +0 | +0 | -∞ | +∞ | NaN |
    | -0 | -y | -0 | +0 | -∞ | +∞ | NaN |
    | +∞ | +∞ | +∞ | +∞ | NaN | +∞ | NaN |
    | -∞ | -∞ | -∞ | -∞ | -∞ | NaN | NaN |
    | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- decimal 减法：

    ```
    decimal operator -(decimal x, decimal y);
    ```

    如果结果值太大而无法用 decimal 格式表示，则引发 System.OverflowException。在进行任何舍入之前，结果的小数位数是两个操作数中小数位数较大者。

    decimal 减法等效于使用 System.Decimal 类型的减法运算符。

- 枚举减法。每个枚举类型都隐式提供以下预定义运算符，其中 E 是枚举类型，U 是 E 的基础类型：

    `U operator -(E x, E y);`

    此运算符完全按照 (U)((U)x - (U)y) 求值。换言之，该运算符计算 x 和 y 的序数值之差，结果的类型是枚举的基础类型。

    `E operator -(E x, U y);`

    此运算符完全按照 (E)((U)x - y) 求值。换言之，该运算符从枚举的基础类型中减去一个值，从而产生枚举值。

- 委托移除。每个委托类型都隐式提供以下预定义运算符，其中 D 是委托类型：

    `D operator -(D x, D y);`

    当两个操作数都是某个委托类型 D 时，二元 - 运算符执行委托移除。如果操作数具有不同的委托类型，则发生绑定期错误。如果第一个操作数为 null，则运算结果为 null。否则，如果第二个操作数为 null，则运算结果是第一个操作数的值。否则，两个操作数都表示具有一个或多个条目的调用列表（§15.1），并且如果第二个操作数的列表是第一个操作数列表的适当连续子列表，则结果是一个新的调用列表，它由从第一个操作数的列表中移除第二个操作数的条目后组成。（为了确定子列表相等性，相应条目按照委托相等运算符（§7.10.8）的方式进行比较。）否则，结果是左操作数的值。在此过程中，两个操作数的列表都不会更改。如果第二个操作数的列表与第一个操作数列表中的多个连续条目子列表匹配，则移除最右侧匹配的连续条目子列表。如果移除导致空列表，则结果为 null。例如：

    ```
    delegate void D(int x);
    class C
    {
        public static void M1(int i) { /* ... */ }
        public static void M2(int i) { /* ... */ }
    }
    class Test
    {
        static void Main() {
            D cd1 = new D(C.M1);
            D cd2 = new D(C.M2);
            D cd3 = cd1 + cd2 + cd2 + cd1;    // M1 + M2 + M2 + M1
            cd3 -= cd1;                       // => M1 + M2 + M2

            cd3 = cd1 + cd2 + cd2 + cd1;      // M1 + M2 + M2 + M1
            cd3 -= cd1 + cd2;                 // => M2 + M1

            cd3 = cd1 + cd2 + cd2 + cd1;      // M1 + M2 + M2 + M1
            cd3 -= cd2 + cd2;                 // => M1 + M1

            cd3 = cd1 + cd2 + cd2 + cd1;      // M1 + M2 + M2 + M1
            cd3 -= cd2 + cd1;                 // => M1 + M2

            cd3 = cd1 + cd2 + cd2 + cd1;      // M1 + M2 + M2 + M1
            cd3 -= cd1 + cd1;                 // => M1 + M2 + M2 + M1
        }
    }
    ```

## 7.9 移位运算符

<< 和 >> 运算符用于执行移位操作。


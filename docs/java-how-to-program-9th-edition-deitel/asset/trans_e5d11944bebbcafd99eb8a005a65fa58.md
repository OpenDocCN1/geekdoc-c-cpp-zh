

Hashcode of "Hello" is 42628b2
Hashcode of null is NULL
Printing a % in a format string
Printing a new line
next line starts here

图 G.11 | 使用 b、B、h、H、% 和 n 转换字符。（第 2 部分，共 2 部分。）

## 常见编程错误 G.2

在格式字符串中使用 % 而不是 %% 来打印字面百分号字符，可能会导致难以察觉的逻辑错误。当 % 出现在格式字符串中时，其后必须跟一个转换字符。这个单独的百分号可能会意外地后跟一个合法的转换字符，从而导致逻辑错误。

## G.9 使用字段宽度和精度打印

数据打印时所在字段的大小由字段宽度指定。如果字段宽度大于所打印的数据，默认情况下数据在该字段中右对齐。我们将在 G.10 节讨论左对齐。在格式说明符中，在 % 和转换字符之间插入一个表示字段宽度的整数（例如 %4d）。图 G.12 打印两组数字，每组五个，将位数少于字段宽度的数字右对齐。字段宽度会被扩大以打印比字段更宽的值，而且负值的减号在字段中占用一个字符位置。此外，如果没有指定字段宽度，数据将按所需位置数精确打印。字段宽度可用于除行分隔符（%n）之外的所有格式说明符。

```
1  // Fig. G.12: FieldWidthTest.java
2  // Right justifying integers in fields.

4  public class FieldWidthTest
5  {
6      public static void main( String[] args )
7      {
8          System.out.printf( "%4d\n", 1 );
9          System.out.printf( "%4d\n", 12 );
10         System.out.printf( "%4d\n", 123 );
11         System.out.printf( "%4d\n", 1234 );
12         System.out.printf( "%4d\n", 12345 ); // data too large

14         System.out.printf( "%4d\n", -1 );
15         System.out.printf( "%4d\n", -12 );
16         System.out.printf( "%4d\n", -123 );
17         System.out.printf( "%4d\n", -1234 ); // data too large
18         System.out.printf( "%4d\n", -12345 ); // data too large
19     } // end main
20 } // end class RightJustifyTest
```

图 G.12 | 在字段中右对齐整数。（第 1 部分，共 2 部分。）

图 G.12 | 在字段中右对齐整数。（第 2 部分，共 2 部分。）

## 常见编程错误 G.3

> 未提供足够大的字段宽度来处理要打印的值，可能会使其他正在打印的数据错位并产生令人困惑的输出。请了解你的数据！

printf 方法还提供了指定数据打印精度的能力。精度对不同类型有不同的含义。当与浮点转换字符 e 和 f 一起使用时，精度是小数点后出现的数字位数。当与转换字符 g、a 或 A 一起使用时，精度是要打印的最大有效数字位数。当与转换字符 s 一起使用时，精度是要从字符串中写入的最大字符数。要使用精度，请在百分号和转换说明符之间放置一个小数点（.），后跟一个表示精度的整数。图 G.13 演示了在格式字符串中使用精度的情况。当浮点值的打印精度小于该值原有小数位数时，该值会被四舍五入。此外，格式说明符 %.3g 表示用于显示浮点值的总位数为 3。由于该值在小数点左边有三位数字，因此该值会被四舍五入到个位。

字段宽度和精度可以组合使用，方法是在百分号和转换字符之间放置字段宽度，后跟一个小数点，再后跟一个精度，如下面的语句所示：

```
printf( "%9.3f", 123.456789 );
```

该语句显示 123.457，小数点右边有三位数字，并在宽度为 9 的字段中右对齐——该数字在其字段中前面会有两个空格。

```
1  // Fig. G.13: PrecisionTest.java
2  // Using precision for floating-point numbers and strings.
3  public class PrecisionTest
4  {
5      public static void main( String[] args )
6      {
7          double f = 123.94536;
8          String s = "Happy Birthday";
```

图 G.13 | 对浮点数和字符串使用精度。（第 1 部分，共 2 部分。）

```
// Fig. G.15: MinusFlagTest.java
// Right justifying and left justifying values.

public class MinusFlagTest
{
    public static void main( String[] args )
    {
        System.out.println( "Columns:" );
        System.out.println( "0123456789012345678901234567890123456789\n" );
        System.out.printf( "%10s%10d%10c%10f\n\n", "hello", 7, 'a', 1.23 );
        System.out.printf(
            "%-10s%-10d%-10c%-10f\n", "hello", 7, 'a', 1.23 );
    } // end main
} // end class MinusFlagTest
```

```
Columns:
0123456789012345678901234567890123456789

      hello         7          a   1.230000
hello       7           a           1.230000
```

图 G.15 | 右对齐和左对齐值。

```
// Fig. G.16: PlusFlagTest.java
// Printing numbers with and without the + flag.

public class PlusFlagTest
{
    public static void main( String[] args )
    {
        System.out.printf( "%d\t%d\n", 786, -786 );
        System.out.printf( "%+d\t%+d\n", 786, -786 );
    } // end main
} // end class PlusFlagTest
```

```
786     -786
+786    -786
```

图 G.16 | 使用和不使用 + 标志打印数字。

图 G.17 使用空格标志在正数前面添加一个空格。这对于对齐位数相同的正数和负数很有用。输出中 -547 前面没有空格，因为它带有负号。图 G.18 使用 # 标志为八进制值添加前缀 0，为十六进制值添加前缀 0x。

```
// Fig. G.17: SpaceFlagTest.java
// Printing a space before non-negative values.
```

图 G.17 | 在非负值前面打印一个空格。（第 1 部分，共 2 部分。）

```
4 public class SpaceFlagTest
5 {
6     public static void main( String[] args )
7     {
8         System.out.printf( "% d\n% d\n", 547, -547 );
9     } // end main
10 } // end class SpaceFlagTest
```

547
-547

图 G.17 | 在非负值前面打印一个空格。（第 2 部分，共 2 部分。）

```
// Fig. G.18: PoundFlagTest.java
// Using the # flag with conversion characters o and x.

public class PoundFlagTest
{
    public static void main( String[] args )
    {
        int c = 31;      // initialize c

        System.out.printf( "#%o\n", c );
        System.out.printf( "#%x\n", c );
    } // end main
} // end class PoundFlagTest
```

037
0x1f

图 G.18 | 将 # 标志与转换字符 o 和 x 一起使用。

图 G.19 结合使用 + 标志、0 标志和空格标志，在宽度为 9 的字段中打印带 + 号和前导零的 452；接着仅使用 0 标志在宽度为 9 的字段中打印 452；然后仅使用空格标志在宽度为 9 的字段中打印 452。

```
// Fig. G.19: ZeroFlagTest.java
// Printing with the 0 (zero) flag fills in leading zeros.

public class ZeroFlagTest
{
    public static void main( String[] args )
    {
        System.out.printf( "%+09d\n", 452 );
        System.out.printf( "%09d\n", 452 );
        System.out.printf( "% 9d\n", 452 );
    } // end main
} // end class ZeroFlagTest
```

图 G.19 | 使用 0（零）标志打印时填充前导零。（第 1 部分，共 2 部分。）

图 G.19 | 使用 0（零）标志打印时填充前导零。（第 2 部分，共 2 部分。）

```
+00000452
000000452
      452
```

图 G.20 使用逗号（,）标志显示带千位分隔符的十进制数和浮点数。图 G.21 使用 ( 标志将负数括在括号中。输出中数字 50 没有被括号括起来，因为它是正数。

```
// Fig. G.20: CommaFlagTest.java
// Using the comma (,) flag to display numbers with thousands separator.

public class CommaFlagTest
{
    public static void main( String[] args )
    {
        System.out.printf( "%,d\n", 58625 );
        System.out.printf( "%,.2f", 58625.21 );
        System.out.printf( "%,.2f", 12345678.9 );
    } // end main
} // end class CommaFlagTest
```

```
58,625
58,625.21
12,345,678.90
```

图 G.20 | 使用逗号（,）标志显示带千位分隔符的数字。

```
// Fig. G.21: ParenthesesFlagTest.java
// Using the ( flag to place parentheses around negative numbers.

public class ParenthesesFlagTest
{
    public static void main( String[] args )
    {
        System.out.printf( "%(d\n", 50 );
        System.out.printf( "%(d\n", -50 );
        System.out.printf( "%( .1e\n", -50.0 );
    } // end main
} // end class ParenthesesFlagTest
```

```
50
(50)
(5.0e+01)
```

图 G.21 | 使用 ( 标志将负数括在括号中。


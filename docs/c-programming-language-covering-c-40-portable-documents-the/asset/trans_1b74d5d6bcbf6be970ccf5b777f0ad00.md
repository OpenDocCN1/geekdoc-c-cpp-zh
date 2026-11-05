
前缀“@”允许将关键字用作标识符，这在与其他编程语言交互时很有用。字符 @ 实际上不是标识符的一部分，因此在其他语言中，该标识符可能被视为不带前缀的普通标识符。带 @ 前缀的标识符称为逐字标识符。对于不是关键字的标识符，允许使用 @ 前缀，但作为风格问题，强烈不建议这样做。

示例

```
class @class
{
    public static void @static(bool @bool) {
        if (@bool)
            System.Console.WriteLine("true");
        else
            System.Console.WriteLine("false");
    }
}

class Class1
{
    static void M() {
        cl\u0061ss.st\u0061tic(true);
    }
}
```

定义了一个名为“class”的类，其中有一个名为“static”的静态方法，该方法接受一个名为“bool”的参数。注意，由于关键字中不允许使用 Unicode 转义，因此标记“cl\u0061ss”是一个标识符，并且与“@class”是同一个标识符。

如果两个标识符在按顺序应用以下变换后相同，则认为它们是同一个标识符：

- 如果使用了前缀“@”，则将其移除。
- 将每个 unicode-escape-sequence 转换为对应的 Unicode 字符。
- 移除任何格式字符。

包含两个连续下划线字符（U+005F）的标识符保留给实现使用。例如，实现可能提供以两个下划线开头的扩展关键字。

## 2.4.3 关键字

关键字是一种类似标识符的字符序列，它是保留的，除非以 @ 字符开头，否则不能用作标识符。

*关键字：以下之一*

| abstract | as | base | bool | break |
|---|---|---|---|---|
| byte | case | catch | char | checked |
| class | const | continue | decimal | default |
| delegate | do | double | else | enum |
| event | explicit | extern | false | finally |
| fixed | float | for | foreach | goto |
| if | implicit | in | int | interface |
| internal | is | lock | long | namespace |
| new | null | object | operator | out |
| override | params | private | protected | public |
| readonly | ref | return | sbyte | sealed |
| short | sizeof | stackalloc | static | string |
| struct | switch | this | throw | true |
| try | typeof | uint | ulong | unchecked |
| unsafe | ushort | using | virtual | void |
| volatile | while |  |  |  |

在语法的某些位置，特定标识符具有特殊含义，但它们不是关键字。此类标识符有时称为“上下文关键字”。例如，在属性声明中，“get”和“set”标识符具有特殊含义（§10.7.2）。在这些位置绝不允许使用 get 或 set 以外的标识符，因此这种用法不会与这些词作为标识符的用法冲突。在其他情况下，例如隐式类型局部变量声明（§8.5.1）中的标识符“var”，上下文关键字可能与已声明名称冲突。在这种情况下，已声明的名称优先于将该标识符用作上下文关键字。

> **ERIC LIPPERT** C# 自最初发布以来没有添加任何新的保留关键字。所有需要新关键字的新语言特性（yield、select 等）都使用“上下文关键字”，这些关键字不是保留的，仅在上下文中具有特殊含义。这一决定有助于保持与现有程序的向后兼容性。

> **VLADIMIR RESHETNIKOV** 如果你需要这些上下文关键字的完整列表（包括支持的特性目标），如下所示：
> 
> ```
> add alias ascending assembly by descending dynamic equals field from get global group into join let method module on orderby param partial property
> remove select set type typevar value var where yield
> ```

## 2.4.4 字面量

字面量是值的源代码表示形式。

```
literal:
    boolean-literal
    integer-literal
    real-literal
    character-literal
    string-literal
    null-literal
```

### 2.4.4.1 布尔字面量

有两个布尔字面量值：true 和 false。

```
boolean-literal:
    true
    false
```

布尔字面量的类型是 bool。

### 2.4.4.2 整数字面量

整数字面量用于书写 int、uint、long 和 ulong 类型的值。整数字面量有两种可能形式：十进制和十六进制。

```
integer-literal:
    decimal-integer-literal
    hexadecimal-integer-literal
```

```
decimal-integer-literal:
    decimal-digits   integer-type-suffix_opt
```

```
decimal-digits:
    decimal-digit
    decimal-digits   decimal-digit
```

```
decimal-digit: one of
    0 1 2 3 4 5 6 7 8 9
```

```
integer-type-suffix: one of
    U u L l UL Ul uL ul LU Lu lU lu
```

hexadecimal-integer-literal:
0x hex-digits integer-type-suffix_opt
0X hex-digits integer-type-suffix_opt

hex-digits:
hex-digit
hex-digits hex-digit

hex-digit: one of
0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f

> **ERIC LIPPERT** C# 不支持八进制字面量，原因有二。首先，如今几乎没有人使用八进制字面量。其次，如果 C# 支持标准“前导零表示八进制”格式的八进制，那么它将成为潜在的错误来源。考虑以下代码：
> 
> `FlightNumber = 0541;`
> 
> 显然，这个表达式意图作为十进制字面量，而不是八进制字面量。

整数字面量的类型按如下方式确定：

- 如果字面量没有后缀，则其类型为下列类型中第一个能够表示其值的类型：int、uint、long、ulong。
- 如果字面量带有 U 或 u 后缀，则其类型为下列类型中第一个能够表示其值的类型：uint、ulong。
- 如果字面量带有 L 或 l 后缀，则其类型为下列类型中第一个能够表示其值的类型：long、ulong。
- 如果字面量带有 UL、Ul、uL、ul、LU、Lu、lU 或 lu 后缀，则其类型为 ulong。

如果整数字面量表示的值超出 ulong 类型的范围，则发生编译时错误。

作为风格问题，建议在书写 long 类型字面量时使用“L”而不是“l”，因为很容易将字母“l”与数字“1”混淆。

为了允许将尽可能小的 int 和 long 值写成十进制整数字面量，存在以下两条规则：

- 当值为 2147483648（2^31）且没有 integer-type-suffix 的 decimal-integer-literal 作为紧跟在一元减运算符标记（§7.7.2）之后的标记出现时，结果是类型为 int、值为 -2147483648（-2^31）的常量。在所有其他情况下，此类 decimal-integer-literal 属于 uint 类型。
- 当值为 9223372036854775808（2^63）且没有 integer-type-suffix 或带有 integer-type-suffix L 或 l 的 decimal-integer-literal 作为紧跟在一元减运算符标记（§7.7.2）之后的标记出现时，结果是类型为 long、值为 -9223372036854775808（-2^63）的常量。在所有其他情况下，此类 decimal-integer-literal 属于 ulong 类型。

> **JOSEPH ALBAHARI** 得益于隐式常量表达式转换（§6.1.8），整数字面量可以直接赋给 uint、long 和 ulong 类型（以及 short、ushort、byte 和 sbyte）：
> 
> ```
> uint x = 3; long y = 3; ulong z = 3;
> ```
> 
> 因此，U 和 L 后缀很少有必要。它们仍然有用的一个示例是，对否则会采用 32 位算术的字面量强制进行 64 位计算：
> 
> ```
> long error = 1000000 * 1000000; // Compile-time error (32-bit overflow)
> long trillion = 1000000L * 1000000L; // Okay -- no overflow
> ```

### 2.4.4.3 实数字面量

实数字面量用于书写 float、double 和 decimal 类型的值。

real-literal:
  decimal-digits . decimal-digits exponent-part_opt real-type-suffix_opt
  . decimal-digits exponent-part_opt real-type-suffix_opt
  decimal-digits exponent-part_opt real-type-suffix_opt
  decimal-digits real-type-suffix

exponent-part:
  e sign_opt decimal-digits
  E sign_opt decimal-digits

sign: one of
  + -

real-type-suffix: one of
  F f D d M m


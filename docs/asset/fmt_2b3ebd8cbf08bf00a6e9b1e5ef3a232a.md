
数值补码方案背后的概念可以简要解释如下：基 `$b$` 的 `$n$` 位数的基数补码定义为 `$b^n-y$`。将此与另一个 `$x$`（其中 `$x \le y$`）相加得到值 `$x+b^n-y$` 或 `$x-y+b^n$`，它始终大于 `$b^n$`。从这个总和中减去 `$b^n$`，我们得到 `$x-y$`，这正是所需的结果。在十进制数字系统中，基数补码称为十补（ten's complement），减小基数补码称为九补（nine's complement）。在二进制数字系统中，基数补码称为二补（two's complement），减小基数补码称为一补（ones' complement）。

由于 `$b^n-1 = b^n-1^n = (b-1)(b^{n-1}+b^{n-2}+...+b+1) = (b-1)b^{n-1}+... + (b-1)$`，我们观察到 `$(b^n-1)$` 只是数字 `$b-1$` 的多次重复。因此，基数补码 `$b^n-y$` 最容易通过向减小基数补码 `$(b^n-1)-y$` 加 1 来得到。即 `$b^n-y=(b^n-1)-y+1$`。减小的

# C# 中的数值方法、算法与工具

一个数的减小基数补码通过从 `$b-1$` 减去 `$y$` 中的每一位找到。

最后，加 1 得到基数补码可以单独进行，但通常与 `$x$` 和 `$y$` 补码的相加结合。对于给定基数的总数字数的任何溢出直接被丢弃。以下两个示例将说明上述描述的算法背后的思想。考虑以下减法：`73-28`，其中 `$x=73$` 且 `$y=28$`。使用补码从另一个数减去 `$y$`，是将 `$y$` 的十补（一补加 1）加到 `$x$`。因此，首先通过确定每个位的补码来获得 `$y$` 的九补。3 的补是 6，7 的补是 2，依此类推。因此，

```
73 (x)
+ 71 (y 的补码)
+ 1 (得到 y 的十补)
====
145
```

丢弃第一位，得到 45，这是正确答案。如果减数的位数少于被减数，必须添加导零并取其一补。例如，`785-91=785+70+1=856`，这显然是错误的答案。

注：原文中多次重复“如果减数的位数少于被减数，必须添加导零并取其一补。例如，785-91=785+70+1=856，这显然是错误的答案”等段落。

| 位 1 | 位 2 | 位 1 & 位 2 | 位 1 | 2 |
| :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 0 | 1 |

`long` 和 `ulong`。位与 `(&)`、位或 `(|)` 和位异或 `(^)` 运算符的操作与其逻辑版本类似，不同在于它们的版本在位上操作。这些运算符的实际功能见表 6.1。此外，*左移* `<<` 将左操作数向左移动右操作数中指定的位数。右侧位被替换为 0，任何左移的 1 丢失。*右移* `>>` 将左操作数向右移动右操作数中指定的位数。左侧空位在数字为正时填充 0，任何右移的 1 丢失。

对于负数，无论符号如何，左移，且当数值无符号或有符号正数时，右移的空位将填充 0。然而，对于有符号的负数，大多数编译器将意图保留值的负符号，并在右移时，空位将被 1 替换而不是 0。如果你有一个负数并想让左侧位变为 0 而不是 1，你可以与一个在空位为 0 在其他位为 1 的掩码进行与运算，右右操作如下：

```csharp
int negvalue = -1;
negvalue = negvalue >> numbitsToShift & 0xF
```

注意，此代码立即在变量 `numbitsToShift` 指定左侧放置 0，指示负值向右移动了多少位。尽管你可以在单个表达式中使用多次移动，但警告读者，如果任何方向的移动超过了所用数据类型允许的总位数，位操作可能会产生未定义的结果。

每个位代表连续的 2 的幂，向右移位的效果是每次移动除以 2。相反，向左移位的效果是每次移动乘以 2。这些移位功能不仅为我们提供了一种计算的替代或华丽方式，还有助于在需要较少移动时提高计算速度。例如，将十进制数转换为相应的二进制、八进制和十六进制的问题。为了将一个十进制数转换为二进制，我们需要通过除以 2 或简单地将数字的位表示位移 1 位来实现。同样，为了转换为八进制，我们需要将目标数字的位表示位移 3 位。转换为转换为十六进制，我们需要位移 4 位，依此类推。下面所示的 `DecToBinOctOrHex` 方法说明了这一思想。该方法还进行了重载，以适应 `int32` 和数据类型的正、负值。此外，基数转换程序现在允许包含数值的小数部分。

```csharp
public static string DecToBinOctOrHex(int number, int basal)
{
    int n, bitcounter, bitshift, startbit;
    string digit = "0123456789ABCDEF";
    switch (basal)
    {
        case 2:
            startbit = 31;
            bitshift = 1;
            break;
        case 8:
            startbit = 30;
            bitshift = 3;
            break;
        case 16:
            startbit = 28;
            bitshift = 4;
            break;
        default:
            startbit = 0;
            bitshift = 0;
            break;
    }
    StringBuilder output = new StringBuilder();
    for (bitcounter = startbit, n = number; bitcounter >= 0;
    {
        output.Append(digit[(n >> bitcounter) & (basal - 1)]);
        bitcounter -= bitshift;
    }
    return output.ToString();
}
```

```csharp
public static string DecToBinOctOrHex(double number, int basal)
{
    int n, bitcounter, bitshift, startbit;
    string digit = "0123456789ABCDEF";
    switch (basal)
    {
        case 2:
            startbit = 31;
            bitshift = 1;
            break;
```

# 位与字节

```csharp
case 8:
    startbit = 30;
    bitshift = 3;
    break;
case 16:
    startbit = 28;
    bitshift = 4;
    break;
default:
    startbit = 0;
    bitshift = 0;
    break;
```

StringBuilder output = new StringBuilder();

for (bitcounter = startbit, n = (int)Math.Truncate(number);

    bitcounter >= 0; bitcounter -= bittift) {

    output.Append(digit[(n >> bitcounter) & (baseval - 1)]);

}

output.Append(number + "*");

for (int i = 0; i < 12; i++) {

    number = (number - Math.Truncate(number)) * baseval;

    output.Append(digit[(int)Math.Truncate(number)]);

}

return output.ToString();

```

```csharp
// 测试代码的简单驱动程序
// 将整数转换为二进制
int intdata = 28;
string msg = "Integer {0} in decimal = {1} in binary.\n";
Console.WriteLine(msg, intdata, DecToBinOctOrHex(intdata, 2));
intdata = -28;
```

```csharp
// 将 double 转换为二进制
double dbldata = 3.141592653589793;
msg = "Double {0} in decimal = {1} in binary.\n";
Console.WriteLine(msg, dbldata, DecToBinOctOrHex(dbldata, 2));
dbldata = -3.141592653589793;
Console.WriteLine(msg, dbldata, DecToBinOctOrHex(dbldata, 2));
```

```csharp
// 将整数转换为八进制
intdata = 28;
msg = "Integer {0} in decimal = {1} in octal.\n";
Console.WriteLine(msg, intdata, DecToBinOctOrHex(intdata, 8));
intdata = -28;
```

```csharp
// 将 double 转换为八进制
double dbldata = 3.141592653589793;
msg = "Double {0} in decimal = {1} in octal.\n";
Console.WriteLine(msg, dbldata, DecToBinOctOrHex(dbldata, 8));
```

© 2010 by Taylor and Francis Group, LLC

# C# 中的数值方法、算法与工具

```csharp
dbldata = -3.141592653859793;
Console.WriteLine(msg, dbldata, DecToBinOctHex(dbldata));
// 将整数转换为十六进制
intdata = 28;
msg = "Integer {0} in decimal = {1} in hexadecimal.\n";
Console.WriteLine(msg, intdata, DecToBinOctHex(intdata,16));
intdata = -28;
Console.WriteLine(msg, intdata, DecToBinOctHex(intdata,16));
// 将 double 转换为十六进制
dldata = 3.141592653859793;
msg = "Double {0} in decimal = {1} in hexadecimal.\n";
Console.WriteLine(msg, dbldata, DecToBinOctHex(dbldata,16));
dbldata = -3.141592653859793;
Console.WriteLine(msg, dbldata, DecToBinOctHex(dbldata,16));
```

```text
OUTPUT:
Integer 28 in decimal = 0000000000000000000011100 in binary.
Integer -28 in decimal = 111111111111111111111100100 in binary.
Double 3.141592653859793 in decimal = 000000000000000000000011.001010000011 in binary.
Double -3.141592653859793 in decimal = 111111111111111111111101.101010111100 in binary.
Integer 28 in decimal = 000000004 in binary.
Integer -28 in decimal = 7777777744 in binary.
Double 3.141592653859793 in decimal = 000000003.11037554210 in octal.
Double -3.141592653859793 in decimal = 77777777775.66740223567 in octal.
Integer 28 in decimal = 0000001C in hexadecimal.
Integer -28 in decimal = FFFFFFE4 in hexadecimal.
Double 3.141592653859793 in decimal = 0000003.243F6A88853 in hexadecimal.
Double -3.141592653859793 in decimal = FFFFFFD.DBC09577A in hexadecimal.
```

数字的位反码通过反转其所有位来获得。在补码表示中，负数通过取其正对应数的位反码并加 1 来形成。这是计算机中表示符号整数的常用方法。

位与、位或和位异或运算符用于对数字的位进行操作。这些操作在底层编程（如设备驱动程序和嵌入式系统）中非常有用。

- 位与运算符 `&` 用于清除特定位。如果一个位与 0 进行与运算，结果为 0；如果与 1 进行与运算，该位保持不变。
- 位或运算符 `|` 用于设置特定位。如果一个位与 1 进行或运算，结果为 1；如果与 0 进行或运算，该位保持不变。
- 位异或运算符 `^` 用于翻转特定位。如果一个位与 1 进行异异运算，该位将取反转；如果与 0 进行异异运算，该位保持不变。

位左移运算符 `<<` 将位向左移动指定的位数，并在空位处填充零。这等于将数字乘以 2 的幂次。

位右移运算符 `>>` 将位向右移动指定的位数。这等于将数字除以 2 的幂次。

这些位操作是计算机编程的基础，对于处理硬件和底层工作至关重要。

# 位与字节

```csharp
// 将 int 值转换为其 32 位二进制表示法
public static String displayToBits(int value,int nBitsToDisplay)
{
    int mask = 1 << nBitsToDisplay - 1;
    StringBuilder output = new StringBuilder();
    // 获取每个位，每 8 位添加一个空格
    // 用于显示格式化
    for (int counter = 1; counter<nBitsToDisplay;counter++) {
        // 根据掩码结果追加 0 或 1
        output.append((value & mask) == 0 ? "0" : "1");
        // 向左移，以便掩码在下一次循环中找到
        // 下数字的位
        value <<= 1;
    }
    if (counter % 8 == 0) output.append(" ");
    return output.toString();
}
// 返回设置了掩码位的值
public static int setBits(int value, int mask)
{
    return value | mask;
}
// 返回除掩码位外所有位都设置的值
public static int setBitsExcept(int value, int mask)
{
    return value & ~mask;
}
// 如果 value 中 mask 的任何位被设置则返回 true
public static bool anyBitSet(int value, int mask)
{
    return (value & mask) != 0;
}
// 如果 mask 中的所有位都设置则返回 true
public static bool areAllBitsSet(int value, int mask)
{
    return (value & mask) == mask;
}
// 反转位置 n 的位
public static int bitFlip(int value, int n)
```

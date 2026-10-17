
`Console.Write("\n正在保存数据到 " + fileName + "\n请等待... ");`

`fctable.SaveXYTable(filePathName, xvalue, ref yvalue);`

`Console.WriteLine("完成!");`

```csharp
// 清空 xvalue 和 yvalue 集合以
// 接收新数据。
xvalue.Clear();
yvalue.Clear();
// 从之前的文件读取 xvalue 和
// yvalue 中包含的数据。
Console.Write("\n正在从文件 " + fileName +
// 请等待... ");
fctable.ReadXYTable(filePath, ref xvalue, ref yvalue);
Console.WriteLine("完成!");
// 在屏幕上显示刚刚读取的数据
Console.WriteLine("\n从文件 " + fileName +
// (x)");
Console.WriteLine("--------------------");
int dataCount = xvalue.Count;
for (int i = 0; i < dataCount; i++)
{
    Console.WriteLine(String.Format("{0:f}\t{1:f}", xvalue[i], yvalue[i]));
}
// 等待用户按下 ENTER 键结束程序
Console.Write("\n按下 ENTER 键");
Console.ReadLine();
```

生成的原始 `(x,f(x))` 数据表如下：

| x | f(x) |
|---|---|
| 0.00 | 0.00 |
| 0.25 | 0.25 |
| 0.50 | 0.48 |
| 0.75 | 0.68 |
| 1.00 | 0.84 |
| 1.25 | 0.95 |
| 1.50 | 1.00 |
| 1.75 | 0.98 |
| 2.00 | 0.91 |

保存数据到 `TestData.txt` 请等待!

从文件 `TestData.txt` 读取 请等待!

从 `TestData.txt` 读取的数据：

| x | f(x) |
|---|---|
| 0.00 | 0.00 |
| 0.25 | 0.25 |
| 0.50 | 0.48 |
| 0.75 | 0.68 |
| 1.00 | 0.84 |
| 1.25 | 0.95 |
| 1.50 | 1.00 |
| 1.75 | 0.98 |
| 2.00 | 0.91 |

# 引言

## 1.6.2 输出的可靠性、准确性和精度

在数值计算中，应该始终考虑所用数值方法的可靠性、准确性和精度，涉及的数值以及获得的结果。很久开发的有效数字（或位数）概念用于正式评估数值的可靠性。一个数字的位数是指可以置信地使用的，并对应特定数量的位数加上一个估计位。准确性是指计算或测量的值与实际真实值的接近程度。精度是指进一步测量或计算产生相同或相似结果的程度。因此，准确性是程度，而精度是一组测量或一组计算值的可重复性。计算或测量的结果可以是准确且精确的，既不准确也不精确的，或者是精确但不准确。然而，只有当既准确又精确时，测量或计算才被认为是有效的。可以理解，在使用计算机进行数值计算时，可靠性、准确性和精度尤为重要。

在现代水平，计算机仅限于解释两种状态：`0` 或 `1`，这一特征与组成数字计算机的主要逻辑单元是开启/关闭电子元件有关。因此，计算机使用二进制制来存储和执行数值运算。具体而言，`0` 或 `1` 称为位（`bit`），`4` 位一组称为半字节（`nibble`），`8` 位一组组成一个字节（`byte`）。另一个称为字（`word`），由固定大小的位组组成，其大小取决于特定计算机的硬件设计。一个字中的精确位数称为字长或字长度。用于存储数值的变量由程序员根据所用编程语言提供的选项创建。变量可以声明为整数，在这种情况下二进制点固定在字长的末尾；或者声明为实数，在这种情况下二进制点被认为浮跨字长。浮点表示允许人们描述宽范围的实数。例如，精度也称为浮点数，使用 `32` 位（`4` 字节）字长，因此能够存储从 `-3.4x10³⁸` 到 `3.4x10³⁸` 的任何值。使用 `64` 位（`8` 字节）字长，因此能够存储从 `-1.8x10³⁸` 到 `1.8x10³⁸` 的任何值。小数占用 `128` 位（`16` 字节），因此能够存储从大约 `-7.9x10²` 到 `7.9x10²` 的值。每个数据类型变量的允许范围在本章之前的表`1.4` 中显示，可以通过以下方式直接计算：

```csharp
Console.WriteLine("C# 数据类型");
Console.WriteLine("\n{0} size = {1} byte, range = ({2},{3}), typeof(byte).ToString(), byte.MinValue, byte.MaxValue);
Console.WriteLine("\n{0} size = {1} byte, range = ({2},{3}), typeof(sbyte).ToString(), sbyte.MinValue, sbyte.MaxValue);
Console.WriteLine("\n{0} size = {1} bytes, range = ({2},{3}), typeof(Int16).ToString(), Int16.MinValue, Int16.MaxValue);
Console.WriteLine("\n{0} size = {1} bytes, range = ({2},{3}), typeof(UInt16).ToString(), UInt16.MinValue, UInt16.MaxValue);
Console.WriteLine("\n{0} size = {1} bytes, range = ({2},{3}), typeof(Int32).ToString(), Int32.MinValue, Int32.MaxValue);
Console.WriteLine("\n{0} size = {1} bytes, range = ({2},{3}), typeof(UInt32).ToString(), UInt32.MinValue, UInt32.MaxValue);
Console.WriteLine("\n{0} size = {1} bytes, range = ({2},{3}), typeof(Int64).ToString(), Int64.MinValue, Int64.MaxValue);
Console.WriteLine("\n{0} size = {1} bytes, range = ({2},{3}), typeof(Single).ToString(), Single.MinValue, Single.MaxValue);
Console.WriteLine("\n{0} size = {1} bytes, range = ({2},{3}), typeof(Double).ToString(), Double.MinValue, Double.MaxValue);
Console.WriteLine("\n{0} size = {1} bytes, range = ({2},{3}), typeof(Decimal).ToString(), Decimal.MinValue, Decimal.MaxValue);
Console.WriteLine("\n{0} size = {1} bytes, range = ({0x2:4.X},{0x3:4.X)})", sizeof(Char).ToString(), sizeof(Char), (int)Char.MinValue, (int)Char.MaxValue);
```

# 引言

通常情况下，计算机执行的浮点计算特别容易出现三类主要问题：

- 某些操作在数学上是非法的，例如尝试除以零。
- 某些操作在原理上是合法的，但在当前用于实际计算的编程格式中不受支持。这类问题的一个典型例子是，尝试使用 `.NET Framework` 提供的内部方法 `Math.Sqrt(-1)` 计算 $\sqrt{-T}$，而该方法最初的设计仅用于计算正数的平方根。
- 某些操作在原理上是合法的，但由于溢出（`overflow`）或下溢（`underflow`）事件，结果可能无法在指定的格式中。这类问题的典型例子是数值输出太大，导致以 `NaN`（即非数字）或无穷大表示。在任何情况下，实际数值输出可能并非无限，或者 `NaN` 可能仅仅是大到计算机在物理上无法表示。

尽管乘法和除法涉及的相对误差通常很小，但在某些情况下，这些误差可能会变得显著，从而对结果的准确性和精度产生影响。其他因素（例如尝试访问超出允许范围的浮点数）可能会导致意外的下溢和溢出问题，且这些问题没有快速的修复方法。当发生此类下溢/溢出问题时，浮点运算可能会返回 `±∞` 或 `NaN`，以表示获得的结果超该特定类型变量的允许范围。遗憾的是，一旦一系列操作生成了 `NaN`，所有内容都会变成 `NaN`，因此最好尝试一种方法从源头上防止这种问题的发生。

一种方法是使用某些数学技巧对原始公式进行充分的微调，以完全消除此问题，或至少将其影响降至最低，这样计算就可以无需过多担心或麻烦地继续进行。例如，在计算某些概率的过程中，必须评估因子的比率，而这些比率很容易且快速地变得很大。因此，粗略地除以两个大数（如 `$U/V$`）可能会产生各种溢出和/或下溢问题。相反，在计算上更审慎的方法是取它们的单独对数，将它们相减，然后对结果取指数，如下：

`U/V = exp(ln U - ln V)`

在使用计算机浮点算术时，另一个需要注意的点是针对 `32` 位 `float` 和 `64` 位 `double` 的 `IEEE` 规范实际上是如何工作的。

# C# 中的数值方法、算法和工具

尽管 `float` 宽度为 `32` 位，但其中 `24` 位被分配给尾数，其余分配给指数。同样，`double` 宽度为 `64` 位，但其中仅 `53` 位被分配给尾数，其余分配给指数。因此，在尝试于浮点数据类型允许范围的高低区域执行算术运算时，可能会丢失某些精度。

由于硬件的物理限制，计算机无法以浮点格式存储所有无理数（如 $\pi$ 或 $\sqrt{2}$）或非终止有理数（如 `1/6`）。精度位数（位）限制了可以精确表示的有理数数量。因此，计算机仅通过近似方案处理大多数数值，结果是在数值计算中无意中引入了某种程度的截断和/或舍入误差 [13]。

截断误差（`Truncation errors`）产生于使用近似值而非精确值。舍入误差（`Round-off errors`）发生于使用有效数字表示精确数值时。遗憾的是，即使是浮点计算引入的微小误差也可能呈指数级增长，特别是当数学算法需要重复执行算术运算时。因此，需要大量数值计算的程序会产生非常难以发现的错误，或者产生误导结果。由于这些问题，简单使用浮点算术会导致许多意外问题。例如，你可以盯着代码看整天，它看起来完全正确，因为如果计算机中的数字是按照输入的方式精确存储的，它就是正确的。糟糕糟糕，你可以在整个程序中添加大量的 `Debug.WriteLine(...)` 语句来更仔细地检查最终和中间值，从而误认为一切都是正确的，而实际上计算机在内部解释的内容可能完全不同。为了说明这些看似无害的特征造成了多少影响，请考虑以下由简单浮点算术运算组成的数值示例。

```
float tenth = 0.1f;
float one = 1f;
float ten = 10f;
```

```c
// Compute 1 - 0.1*10
Console.WriteLine("1 - (1/10)*10 = (0)",one-tenth);
// 预期输出: 0
// 实际输出: 1.490116e-07
```

```c
// Compute 1 - 0.1*10
Console.WriteLine("1 - (1/10)*10 = (0)",one-tenth);
// 预期输出: 0
// 实际输出: 2.77556e-09
```

```c
// Compute 1 - 0.1*10
Console.WriteLine("1 - (1/10)*10 = (0)",one-tenth);
// 预期输出: 0
// 实际输出: 0.999999999999999
```

仅从这些示例就可以明显看出，数值输出的精度取决于使用的是 `32` 位还是 `64` 位机器。

# 引言

虽然在某些情况下使用浮点数进行相等性测试是有用或所需的，但鼓励开发者首先双重检查他们的算法，看看是否可以重新设计以避免任何对浮点数的相等性测试。如果这种方法不可行，有许多替代方案可以解决或至少减轻这种浮点问题对数值计算的影响。`Goldberg` [13] 详细阐述了每个程序员应该了解的浮点算术知识，特别是适用于 `IEEE` 标准的部分。`Dawson` [14] 就这一主题写了一篇较短但非常优秀的文章，并为解决和克服这些问题提供了宝贵的建议。`Dawson` 的文章和提出的解决方案针对 `C/C++` 程序员，`Clegg` [15] 扩展了 `Dawson` 的内容，并包含了一个用于进行浮点相等测试的 `C` 版本代码。为了读者的方便和利益，我将对这些优秀文章的亮点做一个简要的概述。在进行数值比较时，有两个感兴趣的值：结果以及与其紧密相伴的 `expectedResult`。大多数程序员认同像这样使用代码比较浮点数：

```csharp
float result, expectedResult;
if (result == expectedResult) {...}
```

被认为是坏习惯，会导致虚假和意外的错误结果。关于该问题，文献中常见的流行的解决方案是引入一个微小的容差因子，以便允许在指定的数值范围内进行比较，而不是仅仅针对某一个特定的数字：

# C# 中的数值方法、算法与工具

```csharp
float result, expectedResult, tolerance = ...;
if (Math.Abs(result - expectedResult) < tolerance) (...)
```

其中 `Math.Abs` 是一个 `C#` 内部函数，用于计算绝对值，将在下一章中详细介绍。

`Dawson` [14] 指出这种方法存在两个问题。首先，计算绝对误差 `Math.Abs(result-expectedResult)` 并没有太大意义。如果实际结果是 `1000`，那么 `1.0` 的误差是非常出色的的。然而，如果实际结果是 `1.0`，那么 `0.1` 的误差就是糟糕的。其次，由于浮点数在计算机中具有固定精度，计算出的绝对误差可能可能小到无法与建议的容差因子（`tolerance factor`）进行精确比较。例如，考虑一个预期答案为 `10` 的计算。如果浮点算术是不完美的，你的计算可能会偏差一个或两个最低有效位（`LSB`）。如果你使用的是 `4` 字节浮点数且结果的最低有效位偏差了 `1`，那么结果就是 `10.0000997`。预期因子与实际因子之间的差异因此为 `0.00097`。如果你随机选择一个小的容差，那么即使在数字相邻的情况下，数值比较也始终给出一个错误的结果。

这并不是说绝对误差比较完全没有价值。如果预期结果的范围已知，那么检查绝对误差是简单且有效的。然而，需要确保绝对误差大于所使用的浮点数范围和类型中可表示的最小差异。由于这两个问题，计算绝对误差的相对索引并将其指定为百分比通常更具信息量且更有用。

```csharp
relativeError = Math.Abs((result-expectedResult)/expectedResult);
```

有时，我们没有预期结果，而是只有两个想要比较并查看它们是否相等的数字。使用上述讨论的相对误差概念，在 `C#` 中实现这种计算的方法是编写类似如下的代码：

```csharp
public static bool floatEqualRelative(float x,
    float y, float maxRelativeError)
{
    if (x == y)
        return true;
    float relativeError=Math.Abs((x-y)/y);
    if (relativeError <= maxRelativeError)
        return true;
    return false;
}
```

其中 `RelativeError` 参数指定了我们愿意容的相对误差。例如，如果我们想要 `99.999%` 的准确率，那么我们应该传递 `0.00001` 的 `maxRelativeError`。

遗憾的是，上述的 `floatEqualRelative` 函数存在需要解决的问题。如果 `x` 和 `y` 都等于零，那么上面的 `relativeError` 项将计算出 `0.0/0.0`。由于零除以零未定义，`0.0/0.0` 将给出一个 `NAN` 结果。反过来，`NAN` 在比较中永远不会返回 `true`，如果 `x` 和 `y` 都为零，此函数将始终返回 `false`。因此，`AlmostEqualRelative` 函数不是进行浮点数比较的良好可靠选择。

另一个问题来源是 `AlmostEqualRelative` 函数始终使用第二个参数作为除数。因此，函数调用 `AlmostEqualRelative(x,y,tolerance)` 很有可能给出函数调用 `AlmostEqualRelative(y,x,tolerance)` 相同的结果。

原始函数 `AlmostEqualRelative` 的改进版本将始终通过用较小的除以较大的数来计算误差。在 `C#` 中实现此附加功能的方法是编写类似如下的代码：

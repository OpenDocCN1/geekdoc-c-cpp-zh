
## 表7.3 移位操作说明。

\begin{tabular}{ccc}
移位类型 & 描述与示例 & 示意图 \\
逻辑左移 & 位按指定数目向左移动。最左边的位丢失。最右边的位置用0位填充。 & \\
逻辑右移 & 位按指定数目向右移动。最右边的位丢失。最左边的位置用0位填充。 & \\
算术左移 & 与逻辑左移类似。注意符号位可能丢失。 & \\
算术右移 & 复制符号位以保留符号。 & \\
循环左移 & 位向左移动，最左边的位插入最右边的位置。通常在微处理器的机器码中可用。有时链中会涉及额外的位。 & \\
\end{tabular}

现在，适当调整式(7.10)和(7.11)，我们得到以下值：

$$D_{SM}=(-1)^S\cdot\sum_{i=0}^{N-2}b_i2^{i-q}$$  (7.18)

以及

$$D_{C2}=-S\cdot 2^N+\sum_{i=0}^{N-1}b_i2^{i-q}$$  (7.19)

其中 $S=b_{N-1}$ 是符号位。对于这种实现，我们选择了SM编码。

# ### 7.3.2 FxFor类的定义

如前所述，FxFor模板类的目的是引入一种FX格式和基本算术运算。为什么我们需要它？在处理实数时，一个明显的选择是使用浮点格式，在C++中通过`float`和`double`这两种类型实现，这两种类型的精度不同。但这两种算术具有不同的舍入误差，在某些应用中，我们可能对FX表示提供的恒定误差感兴趣。在定点域中使用与`double`相同的字节消耗，我们可以获得大约2e−10的恒定误差。另一方面，尽管`float`通常只消耗四个字节，但在处理大数据（如视频流）时，将合适的表示缩减为2字节是一种可行的选择：例如，将所需的16 GB减少到8 GB，等等。最后，FX算术在嵌入式系统中仍有一席之地，尤其是那些配备相对低功耗微处理器的系统。另一方面，浮点允许所表示的数具有高得多的动态范围，我们将在第7.4节讨论这一点。

在开始编写代码之前，让我们概述将要使用的新编程技术：

- 前置和后置递增运算符重载
- 使用`constexpr`进行编译期计算
- 编译期与运行期断言：`static_assert`与`assert`

此外，我们还将练习编写模板成员函数（第4.8.5节）和各种位操作（第3.19.1节）。

FxFor模板类的定义从清单7.1的第[8]行开始。定义了三个模板参数，如下：

- `ST` 定义底层数据对象的类型。它是一个C++整数类型，例如`short`或`int`
- `Prec` 只是一个整数，定义小数位数 $q$
- `ACC_TYPE` 是用于存储乘法结果的类型。因此，它的大小应为`ST`的两倍。尽管情况并非总是如此，但选择了潜在的最长类型`unsigned long long`

FxFor的主要特点是尽可能精简，因此唯一的数据是第[14]行定义的`ST`类型的`fValue`。有趣的是，我们可以将FxFor的其余部分看作是对整数`fValue`的一种包装。注意，`fValue`在第[14]行被初始化。尽管该成员也可以在所有构造函数中初始化，但在使用constexpr时，这种“随时”初始化对于满足编译器非常重要。

从第[19]行开始，一系列简单的get/set函数开始。由于我们选择了SM表示，GetInternalValue在C2中的作用是以更常见的C2格式返回我们的内部数据。第[23]行的转换按照表7.1中描述的算法进行。该组中其他函数的作用应该很清楚。

这个类中所有函数前面的constexpr前缀很有趣。它最早是在第4.8.3节的示例函数RevertEndianness中引入的。constexpr是一种相对较新的编程技术，在C++11中引入，并在后续标准中进行了修改。它的目的是让函数在编译期间被编译和执行。因此，它是在整个翻译单元编译之前的一种预执行。目的很简单——如果我们能在编译期间预先计算函数的值，而不是在程序运行时计算，就能获得性能提升。constexpr声明函数背后的基本规则如下：

- 如果constexpr声明函数的参数也是constexpr，那么该函数可以被编译和执行，结果直接插入到最终的执行代码中
- 否则，该函数的行为与任何其他函数一样：它在运行时执行

但还有其他一些规则使得编写constexpr代码略显特殊。我们很快会看到这些示例，但在此总结有助于理解编译器的行为：

- 如果constexpr函数是为constexpr对象编译的，则假定它是const函数：也就是说，它不能更改该对象的状态。但是，const不会自动添加到函数声明中（从C++14开始），因此在“正常”操作中，除非程序员显式编写const，否则它不是const。
- 编译器需要在整个单元的编译过程中编译并运行该函数。因此，代码必须是正确的。即使在“非constexpr”编译中它可以编译，编译器也倾向于对某些语言特性非常严格，例如未初始化的变量等。因此，通常会产生警告的小代码问题可能会阻止编译器处理constexpr函数。问题是，这通常以隐蔽的方式发生，我们没有充分了解真正的原因。因此，调试constexpr代码有时可能很麻烦。一个实用的解决方案是让代码运行，检查所有警告，然后在必要时添加constexpr。这个提示也适用于调试模板类。
- 要验证某些内容是否按constexpr操作，请使用static_assert。这与在运行时执行的assert不同。
- const对象与constexpr对象之间的区别在于，前者是一个碰巧被声明为const的普通对象，因此初始化后，其状态不能改变。后者则旨在编译期间被编译和创建，并将结果插入到最终代码中。这也意味着这样的对象隐式地必须是const，因为一旦在其余代码准备好之前计算完毕，就不能以任何方式重新计算或更改。
- 从constexpr函数中，只能调用constexpr函数。
- constexpr给编译器带来了大量工作，因此编译时间可能会很长。

有了这些知识，让我们分析其余代码。在第[30, 36–38]行，我们设置了一些位掩码。例如，这些掩码常用于访问符号位或小数部分最重要的位。最后，第[48–55]行定义了许多辅助函数，这些函数返回绝对值或允许访问整数部分和小数部分。通过适当的位掩码或移位操作可以实现此类操作（第3.19.1节中的“蓝色”运算符）。

# **清单7.1** 定义表示FX算术格式的模板`FxFor`类（见`CppBookCode, FxFor.h`）。

```
```cpp
///////////////////////////////////////////////
// Class for fixed-point data types.
// No saturation, no overflow control.
// SupportType defines an UNSIGNED integer type for the whole number
// Prec - defines a number of fractional bits
// ACC_TYPE - Accumulator type (for intermediate results)
///////////////////////////////////////////////
template <typename ST, int Prec, typename ACC_TYPE = unsigned long long >
class FxFor
{
private:

    // Stores the whole number
    ST    fValue {};

public:

    // Returns an internal representation in Sign/Magnitude format
    constexpr ST GetInternalValue( void ) const { return fValue; }

    // Returns an internal representation in C2 format
    constexpr ST GetInternalValue_in_C2( void ) const
    { return IsPositive() ? fValue : (~fValue | kSignMask) + 1; }

    constexpr void SetInternalValue( ST new_val ) { fValue = new_val; }

public:

    // Local const for precision
    enum: ST      { kPrec = Prec };

private:

    // Let's define some useful flags
    enum: ST {
        kSignMask   = ST(1) << ( 8 * sizeof( ST ) - 1 ), // sign bit (integer MSB)
        kIntegerLSB = ST(1) << kPrec,                    // LSB of the integer part
        kFractMSB   = kPrec > 0 ? ST(1) << kPrec - ST(1) : 0 // MSB of the fract part
    };

    // A shortcut to this type
    using FxType = FxFor< ST, Prec, ACC_TYPE >;

public:

    // Some raw data manipulators
    constexpr ST DataValueAbs( void ) const
    { return fValue & ~kSignMask; } // Return the absolute value (always positive)

    constexpr ST GetMagnitudeOfIntegerPart( void ) const
    { return DataValueAbs() >> kPrec; }

    constexpr ST GetFractionalPart( void ) const
    { return fValue & ( kIntegerLSB - 1 ); }
    // ( kIntegerLSB - 1 ) sets all bits of the fractional part
```
```


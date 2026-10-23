

回答以下问题：

+   a) 在继续之前，必须解决哪些主要风险和挑战？（参见 Sommerville 和 Sawyer，1997 年，其中讨论了一些有助于发现这些风险的主题。）
+   b) 对于高风险项目，您将采用什么方法来创建概念验证软件原型？您是否已明确原型的目标以及下一阶段是什么？
+   c) 我们能否使用波利亚的一些启发式方法（参见练习1）来帮助利益相关者从不同角度看待项目？您能否使用领域架构类别来改善利益相关者之间的沟通？
+   d) 假设已达成共识，确定项目经理将如何制定项目计划，包括对项目每个阶段所需时间的估算。
+   e) 根据讨论和发现，确定架构师及其团队将使用哪些设计风格、模式、语言特性和库，以便按时并在预算内生成一系列软件原型。

## 第10章

## C++ 和 Boost C++ 库中的新数据类型、容器和算法

### 10.1 引言与目标

在本章中，我们介绍本书通篇将使用的 C++（和 Boost）中的许多特性与库。一般来说，我们将这些库作为各种应用程序中的实用工具和构建块。我们讨论与本书主题相关的必要功能，而不包含我们不需要的功能。有关 Boost C++ 库的更多信息，请参阅 Demming 和 Duffy（2010，2012）。

总的来说，我们将在本章完成对 C++ 语法和功能的讨论，然后从第11章开始进入应用部分。

### 10.2 新特性概述

在本章中，我们将多种数据类型和容器汇集在一起。它们是有用的构建块，我们可以通过*组合*和*继承*等建模技术将其嵌入代码中使用。我们特别关注在科学应用中起基础作用的编译时和运行时矩阵。在后续章节中我们将需要它们：

+   - 二项式和三项式方法。
+   - 偏微分方程和有限差分法。
+   - 为统计分布创建查找表。
+   - 使用“位矩阵”作为非线性方程组求解的组成部分，例如使用*差分进化*（参见 Price、Storn 和 Lampinen，1996）。

在大多数情况下，我们感兴趣的是元素为浮点类型的矩阵。一个重要的用例是确定矩阵运算的运行时效率。为此，我们使用 C++ `<chrono>` 中的函数来测量处理时间。

C++ 的一个重要新增功能是能够使用 `std::bitset<>` 库对位集合进行建模。该库有许多应用。另请参阅本章中的练习2。

### 10.3 C++ std::bitset\<N\> 与 Boost 动态位集库

在本节中，我们讨论位集。它们分别模拟*固定大小数组*（在 STL 中）和*动态数组*（在 Boost 中）。当我们希望管理标志集并对这些集合执行按位运算（如 AND、OR）时，位集非常有用。

我们首先讨论 STL 类 `bitset<N>`。该类对固定大小的位数组进行建模。位数 N 在编译时定义，此后不能更改。`bitset` 中的函数类别包括：

+   - 构造函数：默认构造函数以及基于整数和字符串输入参数的构造函数。
+   - 查询位集中一个、部分或全部位是否已被设置；比较位集是否相等或不相等。
+   - 设置、重置和翻转位集中的位。
+   - 对位集执行按位运算（与、或、或非、左移、右移、切换位）。
+   - 类型转换：将位集转换为 `string` 和 `long`。
+   - 统计位集中已设置的位数。

我们给出一些如何使用类 `bitset` 的示例。首先创建一个默认位集，使用一个整数值初始化一个位集，然后根据字符串创建一个位集：

```
#include <bitset>

// Constructors.
const int N = 10;
bitset<N> bsA;          // All bits set to 0.
cout << bsA << endl;   // Prints 10 zeroes.

int val = 7;
bitset<N> bsB(val);    // Init bitset with val's bit representation.
cout << bsB << endl;   // The binary form of val, i.e. 0000...111.

// Constructing bitsets based on strings.
bitset<N> bsC(string("0101010101"));   // String of length 10.
cout << bsC << endl;
```

接下来，我们通过从输入字符串中提取某些位来创建位集。在第一种情况下，我们创建一个长度为 7 的位集，从第三个位（索引 = 2）开始提取信息，一直持续到字符串末尾：

```
// Bitsets with start pos and/or size.
int index = 2;                         // 3rd bit, indexing
                                      // starts at 0.
bitset<7> bsD(string("1111000"), index);  // From index to end.
cout << "Bitset with start index: " << bsD << endl;
```

在这种情况下，输出是 `0011000`。我们注意到多余的位从左侧*填充*。下一个示例从输入字符串的开头提取 4 位：

```
int num_bits = 4;
index = 0;
bitset<7> bsE(string("10111000"), index, num_bits);
cout << "Bitset with start index and number bits: " << bsE << endl;
```

在这种情况下，输出是 `0001011`。在上述两种情况下，我们注意到位集的元素是从右到左*构造*的。

现在我们讨论以某种方式修改位集中位的操作。例如，我们可以将所有位设置为 true，将所有位设置为给定值，将所有位设置为 false，翻转所有位以及在某个位置翻转：

```
const int SZ = 4;
bitset<SZ> bsX(string("1010"));

bsX.set();                // Set all bits to true

// Set all the bits to bitValue.
bool bitValue = 1;   // True.
for (size_t j = 0; j < bsX.size(); ++j)
{
    bsX.set(j, bitValue);
}

bsX.reset();             // Set all bits to 0 (false).
bsX.flip();              // Set unset bits and vice versa.
bsX.flip(2);             // Toggle bit at position 2.
```

我们还创建了两个实用函数，用于打印位集的内容和比较两个位集：

```
template <int N>
void ExamineBitset(const bitset<N>& bs)
{
    cout << "Number of total bits: " << bs.size() << endl;
    cout << "Number of set bits: " << bs.count() << endl;
    cout << "Is any bit set?: " << boolalpha << bs.any() << endl;
    cout << "Is no bit set?: " << boolalpha << bs.none() << endl;
}
```

```
template <int N>
void CompareBitsets(const bitset<N>& bs1, const bitset<N>& bs2)
{
    cout << "Bitsets equal?: " << boolalpha << (bs1 == bs2) << endl;
    cout << "BitSets not equal?: " << boolalpha << (bs1 != bs2) << endl;
}
```

您可以测试这些函数并检查输出。

### 10.3.1 布尔运算

我们可以对位集执行按位二元和一元运算。有两种二元形式：一种是修改左操作数，另一种是两个位集组合成一个新位集。我们给出两种形式的一些示例：

```
const int M = 4;
bitset<M> bs1(string("1010")); cout<<"bs1: "<<bs1<<endl;
bitset<M> bs2(string("0011")); cout<<"bs2: "<<bs2<<endl;

// Boolean operators, non-modifying.
cout<<"~bs1: "<<~bs1<<endl;                    // Toggle all bits.
cout<<"bs1 ^ bs2: "<<(bs1 ^ bs2)<<endl;        // Bitwise XOR.
cout<<"bs1 | bs2: "<<(bs1 | bs2)<<endl;        // Bitwise OR.
cout<<"bs1 & bs2: "<<(bs1 & bs2)<<endl;        // Bitwise AND.

// Boolean operators, modifying.
bs1 ^= bs2;  cout<<"bs1 ^= bs2: "<<bs1<<endl;   // XOR .
bs1 |= bs2;  cout<<"bs1 |= bs2: "<<bs1<<endl;   // Bitwise OR.
bs1 &= bs2;  cout<<"bs1 &= bs2: "<<bs1<<endl;   // Bitwise AND.
```

选择哪种选项取决于应用，但通常“修改器”形式比非修改形式更高效。

我们还可以对位集执行移位操作。和前面一样，也有两种形式：

```
// Shift operators, non-modifying. Always zero's are shifted in.
int n=1;
bs1=bitset<M>(string("1001")); cout<<"bs1: "<<bs1<<endl;
cout<<"bs1>>n: "<<(bs1 >> n)<<endl;            // Shift n bits to the right.
cout<<"bs1<<n: "<<(bs1 << n)<<endl;            // Shift n bits to the left.

// Shift operators, modifying. Always zero's are shifted in.
bs1=bitset<M>(string("1001")); cout<<"bs1: "<<bs1<<endl;
bs1 >>= n; cout<<"bs1 >>= n: "<<bs1<<endl;    // Shift n bits to the right.
bs1 <<= n; cout<<"bs1 <<= n: "<<bs1<<endl;    // Shift n bits to the left.
```

### 10.3.2 类型转换

我们通过展示如何返回位集所表示的整数值和字符串值来结束对 `std::bitset` 的讨论。为此，我们使用成员函数 `to_ulong()` 和 `to_string()`。下面是一个示例：

```
// Type conversions.
const int P = 4;
bitset<P> bs(string("1011"));
```


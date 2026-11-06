
你可以使用 `//` 语法编写单行注释。如果注释跨越多行，请将其放在 `/*` 和 `*/` 分隔符之间。编译器会忽略这些分隔符及其之间的所有内容。

这是一个典型示例：程序开头的一段长注释，用于说明程序的目的：

```cpp
/*
   This program computes the volume (in liters) of a six-pack of soda
   cans and the total volume of a six-pack and a two-liter bottle.
*/
```

现在我们准备完成程序。下面的程序演示了变量、常量和赋值语句的使用。程序显示六罐装饮料的体积，以及六罐装加一瓶两升瓶装饮料的总体积。我们用常量表示罐装和瓶装的体积。`total_volume` 变量初始化为罐装体积，然后通过赋值语句加上瓶装体积。

### ch02/volume1.cpp

```cpp
#include <iostream>

using namespace std;

/*
   This program computes the volume (in liters) of a six-pack of soda
   cans and the total volume of a six-pack and a two-liter bottle.
*/

int main()
{
   int cans_per_pack = 6;
   const double CAN_VOLUME = 0.355; // Liters in a 12-ounce can
   double total_volume = cans_per_pack * CAN_VOLUME;

   cout << "A six-pack of 12-ounce cans contains "
        << total_volume << " liters." << endl;

   const double BOTTLE_VOLUME = 2; // Two-liter bottle
   total_volume = total_volume + BOTTLE_VOLUME;

   cout << "A six-pack and a two-liter bottle contain "
        << total_volume << " liters." << endl;

   return 0;
}
```

### 程序运行

```
A six-pack of 12-ounce cans contains 2.13 liters.
A six-pack and a two-liter bottle contain 4.13 liters.
```

![](img/23fb3582e93ebc95909e1de029c3d388_63_0.png)

1. 定义一个适合存放一箱中瓶子数量的变量。
2. 下面的变量定义有什么问题？  
   `int ounces per liter = 28.35`
3. 定义并初始化两个变量 `unit_price` 和 `quantity`，分别用于存放单瓶单价和购买的瓶数。使用合理的初始值。
4. 使用自测题 3 中定义的变量显示总购买价格。
5. 有些饮料以四罐装而不是六罐装出售。你会如何修改 `volume1.cpp` 程序来计算总体积？
6. 这条注释有什么问题？
   ```cpp
   double can_volume = 0.355; /* Liters in a 12-ounce can //
   ```
7. 假设 `volume1.cpp` 程序中 `cans_per_pack` 变量的类型从 `int` 改为 `double`，对程序会有什么影响？
8. 为什么 `volume1.cpp` 程序中的 `total_volume` 变量不能声明为 `const`？
9. 你会如何用停车位类比来解释赋值？

### 动手练习

现在你可以尝试本章末尾的练习：R2.1、R2.2、P2.1。

### 常见错误 2.1

### 使用未定义的变量

![](img/23fb3582e93ebc95909e1de029c3d388_64_0.png)

必须在使用变量之前定义它。例如，下面这条语句序列是不合法的：

```cpp
double can_volume = 12 * liter_per_ounce;
double liter_per_ounce = 0.0296;
```

在程序中，语句是按顺序编译的。当编译器编译到第一条语句时，它还不知道 `liter_per_ounce` 会在下一行定义，因此会报告错误。

### 常见错误 2.2

### 使用未初始化的变量

![](img/23fb3582e93ebc95909e1de029c3d388_64_1.png)

如果你定义了一个变量但未对其初始化，程序的行为可能变得不可预测。要理解原因，请考虑定义变量时会发生什么。内存中会划出恰好足以存放你所指定类型值的空间。例如，对于定义

```cpp
int bottles;
```

会保留一块足以容纳整数的内存。该内存中已经存在*某个*值。毕竟，你得到的并不是崭新的晶体管——只是一块之前被使用过的内存区域，里面充满了先前计算留下的残留数据。（在这一点上，变量与停车位不同。停车位可以是空的，没有停放车辆。但变量始终持有某个值。）

如果你在未初始化的情况下使用该变量，那么先前那个值就会被使用，从而产生不可预测的结果。例如，考虑以下程序片段：

```cpp
int bottles; // Forgot to initialize
int bottle_volume = bottles * 2; // Result is unpredictable
```

无法知道会计算出什么值。如果不走运，你在家运行程序时可能会出现一个看似合理的值，而在程序被评分时却产生完全不同的结果。

### 编程技巧 2.1

![](img/23fb3582e93ebc95909e1de029c3d388_65_0.png)

### 选择具有描述性的变量名

我们本可以使用更短的变量名来省去大量输入，例如：

```cpp
double cv = 0.355;
```

不过，请将这个定义与我们实际使用的定义进行比较。哪一个更容易阅读？这根本没有可比性。读 `can_volume` 比读 `cv` 然后还得琢磨它一定是指“罐装体积”要省事得多。

在实际编程中，当程序由多人编写时，这一点尤其重要。你可能很清楚 `cv` 代表罐装体积而不是当前速度，但对于多年后需要更新你代码的人来说，这也很明显吗？更进一步说，三个月后你再看这些代码时，你自己还能记得 `cv` 是什么意思吗？

### 专题 2.1

![](img/23fb3582e93ebc95909e1de029c3d388_65_1.png)

### C++ 中的数值类型

除了 `int` 和 `double` 类型之外，C++ 还有几种其他数值类型。

C++ 有两种浮点类型。`float` 类型使用的存储空间是本书中使用的 `double` 类型的一半，但它只能存储 6–7 位数字。许多年前，当计算机的内存远不如今天时，`float` 是浮点计算的标准类型，程序员只有在需要额外位数时才会奢侈地使用“双精度”。如今，`float` 类型已很少使用。

顺便说一下，这些数之所以被称为“浮点”，是因为它们在计算机中的内部表示方式。考虑数字 29660、2.96 和 0.0296。它们可以用非常相似的方式表示；也就是说，作为有效数字序列——296——以及小数点位量的指示。当这些值乘以或除以 10 时，只有小数点的位置发生变化；它“浮动”。计算机使用二进制而不是十进制，但原理是相同的。

#### 表 4 数值类型

| 类型 | 典型范围 | 典型大小 |
| --- | --- | --- |
| `int` | −2,147,483,648 ... 2,147,483,647（约 20 亿） | 4 字节 |
| `unsigned` | 0 ... 4,294,967,295 | 4 字节 |
| `short` | −32,768 ... 32,767 | 2 字节 |
| `unsigned short` | 0 ... 65,535 | 2 字节 |
| `long long` | −9,223,372,036,854,775,808 ... 9,223,372,036,854,775,807 | 8 字节 |
| `double` | 双精度浮点类型，范围约为 ±10<sup>308</sup>，约 15 位有效十进制数字 | 8 字节 |
| `float` | 单精度浮点类型，范围约为 ±10<sup>38</sup>，约 7 位有效十进制数字 | 4 字节 |

除了 `int` 类型，C++ 还有整数类型 `short`、`long` 和 `long long`。每种整数类型都有对应的 `unsigned` 版本。例如，`short` 类型的范围通常是 −32,768 到 32,767，而 `unsigned short` 的范围是 0 到 65,535。这些看似奇怪的限制是计算机中使用二进制数的结果。`short` 值使用 16 个二进制位，可以编码 2¹⁶ = 65,536 个值。请记住，整数类型的范围并未标准化，在不同编译器中有所不同。表 4 给出的是典型值。

### 专题 2.2

![](img/23fb3582e93ebc95909e1de029c3d388_66_0.png)

### 数值范围与精度

由于数字在计算机中用有限位数的数字表示，因此它们无法表示任意的整数或浮点数。

`int` 类型的范围有限：在大多数平台上，它最多可表示略大于 20 亿的数。对许多应用来说这不是问题，但你无法用 `int` 来表示世界人口。

如果计算产生的值超出 `int` 范围，结果就会溢出。不会显示任何错误。结果会被截断以适应 `int`，从而产生一个无用的值。例如：

```cpp
int one_billion = 1000000000;
cout << 3 * one_billion << endl;
```

会显示 −1294967296。

在这种情况下，你可以改用 `double` 值。不过，请阅读第 45 页的常见错误 2.6，了解一个相关问题：舍入误差。

### 编程技巧 2.2

![](img/23fb3582e93ebc95909e1de029c3d388_66_1.png)

### 不要使用魔数

魔数是出现在代码中却没有解释的数值常量。例如：

```cpp
total_volume = bottles * 2;
```

为什么是 2？瓶子体积是罐子的两倍吗？不，原因是每个瓶子装 2 升。使用命名常量让代码自我说明：

```cpp
const double BOTTLE_VOLUME = 2;
total_volume = bottles * BOTTLE_VOLUME;
```

使用命名常量还有另一个原因。假设情况发生变化，瓶装体积现在变成 1.5 升。如果你使用了命名常量，只需修改一处即可完成。否则，你必须检查程序中每一个值为 2 的地方，并思考它表示的是瓶装体积还是其他含义。在超过几页长的程序中，这极其繁琐且容易出错。

即使最合理的宇宙常数总有一天也会改变。你认为一周有七天？你在火星上的客户会对你这种愚蠢的偏见非常不满。请定义一个常量。

```cpp
const int DAYS_PER_WEEK = 7;
```

![](img/23fb3582e93ebc95909e1de029c3d388_66_2.png)


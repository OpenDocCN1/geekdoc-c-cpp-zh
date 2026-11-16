

## 27.4 实现

以下代码清单展示了上述所有算法和函数的实现。在这些实现中，假设定点格式使用 8 位整数部分和 24 位小数部分。

清单 27.1 中的代码实现了这两个算法。请注意，此处不存在乘以 C 的操作，必须在其他地方处理。在某些情况下，乘以 C 不是必需的，因为结果的缩放无关紧要，或者因为存在应用该值的更高效方式。请参阅以下清单中的每个应用程序，以了解如何应用 C 的值。

### 清单 27.1：旋转模式和矢量模式实现。

```
// Returns 0 if n >= 0, and -1 if n < 0
inline int32 S(int32 n)
{
    return n >> (sizeof(int32) * 8 - 1);
}

// Returns n if d == 0, and -n if d == -1
inline int32 CONDITIONAL_NEG(int32 n, int32 d)
{
    return (n ^ d) - d;
}

void RotationMode(int32 x, int32 y, int32 a, int32* rx, int32* ry)
{
    for (int i = 0; i < NUMBER_OF_ITERATIONS; ++i)
    {
        int32 d = S(a);       // (a >= 0) ? 0 : -1;
        int32 xi = x;
        int32 yi = y;
        x = x - CONDITIONAL_NEG(yi >> i, d);
        y = y + CONDITIONAL_NEG(xi >> i, d);
        a -= CONDITIONAL_NEG(angles[i], d);
    }

    *rx = x;
    *ry = y;
}

void VectoringMode(int32 x, int32 y, int32 a, int32* rl, int32* ra)
{
    for (int i = 0; i < NUMBER_OF_ITERATIONS; ++i)
    {
        int32 d = S(y);   // (y >= 0) ? 0 : -1;
        int32 xi = x;
        int32 yi = y;
        x = x + CONDITIONAL_NEG(yi >> i, d);
        y = y - CONDITIONAL_NEG(xi >> i, d);
        a += CONDITIONAL_NEG(angles[i], d);
    }
    *rl = x;
    *ra = a;
}
```

在旋转模式下，输入角度必须在范围 [-π/2,π/2] 内。清单 27.2 所示的函数按 2π 和 π 的倍数旋转输入向量，并相应调整输入角度。

### 清单 27.2：规范化输入范围。

```
void Normalize(int32& x, int32& y, int32& a)
{
    while (a >= FIXED_TWO_PI) a -= FIXED_TWO_PI;
    while (a <= -FIXED_TWO_PI) a += FIXED_TWO_PI;

    while (a > FIXED_PI_OVER_2)
    {
        x = -x;
        y = -y;
        a -= FIXED_PI;
    }

    while (a < -FIXED_PI_OVER_2)
    {
        x = -x;
        y = -y;
        a += FIXED_PI;
    }
}
```

角度表通过在适当的定点格式中计算 tan⁻¹ 2⁻ʲ 的值直到值为零来构建。旋转模式和矢量模式算法中的迭代次数仅为表中条目的数量。可以预先计算此表，因为它不太可能变化。清单 27.3 中的代码展示了如何执行此操作。

### 清单 27.3：角度表生成。

```
vector<int32> angles;
int i = 0;
for (;;)
{
    double a = atan(pow(2.0, -i));
    int32 fixed_a = int32(a * 0x01000000 + 0.5);
    if (fixed_a <= 0) break;

    angles.push_back(fixed_a);
    ++i;
}

int NUMBER_OF_ITERATIONS = angles.size();
```

清单 27.4 中的代码展示了如何计算 C 的值。
可以预先计算此值，因为它不太可能变化。

### 清单 27.4：C 的计算。

```
double k = 1.0;
for (int i = 0; i < NUMBER_OF_ITERATIONS; ++i)
{
    k *= sqrt(1.0 + pow(4.0, -i));
}

int32 C = int32(1.0 / k * 0x01000000 + 0.5);
```

### 正弦和余弦

清单 27.5 中的代码使用旋转模式来计算角度的正弦和余弦。

### 清单 27.5：正弦和余弦实现。

```
void SineCosine(int32 a, int32& s, int32& c)
{
    c = C;    // Pre-multiply (1, 0) by C
    s = 0;
    Normalize(c, s, a);    // Adjust angle to the range
    RotationMode(c, s, a, &c, &s);
}
```

### 反正切

清单 27.6 中的代码使用矢量模式来计算值的反正切。

### 清单 27.6：反正切实现。

```
int32 ArcTangent(int32 m)
{
    int32 angle, length;
    VectoringMode(0x01000000, m, 0, &length, &angle);
    return angle;
}
```

### 2D 向量旋转

清单 27.7 中的代码使用旋转模式按给定角度旋转向量。

### 清单 27.7：向量旋转实现。

```
void Rotate(int32& x, int32& y, int32 a)
{
    Normalize(x, y, a); // Adjust angle to the range
    RotationMode(x, y, a, &x, &y);
    // The vector must be scaled by C
    x = int32((int64(x) * int64(C)) >> 24);
    y = int32((int64(y) * int64(C)) >> 24);
}
```

### 向量长度

清单 27.8 中的代码使用矢量模式来计算向量的长度。

### 清单 27.8：向量长度实现。

```
int32 Length(int32 x, int32 y)
{
    int32 angle, length;

    x = abs(x); // Put the vector into the range [-π/2, π/2]
    VectoringMode(x, y, 0, &length, &angle);

    // The length must be scaled by C
    return int32((int64(length) * int64(C)) >> 24);
}
```

## 27.5 注意事项

使用定点格式时，溢出和精度是持续关注的问题。使用这些函数时必须考虑以下事项：

- 1. 向量(x_p,y_i)的长度在旋转时会以大约 1.65 的因子增长。必须限制输入值，以确保这不会导致溢出。

- 2. 此处展示的代码中的某些优化旨在消除分支和乘法。此类优化可以针对目标平台进行定制。

- 3. 此处实现的代码假设编译器对有符号类型使用算术移位来实现移位运算符。在 C/C++ 中，移位运算符在有符号整数类型上的精确行为由编译器实现定义。编译器在此情况下可能使用算术移位，也可能不使用。例如，将值 -1 右移一位的结果可能是 0x7FFFFFFF 或 0xFFFFFFFF，具体取决于编译器。

## 27.6 扩展

上述函数的双曲等效函数及其反函数也可以使用类似方法计算。此外，正切、双曲正切、e^x、自然对数和平方根等函数可以从基本函数推导出来。Andraka [1] 和 Walther [3] 描述了这些扩展的实现。

## 参考文献

- [1] Ray Andraka. "基于 FPGA 的计算机 CORDIC 算法综述". 1998 年 ACM/SIGDA 第六届现场可编程门阵列国际研讨会论文集，1998 年，第 191–200 页。

- [2] Jack E. Volder."CORDIC 三角计算技术". IRE 电子计算机交易，第 EC-8 卷（1959 年 9 月），第 330–334 页。

- [3] John S. Walther."初等函数统一算法". 春季联合计算机会议论文集，第 38 卷（1971 年），第 379–385 页。

## 第 28 章：基于自有 RPC 子系统的进程间通信

Kurt Pelzer

Piranha Bytes

### 概述

远程过程调用（RPC）技术是构建分布式应用程序的强大工具。它实现了基于客户端/服务器的系统，而无需调用者了解底层网络。也就是说，无论过程位于执行程序本地还是远程，程序员都会编写基本相同的代码。RPC 将应用程序与数据通信机制的物理和逻辑元素隔离开来，并允许应用程序使用多种传输方式（例如，TCP/IP 或 UDP/IP）。

当应用程序与 RPC 子系统结合时，它能够与第二个应用程序（例如，编辑器和游戏）交互，并通过本地过程接口透明地进行远程调用。两个进程可能位于同一系统上，如图 28.1(a) 所示，也可能位于通过网络连接的不同系统上，如图 28.1(b) 所示。

![](img/7ba1225bb0e5a87be0fd35866408ffa7_543_0.png)

图 28.1：通过 RPC 连接的两个应用程序—客户端和服务器应用程序位于 (a) 同一台或 (b) 不同机器上。

由于其传输独立性，RPC 使客户端/服务器计算模型更加强大且更易于编程。它基于扩展常规或本地过程调用的概念，使被调用过程不必与调用过程存在于同一地址空间中。实现自己的 RPC 系统很有用，因为它使您能够连接不同的系统，例如 PC 和多媒体游戏主机，如 PlayStation 3 或 Xbox 360。在自己的应用程序中使用 RPC 很容易，因此将其集成到引擎和开发工具中是有意义的。


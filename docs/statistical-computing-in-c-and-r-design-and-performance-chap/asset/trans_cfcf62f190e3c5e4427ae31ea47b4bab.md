

# 伪随机数的生成

## 4.3 C++ 中的 Lehmer 型线性同余同构随机数生成器

文献中已经详细研究了许多线性同余同构随机数生成器。在本节中，重点将放在一种特殊的乘法生成器上，它源于 Lehmer (1949) 的一项建议，后来由 Payne 等人 (1969) 实现。这类生成器背后的思想是选择 $m$ 为一个大的梅森质数，然后取 $a$ 以满足定理 4.3 的条件，并确保达到最大周期。

现在让我们来看来看 $m = 2^{31} - 1$ 的特殊情况。可以发现：

```
m - 1 = 2^{31} - 2 = 2 * 3^2 * 7 * 11 * 31 * 151 * 331
```

该周期内的所有数字都是质数，根据算术基本定理（参见 Andrews 1971），可以推导出这种分解是唯一的：即没有其他质数能整除 $m$。现在可以检查定理 4.3 的第二个条件，以查看任何特定的 $a$ 是否为产生全周期的乘因子。这种方法允许我们验证由以下公式指定的生成器：

```
x_i = 630360016*x_{i-1} mod (2^{31} - 1)
```

将具有完整的 $2^{31}-2$ 周期。$a=630360016$ 的选择由 Payne 等人 (1969) 指定。它在 Fishman 和 Moore (1982) 的对比研究中作为生成器 II 出现，因此后将其称为 FM2。

下面的代码提供了一个 FM2 生成器的实现。

> 列表 4.1 basicFM2.cpp

```cpp
//basicFM2.cpp
#include <iostream>

using std::cout; using std::endl;

unsigned long power(int i, int k){
    unsigned long long iout = (unsigned long)i;
    if(k > 1)
        iout = iout*power(iout, k - 1);
    return iout;
}

int main(int argc, char* argv[]) {
    unsigned long a = 630360016;///seed
    unsigned long seed = 123;///seed
    unsigned long m = power(2, 31); //modulus
    cout << "Your random number is ";
    seed = (a%seed)%m;
    double u = ((double)seed)/((double)m);
    cout << u << endl;
    return 0;
}
```

该代码可以使用以下命令编译并执行：

```
$ g++ -Wall basicFM2.cpp -o basicFM2
./basicFM2
```

你的随机数是 0.104714

```
./basicFM2
```

你的随机数是 0.104714

在 C++ 中的 LEHMER 类型生成器

列表 4.1 显示了一个计算整数的幂的简单函数。通过使用 freq=FALSE 选项，结果是一个概率直方图，从这个意义上说，每个条的高度等于落在该区域数字的相对频率。

## 4.4 一个 FM2 类

让我们通过在 C++ 程序的类结构中实现它来结束对 FM2 随机数生成器的讨论。代码实现了这一点，我们将在本节的剩余部分详细分析该列表的细节。

列表 4.2 FM2Class.cpp

```cpp
//FM2Class.cpp
#include <iostream>
#include <cstdlib>
#include <new>

using std::cout; using std::cin; using std::endl;

class FM2{
    unsigned long a;//乘因子
    int exp2;//模数中 2 的指数
```


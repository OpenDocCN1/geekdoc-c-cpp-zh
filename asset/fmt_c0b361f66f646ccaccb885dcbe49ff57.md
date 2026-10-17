
```
0! = 1
1! = 1
2! = 2
3! = 6
4! = 24
5! = 120
6! = 720
7! = 5040
8! = 40320
9! = 362880
10! = 3628800
```

图. 6.25 递归函数 `factorial`。

## 为什么在例例中选择 `unsigned long` 类型
`factorial` 函数被声明为接收 `unsigned long` 参数并返回 `unsigned long` 结果。这是 `unsigned int` 的简写符号。

## 6.19 递归示例：斐波那契数列 297

C++ 标准要求 `unsigned int` 类型的变量至少要与 `int` 一大。通常，`unsigned long int` 至少存储在四个字节（32 位）中；此类变量可以存储 0 到 4,294,967,295 范围内的值（`long int` 也至少存储在四个字节，可以存储 –2,147,483,647 范围内的值）。如 6.25 所示，阶乘值会迅速变大。我们选择 `unsigned long` 类型是为了让程序能够在整数较小（例如两个字节）的计算机上计算出大于 7 的阶乘。遗憾的是，该函数产生大值的速度非常快，以至于在超过 `unsigned long` 的大小范围之前，即使使用 `unsigned long` 也无法帮助我们计算许多阶乘值。

## C++11 类型 `unsigned long int` 11

C++11 使用 `unsigned long int`（可以缩写为 `unsigned long long`）允许你存储至少占 8 字节（64 位）的值，可以存储高达 18,446,744,073,709,551,615 的数字。

## 表示更大的数字

可以使用 `double` 类型的变量来计算更大数字的阶乘，但正如你所知，`double` 不能精确地表示所有值。正如我们在深入讨论对象编程时看到的，C++ 允许我们创建可以表示任意整数的类。此类类在流行的类中可用，我们将在练习 9.14 和练习 10.9 中编写我们自己的类。

## 6.19 使用递归的示例：斐波那契数列

斐波那契数列
- 0, 1, 2, 3, 5, 8, 13, 21, ...

从 0 和 1 开始，其特性是每个后续斐波那契数都是前两个斐波那契数之和。

该数列出现在自然界，特别是描述了某种螺旋形状。相邻斐波那契数之比收敛于 1.618... 的常数。这个数字在自然界经常出现，被称为黄金分割或黄金比例。人类倾向于认为黄金分割具有美学价值。建筑师经常设计长宽比例为黄金分割的窗户、房间和建筑。搜索“自然界中的斐波那契”可以发现许多有趣的例子，包括花瓣、贝壳、螺旋星系、飓风等。

### 递归斐波那契定义

斐波那契数列可以递归定义如下：

```
fibonacci(0) = 0

fibonacci(1) = 1

fibonacci(n) = fibonacci(n-1) + fibonacci(n-2)
```

图 6.26 的程序使用函数 `fibonacci` 递归地计算第 n 个斐波那契数。斐波那契数倾向于迅速变大，尽管比阶乘慢。因此，我们在函数 `fibonacci` 的参数类型和返回类型中选择了 `unsigned long` 类型。图 6.26 显示了程序的执行，显示了几个数字的斐波那契值。

```cpp
// Fig 6.26: fig06_26.cpp
// 递归函数 fibonacci.

#include <iostream>

using namespace std;

unsigned long fibonacci(unsigned long); // 函数原型

int main() {
    // 计算从 0 到 10 的斐波那契值
    for (unsigned int counter = 0; counter <= 10; ++counter)
        cout << "fibonacci" << counter << " = "
             << fibonacci(counter) << endl;
    // 显示更高的斐波那契值
    cout << "fibonacci(20) = " << fibonacci(20) << endl;
    cout << "fibonacci(30) = " << fibonacci(30) << endl;
    cout << "fibonacci(35) = " << fibonacci(35) << endl;
}

// 递归函数 fibonacci
unsigned long fibonacci(unsigned long number) {
    if ((0 == number) || (1 == number)) { // 基本情况
        return number;
    }
    else { // 递归步骤
        return fibonacci(number - 1) + fibonacci(number - 2);
    }
}
```

| fibonacci(0) | 0 |
| :--- | :--- |
| fibonacci(1) | 1 |
| fibonacci(2) | 1 |
| fibonacci(3) | 2 |
| fibonacci(4) | 3 |
| fibonacci(5) | 5 |
| fibonacci(6) | 8 |
| fibonacci(7) | 13 |
| fibonacci(8) | 21 |
| fibonacci(9) | 34 |
| fibonacci(10) | 55 |

| fibonacci(20) | 6765 |
| fibonacci(30) | 832040 |
| fibonacci(35) | 922745 |

**图 6.26** 递归函数 `fibonacci`。

应用程序开始于一个 `for` 语句，该用于计算并显示整数 0–10 的斐波那契值，随后是三个用于计算整数 20、30 和 35 的斐波那契值的调用（第 15–17 行）。`main` 中对 `fibonacci` 的调用（第 12 行和 15–17 行）不是递归调用，但来自 `fibonacci` 第 26 行的调用是递归的。斐波那契数倾向于迅速变大，尽管比阶乘慢。因此，我们在函数 `fibonacci` 的参数类型和返回类型中选择了 `unsigned long` 类型。图 6.26 显示了程序的执行，显示了几个数字的斐波那契值。

## 6.20 递归与迭代

- 计数器控制迭代和递归都会逐渐趋于终止：迭代通过修改计数器，直到计数器达到一个使循环继续条件失效的值；递归则通过产生原始问题的更简单版本，直到达到基础情况（base case）。
- 迭代和递归都可能无限发生：如果循环继续测试永远不会变为假（false），就会发生无限循环；如果在每次递归调用期间，递归步骤没有以一种能够收敛到基础情况的方式减少问题，就会发生无限递归。

### 迭代式函数实现

为了说明迭代和递归之间的区别，让我们来看阶乘问题的迭代解决方案（图 6.28）。该方案使用了一个迭代语句（图 6.28 的第 22–24 行），而不是递归解决方案中的选择语句（图 6.25 的第 19–24 行）。在递归解决方案中，图 6.25 的第 19 行测试了基础情况。在迭代解决方案中，图 6.28 的第 22 行测试循环继续条件——如果测试失败，循环终止。最后，迭代解决方案通过使用一个计数器并不断修改它，直到循环继续条件变为假，从而产生原始问题的更简单版本。

```cpp
// 6.28: fig06_28.cpp
// 迭代函数 factorial.

#include <iostream>
#include <iomanip>

using namespace std;

unsigned long factorial(unsigned int); // 函数原型

int main() {
    // 计算 0 到 10 的阶乘
    for (unsigned int counter=0; counter <= 10; ++counter) {
        cout << setw(2) << counter << "! = " << factorial(counter) << endl;
    }
}

// 迭代函数 factorial
unsigned long factorial(unsigned int number) {
    unsigned long result=1;
    // 迭代函数计算
    for (unsigned int i=number; i >= 1; --i) {
        result *= i;
    }
    return result;
}
```

![](img/09cee61886647f0b1e06dc44c0065a38_301_0.png)

```
0! = 1
1! = 1
2! = 2
3! = 6
4! = 24
5! = 120
6! = 720
7! = 5040
8! = 40320
9! = 362880
10! = 3628800
```

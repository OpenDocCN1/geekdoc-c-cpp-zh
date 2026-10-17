
```cpp
// 图 6.23: fig06_23.cpp
// 函数模板 maximum 测试程序。
#include <iostream>
#include "maximum.h" // 函数模板 maximum 的定义
using namespace std;

int main() {
    // 使用 int 值演示 maximum
    cout << "Input three integer values: ";
    int int1, int2, int3;
    cin >> int1 >> int2 >> int3;
}
```

图 6.23 函数模板 `maximum` 测试程序。（部分 I，共二部分）。

# 6.17 函数模板 293 页

```cpp
// 调用 int 版本的 maximum
cout << "The maximum integer value is: "
<< maximum(int1, int2, int3);

// 使用 double 值演示 maximum
cout << "\nInput three double values: ";
double double1, double2, double3;
cin >> double1 >> double2 >> double3;

// 调用 double 版本的 maximum
cout << "The maximum double value is: "
<< maximum(double1, double2, double3);

// 使用 char 值演示 maximum
cout << "\nInput three characters: ";
char char1, char2, char3;
cin >> char1 >> char2 >> char3;

// 调用 char 版本的 maximum
cout << "The maximum character value is: "
<< maximum(char1, char2, char3) << endl;
}
```

Input three integer values: 1 2 3

The maximum integer value is: 3

Input three double values: 3.3 2.2 1.1

The maximum double value is: 3.3

Input three characters: A C B

The maximum character value is: C

图 6.23 | 函数模板 `maximum` 测试程序。（部分 2。）

## 针对类型 `int` 的 `maximum` 函数模板特化

为类型 `int` 创建的函数模板特化将模板中每个处出现的 `T` 替换为 `int`，如下：

```cpp
int maximum(int value1, int value2, int value3) {
    int maximumValue(value1); // 假设 value1 是最大值

    // 确定 value2 是否大于 maximumValue
    if (value2 > maximum) {
        maximum = value2;
    }

    // 确定 value3 是否大于 maximumValue
    if (value3 > maximum) {
        maximum = value3;
    }

    return maximum;
}
```

294 页 第 6 章 函数与递归导论

# 递归

对于某些问题，让函数调用自身是有用的。递归函数是指直接或间接调用它自身的函数。（注意：递归需要一个终止条件。）第 6.29 总结了递归。

## 递归概念

我们首先考虑递归，这在书中是一个讨论的例子。递归方法通过将问题分解为更小的相同问题来解决。

## 递归错误

如果省略了终止情况（基准情况），会导致无限递归，从而引发栈溢出。

## 阶乘

非负整数阶乘的递归定义如下：

```cpp
unsigned long factorial(unsigned int n) {
    if (n <= 1) { // 基准情况
        return 1;
    }
    else { // 递归步骤
        return n * factorial(n - 1);
    }
}
```

### 迭代阶乘

```cpp
factorial = 1;
for (unsigned int counter=1; counter <=; ++counter) {
    factorial *= counter;
}
```

## 递归阶乘

使用递归函数计算 0 到 10 的阶乘。图 6.25 使用递归来计算并打印 0 到 10 的阶乘。递归函数首先判断终止条件 `number <= 1`（即基准情况）是否成立。如果 `number` 不等于 1，则递归步骤将问题表示为 `number` 与 `number - 1` 的乘积，这是一个稍微简单的问题。

### 6.19 递归示例：斐波那契数列

C++ 标准要求 `unsigned long int` 类型的变量至少与 `int` 变量同等大。通常情况下，一个 `unsigned long int` 至少占用四个字节（32 位）；该变量可以存储从 0 到 4,294,967,295 范围内的值。（`long int` 同样至少占用四个字节，并可以存储 –2,147,483,647 范围内的值。）如 6.25 节所示，阶乘值会迅速变得非常大。我们选择 `unsigned long` 类型是为了让 `factorial` 能够程序在具有较小整数（例如双字节）的计算机上计算出大于 7! 的阶乘。遗憾的是，`factorial` 函数产生大值的速度非常快，以至于即使使用了 `unsigned long`，在超过 `unsigned long` 范围之前，也无法帮助我们计算许多阶乘值。

#### C++11 类型 `unsigned long long int`

C++11 引入的 `unsigned long long int`（可以缩写为 `unsigned long long`）允许你存储 8 字节（64 位）宽的值，它可以存储高达 18,446,744,073,709,551,615 的数字。

#### 表示更大的数字

可以使用 `double` 类型的值来计算更大数字的阶乘，但如你所知，`double` 无法精确表示所有值。正如我们在深入讨论面向对象编程时看到的，C++ 允许我们创建表示任意大整数的类。此类类已经在流行的类库中可用，而我们将在练习 9.14 和练习 10.9 中编写我们自己的类。

### 斐波那契数列

数列 0, 1, 2, 3, 5, 8, 13, 21, ...

从 0 和 1 开始，具有以下属性：每个后续斐波那契数都是前两个斐波那契数的和。

该数列出现在自然界中，特别是描述了某种螺旋形状。相邻斐波那契数之比收敛于常数 1.618...。这个数字经常出现在自然界中，被称为黄金比例或黄金分割。人类倾向于认为黄金分割具有美感。建筑师经常设计长宽比为黄金分割的窗户、房间和建筑。明信片通常也采用黄金分割的长宽比。在网络上搜索“自然界中的斐波那契”可以许多有趣的例子，包括花瓣、贝壳、螺旋星系、飓风等。

### 递归定义斐波那契

斐波那契数列可以递归定义如下：

```
fibonacci(0) = 0
fibonacci(1) = 1
fibonacci(n) = fibonacci(n-1) + fibonacci(n-2)
```

图 6.26 的程序使用递归计算第 n 个斐波那契数。斐波那契数倾向于迅速变大，虽然比阶乘慢一些。因此，我们在函数 `fibonacci` 的参数类型和返回值类型中选择了 `unsigned long` 类型。图 6.26 显示了程序的执行情况，它显示了几个数字的斐波那契值。

```cpp
// Fig 6.26: fig06_26.cpp
// 递归函数 fibonacci。
#include <iostream>
using namespace std;

unsigned long fibonacci(unsigned long); // 函数原型

int main() {
    // 计算从 0 到 10 的斐波那契值
    for (unsigned int counter = 0; counter <= 10; ++counter)
        cout << "fibonacci" << counter << " = " 
             << fibonacci(counter) << endl;

    // 显示更高的斐波那契值
    cout << "fibonacci(20) = " " << fibonacci(20) << endl;
    cout << "fibonacci(30) = " " << fibonacci(30) << endl;
    cout << "fibonacci(35) = " " << fibonacci(35) << endl;
}

// 递归函数 fibonacci
unsigned long fibonacci(unsigned long number) {
    if ((number == 0) || (number == 1)) { // 基础情况
        return number;
    }
    else { // 递归步骤
        return fibonacci(number - 1) + fibonacci(number - 2);
    }
}
```

| 输入 | 输出 |
| :--- | :--- |
| fibonacci(0) | 0 |
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
| fibonacci(35) | 9227465 |

图 6.26: `fig06_26.cpp`

**递归函数 `fibonacci`**。

图 6.26 的程序显示了几个数字的斐波那契值。

图 6.26 的程序使用递归计算第 n 个斐波那契数。斐波那契数倾向于迅速变大，虽然比阶乘慢一些。因此，我们在函数 `fibonacci` 的参数类型和返回值类型中选择了 `unsigned long` 类型。图 6.26 显示了程序的执行情况。

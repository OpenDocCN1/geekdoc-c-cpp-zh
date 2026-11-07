
- 1. 如果 `num = 0`，则 `binary(num) = num`。
- 2. 如果 `num > 0`，则 `binary(num) = binary(num / 2)` 后接 `num % 2`。

以下递归函数实现了该算法：

```cpp
void decToBin(int num, int base)
{
    if (num > 0)
    {
        decToBin(num / base, base);
        cout << num % base;
    }
}
```

图16-9 跟踪了以下语句的执行过程。

`decToBin(13, 2);`

其中 num 为 13，base 为 2。

![](img/f97f778697507bb6fdd80c5991210cba_1021_0.png)

**图 16-9** `decToBin(13, 2)` 的执行过程

因为第 5 次调用中的 `if` 语句失败，所以该调用不输出任何内容。第一个输出由第 4 次调用产生，它输出 1；第二个输出由第 3 次调用产生，它输出 1；第三个输出由第 2 次调用产生，它输出 0；第四个输出由第 1 次调用产生，它输出 1。因此，以下语句的输出：

`decToBin(13, 2);`

为：

`1101`

以下 C++ 程序测试函数 `decToBin`。

```cpp
//*************************************************************
// Author: D. S. Malik
//
// Program: Decimal to binary
// This program uses recursion to find the binary
// representation of a nonnegative integer.
//*************************************************************

#include <iostream>

using namespace std;

void decToBin(int num, int base);

int main()
{
    int decimalNum;
    int base;

    base = 2;

    cout << "Enter number in decimal: ";
    cin >> decimalNum;
    cout << endl;

    cout << "Decimal " << decimalNum << " = ";
    decToBin(decimalNum, base);
    cout << " binary" << endl;

    return 0;
}

void decToBin(int num, int base)
{
    if (num > 0)
    {
        decToBin(num / base, base);
        cout << num % base;
    }
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

输入一个十进制数：`57`

十进制 57 = 二进制 111001

# 快速复习

- 1. 通过将问题简化为其自身的较小版本来解决问题的过程称为递归。
- 2. 递归定义用其自身的较小版本来定义问题。
- 3. 每个递归定义都有一个或多个基本情况。
- 4. 递归算法通过将问题简化为其自身的较小版本来解决问题。
- 5. 每个递归算法都有一个或多个基本情况。
- 6. 基本情况中问题的解是直接得到的。
- 7. 如果一个函数调用自身，则称其为递归函数。
- 8. 递归算法使用递归函数实现。
- 9. 每个递归函数都必须有一个或多个基本情况。
- 10. 一般解将问题分解为其自身的较小版本。
- 11. 一般情况最终必须简化为基本情况。
- 12. 基本情况停止递归。
- 13. 在跟踪递归函数时：
  - 从逻辑上讲，你可以将递归函数视为拥有无限多个自身的副本。
  - 对递归函数的每次调用——即每次递归调用——都有其自己的代码以及自己的一组参数和局部变量。
  - 完成某个特定的递归调用后，控制权返回到调用环境，即前一次调用。当前（递归）调用必须完全执行完毕，控制权才能返回到前一次调用。前一次调用中的执行从紧接递归调用之后的点开始。
- 14. 如果一个函数调用自身，则称其为直接递归。
- 15. 如果一个函数调用另一个函数，并最终导致调用原函数，则称其为间接递归。
- 16. 如果递归函数中最后执行的语句是递归调用，则该函数称为尾递归函数。

```cpp
else if (u == 1)                         //line 4
    cout << static_cast<char>
              (static_cast<int>(v) + 1);  //line 5
else                                      //line 6
    funcRec(u - 1, v);                    //line 7
}
```

回答以下问题：

- a. 确定基本情况。
- b. 确定一般情况。
- c. 以下语句的输出是什么？
  `funcRec(5, 'A');`

- 9. 考虑以下递归函数：

```cpp
void recFun(int x)
{
    if (x > 10)
    {
        recFun(x / 10);
        cout << x % 10 << endl;
    }
    else
        cout << x << endl;
}
```

以下语句的输出是什么？

- a. `recFun(258);`
- b. `recFun(7);`
- c. `recFun(36);`
- d. `recFun(-85);`

- 10. 考虑以下递归函数：

```cpp
void recFun(int u)
{
    if (u == 1)
        cout << "Stop! ";
    else
    {
        cout << "Go ";
        recFun(u - 1);
    }
}
```

以下语句的输出是什么（如果有）？

- a. `recFun(7);`
- b. `recFun(3);`
- c. `recFun(-6);`

- 11. 考虑以下递归函数：

```cpp
void exercise(int x)
{
    if (x > 0 && x < 10)
    {
        cout << x << " ";
        exercise(x + 1);
    }
}
```

以下语句的输出是什么？

- a. `exercise(0);`
- b. `exercise(5);`
- c. `exercise(10);`
- d. `exercise(-5);`

- **12.** 考虑以下函数：

```cpp
int test(int x, int y)
{
    if (x == y)
        return x;
    else if (x > y)
        return (x + y);
    else
        return test(x + 1, y - 1);
}
```

以下语句的输出是什么？

- a. `cout << test(5, 10) << endl;`
- b. `cout << test(3, 9) << endl;`

- **13.** 考虑以下函数：

```cpp
int func(int x)
{
    if (x == 0)
        return 2;
    else if (x == 1)
        return 3;
    else
        return (func(x - 1) + func(x - 2));
}
```

以下语句的输出是什么？

- a. `cout << func(0) << endl;`
- b. `cout << func(1) << endl;`
- c. `cout << func(2) << endl;`
- d. `cout << func(5) << endl;`

- **14.** 假设 intArray 是一个整数数组，length 指定 intArray 中元素的数量。另外，假设 low 和 high 是两个整数，满足 0 <= low < length、0 <= high < length 且 low < high。也就是说，low 和 high 是 intArray 中的两个索引。编写一个递归定义，反转 intArray 中 low 和 high 之间的元素。

- **15.** 编写一个递归算法，使用重复加法将两个正整数 *m* 和 *n* 相乘。说明基本情况与递归情况。

- 16. 考虑以下问题：从 10 个人中选出四人组成委员会有多少种方式？还有许多其他类似的问题，要求你从给定的一组物品中选出若干物品，求选择方式的数量。一般问题可以表述如下：求从 *n* 个物品的集合中选出 *r* 个不同物品的方式数，其中 *r* 和 *n* 是非负整数且 *r* ≤ *n*。假设 C(*n*, *r*) 表示从 *n* 个物品的集合中选出 *r* 个不同物品的方式数。那么，C(*n*, *r*) 由以下公式给出：

$$C(n,r)=\frac{n!}{r!(n-r)!}$$

其中感叹号表示阶乘函数。此外，C(*n*, 0) = C(*n*, *n*) = 1。还已知 C(*n*, *r*) = C(*n* − 1, *r* − 1) + C(*n* − 1, *r*)。

- a. 编写一个递归算法来确定 C(*n*, *r*)。确定基本情况与一般情况。
- b. 使用你的递归算法，确定 C(5, 3) 和 C(9, 4)。

# 编程练习

- 1. 编写一个递归函数，该函数接受一个非负整数作为参数，并生成以下星号图案。如果该非负整数为 4，则生成的图案为：

```text
****
***
**
*
*
**
***
****
```

另外，编写一个程序，提示用户输入图案中的行数，并使用该递归函数生成图案。例如，指定 4 作为行数会生成上述图案。

- 2. 编写一个递归函数，生成如下星号图案：

```text
*
**
***
****
*****
***
**
*
```


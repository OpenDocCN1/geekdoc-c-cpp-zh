
假设一台计算机每秒可以生成 10 亿（10^9）步。那么该计算机在一年内可以生成的步数为：

(3.2 × 10^7) × 10^9 = 3.2 × 10^16

因此，生成 2^64 步所需的计算机时间为：

2^64 ≈ 1.6 × 10^19 = 1.6 × 10^16 × 10^3 = (3.2 × 10^16) × 500

所以，以每秒 10 亿步的速度，计算机生成 2^64 步大约需要 500 年。

## 递归还是迭代？

在第 5 章中，我们设计了一个程序来确定所需的斐波那契数。该程序使用循环来执行计算。换句话说，第 5 章中的程序使用迭代控制结构来重复一组语句。更正式地说，**迭代控制结构**使用循环结构，例如 `while`、`for` 或 `do...while`，来重复一组语句。在示例 17-2 中，我们设计了一个递归函数来计算斐波那契数。从这里的示例可以看出，在递归中，一组语句通过让函数调用自身来重复。此外，递归中使用选择控制结构来控制重复调用。

同样，在第 9 章中，我们使用迭代控制结构（for 循环）来确定列表中的最大元素。在本章中，我们使用递归来确定列表中的最大元素。此外，本章一开始设计了一个递归函数来求非负整数的阶乘。使用迭代控制结构，我们也可以编写算法来求非负整数的阶乘。给出阶乘问题的递归解的唯一原因是为了说明递归是如何工作的。

因此我们看到，解决特定问题通常有两种方法——迭代和递归。显而易见的问题是哪种方法更好——迭代还是递归？没有简单的答案。除了问题的性质之外，确定最佳解决方法方法的另一个关键因素是效率。

示例 7-7（第 7 章）在跟踪程序执行时向我们表明，每当调用函数时，都会为其形参和（自动）局部变量分配内存空间。当函数终止时，该内存空间随后被释放。

本章在跟踪递归函数的执行时也向我们表明，每次（递归）调用都有自己的一组参数和（自动）局部变量。也就是说，每次（递归）调用都要求系统为其形参和（自动）局部变量分配内存空间，并在函数退出时释放该内存空间。因此，执行（递归）函数会带来内存空间和计算机时间方面的开销。因此，递归函数执行起来比其迭代对应版本更慢。在较慢的计算机上，尤其是内存空间有限的计算机上，递归函数的（缓慢）执行会是可见的。

然而，今天的计算机速度快且内存便宜。因此，递归函数的执行并不明显。保持当今计算机的能力

要编写一个将二进制数转换为等价十进制数的程序，我们注意两件事：(1) 必须知道二进制数中每一位的权重，(2) 权重是从右到左分配的。由于我们事先不知道二进制数中有多少位，因此必须从右到左处理这些位。处理完一位后，我们可以将其权重加 1，从而得到其左侧相邻位的权重。此外，必须从二进制数中提取每一位，并乘以 2 的权重次方。要提取一位，我们可以使用取模运算符。考虑以下递归算法，它以伪代码给出。

```text
if (binaryNumber > 0)
{
    bit = binaryNumber % 10;        //extract the rightmost bit
    decimal = decimal + bit * power(2, weight);
    binaryNumber = binaryNumber / 10; //remove the rightmost
                                      //bit
    weight++;
    convert the binaryNumber into decimal
}
```

该算法假设在使用该算法之前，内存位置 decimal 和 weight 已初始化为 0。该算法转换为以下 C++ 递归函数：

```cpp
void binToDec(int binaryNumber, int& decimal, int& weight)
{
    int bit;

    if (binaryNumber > 0)
    {
        bit = binaryNumber % 10;
        decimal = decimal
                + bit * static_cast<int>(pow(2.0, weight));
        binaryNumber = binaryNumber / 10;
        weight++;
        binToDec(binaryNumber, decimal, weight);
    }
}
```

在这个函数中，decimal 和 weight 都是引用参数。与这些参数对应的实参被初始化为 0。提取最右边的位后，该函数更新十进制数和下一位的权重。假设 decimalNumber 和 bitWeight 是 int 变量。考虑以下语句：

```cpp
decimalNumber = 0;
bitWeight = 0;
binToDec(1101, decimalNumber, bitWeight);
```

图 17-8 跟踪最后一条语句的执行，即 `binToDec(1101, decimalNumber, bitWeight);`。它在每个函数调用旁边显示了变量 decimalNumber 和 bitWeight 的内容。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1049_0.png)

**图 17-8** binToDec(1101, decimalNumber, bitWeight); 的执行

在图 17-8 中，每个向下箭头表示相继的函数调用。由于函数 binToDec 的最后一条语句是函数调用，因此该语句执行后，不会发生其他事情。在语句：

`binToDec(1101, decimalNumber, bitWeight);` 执行后，变量 `decimalNumber` 的值为 13。以下 C++ 程序测试函数 `binToDec`：

```cpp
/************************************************************
// Author: D. S. Malik
//
// Program: Binary to decimal
// This program uses recursion to find the decimal
// representation of a binary number.
************************************************************/

#include <iostream>
#include <cmath>

using namespace std;

void binToDec(int binaryNumber, int& decimal, int& weight);

int main()
{
    int decimalNum;
    int bitWeight;
    int binaryNum;

    decimalNum = 0;
    bitWeight = 0;

    cout << "Enter number in binary: ";
    cin >> binaryNum;
    cout << endl;

    binToDec(binaryNum, decimalNum, bitWeight);
    cout << "Binary " << binaryNum << " = " << decimalNum
         << " decimal" << endl;

    return 0;
}

void binToDec(int binaryNumber, int& decimal, int& weight)
{
    int bit;

    if (binaryNumber > 0)
    {
        bit = binaryNumber % 10;
        decimal = decimal
                + bit * static_cast<int>(pow(2.0, weight));
        binaryNumber = binaryNumber / 10;
```

- 1. 如果 `num = 0`，则 `binary(num) = num`。
- 2. 如果 `num > 0`，则先执行 `binary(num / 2)`，然后执行 `num % 2`。

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

图 17-9 跟踪以下语句的执行：

```cpp
decToBin(13, 2);
```

其中 num 为 13，base 为 2。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1052_0.png)

**图 17-9** `decToBin(13, 2)` 的执行

**示例运行：** 在此示例运行中，用户输入以阴影显示。

`Enter a number in decimal: 57`

`Decimal 57 = 111001 binary`

## 快速复习

- 1. 通过将问题简化为其自身的较小版本来解决问题的过程称为递归。
- 2. 递归定义用其自身的较小版本来定义问题。
- 3. 每个递归定义都有一个或多个基本情况。
- 4. 递归算法通过将问题简化为其自身的较小版本来解决问题。
- 5. 每个递归算法都有一个或多个基本情况。
- 6. 基本情况中问题的解是直接获得的。
- 7. 如果一个函数调用自身，则称其为递归函数。
- 8. 递归算法使用递归函数实现。
- 9. 每个递归函数必须有一个或多个基本情况。
- 10. 一般解将问题分解为其自身的较小版本。
- 11. 一般情况最终必须归约到基本情况。
- 12. 基本情况停止递归。
- 13. 在跟踪递归函数时：
    - 从逻辑上讲，你可以将递归函数视为拥有无限多个自身的副本。
    - 对递归函数的每次调用——即每次递归调用——都有自己的代码以及自己的一组参数和局部变量。
    - 完成某个特定递归调用后，控制权返回到调用环境，即前一次调用。当前（递归）调用必须完全执行完毕，控制权才能返回到前一次调用。前一次调用中的执行从紧跟在递归调用之后的点开始。
- 14. 如果一个函数调用自身，则称其为直接递归。
- 15. 如果一个函数调用另一个函数并最终导致对原函数的调用，则称其为间接递归。
- 16. 如果最后执行的语句是递归调用，则这样的递归函数称为尾递归函数。

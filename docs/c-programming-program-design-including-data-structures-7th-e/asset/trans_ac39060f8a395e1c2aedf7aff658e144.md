
```cpp
if (binaryNumber > 0)
{
    bit = binaryNumber % 10;        // extract the rightmost bit
    decimal = decimal + bit * power(2, weight);
    binaryNumber = binaryNumber / 10; // remove the rightmost
                                      // bit

    weight++;
    convert the binaryNumber into decimal
}
```

该算法假设在使用之前，内存位置 decimal 和 weight 已被初始化为0。该算法可转化为以下 C++ 递归函数：

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

在这个函数中，decimal 和 weight 都是引用参数。与这些参数对应的实际参数被初始化为0。提取最右位后，该函数会更新十进制数以及下一位的权重。假设 decimalNumber 和 bitWeight 是 int 变量。考虑以下语句：

```cpp
decimalNumber = 0;
bitWeight = 0;
binToDec(1101, decimalNumber, bitWeight);
```

图15-8跟踪了最后一条语句（即 binToDec(1101, decimalNumber, bitWeight)）的执行过程。它在每次函数调用旁边显示了变量 decimalNumber 和 bitWeight 的内容。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1107_0.png)

**图 15-8** `binToDec(1101, decimalNumber, bitWeight);` 的执行过程

在图15-8中，每个向下箭头表示相继的函数调用。因为函数 `binToDec` 的最后一条语句是一个函数调用，所以这条语句执行后不会发生任何事情。在语句 `binToDec(1101, decimalNumber, bitWeight);` 执行后，变量 decimalNumber 的值为13。

以下 C++ 程序测试函数 binToDec：

```cpp
//**********************************************************
// Author: D. S. Malik
//
// Program: Binary to decimal
// This program uses recursion to find the decimal
// representation of a binary number.
//**********************************************************

#include <iostream>
#include <cmath>

using namespace std;

void binToDec(int binaryNumber, int& decimal, int& weight);

int main()
{
    int decimalNumber;
    int bitWeight;
    int binaryNum;

    decimalNumber = 0;
    bitWeight = 0;

    cout << "Enter number in binary: ";
    cin >> binaryNum;
    cout << endl;

    binToDec(binaryNum, decimalNumber, bitWeight);
    cout << "Binary " << binaryNum << " = " << decimalNumber
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
        weight++;
        binToDec(binaryNumber, decimal, weight);
    }
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```
Enter a number in binary: 11010110
Binary 11010110 = 214 decimal
```

### 编程示例：将数从十进制转换为二进制

上一个编程示例讨论并设计了一个程序，用于将数从二进制表示转换为十进制格式——即从基2转换为基10。本编程示例讨论并设计一个程序，该程序使用递归将一个十进制格式（即基10）的非负整数转换为等价的二进制数（即基2）。首先，我们定义一些术语。

设 *x* 为一个整数。我们将 *x* 除以2后的余数称为 *x* 的**最右位**。因此，33的最右位是1，因为33 % 2为1；28的最右位是0，因为28 % 2为0。

我们首先借助一个示例来说明将基10整数转换为等价二进制格式数的算法。

假设我们想求35的二进制表示。首先，我们将35除以2。商为17，余数——即35的**最右位**——为1。接着，我们将17除以2。商为8，余数——即17的**最右位**——为1。接着，我们将8除以2。商为4，余数——即8的**最右位**——为0。我们继续这一过程，直到商变为0。

35的**最右位**要等到打印出17的**最右位**之后才能打印。17的**最右位**要等到打印出8的**最右位**之后才能打印，依此类推。因此，35的二进制表示是17的二进制表示（即35除以2后的商），后面接35的**最右位**。

因此，要将基10整数 *num* 转换为等价的二进制数，我们首先将商 *num* / 2 转换为等价的二进制数，然后将 *num* 的**最右位**追加到 *num* / 2 的二进制表示后面。

上述讨论可转化为以下递归算法，其中 `binary(num)` 表示 *num* 的二进制表示。

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

图15-9跟踪了以下语句的执行过程：

```cpp
decToBin(13, 2);
```

其中 num 为13，base 为2。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1110_0.png)

**图 15-9** `decToBin(13, 2)` 的执行过程

- c. 找出基本情况，并为每个基本情况提供直接解。
- d. 找出一般情况，并用其自身的较小版本来为每个一般情况提供解。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1113_0.png)

## 练习

每道练习题末尾括号中的数字指本章开头列出的学习目标。

- 1. 判断以下陈述为真或假。

  - a. 问题的递归解法将问题化简为自身的较小版本。(1)
  - b. 每个递归定义都必须有一个或多个基本情况。(2)
  - c. 一般情况会停止递归。(2, 3)
  - d. 在一般情况下，问题的解是直接得到的。(2, 3)
  - e. 递归函数不一定需要基本情况，因为一般情况提供了问题的解。(2, 4)
  - f. 递归函数总是返回一个值。(4)
  - g. 每次调用递归函数都有自己的代码以及自己的一组参数和局部变量。(4)
  - h. 调用自身的函数称为直接递归函数。(5)

- 2. 什么是基本情况？(2)
- 3. 什么是递归情况？(2)
- 4. 什么是直接递归？(5)
- 5. 什么是间接递归？(5)
- 6. 什么是尾递归？(1, 5)

- 7. 考虑以下递归函数：(2, 3, 4, 6)

  ```cpp
  int mystery(int number)                 //Line 1
  {
      if (number == 0)                      //Line 2
          return number;                    //Line 3
      else                                 //Line 4
          return(mystery(number + 1) - number); //Line 5
  }
  ```

  - a. 找出基本情况。
  - b. 找出一般情况。
  - c. 哪些有效值可以作为参数传递给函数 `mystery`？
  - d. 如果 `mystery(0)` 是有效调用，它的值是什么？如果不是，请解释原因。
  - e. 如果 `mystery(10)` 是有效调用，它的值是什么？如果不是，请解释原因。
  - f. 如果 `mystery(-3)` 是有效调用，它的值是什么？如果不是，请解释原因。


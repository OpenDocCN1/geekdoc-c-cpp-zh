
> **注意** `for` 循环的语法如下：
>
> ```cpp
> for (initial expression; logical expression; update expression)
>     statement
> ```
>
> 在功能上等价于以下 `while` 语句：
>
> ```cpp
> initial expression
> while (expression)
> {
>     statement
>     update expression
> }
> ```
>
> 例如，下面的 `for` 和 `while` 循环是等价的：
>
> ```cpp
> for (int i = 0; i < 10; i++)
>     cout << i << " ";
> cout << endl;
> ```
>
> ```cpp
> int i = 0;
> while (i < 10)
> {
>     cout << i << " ";
>     i++;
> }
> cout << endl;
> ```
>
> 如果循环的迭代次数已知或可以预先确定，程序员通常使用 `for` 循环。

### 示例 5-16（斐波那契数程序：修订版）

上一节给出的编程示例：斐波那契数使用 `while` 循环来确定所需的斐波那契数。你可以将 `while` 循环替换为如下等价的 `for` 循环：

```cpp
for (counter = 3; counter <= nthFibonacci; counter++)
{
    current = previous2 + previous1;
    previous1 = previous2;
    previous2 = current;
} //end for
```

使用 `for` 循环确定所需斐波那契数的程序的完整程序清单见本书配套网站。该程序名为 `Ch5_FibonacciNumberUsingAForLoop.cpp`。

在下面的 C++ 程序中，我们建议你逐步走查每个步骤。

## 编程示例：数字分类

该程序读取给定的一组整数，然后打印奇数和偶数的个数。它还输出零的个数。

该程序读取 20 个整数，但你可以轻松修改它以读取任意一组数字。事实上，你可以修改程序，使其首先提示用户指定要读取多少个整数。

**输入** 20 个整数——正数、负数或零。

**输出** 零、偶数和奇数的个数。

### 问题分析与算法设计

读取一个数字后，你需要检查它是偶数还是奇数。假设该值存储在 number 中。将 number 除以 2 并检查余数。如果余数为 0，则 number 是偶数。递增偶数计数，然后检查 number 是否为 0。如果是，则递增零计数。如果余数不为 0，则递增奇数计数。

该程序使用 `switch` 语句来判断 number 是奇数还是偶数。假设 number 是奇数。如果 number 为正数，除以 2 的余数为 1；如果为负数，余数为 −1。如果 number 是偶数，则无论 number 是正数还是负数，除以 2 的余数都是 0。你可以使用取模运算符 % 来求余数。例如：

```cpp
6 % 2 = 0; −4 % 2 = 0; −7 % 2 = −1; 15 % 2 = 1
```

对列表中的每个数字重复上述分析数字的过程。

上述讨论可转化为以下算法：

- 1. 对列表中的每个数字：
  - a. 获取该数字。
  - b. 分析该数字。
  - c. 递增相应的计数。
- 2. 打印结果。

### 变量

因为你要统计零、偶数和奇数的个数，所以需要三个 `int` 类型的变量——比如 zeros、evens 和 odds——来记录计数。你还需要一个变量——比如 number——来读取并存储要分析的数字，以及另一个变量——比如 counter——来统计已分析的数字个数。因此，程序中需要以下变量：

```cpp
int counter;   //loop control variable
int number;    //variable to store the number read
int zeros;     //variable to store the zero count
int evens;     //variable to store the even count
int odds;      //variable to store the odd count
```

显然，必须将变量 zeros、evens 和 odds 初始化为 0。可以在声明这些变量时对它们进行初始化。

### 主算法

- 1. 初始化变量。
- 2. 提示用户输入 20 个数字。
- 3. 对列表中的每个数字：
  - a. 读取该数字。
  - b. 输出该数字（回显输入）。
  - c. 如果该数字是偶数：
    - i. 递增偶数计数。
    - ii. 如果该数字为零，递增零计数。
  - 否则：
    - 递增奇数计数。
- 4. 打印结果。

在编写 C++ 程序之前，让我们更详细地描述步骤 1–4。这样你之后用 C++ 编写指令就会容易得多。

- 1. 初始化变量。可以在声明变量 zeros、evens 和 odds 时对它们进行初始化。
- 2. 使用输出语句提示用户输入 20 个数字。
- 3. 对于步骤 3，你可以使用 `for` 循环来处理和分析这 20 个数字。用伪代码表示，这一步写作如下：

```cpp
for (counter = 1; counter <= 20; counter++)
{
    read the number;
    output number;

    switch (number % 2)    // check the remainder
    {
    case 0:
        increment even count;
        if (number == 0)
            increment zero count;
        break;
    case 1:
    case -1:
        increment odd count;
    } //end switch
} //end for
```

- 4. 打印结果。输出变量 zeros、evens 和 odds 的值。

### 完整程序清单

```cpp
/*************************************************************
// Author: D.S. Malik
//
// Program: Counts zeros, odds, and evens
// This program counts the number of odd and even numbers.
// The program also counts the number of zeros.
*************************************************************/
#include <iostream>
#include <iomanip>

using namespace std;

const int N = 20;

int main()
{
            //Declare variables
    int counter;    //loop control variable
    int number;     //variable to store the new number
    int zeros = 0;                         //Step 1
    int odds = 0;                          //Step 1
    int evens = 0;                         //Step 1

    cout << "Please enter " << N << " integers, "
         << "positive, negative, or zeros."
         << endl;                          //Step 2

    cout << "The numbers you entered are:" << endl;

    for (counter = 1; counter <= N; counter++)       //Step 3
    {
        cin >> number;                              //Step 3a
        cout << number << " ";                      //Step 3b

                                                    //Step 3c
        switch (number % 2)
        {
        case 0:
            evens++;
            if (number == 0)
                zeros++;
            break;
        case 1:
        case -1:
            odds++;
        } //end switch
    } //end for loop

    cout << endl;            //Step 4
    cout << "There are " << evens << " evens, "
         << "which includes " << zeros << " zeros."
         << endl;
    cout << "The number of odd numbers is: " << odds
         << endl;

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```
Please enter 20 integers, positive, negative, or zeros.
The numbers you entered are:
0 0 -2 -3 -5 6 7 8 0 3 0 -23 -8 0 2 9 0 12 67 54
0 0 -2 -3 -5 6 7 8 0 3 0 -23 -8 0 2 9 0 12 67 54
There are 13 evens, which includes 6 zeros.
The number of odd numbers is: 7
```

我们建议你使用上面的示例输入对该程序进行一次走查。

## do...while 循环（重复）结构

本节介绍第三种循环或重复结构，称为 do...while 循环。do...while 语句的一般形式如下：

```cpp
do
    statement
while (expression);
```

当然，语句可以是简单语句或复合语句。如果它是复合语句，请将其括在花括号中。图 5–3 显示了 do...while 循环的执行流程。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_325_0.png)

**图 5-3** do...while 循环

在 C++ 中，do 是保留字。

先执行语句，然后对表达式求值。如果表达式的求值结果为 true，则再次执行该语句。只要 do...while 语句中的表达式为 true，语句就会执行。为避免无限循环，你必须再次确保循环体包含一个最终使表达式为 false 并确保循环正确退出的语句。

### 示例 5-18

```cpp
i = 0;

do
{
    cout << i << " ";
    i = i + 5;
} while (i <= 20);
```

这段代码的输出是：

```
0 5 10 15 20
```

在输出 20 之后，语句：

```cpp
i = i + 5;
```

将 `i` 的值改为 25，因此 `i <= 20` 变为 `false`，从而停止循环。


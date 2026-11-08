

## 编程示例：数字分类

该程序读取一组给定的整数，然后输出奇数和偶数的个数，同时输出零的个数。

程序读取20个整数，但你可以轻松修改它以读取任意数量的数字。事实上，你可以修改程序，使其首先提示用户指定要读取多少个整数。

- **输入** 20个整数——正数、负数或零。
- **输出** 零、偶数和奇数的个数。

### 问题分析与算法设计

读取一个数字后，你需要检查它是偶数还是奇数。假设该值存储在`number`中。将`number`除以2并检查余数。如果余数为0，则`number`是偶数。递增偶数计数，然后检查`number`是否为0。如果是，则递增零计数。如果余数不为0，则递增奇数计数。

程序使用switch语句来判断`number`是奇数还是偶数。假设`number`是奇数。若`number`为正数，除以2的余数为1；若为负数，余数为-1。若`number`是偶数，无论正负，除以2的余数都为0。你可以使用取模运算符`%`来求余数。例如：

```text
6 % 2 = 0; -4 % 2 = 0; -7 % 2 = -1; 15 % 2 = 1
```

对列表中的每个数字重复上述分析过程。

这一讨论可转化为以下算法：

- 1. 对列表中的每个数字：
  - a. 获取该数字。
  - b. 分析该数字。
  - c. 递增相应的计数。
- 2. 输出结果。

**变量**

由于需要统计零、偶数和奇数的个数，你需要三个int类型的变量——比如`zeros`、`evens`和`odds`——来跟踪计数。你还需要一个变量——比如`number`——来读取并存储待分析的数字，以及另一个变量——比如`counter`——来计数已分析的数字。因此，程序中需要以下变量：

```cpp
int counter;    //loop control variable
int number;     //variable to store the number read
int zeros;      //variable to store the zero count
int evens;      //variable to store the even count
int odds;       //variable to store the odd count
```

显然，你必须将变量`zeros`、`evens`和`odds`初始化为0。你可以在声明这些变量时进行初始化。

### 主算法

- 1. 初始化变量。
- 2. 提示用户输入20个数字。
- 3. 对列表中的每个数字：
  - a. 读取该数字。
  - b. 输出该数字（回显输入）。
  - c. 如果该数字是偶数：
    ```text
    {
        i. 递增偶数计数。
        ii. 如果该数字为零，递增零计数。
    }
    否则
        递增奇数计数。
    ```
- 4. 输出结果。

在编写C++程序之前，让我们更详细地描述步骤1–4。这样你会更容易用C++编写指令。

- 1. 初始化变量。你可以在声明变量`zeros`、`evens`和`odds`时初始化它们。
- 2. 使用输出语句提示用户输入20个数字。
- 3. 对于步骤3，你可以使用`for`循环来处理和分析这20个数字。用伪代码表示，该步骤可写成：

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

- 4. 输出结果。输出变量`zeros`、`evens`和`odds`的值。

### 完整程序清单

```cpp
//************************************************************
// Author: D.S. Malik
//
// Program: Counts zeros, odds, and evens
// This program counts the number of odd and even numbers.
// The program also counts the number of zeros.
//************************************************************

#include <iostream>
#include <iomanip>

using namespace std;

const int N = 20;

int main()
{
        //Declare variables
        int counter;    //loop control variable
        int number;     //variable to store the new number
        int zeros = 0;                                  //Step 1
        int odds = 0;                                   //Step 1
        int evens = 0;                                  //Step 1

        cout << "Please enter " << N << " integers, "
             << "positive, negative, or zeros."
             << endl;                                   //Step 2

        cout << "The numbers you entered are:" << endl;

        for (counter = 1; counter <= N; counter++)      //Step 3
        {
                cin >> number;                         //Step 3a
                cout << number << " ";                  //Step 3b

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

        cout << endl;       //Step 4

        cout << "There are " << evens << " evens, "
             << "which includes " << zeros << " zeros."
             << endl;
        cout << "The number of odd numbers is: " << odds
             << endl;

        return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

Please enter 20 integers, positive, negative, or zeros.
The numbers you entered are:

0 0 -2 -3 -5 6 7 8 0 3 0 -23 -8 0 2 9 0 12 67 54

There are 8 evens, which includes 6 zeros.
The number of odd numbers is: 7

我们建议你使用上述示例输入对该程序进行走查。

## do...while 循环（重复）结构

本节介绍第三种类型的循环或重复结构，称为 do...while 循环。do...while 语句的一般形式如下：

```text
do
    statement
while (expression);
```

当然，statement 可以是简单语句或复合语句。如果是复合语句，请用花括号将其括起来。图5-3展示了 do...while 循环的执行流程。

在 while 和 for 循环中，循环条件在执行循环体之前被求值。因此，while 和 for 循环被称为**前测循环**。另一方面，do...while 循环的循环条件在执行循环体之后被求值。因此，do...while 循环被称为**后测循环**。

由于 while 和 for 循环都有入口条件，这些循环可能永远不会激活。而 do...while 循环具有出口条件，因此其语句至少执行一次。

### 示例5-19

考虑以下两个循环：

```cpp
a.  i = 11;
    while (i <= 10)
    {
        cout << i << " ";
        i = i + 5;
    }
    cout << endl;

b.  i = 11;
    do
    {
        cout << i << " ";
        i = i + 5;
    }
    while (i <= 10);

    cout << endl;
```

在 (a) 中，while 循环不产生任何输出。在 (b) 中，do...while 循环输出数字11，并将 i 的值改为16。

do...while 循环可用于输入验证。假设某程序提示用户输入一个测试分数，该分数必须大于等于0且小于等于50。如果用户输入的分数小于0或大于50，则应提示用户重新输入分数。以下 do...while 循环可实现此目标：

```cpp
int score;

do
{
    cout << "Enter a score between 0 and 50: ";
    cin >> score;
    cout << endl;
}
while (score < 0 || score > 50);
```

### 示例9-20

### 被3和9整除的测试

假设 m 和 n 是整数，且 m 非零。那么，如果存在某个整数 r 使得 n = mr，则称 m 是 n 的**除数**；也就是说，当 m 整除 n 时，余数为0。

设 n = dₖdₖ₋₁...d₁d₀ 是一个整数。令 s = dₖ + dₖ₋₁ + dₖ₋₂ + ... + d₁ + d₀ 为 n 的各数字之和。已知 n 能被3整除当且仅当 s 能被3整除；n 能被9整除当且仅当 s 能被9整除。换句话说，一个整数能被3和9整除，当且仅当其数字之和能被3和9整除。

例如，假设 n = 27193257。那么 s = 2 + 7 + 1 + 9 + 3 + 2 + 5 + 7 = 36。由于36既能被3整除也能被9整除，因此27193257既能被3整除也能被9整除。

接下来，我们编写一个程序，通过先求一个正整数的数字之和，再检查该和是否能被3和9整除，来判断该正整数是否能被3和9整除。

为了求一个正整数的数字之和，我们需要提取该数的每一位数字。考虑数字951372。注意 951372 % 10 = 2，这是951372的最后一位数字。还要注意 951372 / 10 = 95137；也就是说，当该数除以10时，会移除最后一位数字。接下来，我们对95137重复这一过程。当然，我们需要将提取的数字相加。

假设 sum 和 num 是 int 变量，且正整数存储在 num 中。于是我们有以下求数字之和的算法：

```cpp
sum = 0;

do
{
    sum = sum + num % 10;  //extract the last digit
                           //and add it to sum
    num = num / 10;        //remove the last digit
}
while (num > 0);
```

使用该算法，我们可以编写以下程序，该程序使用 do...while 循环实现上述整除性测试算法。

```cpp
//Program: Divisibility test by 3 and 9

#include <iostream>

using namespace std;

int main()
{
    int num, temp, sum;

    cout << "Enter a positive integer: ";
    cin >> num;
```


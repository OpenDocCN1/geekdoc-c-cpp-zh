

对列表中的每个数重复前述分析一个数的过程。这段讨论可转化为以下算法：

- 1. 对列表中的每个数：
  - a. 获取该数。
  - b. 分析该数。
  - c. 将相应的计数加 1。
- 2. 输出结果。

### 变量

因为要统计零、偶数和奇数的个数，所以需要三个 int 类型变量——比如 zeros、evens 和 odds——来记录计数。还需要一个变量——比如 number——来读取并存储待分析的数字，以及另一个变量——比如 counter——来统计已分析数字的个数。因此，程序中需要以下变量：

```cpp
int counter;    //loop control variable
int number;     //variable to store the number read
int zeros;      //variable to store the zero count
int evens;      //variable to store the even count
int odds;       //variable to store the odd count
```

显然，必须将变量 zeros、evens 和 odds 初始化为 0。可以在声明这些变量时进行初始化。

### 主算法

- 1. 声明并初始化变量。
- 2. 提示用户输入 20 个数字。
- 3. 对列表中的每个数：
  - a. 读取该数。
  - b. 输出该数（回显输入）。
  - c. 如果该数是偶数：
    - i. 将偶数计数加 1。
    - ii. 如果该数为零，将零计数加 1。

    否则
    将奇数计数加 1。
- 4. 输出结果。

在编写 C++ 程序之前，让我们更详细地描述步骤 1–4。这样，用 C++ 编写指令就会容易得多。

- 1. 初始化变量。可以在声明变量 zeros、evens 和 odds 时初始化它们。
- 2. 使用输出语句提示用户输入 20 个数字。
- 3. 对于步骤 3，可以使用 `for` 循环来处理和分析这 20 个数字。用伪代码表示，这一步写为：

```text
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
    }//end switch
}//end for
```

- 4. 输出结果。输出变量 zeros、evens 和 odds 的值。

### 完整程序清单

```cpp
/************************************************
// Author: D.S. Malik
//
// Program: Counts zeros, odds, and evens
// This program counts the number of odd and even numbers.
// The program also counts the number of zeros.
*************************************************/

#include <iostream>
#include <iomanip>

using namespace std;

const int N = 20;

int main()
{
        //Declare variables
        int counter;        //loop control variable
        int number;         //variable to store the new number
        int zeros = 0;                                      //Step 1
        int odds = 0;                                       //Step 1
        int evens = 0;                                      //Step 1

        cout << "Please enter " << N << " integers, "
             << "positive, negative, or zeros."
             << endl;                         //Step 2

        cout << "The numbers you entered are:" << endl;

        for (counter = 1; counter <= N; counter++)    //Step 3
        {
            cin >> number;                            //Step 3a
            cout << number << " ";                    //Step 3b

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

        cout << endl;

        cout << "There are " << evens << " evens, "
             << "which includes " << zeros << " zeros."
             << endl;
        cout << "The number of odd numbers is: " << odds
             << endl;

        return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Please enter 20 integers, positive, negative, or zeros.
The numbers you entered are:
0 0 -2 -3 -5 6 7 8 0 3 0 -23 -8 0 2 9 0 12 67 54
0 0 -2 -3 -5 6 7 8 0 3 0 -23 -8 0 2 9 0 12 67 54
There are 13 evens, which includes 6 zeros.
The number of odd numbers is: 7
```

建议使用上面的示例输入对此程序进行一次走查。

## do...while 循环（重复）结构

本节介绍第三种循环或重复结构，称为 do...while 循环。do...while 语句的一般形式如下：

```cpp
do
    statement
while (expression);
```

当然，语句可以是简单语句或复合语句。如果是复合语句，请将其括在花括号中。图 5–3 展示了 do...while 循环的执行流程。

![](img/d0be7fc6d804b63484835c6c8bc67a07_357_0.png)

**图 5–3**  do...while 循环

在 C++ 中，do 是保留字。

语句先执行，然后对表达式求值。如果表达式的求值为 true，则语句再次执行。只要 do...while 语句中的表达式为 true，语句就会执行。为避免无限循环，你必须再次确保循环体包含最终使表达式为 false 的语句，并保证循环能正确退出。

### 例 5-18

```cpp
i = 0;

do
{
    cout << i << " ";
    i = i + 5;
}
while (i <= 20);
```

这段代码的输出是：

```text
0 5 10 15 20
```

输出 20 后，语句：

```cpp
i = i + 5;
```

将 `i` 的值改为 25，因此 `i <= 20` 变为 **false**，从而终止循环。

在 `while` 和 `for` 循环中，循环条件在循环体执行*之前*求值。因此，`while` 和 `for` 循环称为**前测循环**。另一方面，`do...while` 循环中的循环条件在循环体执行*之后*求值。因此，`do...while` 循环称为**后测循环**。

由于 `while` 和 `for` 循环都有入口条件，这些循环可能根本不会执行。另一方面，`do...while` 循环有出口条件，因此语句至少会执行一次。

### 例 5-19

考虑以下两个循环：

- a.

  ```cpp
  i = 11;
  while (i <= 10)
  {
      cout << i << " ";
      i = i + 5;
  }
  cout << endl;
  ```

- b.

  ```cpp
  i = 11;
  do
  {
      cout << i << " ";
      i = i + 5;
  }
  while (i <= 10);
  cout << endl;
  ```

在 (a) 中，`while` 循环不产生任何输出；语句从不执行。在 (b) 中，`do...while` 循环输出数字 11，并将 `i` 的值改为 16。这是符合预期的，因为在 `do...while` 中，语句必须*始终*至少执行一次。

`do...while` 循环可用于输入验证。假设程序提示用户输入一个测试分数，该分数必须大于或等于 0 且小于或等于 50。如果用户输入的分数小于 0 或大于 50，则应提示用户重新输入分数。可以使用以下 `do...while` 循环来实现此目标：

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

### 例 5-20：3 和 9 的整除性测试

假设 *m* 和 *n* 是整数，且 *m* 非零。若存在某个整数 *q* 使得 *n = mq*，则称 *m* 为 *n* 的**因子**；也就是说，当 *m* 整除 *n* 时，余数为 0。

设 \(n = a_k a_{k-1}a_{k-2}\cdots a_1a_0\) 为一个整数。设 \(s = a_k + a_{k-1} + a_{k-2} + \cdots + a_1 + a_0\) 为 \(n\) 的各位数字之和。已知若 \(s\) 能被 3 和 9 整除，则 \(n\) 能被 3 和 9 整除。换句话说，一个整数能被 3 和 9 整除当且仅当其各位数字之和能被 3 和 9 整除。

例如，假设 \(n = 27193257\)。则 \(s = 2 + 7 + 1 + 9 + 3 + 2 + 5 + 7 = 36\)。由于 36 同时能被 3 和 9 整除，因此 27193257 也能同时被 3 和 9 整除。

接下来，我们编写一个程序，先求出一个正整数的各位数字之和，然后检查该和是否能被 3 和 9 整除，从而判断该正整数是否能被 3 和 9 整除。

要求一个正整数的各位数字之和，需要提取该数的每一位数字。考虑数字 951372。注意 951372 % 10 = 2，这是 951372 的最后一位数字。还要注意 951372 / 10 = 95137；也就是说，当该数除以 10 时，会去掉最后一位数字。接下来，我们对数字 95137 重复此过程。当然，我们需要将提取出的数字相加。


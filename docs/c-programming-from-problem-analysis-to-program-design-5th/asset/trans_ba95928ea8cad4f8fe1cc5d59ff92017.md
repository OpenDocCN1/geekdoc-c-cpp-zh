
在 **while** 和 **for** 循环中，循环条件在执行循环体之前进行求值。因此，**while** 和 **for** 循环称为 **前测试循环**。另一方面，**do...while** 循环中的循环条件在执行循环体之后进行求值。因此，**do...while** 循环称为 **后测试循环**。

由于 **while** 和 **for** 循环都有入口条件，这些循环可能永远不会被激活。另一方面，**do...while** 循环有出口条件，因此总是至少执行一次语句。

### 示例 5-19

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

在 (a) 中，**while** 循环不产生任何输出。在 (b) 中，**do...while** 循环输出数字 11，并且还将 i 的值改为 16。

**do...while** 循环可用于输入验证。假设程序提示用户输入一个测试分数，该分数必须大于或等于 0 且小于或等于 50。如果用户输入的分数小于 0 或大于 50，则应提示用户重新输入分数。可以使用以下 **do...while** 循环来实现此目标：

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

### 示例 5-20：3 和 9 的整除性测试

假设 $m$ 和 $n$ 是整数，且 $m$ 非零。那么，如果对于某个整数 $t$ 有 $n = mt$，则称 $m$ 是 $n$ 的 **约数**；也就是说，当 $m$ 整除 $n$ 时，余数为 0。

设 $n = a_k a_{k-1} a_{k-2} ... a_1 a_0$ 为一个整数。设 $s = a_k + a_{k-1} + a_{k-2} + ... + a_1 + a_0$ 为 $n$ 的各位数字之和。已知如果 $s$ 能被 3 和 9 整除，则 $n$ 能被 3 和 9 整除。换句话说，一个整数能被 3 和 9 整除当且仅当其各位数字之和能被 3 和 9 整除。

例如，假设 $n = 27193257$。那么 $s = 2 + 7 + 1 + 9 + 3 + 2 + 5 + 7 = 36$。因为 36 能同时被 3 和 9 整除，所以 27193257 能同时被 3 和 9 整除。

接下来，我们编写一个程序，通过先求各位数字之和，然后检查该和是否能被 3 和 9 整除，来判断一个正整数是否能被 3 和 9 整除。

要求一个正整数的各位数字之和，我们需要提取该数字的每一位。考虑数字 951372。注意 951372 % 10 = 2，这是 951372 的最后一位数字。还要注意 951372 / 10 = 95137；也就是说，当该数字除以 10 时，会移除最后一位数字。接下来，我们对数字 95137 重复此过程。当然，我们需要将提取出的数字相加。

假设 `sum` 和 `num` 是 `int` 变量，且正整数存储在 `num` 中。因此，我们有以下算法来求各位数字之和：

```cpp
sum = 0;

do
{
    sum = sum + num % 10; //extract the last digit
                          //and add it to sum
    num = num / 10;       //remove the last digit
}
while (num > 0);
```

使用此算法，我们可以编写以下程序，该程序使用 *do...while* 循环来实现前面的整除性测试算法。

```cpp
//Program: Divisibility test by 3 and 9

#include <iostream>

using namespace std;

int main()
{
    int num, temp, sum;

    cout << "Enter a positive integer: ";
    cin >> num;

    cout << endl;

    temp = num;

    sum = 0;

    do
    {
        sum = sum + num % 10;      //extract the last digit
                                   //and add it to sum
        num = num / 10;            //remove the last digit
    }
    while (num > 0);

    cout << "The sum of the digits = " << sum << endl;

    if (sum % 3 == 0)
        cout << temp << " is divisible by 3" << endl;
    else
        cout << temp << " is not divisible by 3" << endl;

    if (sum % 9 == 0)
        cout << temp << " is divisible by 9" << endl;
    else
        cout << temp << " is not divisible by 9" << endl;
}
```

**示例运行：** 在这些示例运行中，用户输入以底纹显示。

**示例运行 1：**

```text
Enter a positive integer: 27193257

The sum of the digits = 36
27193257 is divisible by 3
27193257 is divisible by 9
```

**示例运行 2：**

```text
Enter a positive integer: 609321

The sum of the digits = 21
609321 is divisible by 3
609321 is not divisible by 9
```

**示例运行 3：**

```text
Enter a positive integer: 161905102

The sum of the digits = 25
161905102 is not divisible by 3
161905102 is not divisible by 9
```

## 选择合适的循环结构

所有三种循环在 C++ 中都有其适用之处。如果你知道，或者程序能够预先确定所需的重复次数，那么 `for` 循环是正确选择。如果你不知道，并且程序无法预先确定所需的重复次数，而且重复次数可能为零，那么 `while` 循环是正确选择。如果你不知道，并且程序无法预先确定所需的重复次数，而且重复次数至少为一次，那么 `do...while` 循环是正确选择。

## break 和 continue 语句

`break` 语句在 `switch` 结构中执行时，会立即退出 `switch` 结构。类似地，你可以在 `while`、`for` 和 `do...while` 循环中使用 `break` 语句。当 `break` 语句在重复结构中执行时，它会立即退出该结构。`break` 语句通常用于两个目的：

- 提前退出循环。
- 跳过 `switch` 结构的剩余部分。

`break` 语句执行后，程序继续执行该结构之后的第一个语句。在循环中使用 `break` 语句可以消除某些（标志）变量的使用。以下 C++ 代码段有助于说明这一想法。（假设所有变量都已正确声明。）

```cpp
sum = 0;
isNegative = false;

cin >> num;

while (cin && !isNegative)
{
    if (num < 0)    //if num is negative, terminate the loop
                    //after this iteration
    {
        cout << "Negative number found in the data." << endl;
        isNegative = true;
    }
    else
    {
        sum = sum + num;
        cin >> num;
    }
}
```

这个 `while` 循环应该求一组正数之和。如果数据集中包含负数，循环会以适当的错误消息终止。这个 `while` 循环使用标志变量 `isNegative` 来达到所需结果。变量 `isNegative` 在 `while` 循环之前初始化为 `false`。在将 num 加入

```cpp
while (cin)
{
    if (num < 0)
    {
        cout << "Negative number found in the data." << endl;
        cin >> num;
        continue;
    }

    sum = sum + num;
    cin >> num;
}
```

前面已经说明，所有三种循环在 C++ 中都有其适用之处，并且一种循环通常可以替代另一种循环。然而，`continue` 语句的执行正是 `while` 和 `do...while` 结构与 `for` 结构的不同之处。当 `continue` 语句在 `while` 或 `do...while` 循环中执行时，更新语句可能不会执行。在 `for` 结构中，更新语句总是会执行。

## 嵌套控制结构

在本节中，我们给出示例，说明如何使用嵌套循环来获得有用的结果并处理数据。

### 示例 5-21

假设你想创建以下图案：

```text
*
**
***
****
*****
```

显然，你想打印五行星号。在第一行中，你想打印一个星号，在第二行中打印两个星号，依此类推。因为将打印五行，所以从以下 `for` 语句开始：

```cpp
for (i = 1; i <= 5; i++)
```

i 的值在第一次迭代中为 1，在第二次迭代中为 2，依此类推。你可以将 i 的值用作嵌套在此循环内的另一个 `for` 循环中的限制条件，以控制一行中的星号数量。再稍加思考，便可得到以下代码：

```cpp
for (i = 1; i <= 5; i++)          //Line 1
{                                  //Line 2
    for (j = 1; j <= i; j++)      //Line 3
        cout << "*";              //Line 4
    cout << endl;                  //Line 5
}                                  //Line 6
```


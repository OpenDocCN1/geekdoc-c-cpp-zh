
## 示例 5-11

下面的 `for` 循环执行五条空语句：

```cpp
for (i = 0; i < 5; i++);    //Line 1
    cout << "*" << endl;    //Line 2
```

`for` 语句末尾（输出语句之前，第 1 行）的分号会终止 for 循环。这个 for 循环的动作是空的，即 null。

前面的示例表明，要让 `for` 循环执行所需动作需要小心。

以下是关于 `for` 循环的一些说明：

- 如果循环条件最初为假，则循环体不执行。
- 更新表达式执行时会改变循环控制变量（由初始化表达式初始化）的值，最终使循环条件的值为假。如果循环条件始终为真，则 `for` 循环体会无限执行。
- C++ 允许对 double 类型（或任何实数数据类型）的循环控制变量使用小数值。由于不同计算机可能给这些循环控制变量不同结果，应避免使用此类变量。
- `for` 语句末尾（正好在循环体之前）的分号是语义错误。在这种情况下，`for` 循环的动作是空的。
- 在 `for` 语句中，如果省略循环条件，则假定为真。
- 在 `for` 语句中，可以省略全部三条语句——初始化语句、循环条件和更新语句。下面是一个合法的 `for` 循环：

```cpp
for (;;)
    cout << "Hello" << endl;
```

这是一个无限 `for` 循环，会不断打印单词 Hello。

下面是更多 `for` 循环的示例。

## 示例 5-12

如果正确设置 for 循环控制表达式，可以使用 for 循环倒计数。

例如，考虑下面的 for 循环：

```cpp
for (i = 10; i >= 1; i--)
    cout << " " << i;
cout << endl;
```

输出为：

10 9 8 7 6 5 4 3 2 1

在此 for 循环中，变量 i 初始化为 10。每次循环迭代后，i 减 1。只要 i >= 1，循环就继续执行。

## 示例 5-13

可以按任意固定数增加（或减少）循环控制变量。在下面的 for 循环中，变量初始化为 1；在 for 循环末尾，i 增加 2。这个 for 循环输出前 10 个正奇数。

```cpp
for (i = 1; i <= 20; i = i + 2)
    cout << " " << i;
cout << endl;
```

## 示例 5-14

假设 i 是一个 int 变量。

- 1. 考虑下面的 for 循环：

```cpp
for (i = 10; i <= 9; i++)
    cout << i << " ";
cout << endl;
```

在此 for 循环中，初始化语句将 i 设为 10。因为循环条件（i <= 9）最初为假，所以什么也不发生。

- 2. 考虑下面的 for 循环：

```cpp
for (i = 9; i >= 10; i--)
    cout << i << " ";
cout << endl;
```

在此 for 循环中，初始化语句将 i 设为 9。因为循环条件（i >= 10）最初为假，所以什么也不发生。

- 3. 考虑下面的 for 循环：

```cpp
for (i = 10; i <= 10; i++)        //Line 1
    cout << i << " ";             //Line 2
cout << endl;                     //Line 3
```

在此 for 循环中，初始化语句将 i 设为 10。循环条件（i <= 10）求值为真，因此第 2 行中的输出语句执行，输出 10。

接下来，更新语句将 i 的值增加 1，因此 i 的值变为 11。现在循环条件求值为假，for 循环终止。注意第 2 行中的输出语句只执行一次。

- 4. 考虑下面的 for 循环：

```cpp
for (i = 1; i <= 10; i++);   //Line 1
    cout << i << " ";        //Line 2
    cout << endl;              //Line 3
```

这个 for 循环对第 2 行中的输出语句没有影响。for 语句末尾的分号终止了 for 循环；因此 for 循环的动作是空的。输出语句独立存在，只执行一次。

- 5. 考虑下面的 for 循环：

```cpp
for (i = 1; ; i++)
    cout << i << " ";
    cout << endl;
```

在此 for 循环中，因为 for 语句省略了循环条件，所以循环条件始终为真。这是一个无限循环。

## 示例 5-15

在此示例中，for 循环读取五个数字并求它们的和与平均值。考虑下面的程序代码，其中 i、newNum、sum 和 average 是 int 变量。

```cpp
sum = 0;

for (i = 1; i <= 5; i++)
{
    cin >> newNum;
    sum = sum + newNum;
}

average = sum / 5;
cout << "The sum is " << sum << endl;
cout << "The average is " << average << endl;
```

在前面的 for 循环中，读取 newNum 后，将该值加到此前已计算的（部分）和中，该和包含当前数字之前读取的所有数字。变量 sum 在 for 循环之前初始化为 0。因此，程序读取第一个数字并将其加到 sum 的值后，变量 sum 保存第一个数字的正确和。

for 循环的语法如下：

```cpp
for (initial expression; logical expression; update expression)
    statement
```

在功能上等价于下面的 while 语句：

```cpp
initial expression
while (expression)
{
    statement
    update expression
}
```

例如，下面的 for 和 while 循环等价：

```cpp
for (int i = 0; i < 10; i++)
    cout << i << " ";
cout << endl;
```

```cpp
int i = 0;
while (i < 10)
{
    cout << i << " ";
    i++;
}
cout << endl;
```

如果循环的迭代次数已知或可以预先确定，程序员通常使用 for 循环。

## 示例 5-16（斐波那契数程序：再访）

上一节给出的编程示例：斐波那契数使用 while 循环来确定所需的斐波那契数。可以按如下方式用等价的 for 循环替换 while 循环：

```cpp
for (counter = 3; counter <= nthFibonacci; counter++)
{
    current = previous2 + previous1;
    previous1 = previous2;
    previous2 = current;
}//end for
```

使用 for 循环确定所需斐波那契数的程序的完整程序清单见本书配套网站。该程序名为 Ch5_FibonacciNumberUsingAForLoop.cpp。

在下面的 C++ 程序中，我们建议你逐步走查每一步。

## 示例 5-17

下面的 C++ 程序求前 n 个正整数的和。

```cpp
//Program to determine the sum of the first n positive integers.

#include <iostream>

using namespace std;

int main()
{
    int counter;    //loop control variable
    int sum;        //variable to store the sum of numbers
    int n;          //variable to store the number of
                   //first positive integers to be added

    cout << "Line 1: Enter the number of positive "
         << "integers to be added: ";                 //Line 1
    cin >> n;                                          //Line 2
    sum = 0;                                           //Line 3
    cout << endl;                                      //Line 4

    for (counter = 1; counter <= n; counter++)         //Line 5
        sum = sum + counter;                           //Line 6

    cout << "Line 7: The sum of the first " << n
         << " positive integers is " << sum
         << endl;                                      //Line 7

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

Line 1: Enter the number of positive integers to be added: 100

Line 7: The sum of the first 100 positive integers is 5050

第 1 行中的语句提示用户输入要相加的正整数个数。第 2 行中的语句将用户输入的数字存入 n，第 3 行中的语句将 sum 初始化为 0。第 5 行中的 for 循环执行 n 次。在 for 循环中，counter 初始化为 1，并在每次循环迭代后增加 1。因此，counter 的范围从 1 到 n。每次通过循环时，counter 的值被加到 sum。变量 sum 初始化为 0，counter 的范围从 1 到 n，并且 counter 的当前值被加到 sum 的值。因此，for 循环执行后，sum 包含前 n 个值的和，在示例运行中即 100 个正整数。

回想一下，将一个控制结构语句放在另一个控制结构语句内部称为**嵌套**。下面的编程示例演示了一个简单的嵌套实例。它还很好地演示了计数。

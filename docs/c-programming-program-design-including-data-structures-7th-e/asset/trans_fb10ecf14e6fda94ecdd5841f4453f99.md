

## 例 5-11

以下 `for` 循环执行五条空语句：

```cpp
for (i = 0; i < 5; i++);    //Line 1
    cout << "*" << endl;    //Line 2
```

`for` 语句末尾（输出语句之前，第 1 行）的分号终止了 `for` 循环。此 `for` 循环的动作为空，即 null。如例 5-10(2) 所示，第 2 行的缩进具有误导性。

前面的示例表明，要让 `for` 循环执行所需操作，需要小心。

以下是对 `for` 循环的一些说明：

- 如果循环条件最初为 `false`，则循环体不会执行。
- 更新表达式执行时会改变循环控制变量的值（该变量由初始表达式初始化），这种改变应最终使循环条件的值变为 `false`。如果循环条件始终为 `true`，则 `for` 循环体会无限执行。
- C++ 允许对 `double` 类型（或任何实数数据类型）的循环控制变量使用小数值。由于不同计算机可能对这些循环控制变量给出不同结果，应避免使用此类变量。
- `for` 语句末尾（紧挨循环体之前）的分号是语义错误。在这种情况下，`for` 循环的动作为空。
- 在 `for` 语句中，如果省略循环条件，则假定其为 `true`。
- 在 `for` 语句中，可以省略全部三条语句——初始化语句、循环条件和更新语句。但是，`for` 语句必须包含两个分号。以下是一个合法的 `for` 循环：

```cpp
for (;;)
    cout << "Hello" << endl;
```

这是一个无限 `for` 循环，会不断打印单词 Hello。

以下是更多 `for` 循环的示例。

## 例 5-12

如果正确设置 `for` 循环控制表达式，就可以使用 `for` 循环倒计数。

例如，考虑以下 `for` 循环：

```cpp
for (i = 10; i >= 1; i--)
    cout << " " << i;
cout << endl;
```

输出为：

10  9  8  7  6  5  4  3  2  1

在此 `for` 循环中，变量 `i` 初始化为 10。每次循环迭代后，`i` 减 1。只要 `i >= 1`，循环就继续执行。

## 例 5-13

可以按任意固定数值递增（或递减）循环控制变量。在以下 `for` 循环中，变量初始化为 1；在 `for` 循环末尾，`i` 递增 2。此 `for` 循环输出前 10 个正奇数。

```cpp
for (i = 1; i <= 20; i = i + 2)
    cout << " " << i;
cout << endl;
```

输出为：

1 3 5 7 9 11 13 15 17 19

## 例 5-14

假设 `i` 是 `int` 变量。

- 1. 考虑以下 `for` 循环：

    ```cpp
    for (i = 10; i <= 9; i++)
        cout << i << " ";
    cout << endl;
    ```

    在此 `for` 循环中，初始化语句将 `i` 设为 10。由于最初循环条件（`i <= 9`）为 `false`，所以什么也不发生。

- 2. 考虑以下 `for` 循环：

    ```cpp
    for (i = 9; i >= 10; i--)
        cout << i << " ";
    cout << endl;
    ```

    在此 for 循环中，初始化语句将 i 设为 9。由于最初循环条件（i >= 10）为 false，所以什么也不发生。

- 3. 考虑以下 for 循环：

    ```cpp
    for (i = 10; i <= 10; i++)        //Line 1
        cout << i << " ";             //Line 2
    cout << endl;                     //Line 3
    ```

    在此 for 循环中，初始化语句将 i 设为 10。循环条件（i <= 10）求值为 true，因此第 2 行中的输出语句执行，输出 10。接着，更新语句将 `i` 的值递增 1，所以 `i` 的值变为 11。现在循环条件求值为 false，for 循环终止。注意，第 2 行中的输出语句只执行一次。

- 4. 考虑以下 for 循环：

    ```cpp
    for (i = 1; i <= 10; i++); //Line 1
        cout << i << " ";      //Line 2
    cout << endl;              //Line 3
    ```

    此 for 循环对第 2 行中的输出语句没有影响。for 语句末尾的分号终止了 for 循环；因此 for 循环的动作为空。输出语句完全独立，只执行一次。

- 5. 考虑以下 for 循环：

    ```cpp
    for (i = 1; ; i++)
        cout << i << " ";
    cout << endl;
    ```

    在此 for 循环中，因为 for 语句省略了循环条件，所以循环条件始终为 true。这是一个无限循环。

- 6. 以下 for 循环输出不超过 100 的 2 的正整数次幂。

    ```cpp
    for (i = 2; i < 100; i = 2 * i)
        cout << i << " "; //output power of 2
    cout << endl;
    ```

    输出为：

    2 4 8 16 32 64

## 例 5-16（斐波那契数程序：再探）

上一节给出的编程示例：斐波那契数，使用 `while` 循环确定所需的斐波那契数。可以按如下方式用等价的 `for` 循环替换 `while` 循环：

```cpp
for (counter = 3; counter <= nthFibonacci; counter++)
{
    current = previous2 + previous1;
    previous1 = previous2;
    previous2 = current;
    counter++;
}//end for
```

使用 `for` 循环确定所需斐波那契数的程序的完整程序清单见本书配套网站。该程序名为 Ch5_FibonacciNumberUsingAForLoop.cpp。

在以下 C++ 程序中，建议你逐步走查每一步。

## 例 5-17

以下 C++ 程序求前 n 个正整数之和。

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
         << "integers to be added: ";                     //Line 1
    cin >> n;                                              //Line 2
    sum = 0;                                               //Line 3
    cout << endl;                                          //Line 4

    for (counter = 1; counter <= n; counter++)             //Line 5
        sum = sum + counter;                               //Line 6

    cout << "Line 7: The sum of the first " << n
         << " positive integers is " << sum
         << endl;                                          //Line 7

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

第 1 行：输入要相加的正整数个数：`100`

第 7 行：前 100 个正整数之和为 5050

第 1 行中的语句提示用户输入要相加的正整数个数。第 2 行中的语句将用户输入的数存入 `n`，第 3 行中的语句将 `sum` 初始化为 0。第 5 行中的 `for` 循环执行 `n` 次。在 `for` 循环中，`counter` 初始化为 1，并在每次循环迭代后递增 1。因此，`counter` 的范围从 1 到 `n`。每次循环时，`counter` 的值被加到 `sum` 中。变量 `sum` 初始化为 0，`counter` 的范围从 1 到 `n`，并且 `counter` 的当前值被加到 `sum` 的值中。因此，`for` 循环执行后，`sum` 包含前 `n` 个值之和，在示例运行中即 100 个正整数之和。

回想一下，将一个控制结构语句放在另一个控制结构语句内部称为**嵌套**。以下编程示例演示了一个简单的嵌套实例，也很好地演示了计数。

## 编程示例：数字分类

此程序读取给定的一组整数，然后打印奇数和偶数的个数。它还输出零的个数。

该程序读取 20 个整数，但你可以轻松修改它以读取任意一组数。事实上，你可以修改程序，使其首先提示用户指定要读取多少个整数。

- **输入：** 20 个整数——正数、负数或零。
- **输出：** 零、偶数和奇数的个数。

### 问题分析与算法设计

读取一个数后，需要检查它是偶数还是奇数。假设该值存储在 `number` 中。将 `number` 除以 2 并检查余数。如果余数为 0，则 `number` 是偶数。递增偶数计数，然后检查 `number` 是否为 0。如果是，则递增零计数。如果余数不为 0，则递增奇数计数。

程序使用 `switch` 语句判断 `number` 是奇数还是偶数。假设 `number` 是奇数。如果 `number` 为正数，除以 2 得到余数 1；如果为负数，得到余数 -1。如果 `number` 是偶数，无论 `number` 是正数还是负数，除以 2 的余数都是 0。可以使用取模运算符 `%` 求余数。例如：

```
6 % 2 = 0; -4 % 2 = 0; -7 % 2 = -1; 15 % 2 = 1
```



当你发现自己需要一个函数时，先写下参数变量和返回值的描述。

这个函数如何完成它的工作？我们先来看一个简单的情况。如果数字在 1 到 9 之间，我们需要计算出 "one" ... "nine"。事实上，我们需要对百位（*two hundred*）*再次* 进行相同的计算。利用逐步分解的过程，我们为这个更简单的任务设计了另一个函数。同样，我们没有直接实现该函数，而是先编写注释：

```cpp
/*
    Turns a digit into its English name.
    @param digit an integer between 1 and 9
    @return the name of digit ("one" ... "nine")
*/
string digit_name(int digit)
```

一个函数可能需要更简单的函数来完成其工作。

这听起来实现起来很简单，使用一个带有九个分支的 if 语句即可。完成 *digit_name* 函数应该不需要其他函数，所以我们稍后再处理实现细节。

10 到 19 之间的数字是特殊情况。让我们用一个单独的函数 *teen_name* 将它们转换为字符串 "eleven"、"twelve"、"thirteen" 等等：

```cpp
/*
    Turns a number between 10 and 19 into its English name.
    @param number an integer between 10 and 19
    @return the name of the number ("ten" ... "nineteen")
*/
string teen_name(int number)
```

接下来，假设数字在 20 到 99 之间。然后我们将十位显示为 "twenty"、"thirty"、...、"ninety"。为了简单和一致，把该计算放入一个单独的函数中：

```cpp
/*
    Gives the name of the tens part of a number between 20 and 99.
    @param number an integer between 20 and 99
    @return the name of the tens part of the number ("twenty" ... "ninety")
*/
string tens_name(int number)
```

现在假设数字至少为 20 且最多为 99。如果该数字能被 10 整除，我们使用 *tens_name*，然后就完成了。否则，我们用 *tens_name* 打印十位，用 *digit_name* 打印个位。如果数字在 100 到 999 之间，则我们显示一个数字、单词 "hundred" 以及如前所述的余数。

下面是对该算法的伪代码描述：

```text
part = number (The part that still needs to be converted)
name = "" (The name of the number)

if part >= 100
    name = name of hundreds in part + " hundred"
    Remove hundreds from part.

if part >= 20
    Append tens_name(part) to name.
    Remove tens from part.
else if part >= 10
    Append teen_name(part) to name.
    part = 0

if (part > 0)
    Append digit_name(part) to name.
```

这段伪代码相对于口头描述有许多重要的改进。它展示了如何安排测试，先从与较大数字的比较开始，并展示了较小的数字随后如何在后续的 if 语句中被处理。

另一方面，这段伪代码对于各部分的实际转换是模糊的，只是提到了“百位的名称”等等。此外，我们对空格的处理也比较模糊。照现在的样子，代码会产生没有空格的字符串，例如 twohundredseventyfour。与主问题的复杂性相比，人们会希望空格只是一个次要问题。最好不要用次要细节把伪代码弄乱。

现在把伪代码转换成真正的代码。最后三种情况很容易，因为已经为它们开发了辅助函数：

```cpp
if (part >= 20)
{
    name = name + " " + tens_name(part);
    part = part % 10;
}
else if (part >= 10)
{
    name = name + " " + teen_name(part);
    part = 0;
}

if (part > 0)
{
    name = name + " " + digit_name(part);
}
```

最后，让我们处理 100 到 999 之间的数字。因为 part < 1000，part / 100 是一位数，我们通过调用 digit_name 获取其名称。然后我们添加 "hundred" 后缀：

```cpp
if (part >= 100)
{
    name = digit_name(part / 100) + " hundred";
    part = part % 100;
}
```

现在你已经看到了 int_name 函数的所有重要构建块。下面是完整的程序：

## ch05/intname.cpp

```cpp
#include <iostream>
#include <string>

using namespace std;

/**
    Turns a digit into its English name.
    @param digit an integer between 1 and 9
    @return the name of digit ("one" ... "nine")
*/
string digit_name(int digit)
{
    if (digit == 1) return "one";
    if (digit == 2) return "two";
    if (digit == 3) return "three";
    if (digit == 4) return "four";
    if (digit == 5) return "five";
    if (digit == 6) return "six";
    if (digit == 7) return "seven";
    if (digit == 8) return "eight";
    if (digit == 9) return "nine";
    return "";
}

/**
 * Turns a number between 10 and 19 into its English name.
 * @param number an integer between 10 and 19
 * @return the name of the given number (“ten” ... “nineteen”)
 */
string teen_name(int number)
{
    if (number == 10) return "ten";
    if (number == 11) return "eleven";
    if (number == 12) return "twelve";
    if (number == 13) return "thirteen";
    if (number == 14) return "fourteen";
    if (number == 15) return "fifteen";
    if (number == 16) return "sixteen";
    if (number == 17) return "seventeen";
    if (number == 18) return "eighteen";
    if (number == 19) return "nineteen";
    return "";
}

/**
 * Gives the name of the tens part of a number between 20 and 99.
 * @param number an integer between 20 and 99
 * @return the name of the tens part of the number (“twenty” ... “ninety”)
 */
string tens_name(int number)
{
    if (number >= 90) return "ninety";
    if (number >= 80) return "eighty";
    if (number >= 70) return "seventy";
    if (number >= 60) return "sixty";
    if (number >= 50) return "fifty";
    if (number >= 40) return "forty";
    if (number >= 30) return "thirty";
    if (number >= 20) return "twenty";
    return "";
}

/**
 * Turns a number into its English name.
 * @param number a positive integer < 1,000
 * @return the name of the number (e.g. “two hundred seventy four”)
 */
string int_name(int number)
{
    int part = number;  // The part that still needs to be converted
    string name; // The return value

    if (part >= 100)
    {
        name = digit_name(part / 100) + " hundred";
        part = part % 100;
    }

    if (part >= 20)
    {
        name = name + " " + tens_name(part);
        part = part % 10;
    }
    else if (part >= 10)
    {
        name = name + " " + teen_name(part);
        part = 0;
    }

    if (part > 0)
    {
        name = name + " " + digit_name(part);
    }

    return name;
}

int main()
{
    cout << "Please enter a positive integer: ";
    int input;
    cin >> input;
    cout << int_name(input) << endl;
    return 0;
}
```

## 程序运行

```text
Please enter a positive integer: 729
seven hundred twenty nine
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_242_0.png)

- 23. 解释如何改进 int_name 函数，使其能够处理最多 9,999 的参数。
- 24. 为什么第 87 行设置 part = 0？
- 25. 当你调用 int_name(0) 时会发生什么？如何修改 int_name 函数以正确处理这种情况？
- 26. 如编程提示 5.4 所述，跟踪函数调用 int_name(72)。
- 27. 使用逐步分解的过程，将打印以下表格的任务分解为更简单的任务。

| i | i * i * i |
|---:|---:|
| 1 | 1 |
| 2 | 8 |
| ... | ... |
| 20 | 8000 |

**练习一下** 现在你可以尝试本章末尾的这些练习：R5.12、P5.16、P5.19。

## 编程提示 5.3

### 保持函数简短

![](img/5e58fb4c840712efd6ed6fa82bb97f57_243_0.png)

编写一个函数是有一定成本的。你需要设计、编码和测试这个函数。函数需要文档化。你需要花费一些精力使函数可复用，而不是局限于特定上下文。为了避免这种成本，人们总是倾向于把越来越多的代码塞到一个地方，而不是费心将代码分解为单独的函数。经常可以看到经验不足的程序员编写出数百行长的函数。

根据经验，如果一个函数太长，其代码在开发环境中一个屏幕显示不下，那么它可能应该被拆分。

## 编程提示 5.4

### 跟踪函数

![](img/5e58fb4c840712efd6ed6fa82bb97f57_243_1.png)

当你设计一个复杂的函数集时，在将程序交给计算机之前，进行手工**走查**是一个好主意。

拿一张索引卡或一张纸，写下你想研究的函数调用。写下函数名称以及参数变量的名称和值，如下所示：

| `int_name(number = 416)` |
| --- |
|  |
|  |

然后写下函数变量的名称和初始值。把它们写在一个表格中，因为你将在走查代码时更新它们。

**`int_name(number = 416)`**

| part | name |
| --- | --- |
| 416 | --- |

我们进入测试 `part >= 100`。`part / 100` 是 4，`part % 100` 是 16。很容易看出 `digit_name(4)` 是 "four"。（如果 `digit_name` 很复杂，你就需要用另一张纸来弄清楚这个函数调用。以这种方式积累好几张纸是很常见的。）

现在 `name` 变成了 `name + " " + digit_name(part / 100) + " hundred"`，即 "four hundred"，而 `part` 变成了 `part % 100`，即 16。

**`int_name(number = 416)`**

| part | name |
| --- | --- |
| 416 | --- |
| 16 | "four hundred" |


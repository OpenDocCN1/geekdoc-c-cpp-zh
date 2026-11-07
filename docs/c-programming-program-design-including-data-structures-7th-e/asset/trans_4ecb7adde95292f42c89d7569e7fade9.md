
```cpp
case false:
    cout << "Not old enough to be drafted." << endl;
    cout << "Not old enough to vote." << endl;
    cout << "Not old enough to drink." << endl;
}
```

正如从前面示例中可以看到的，switch 语句是实现多重选择的一种优雅方式。你将在本章末尾的编程示例中看到 switch 语句的使用。尽管不存在可用于决定是使用 if...else 结构还是 switch 结构来实现多重选择的固定规则，但应记住以下考虑事项。如果多重选择涉及一个值范围，你可以使用 switch 结构（其中将每个范围转换为有限的值集合），也可以使用 if...else 结构。

例如，在示例 4-24 中，grade 的值取决于 score 的值。如果 score 在 0 到 59 之间，则 grade 为 'F'。由于 score 是 int 变量，因此有 60 个值对应于 'F' 等级。如果将全部 60 个值列为 case 值，则 switch 语句可能会非常长。然而，除以 10 可将这 60 个值减少为仅 6 个值：0、1、2、3、4 和 5。

如果值范围由无限多个值组成，并且无法将其缩减为包含有限个值的集合，则必须使用 if...else 结构。例如，如果 score 恰好是 double 变量且可能出现小数成绩，那么 0 到 60 之间的值数量是无限的。然而，你可以使用表达式 static_cast<int>(score) / 10，仍可将这个无限的值数量缩减为仅六个值。

### 通过避免对概念和技术的一知半解来避免错误（再探）

本章前面，我们讨论了对一个概念或技术的一知半解如何导致程序中的错误。在本节中，我们给出另一个示例来说明使用一知半解的概念和技术所导致的问题。在示例 4-24 中，我们说明了如何根据 0 到 100 之间的测试分数来分配等级。接下来，考虑以下根据测试分数分配等级的程序：

```cpp
//Grade program with bugs.

#include <iostream>                              //Line 1

using namespace std;                             //Line 2

int main()                                        //Line 3
{
    int testScore;                                //Line 4
                                                 //Line 5
    cout << "Enter the test score: ";            //Line 6
    cin >> testScore;                             //Line 7
    cout << endl;                                      //Line 8

    switch (testScore / 10)                            //Line 9
    {                                                  //Line 10
    case 0:                                            //Line 11
    case 1:                                            //Line 12
    case 2:                                            //Line 13
    case 3:                                            //Line 14
    case 4:                                            //Line 15
    case 5:                                            //Line 16
        cout << "The grade is F." << endl;        //Line 17
    case 6:                                            //Line 18
        cout << "The grade is D." << endl;        //Line 19
    case 7:                                            //Line 20
        cout << "The grade is C." << endl;        //Line 21
    case 8:                                            //Line 22
        cout << "The grade is B." << endl;        //Line 23
    case 9:                                            //Line 24
    case 10:                                           //Line 25
        cout << "The grade is A." << endl;        //Line 26
    default:                                           //Line 27
        cout << "Invalid test score." << endl;    //Line 28
    }                                                  //Line 29

    return 0;                                          //Line 30
}                                                      //Line 31
```

**示例运行：** 在这些示例运行中，用户输入以底纹显示。

**示例运行 1：**

```text
Enter the test score: 110

Invalid test score.
```

**示例运行 2：**

```text
Enter the test score: -70

Invalid test score.
```

**示例运行 3：**

```text
Enter the test score: 75

The grade is C.
The grade is B.
The grade is A.
Invalid test score.
```

从这些示例运行可以得出，如果 testScore 的值小于 0 或大于 100，则程序产生正确结果；但如果 testScore 的值在 0 到 100 之间，比如 75，则程序产生错误结果。你能看出原因吗？

![](img/d0be7fc6d804b63484835c6c8bc67a07_283_0.png)

如示例运行 3 所示，假设 `testScore` 的值为 75。那么，`testScore / 10 = 7`，并且该值与 `case` 标签 7 匹配。因此，按我们的意图，它应打印 The grade is C。然而，输出是：

```text
The grade is C.
The grade is B.
The grade is A.
Invalid test score.
```

但为什么呢？显然，每个 `case` 标签至多只关联一个 `cout` 语句。问题在于对 `switch` 结构如何工作只有一知半解。正如我们所看到的，该 `switch` 语句不包含任何 `break` 语句。因此，在执行与匹配的 `case` 标签关联的语句之后，执行会继续执行与下一个 `case` 标签关联的语句，从而导致打印出四行非预期输出。

为了正确输出结果，switch 结构必须在每个 `case` 语句之后包含一个 `break` 语句，最后一个 `case` 语句除外。我们将修改该程序以使其输出正确结果留作练习。

我们再次可以看到，对概念的一知半解可能导致程序中的严重错误。因此，花时间完全理解每个概念和技术，将为你节省数小时的调试时间。

### 使用 `assert` 函数终止程序

程序中可能会出现某些非常难以捕获的错误。例如，使用你迄今为止研究过的任何编程技术，都可能难以捕获除以零错误。C++ 包含一个预定义函数 `assert`，它在某些难以捉摸的错误发生时停止程序执行很有用。对于除以零的情况，你可以使用 `assert` 函数确保程序终止，并给出适当的错误消息，指明错误类型以及错误发生所在的程序位置。

考虑以下语句：

```cpp
int numerator;
int denominator;
int quotient;
double hours;
double rate;
double wages;
char ch;
```

- 1. `quotient = numerator / denominator;`
- 2. `if (hours > 0 && (0 < rate && rate <= 15.50))`
  `wages = rate * hours;`
- 3. `if ('A' <= ch && ch <= 'Z')`

在第一条语句中，如果 denominator 为 0，那么从逻辑上讲你不应执行除法。然而在执行期间，计算机会尝试执行除法。如果 denominator 为 0，程序将终止，并给出错误消息，说明发生了非法操作。

第二条语句设计为仅当 hours 大于 0 且 rate 为正数且小于或等于 15.50 时才计算 wages。第三条语句设计为仅当 ch 为大写字母时才执行某些语句。

对于所有这些语句（就此而言，在任何情况下），如果条件不满足，那么以一条指明程序中错误发生位置的消息来暂停程序执行会很有用。你可以通过在程序中包含输出语句和 return 语句来处理这类情况。然而，C++ 通过 assert 函数提供了一种有效方法，在所需条件不满足时暂停程序。

使用 assert 函数的语法是：

```cpp
assert(expression);
```

这里，expression 是任意逻辑表达式。如果 expression 求值为 true，则执行下一条语句。如果 expression 求值为 false，则程序终止，并指出程序中错误发生的位置。

assert 函数的规范位于头文件 cassert 中。因此，程序要使用 assert 函数，必须包含以下语句：

```cpp
#include <cassert>
```

使用 assert 函数的语句有时称为 assert 语句。

回到前面的语句，你可以使用 assert 函数重写语句 1（quotient = numerator / denominator;）。因为仅当 denominator 非零时才应计算 quotient，所以你要在赋值语句之前包含一个 assert 语句，如下所示：

```cpp
assert(denominator);
quotient = numerator / denominator;
```

现在，如果 denominator 为 0，则 assert 语句会暂停程序执行，并给出类似以下的错误消息：

```text
Assertion failed: denominator, file c:\temp\assert
function\assertfunction.cpp, line 20
```

该错误消息表明对 denominator 的断言失败。错误消息还给出了包含源代码的文件名以及断言失败所在的行号。

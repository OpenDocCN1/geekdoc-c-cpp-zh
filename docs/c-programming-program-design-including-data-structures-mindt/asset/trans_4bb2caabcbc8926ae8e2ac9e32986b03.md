
```cpp
cout << endl;                                      //Line 8

switch(num)                                         //Line 9
{                                                   //Line 10
case 0:                                              //Line 11
case 1:                                              //Line 12
    cout << "Learning to use ";                    //Line 13
case 2:                                              //Line 14
    cout << "C++'s ";                              //Line 15
case 3:                                              //Line 16
    cout << "switch structure." << endl;           //Line 17
    break;                                          //Line 18
case 4:                                              //Line 19
    break;                                          //Line 20
case 5:                                              //Line 21
    cout << "This program shows the effect ";      //Line 22
case 6:                                              //Line 23
case 7:                                              //Line 24
    cout << "of the break statement." << endl;     //Line 25
    break;                                          //Line 26
default:                                             //Line 27
    cout << "The number is out of range." << endl; //Line 28
}                                                   //Line 29

cout << "Out of the switch structure." << endl;    //Line 30

return 0;                                           //Line 31
}                                                   //Line 32
```

**示例运行：** 这些输出是通过多次执行前面的程序得到的。在每次示例运行中，用户输入以底纹显示。

## 示例运行 1：

```
Enter an integer between 0 and 7: 0

Learning to use C++'s switch structure.
Out of the switch structure.
```

## 示例运行 2：

```
Enter an integer between 0 and 7: 2

C++'s switch structure.
Out of the switch structure.
```

## 示例运行 3：

```
Enter an integer between 0 and 7: 4

Out of the switch structure.
```

## 示例运行 4：

```
This program shows the effect of the break statement.
Out of the switch structure.
```

## 示例运行 5：

```
Enter an integer between 0 and 7: 7

of the break statement.
Out of the switch structure.
```

## 示例运行 6：

```
Enter an integer between 0 and 7: 8

The number is out of range.
Out of the switch structure.
```

使用 `switch` 表达式 `num` 的某些值来逐步讲解这个程序，可以帮助你理解 `break` 语句如何起作用。如果 `num` 的值为 0，则 `switch` 表达式的值与 `case` 值 0 匹配。`case 0:` 之后的所有语句都会执行，直到出现 `break` 语句。

第一个 `break` 语句出现在第 18 行，正好在 `case` 值 4 之前。即使 `switch` 表达式的值与 `case` 值 1、2 或 3 中的任何一个都不匹配，这些值之后的语句仍会执行。

当 `switch` 表达式的值与某个 `case` 值匹配时，所有语句都会执行，直到遇到 `break`，并且程序会跳过其间的所有 `case` 标签。同样，如果 `num` 的值为 3，它匹配 `case` 值 3，并且该标签之后的语句会执行，直到在第 18 行遇到 `break` 语句。如果 `num` 的值为 4，它匹配 `case` 值 4。在这种情况下，动作是空的，因为 `case` 值 4 之后只有第 20 行的 `break` 语句。

## 示例 4-24

尽管 `switch` 结构的 `case` 值（标签）是有限的，但 `switch` 语句的表达式可以按需要任意复杂。例如，考虑以下 `switch` 语句：

```cpp
switch (score / 10)
{
case 0:
case 1:
case 2:
case 3:
case 4:
case 5:
    grade = 'F';
    break;
}
```

这些值对应成绩 'F'。如果将全部 60 个值都列为 case 值，`switch` 语句可能会非常长。然而，除以 10 可将这 60 个值减少到只有 6 个值：0、1、2、3、4 和 5。

如果值的范围包含无限多个值，并且无法将它们缩减为包含有限个值的集合，则必须使用 `if...else` 结构。例如，如果 `score` 恰好是 `double` 变量，并且可能存在小数分数，那么 0 到 60 之间的值的数量是无限的。然而，你可以使用表达式 `static_cast<int>(score) / 10`，仍可将这无限多个值缩减为仅仅六个值。

## 通过避免一知半解的概念和技术来避免缺陷（重访）

在本章前面，我们讨论了对某个概念或技术的一知半解如何导致程序中的错误。在本节中，我们给出另一个示例，以说明使用一知半解的概念和技术所带来的问题。在示例 4-24 中，我们说明了如何根据 0 到 100 之间的考试分数评定成绩。接下来，考虑以下根据考试分数评定成绩的程序：

```cpp
//Grade program with bugs.

#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

int main()                                               //Line 3
{
    int testScore;                                       //Line 4
                                                         //Line 5
    cout << "Enter the test score: ";                   //Line 6
    cin >> testScore;                                    //Line 7
    cout << endl;                                        //Line 8

    switch (testScore / 10)                              //Line 9
    {                                                    //Line 10
    case 0:                                              //Line 11
    case 1:                                              //Line 12
    case 2:                                              //Line 13
    case 3:                                              //Line 14
    case 4:                                              //Line 15
    case 5:                                              //Line 16
        cout << "The grade is F." << endl;              //Line 17
    case 6:                                              //Line 18
        cout << "The grade is D." << endl;              //Line 19
    case 7:                                              //Line 20
        cout << "The grade is C." << endl;              //Line 21
    case 8:                                              //Line 22
        cout << "The grade is B." << endl;              //Line 23
```

我们再次可以看到，一知半解的概念可能导致程序中出现严重错误。因此，花时间彻底理解每个概念和技术，将为你节省数小时的调试时间。

## 使用 **assert** 函数终止程序

程序中可能会出现某些非常难以捕获的错误。例如，使用你到目前为止学过的任何编程技术，都可能难以捕获除零错误。C++ 包含一个预定义函数 **assert**，它在某些难以察觉的错误发生时停止程序执行方面很有用。在除零的情况下，你可以使用 **assert** 函数来确保程序终止时给出适当的错误消息，指出错误类型以及错误发生的程序位置。

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

在第一条语句中，如果 **分母** 为 0，从逻辑上讲不应执行除法。然而在执行期间，计算机仍会尝试执行除法。如果分母为 0，程序会停止，并给出错误消息，指出发生了非法操作。

第二条语句设计为仅在 hours 大于 0 且 rate 为正数且小于或等于 15.50 时才计算工资。第三条语句设计为仅当 ch 是大写字母时才执行某些语句。

对于所有这些语句（就此而言，在任何情况下），如果条件不满足，那么终止程序执行并给出消息指出程序中发生错误的位置，将会很有用。你可以通过在程序中包含输出语句和 return 语句来处理这类情况。然而，C++ 通过 **assert** 函数提供了一种有效方法，在所需条件不满足时终止程序。

使用 **assert** 函数的语法是：

```cpp
assert(expression);
```

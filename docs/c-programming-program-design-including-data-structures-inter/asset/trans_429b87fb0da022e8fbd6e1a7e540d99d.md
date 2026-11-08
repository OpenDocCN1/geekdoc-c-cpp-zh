
## 示例 4.1

考虑以下语句，其中 grade 是 char 类型的变量：

```cpp
switch (grade)
{
    case 'A':
        cout << "The grade point is 4.0.";
        break;
    case 'B':
        cout << "The grade point is 3.0.";
        break;
    case 'C':
        cout << "The grade point is 2.0.";
        break;
    case 'D':
        cout << "The grade point is 1.0.";
        break;
    case 'F':
        cout << "The grade point is 0.0.";
        break;
    default:
        cout << "The grade is invalid.";
}
```

在这个示例中，switch 语句中的表达式是一个变量标识符。变量 grade 的类型是 char，属于整型。grade 的可能值为 'A'、'B'、'C'、'D' 和 'F'。每个 case 标签指定一个不同的动作，具体取决于 grade 的值。如果 grade 的值为 'A'，则输出为：

成绩点是 4.0。

## 示例 4.2

下面的程序说明 break 语句的作用。它要求用户输入一个 0 到 10 之间的数。

```cpp
//Program: Effect of break statements in a switch structure

#include <iostream>

using namespace std;

int main()
{
    int num;

    cout << "Enter an integer between 0 and 7: ";    //Line 1
    cin >> num;                                      //Line 2
    cout << endl;                                    //Line 3
```

### 示例运行 4：

```text
Enter an integer between 0 and 7: 5
The number you entered is 5
This program shows the effect of the break statement.
Out of the switch structure.
```

### 示例运行 5：

```text
Enter an integer between 0 and 7: 7
The number you entered is 7
of the break statement.
Out of the switch structure.
```

### 示例运行 6：

```text
Enter an integer between 0 and 7: 8
The number you entered is 8
The number is out of range.
Out of the switch structure.
```

使用 switch 表达式 num 的某些值来逐步分析这个程序，可以帮助你理解 break 语句如何起作用。如果 num 的值为 0，则 switch 表达式的值与 case 值 0 匹配。case 0: 之后的所有语句都会执行，直到出现 break 语句。

第一个 break 语句出现在第 13 行，就在 case 值 4 之前。即使 switch 表达式的值不匹配任何 case 值（即 1、2 或 3），这些值后面的语句仍会执行。

当 switch 表达式的值与某个 case 值匹配时，会执行所有语句，直到遇到 break；程序会跳过其间的所有 case 标签。类似地，如果 num 的值为 3，则它与 case 值 3 匹配，此标签后面的语句会一直执行，直到在第 13 行遇到 break 语句。如果 num 的值为 4，则它与 case 值 4 匹配。在这种情况下，动作是空的，因为 case 值 4 后面只有第 15 行的一条 break 语句。

## 示例 4-23

尽管 switch 结构的 case 值（标签）有限，但 switch 语句的表达式可以按需要任意复杂。例如，考虑以下 switch 语句：

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
case 6:
    grade = 'D';
    break;
case 7:
    grade = 'C';
    break;
case 8:
    grade = 'B';
    break;
case 9:
case 10:
    grade = 'A';
    break;
default:
    cout << "Invalid test score." << endl;
}
```

假设 score 是一个 int 变量，取值在 0 到 100 之间。如果 score 为 75，则 score / 10 = 75 / 10 = 7，赋予的成绩为 'C'。如果 score 的值在 0 到 59 之间，则成绩为 'F'。如果 score 在 0 到 59 之间，那么 score / 10 为 0、1、2、3、4 或 5。这些值中的每一个都对应成绩 'F'。

因此，在这个 switch 结构中，case 0、case 1、case 2、case 3、case 4 和 case 5 的动作语句全都相同。不必为 case 值 0、1、2、3、4 和 5 分别写出语句 `grade = 'F';` 及其后的 break 语句，你可以先指定所有 case 值（如前面的代码所示），再指定所需的动作语句，从而简化程序代码。case 值 9 和 10 也遵循类似的约定。

除了可以是变量标识符或复杂表达式之外，switch 表达式还可以求值为逻辑值。考虑以下语句：

```cpp
switch (age >= 18)
{
case 1:
    cout << "Old enough to be drafted." << endl;
    cout << "Old enough to vote." << endl;
    break;
case 0:
    cout << "Not old enough to be drafted." << endl;
    cout << "Not old enough to vote." << endl;
}
```

如果 age 的值为 25，则表达式 age >= 18 求值为 1——即 true。如果表达式求值为 1，则 case 标签 1 后面的语句会执行。如果 age 的值为 14，则表达式 age >= 18 求值为 0——即 false——并且 case 标签 0 后面的语句会执行。

你可以在 case 标签中分别使用 true 和 false 代替 1 和 0，并将前面的 switch 语句重写如下：

```cpp
switch (age >= 18)
{
case true:
    cout << "Old enough to be drafted." << endl;
    cout << "Old enough to vote." << endl;
    break;
case false:
    cout << "Not old enough to be drafted." << endl;
    cout << "Not old enough to vote." << endl;
}
```

从前面的示例可以看出，switch 语句是实现多重选择的一种优雅方式。你将在本章末尾的编程示例中看到 switch 语句的使用。尽管没有固定规则可用于决定是使用 if...else 结构还是 switch 结构来实现多重选择，但应记住以下考虑因素。如果多重选择涉及一个值范围，则应使用 if...else 结构或 switch 结构，并将每个范围转换为有限的值集合。

例如，在示例 4-23 中，grade 的值取决于 score 的值。如果 score 在 0 到 59 之间，则 grade 为 'F'。因为 score 是 int 变量，所以有 60 个值对应成绩 'F'。如果你将所有 60 个值都列为 case 值，switch 语句可能会非常长。然而，除以 10 可将这 60 个值减少为仅 6 个值：0、1、2、3、4 和 5。

如果值范围包含无限多个值，并且无法将它们缩减为包含有限个值的集合，则必须使用 if...else 结构。例如，如果 score 恰好是 double 变量，则 0 到 60 之间的值有无限多个。然而，你可以使用表达式 static_cast<int>(score) / 10，仍然将这个无限多的值缩减为仅六个值。

## 避免因对概念和技术一知半解而引发错误（再论）

本章前面讨论了概念或技术的一知半解如何导致程序错误。在本节中，我们给出另一个示例来说明使用一知半解的概念和技术所带来的问题。在示例 4-23 中，我们说明了如何根据 0 到 100 之间的测试分数来赋予成绩。接下来，考虑下面这个根据测试分数赋予成绩的程序：

```cpp
//Grade program with bugs.

#include <iostream>                                      //Line 1

using namespace std;                                    //Line 2

int main()                                      //Line 3
{                                               //Line 4
    int testScore;                              //Line 5

    cout << "Enter the test score: ";          //Line 6
    cin >> testScore;                           //Line 7
    cout << endl;                               //Line 8

    switch (testScore / 10)                     //Line 9
    {                                           //Line 10
    case 0:                                     //Line 11
    case 1:                                     //Line 12
    case 2:                                     //Line 13
    case 3:                                     //Line 14
    case 4:                                     //Line 15
    case 5:                                     //Line 16
        cout << "The grade is F." << endl;     //Line 17
    case 6:                                     //Line 18
        cout << "The grade is D." << endl;     //Line 19
    case 7:                                     //Line 20
        cout << "The grade is C." << endl;     //Line 21
    case 8:                                     //Line 22
        cout << "The grade is B." << endl;     //Line 23
    case 9:                                     //Line 24
    case 10:                                    //Line 25
        cout << "The grade is A." << endl;     //Line 26
    default:                                    //Line 27
        cout << "Invalid test score." << endl; //Line 28
    }                                           //Line 29

    return 0;                                   //Line 30
}                                               //Line 31
```

**示例运行：** 在这些示例运行中，用户输入以底纹显示。

**示例运行 1：**

输入测试分数：`110`

无效的测试分数。

**示例运行 2：**

输入测试分数：`70`

无效的测试分数。

**示例运行 3：**

输入测试分数：`75`

成绩为 C。
成绩为 B。
成绩为 A。
无效的测试分数。


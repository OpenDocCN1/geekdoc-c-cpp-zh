

除了读取无效数据外，还有其他事件会导致输入流进入失败状态。导致输入失败的另外两个常见原因是：

- 尝试打开一个不存在的输入文件
- 尝试读取输入文件中超出末尾的数据

解决这些输入失败原因的一种方法是检查输入流变量的状态。你可以通过将输入流变量用作 `if` 语句中的逻辑表达式来检查其状态。如果最后一次输入成功，输入流变量的值为 `true`；如果最后一次输入失败，其值为 `false`。

语句：

```cpp
if (cin)
    cout << "Input is OK." << endl;
```

如果来自标准输入设备的最后一次输入成功，则输出：

```
Input is OK.
```

类似地，如果 `infile` 是一个 `ifstream` 变量，则语句：

```cpp
if (!infile)
    cout << "Input failed." << endl;
```

如果与流变量 `infile` 相关联的最后一次输入失败，则输出：

```
Input failed.
```

假设某个输入流变量试图打开一个文件以向程序输入数据。如果输入文件不存在，你可以将输入流变量的值与 `return` 语句结合使用来终止程序。

回想一下，函数 `main` 中的最后一条语句是：

```
return 0;
```

当程序终止时，这条语句向操作系统返回一个值 0。值 0 表示程序正常终止，并且在程序执行期间没有发生错误。除了 0 以外的 `int` 类型的值也可以通过 `return` 语句返回给操作系统。但是，返回任何非 0 的值都表示程序执行期间出现了问题。

`return` 语句可以出现在程序的任何位置。每当执行 `return` 语句时，它会立即退出其所在的函数。对于函数 `main` 而言，当执行 `return` 语句时程序即终止。你可以利用 `return` 语句的这些特性，在输入流进入失败状态时终止函数 `main`。当程序试图打开一个输入文件时，这种技术尤其有用。请考虑以下语句：

```cpp
ifstream infile;
infile.open("inputdat.dat");   // 打开 inputdat.dat

if (!infile)
{
    cout << "Cannot open the input file. "
         << "The program terminates." << endl;
    return 1;
}
```

假设文件 `inputdat.dat` 不存在。打开该文件的操作失败，导致输入流进入失败状态。作为逻辑表达式，文件流变量 `infile` 此时求值为 `false`。由于 `infile` 求值为 `false`，表达式 `!infile`（在 `if` 语句中）的值变为 `true`，因此执行 `if` 语句体。屏幕上会打印消息：

Cannot open the input file. The program terminates.

然后 `return` 语句将值 1 返回给操作系统，从而终止程序。

现在，让我们在“编程示例：第 3 章的学生成绩”中加入这些响应输入失败的代码。回忆一下，该程序根据输入文件中的数据计算平均测试分数，然后将结果输出到另一个文件。下面的编程代码与第 3 章的代码相同，只是增加了在输入文件不存在时退出程序的语句。

```cpp
//Program to calculate the average test score.

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>
using namespace std;

int main()
{
    ifstream inFile;    //input file stream variable
    ofstream outFile;   //output file stream variable

    double test1, test2, test3, test4, test5;
    double average;

    string firstName;
    string lastName;

    inFile.open("test.txt"); //open the input file

    if (!inFile)
    {
        cout << "Cannot open the input file. "
             << "The program terminates." << endl;
        return 1;
    }
    outFile.open("testavg.out");  // open the output file

    outFile << fixed << showpoint;
    outFile << setprecision(2);

    cout << "Processing data" << endl;

    inFile >> firstName >> lastName;
    outFile << "Student name: " << firstName
            << " " << lastName << endl;

    inFile >> test1 >> test2 >> test3
           >> test4 >> test5;
    outFile << "Test scores: " << setw(4) << test1
            << setw(4) << test2 << setw(4) << test3
            << setw(4) << test4 << setw(4) << test5
            << endl;

    average = (test1 + test2 + test3 + test4 + test5) / 5.0;

    outFile << "Average test score: " << setw(6)
            << average << endl;

    inFile.close();
    outFile.close();

    return 0;
}
```

## 混淆相等运算符（==）与赋值运算符（=）

回想一下，如果 `if` 语句中的判断表达式求值为 `true`，则会执行 `if` 语句的语句部分。此外，该表达式通常是一个逻辑表达式。然而，C++ 允许你使用任何可以求值为 `true` 或 `false` 的表达式作为 `if` 语句中的表达式。请考虑以下语句：

```cpp
if (x = 5)
    cout << "The value is five." << endl;
```

`if` 语句中的表达式——即判断条件——是 `x = 5`。表达式 `x = 5` 被称为**赋值表达式**，因为运算符 `=` 出现在表达式中，且末尾没有分号。

该表达式的求值过程如下。首先，求运算符 `=` 右侧的值，结果为 5。然后将值 5 赋给 `x`。而且，值 5——即

将表达式 `y + z` 的值赋给 `x`。而语句：

```
x == y + z;
```

比较表达式 `y + z` 的值与 `x` 的值；但 `x` 的值保持不变。如果在程序的其它地方你依赖于 `x` 的值等于 `y + z`，则会发生逻辑错误，程序输出将是错误的，而且你不会从编译器那里收到任何关于这种情况的警告。编译器只提供关于语法错误的反馈，而不是逻辑错误。因此，在使用相等运算符和赋值运算符时必须格外小心。

## 条件运算符（?:）

> **注意** 读者可以跳过本节，不会影响学习的连续性。

某些 `if...else` 语句可以通过使用 C++ 的条件运算符来编写得更简洁。**条件运算符**写作 `?:`，是一个**三元运算符**，这意味着它接受三个参数。使用条件运算符的语法是：

```
expression1 ? expression2 : expression3
```

这种类型的语句被称为**条件表达式**。条件表达式的求值方式如下：如果 expression1 的值为非零整数（即 `true`），则条件表达式的结果是 expression2；否则，条件表达式的结果是 expression3。

请考虑以下语句：

```cpp
if (a >= b)
    max = a;
else
    max = b;
```

你可以使用条件运算符将这条 `if...else` 语句简化书写为：

```cpp
max = (a >= b) ? a : b;
```

## 程序风格与格式（再讨论）：缩进

在第 2 章的“程序风格与格式”一节中，我们给出了一些编写程序的指导准则。既然我们已经开始讨论控制结构，在本节中，我们将给出一些正确缩进程序的通用指导准则。

当你编写程序时，拼写错误和逻辑错误是不可避免的。如果你的程序缩进得当，你就能快速发现并修复错误，本章中的几个示例就说明了这一点。通常情况下，你使用的 IDE 会自动缩进你的程序。如果由于某种原因你的 IDE 没有缩进程序，你可以自己缩进程序。

正确的缩进可以显示语句的自然分组。你应该在自然分离的语句之间插入一个空行。在本书中，花括号内的语句、选择结构的语句以及 `if` 语句内的 `if` 语句都向右缩进四个空格。在整本书中，我们使用四个空格来缩进语句，尤其是为了显示控制结构嵌套在其它控制结构中的层级。你也可以使用四个空格进行缩进。

放置花括号有两种常用的风格。在本书中，我们将花括号单独放在一行上。同时，匹配的左、右花括号位于同一列，即它们距离程序左边缘的空格数相同。这种放置花括号的风格可以轻松显示语句的分组，并且能使左右花括号匹配。你也可以采用这种风格来放置和缩进花括号。

在第二种放置花括号的风格中，左花括号不必单独占一行。通常，对于控制结构，左花括号放在（逻辑）表达式的最后一个右括号后面，而右花括号单独占一行。这种风格可能会节省一些空间。然而，有时这种风格可能无法立即显示语句的分组或块。

无论你使用什么缩进风格，你都应该在程序中保持一致性，并且缩进应该显示程序的结构。

## 使用伪代码开发、测试和调试程序

开发程序的方法有多种。一种方法涉及使用 C++ 和自然语言的非正式混合体，称为**伪代码**或简称为 **pseudo**。有时伪代码在将程序放入正式的 C++ 代码之前，为勾勒和细化程序提供了一种有用的手段。当你构建涉及复杂嵌套控制结构的程序时，伪代码可以帮助你快速开发出正确的程序结构，并避免犯常见错误。

一个有用的程序片段确定两个整数中较大的一个。如果 `x` 和 `y` 是整数，使用伪代码，你可以快速编写以下内容：

- a. `if (x > y) then`  
  `x is larger`
- b. `if (y > x) then`  
  `y is larger`


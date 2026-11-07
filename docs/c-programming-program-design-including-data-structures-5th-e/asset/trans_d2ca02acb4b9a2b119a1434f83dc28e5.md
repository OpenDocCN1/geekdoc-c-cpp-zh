

```cpp
if (gpa >= 2.0)
{
    if (gpa >= 3.9)
        cout << "Dean's Honor List." << endl;        //Line 9
}                                                   //Line 10
    else                                            //Line 11
        cout << "The GPA is below the graduation "  //Line 12
             << "requirement. \nSee your "           //Line 13
             << "academic advisor." << endl;         //Line 14
                                                    //Line 15
    return 0;                                       //Line 16
}                                                   //Line 17
```

**示例运行：** 在这些示例运行中，用户输入以底纹显示。

**示例运行 1：**

输入 GPA：`3.91`

院长荣誉名单。

**示例运行 2：**

输入 GPA：`3.8`

**示例运行 3：**

输入 GPA：`1.95`

GPA 低于毕业要求。
请咨询你的学业顾问。

在此类情况下，一般规则是：不能查看块内部（也就是花括号内部）来将 `else` 与 `if` 配对。第 14 行的 `else` 不能与第 11 行的 `if` 配对，因为第 11 行的 `if` 语句被包含在花括号内，而第 14 行的 `else` 不能查看这些花括号内部。因此，第 14 行的 `else` 与第 9 行的 `if` 配对。

本书按照逻辑顺序介绍 C++ 编程概念和技术。当这些概念和技术按照逻辑顺序逐一学习时，它们足够简单，可以完全理解。在使用某个概念或技术之前完全理解它，将为你节省大量调试时间。

### 输入失败与 `if` 语句

在第 3 章中，你已经看到，尝试读取无效数据会导致输入流进入失败状态。一旦输入流进入失败状态，与该输入流关联的所有后续输入语句都会被忽略，而计算机会继续执行程序，从而产生错误结果。你可以使用 `if` 语句检查输入流变量的状态，并且如果输入流进入失败状态，就加入停止程序执行的指令。

除了读取无效数据之外，其他事件也可能导致输入流进入失败状态。另外两个常见的输入失败原因如下：

- 尝试打开不存在的输入文件
- 尝试读取超过输入文件末尾的内容

处理这些输入失败原因的一种方法是检查输入流变量的状态。你可以将输入流变量用作 `if` 语句中的逻辑表达式来检查状态。如果上一次输入成功，输入流变量的求值结果为 `true`；如果上一次输入失败，则求值结果为 `false`。

以下语句：

```cpp
if (cin)
    cout << "Input is OK." << endl;
```

会输出：

```
Input is OK.
```

如果来自标准输入设备的上一次输入成功。类似地，如果 `infile` 是一个 `ifstream` 变量，那么以下语句：

```cpp
if (!infile)
    cout << "Input failed." << endl;
```

会输出：

```
Input failed.
```

如果与流变量 `infile` 关联的上一次输入失败。

假设一个输入流变量尝试打开文件，以便将数据输入到程序中。如果输入文件不存在，你可以结合 `return` 语句使用该输入流变量的值来终止程序。

回想一下，函数 `main` 中包含的最后一条语句是：

```cpp
return 0;
```

当程序终止时，这条语句会向操作系统返回 0。值 0 表示程序正常终止，并且程序执行期间没有发生错误。也可以通过 `return` 语句向操作系统返回 `int` 类型的非 0 值。然而，返回任何非 0 值都表示程序执行期间出了问题。

`return` 语句可以出现在程序中的任何位置。每当执行 `return` 语句时，它都会立即退出所在的函数。对于函数 `main` 来说，当 `return` 语句执行时，程序就会终止。你可以利用 `return` 语句的这些特性，在输入流失败时终止函数 `main`。当程序尝试打开输入文件时，这种技术尤其有用。考虑以下语句：

```cpp
ifstream infile;

infile.open("inputdat.dat");  //open inputdat.dat

if (!infile)
{
    cout << "Cannot open the input file. "
         << "The program terminates." << endl;
    return 1;
}
```

假设文件 inputdat.dat 不存在。打开该文件的操作失败，导致输入流进入失败状态。作为逻辑表达式，文件流变量 infile 随后求值为 false。因为 infile 求值为 false，所以表达式 !infile（在 if 语句中）求值为 true，并执行 if 语句体。消息：

```
Cannot open the input file. The program terminates.
```

会打印到屏幕上，而 return 语句通过向操作系统返回值 1 来终止程序。

现在，让我们使用响应输入失败的代码，把这些特性加入第 3 章的编程示例：学生成绩中。回想一下，该程序根据输入文件中的数据计算平均测试成绩，然后将结果输出到另一个文件。下面的编程代码与第 3 章中的代码相同，不同之处在于它包含在输入文件不存在时退出程序的语句。

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

    outFile.open("testavg.out");  //open the output file

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

### 相等运算符（==）与赋值运算符（=）的混淆

回想一下，如果 `if` 语句中的决策表达式求值为 `true`，则执行 `if` 语句的语句部分。此外，该表达式通常是逻辑表达式。然而，C++ 允许你将任何可求值为 `true` 或 `false` 的表达式用作 `if` 语句中的表达式。考虑以下语句：

```cpp
if (x = 5)
    cout << "The value is five." << endl;
```

`if` 语句中的表达式——也就是决策条件——是 `x = 5`。表达式 `x = 5` 被称为赋值表达式，因为表达式中出现了运算符 `=`，而且末尾没有分号。

该表达式的求值过程如下。首先，对运算符 `=` 的右侧求值，结果为 5。然后，将值 5 赋给 x。此外，值 5——也就是，

![](img/f97f778697507bb6fdd80c5991210cba_250_0.png)


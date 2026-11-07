
解决问题所采用的方法必须正确使用概念和技术；否则，你的解决方案要么不正确，要么有缺陷。使用一知半解的概念和技术所导致的问题，可以通过下面的程序来说明。

假设我们要编写一个分析学生 GPA 的程序。如果 GPA 大于或等于 3.9，该学生进入院长荣誉名单。如果 GPA 小于 2.00，则向该学生发送一封警告信，说明其 GPA 低于毕业要求。因此，考虑下面的程序：

```cpp
//GPA program with bugs.

#include <iostream>                         //line 1

using namespace std;                         //line 2

int main()                                   //line 3
{
    double gpa;                               //line 5

    cout << "Enter the GPA: ";               //line 6
    cin >> gpa;                               //line 7
    cout << endl;                              //line 8

    if (gpa >= 2.0)                            //line 9
        if (gpa >= 3.9)                        //line 10
            cout << "Dean's Honor List." << endl;  //line 11
        else                                  //line 12
            cout << "The GPA is below the graduation "
                 << " requirement. \nSee your "
                 << "academic advisor." << endl;     //line 13

    return 0;                                  //line 14
}                                             //line 15
```

**示例运行：** 在这些示例运行中，用户输入以底纹显示。

**示例运行 1：**

Enter the GPA: `3.91`

Dean's Honor List.

**示例运行 2：**

Enter the GPA: `3.8`

The GPA is below the graduation requirement.  
See your academic advisor.

**示例运行 3：**

Enter the GPA: `1.95`

让我们看看这些示例运行。显然，示例运行 1 中的输出是正确的。在示例运行 2 中，输入为 3.8，输出表明该 GPA 低于毕业要求。然而，GPA 为 3.8 的学生毕业时会获得某种荣誉。因此，示例运行 2 中的输出不正确。在示例运行 3 中，输入为 1.95，而输出没有显示任何警告信息。因此，示例运行 3 中的输出也不正确。这意味着第 9 行到第 13 行的 `if...else` 语句不正确。让我们看看这些语句，即：

```cpp
if (gpa >= 2.0)                                      //Line 9
    if (gpa >= 3.9)                                  //Line 10
        cout << "Dean's Honor List." << endl;        //Line 11
else                                                //Line 12
    cout << "The GPA is below the graduation "
         << "requirement. \nSee your "
         << "academic advisor." << endl;             //Line 13
```

按照将 `else` 与 `if` 配对的原则，第 12 行的 `else` 与第 10 行的 `if` 配对。换句话说，使用正确的缩进，代码为：

```cpp
if (gpa >= 2.0)                                      //Line 9
    if (gpa >= 3.9)                                  //Line 10
        cout << "Dean's Honor List." << endl;        //Line 11
    else                                            //Line 12
        cout << "The GPA is below the graduation "
             << "requirement. \nSee your "
             << "academic advisor." << endl;         //Line 13
```

现在我们可以看到，第 9 行的 `if` 语句是单向选择。因此，如果输入的数字小于 2.0，将不会执行任何操作，也就是说，不会打印警告信息。现在，假设输入为 3.8。那么，第 9 行的表达式求值为 `true`，因此第 10 行的表达式会被求值，其结果为 `false`。这意味着第 13 行的输出语句会执行，从而导致不令人满意的结果。

事实上，程序只应在 GPA 小于 2.0 时打印警告信息，并且应在 GPA 大于或等于 3.9 时打印以下消息：

Dean's Honor List.

为了实现该结果，第 12 行的 `else` 需要与第 9 行的 `if` 配对。要将第 12 行的 `else` 与第 9 行的 `if` 配对，需要使用复合语句，如下所示：

```cpp
if (gpa >= 2.0)                                      //Line 9
{
    if (gpa >= 3.9)                                  //Line 10
        cout << "Dean's Honor List." << endl;        //Line 11
}
else                                                //Line 12
    cout << "The GPA is below the graduation "
         << "requirement. \nSee your "
         << "academic advisor." << endl;             //Line 13
```

正确的程序如下：

```cpp
//Correct GPA program.

#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

int main()                                               //Line 3
{                                                        //Line 4
    double gpa;                                           //Line 5

    cout << "Enter the GPA: ";                           //Line 6
    cin >> gpa;                                           //Line 7
    cout << endl;                                         //Line 8

    if (gpa >= 2.0)                                       //Line 9
    {                                                    //Line 10
        if (gpa >= 3.9)                                   //Line 11
            cout << "Dean's Honor List." << endl;        //Line 12
    }                                                    //Line 13
    else                                                 //Line 14
        cout << "The GPA is below the graduation "
             << "requirement. \nSee your "
             << "academic advisor." << endl;             //Line 15

    return 0;                                             //Line 16
}                                                        //Line 17
```

**示例运行：** 在这些示例运行中，用户输入以底纹显示。

**示例运行 1：**

Enter the GPA: `3.91`

Dean's Honor List.

**示例运行 2：**

Enter the GPA: `3.8`

**示例运行 3：**

Enter the GPA: `1.95`

The GPA is below the graduation requirement.  
See your academic advisor.

在此类情况下，一般规则是：不能查看块内部（即花括号内部）来将 else 与 if 配对。第 14 行的 else 不能与第 11 行的 if 配对，因为第 11 行的 if 语句被包含在花括号中，而第 14 行的 else 不能查看这些花括号内部。因此，第 14 行的 else 与第 9 行的 if 配对。

在本书中，C++ 编程概念和技术按逻辑顺序呈现。在使用某个概念或技术之前完全理解它，将为你节省大量调试时间。

## 输入失败与 `if` 语句

在第 3 章中，你已经看到，尝试读取无效数据会导致输入流进入失败状态。一旦输入流进入失败状态，与该输入流关联的所有后续输入语句都会被忽略，而计算机会继续执行程序，从而产生错误的结果。你可以使用 `if` 语句检查输入流变量的状态；如果输入流进入失败状态，可以加入停止程序执行的指令。

除了读取无效数据之外，其他事件也可能导致输入流进入失败状态。另外两个常见的输入失败原因如下：

- 尝试打开不存在的输入文件
- 尝试读取超出输入文件末尾的内容

![](img/d0be7fc6d804b63484835c6c8bc67a07_267_0.png)

处理这些输入失败原因的一种方法是检查输入流变量的状态。你可以将输入流变量用作 `if` 语句中的逻辑表达式来检查状态。如果上一次输入成功，该输入流变量求值为 `true`；如果上一次输入失败，则求值为 `false`。

语句：

```cpp
if (cin)
    cout << "Input is OK." << endl;
```

如果来自标准输入设备的上一次输入成功，则打印：

Input is OK.

类似地，如果 `infile` 是 ifstream 变量，则语句：

```cpp
if (!infile)
    cout << "Input failed." << endl;
```

如果与流变量 `infile` 关联的上一次输入失败，则打印：

Input failed.

假设一个输入流变量尝试打开文件以将数据输入程序。如果输入文件不存在，你可以结合 `return` 语句使用该输入流变量的值来终止程序。

回顾一下，函数 main 中包含的最后一条语句是：

```cpp
return 0;
```

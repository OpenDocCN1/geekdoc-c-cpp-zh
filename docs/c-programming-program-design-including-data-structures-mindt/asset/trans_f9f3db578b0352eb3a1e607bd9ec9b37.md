

```cpp
else                                      //第12行
    cout << "The GPA is below the graduation "
         << "requirement. \nSee your "
         << "academic advisor." << endl;    //第13行
```

按照 `else` 与 `if` 配对的原则，第12行的 `else` 与第10行的 `if` 配对。换句话说，使用正确的缩进后，代码如下：

```cpp
if (gpa >= 2.0)                         //第9行
    if (gpa >= 3.9)                      //第10行
        cout << "Dean's Honor List." << endl;  //第11行
    else                                 //第12行
        cout << "The GPA is below the graduation "
             << "requirement. \nSee your "
             << "academic advisor." << endl;     //第13行
```

现在我们可以看到，第9行的 `if` 语句是一个单分支选择。因此，如果输入的数字小于2.0，不会发生任何操作，也就是说，不会打印任何警告信息。现在，假设输入是3.8。那么第9行的表达式计算结果为 `true`，因此会继续计算第10行的表达式，其计算结果为 `false`。这意味着第13行的输出语句会执行，从而产生不令人满意的结果。

实际上，程序只应在 GPA 小于2.0时打印警告信息，并且当 GPA 大于或等于3.9时，应打印以下信息：

Dean's Honor List.

为了达到这个结果，第12行的 `else` 需要与第9行的 `if` 配对。要将第12行的 `else` 与第9行的 `if` 配对，需要使用复合语句，如下所示：

```cpp
if (gpa >= 2.0)                         //第9行
{
    if (gpa >= 3.9)                      //第10行
        cout << "Dean's Honor List." << endl;  //第11行
}                                        //第12行
else
    cout << "The GPA is below the graduation "
         << "requirement. \nSee your "
         << "academic advisor." << endl;    //第13行
```

正确的程序如下：

```cpp
//正确的GPA程序。

#include <iostream>                     //第1行

using namespace std;                    //第2行

int main()                                //第3行
{
    double gpa;                           //第5行

    cout << "Enter the GPA: ";        //第6行
    cin >> gpa;                         //第7行
    cout << endl;                       //第8行

    if (gpa >= 2.0)                     //第9行
    {
        if (gpa >= 3.9)                 //第11行
            cout << "Dean's Honor List." << endl; //第12行
    }
    else                                //第14行
        cout << "The GPA is below the graduation "
             << "requirement. \nSee your "
             << "academic advisor." << endl;        //第15行

    return 0;                           //第16行
}                                   //第17行
```

**示例运行：** 在这些示例运行中，用户输入以阴影显示。

### 示例运行1：

```cpp
Enter the GPA: 3.91
Dean's Honor List.
```

### 示例运行2：

```cpp
Enter the GPA: 3.8
```

### 示例运行3：

```cpp
Enter the GPA: 1.95
The GPA is below the graduation requirement.
See your academic advisor.
```

在这种情况下，一般规则是：你不能查看块内部（即花括号内部）来将 `else` 与 `if` 配对。第14行的 `else` 不能与第11行的 `if` 配对，因为第11行的 `if` 语句被花括号括起来，而第14行的 `else` 不能查看这些花括号内部。因此，第14行的 `else` 与第9行的 `if` 配对。

在本书中，C++编程概念和技术按逻辑顺序呈现。在使用某个概念或技术之前完全理解它，将为你节省大量的调试时间。

## 输入失败与 `if` 语句

在第3章中，你了解到尝试读取无效数据会导致输入流进入失败状态。一旦输入流进入失败状态，所有与该输入流相关的后续输入语句都会被忽略，计算机继续执行程序，从而产生错误结果。你可以使用 `if` 语句来检查输入流变量的状态，如果输入流进入失败状态，则包含停止程序执行的指令。

除了读取无效数据之外，其他事件也可能导致输入流进入失败状态。另外两个常见的输入失败原因是：

- 尝试打开不存在的输入文件
- 尝试读取超过输入文件末尾的数据

解决输入失败原因的一种方法是检查输入流变量的状态。你可以通过在 `if` 语句中将输入流变量作为逻辑表达式来检查其状态。如果最后一次输入成功，输入流变量的计算结果为 `true`；如果最后一次输入失败，其计算结果为 `false`。

语句：

```cpp
if (cin)
    cout << "Input is OK." << endl;
```

如果标准输入设备的最后一次输入成功，则打印：

```cpp
Input is OK.
```

类似地，如果 `infile` 是一个 ifstream 变量，语句：

```cpp
if (!infile)
    cout << "Input failed." << endl;
```

如果与流变量 `infile` 相关的最后一次输入失败，则打印：

```cpp
Input failed.
```

假设一个输入流变量尝试打开一个文件以将数据输入到程序中。如果输入文件不存在，你可以使用输入流变量的值，结合 `return` 语句来终止程序。

回想一下，函数 `main` 中包含的最后一条语句是：

```cpp
return 0;
```

当程序终止时，该语句向操作系统返回一个值0。值0表示程序正常终止，并且在程序执行期间没有发生错误。除0以外的 `int` 类型值也可以通过 `return` 语句返回给操作系统。但是，返回任何非0值都表示程序执行期间出现了问题。

`return` 语句可以出现在程序中的任何位置。每当执行 `return` 语句时，它会立即退出该语句所在的函数。对于函数 `main`，当 `return` 语句执行时，程序终止。你可以利用 `return` 语句的这些特性，在输入流失败时终止函数 `main`。当程序尝试打开输入文件时，这种技术尤其有用。请考虑以下语句：

```cpp
ifstream infile;

infile.open("inputdat.dat");    //打开文件 inputdat.dat

if (!infile)
{
    cout << "Cannot open the input file. "
         << "The program terminates." << endl;
    return 1;
}
```

假设文件 `inputdat.dat` 不存在。打开该文件的操作失败，导致输入流进入失败状态。作为逻辑表达式，文件流变量 `infile` 的计算结果为 `false`。由于 `infile` 的计算结果为 `false`，表达式 `!infile`（在 `if` 语句中）的计算结果为 `true`，因此 `if` 语句的主体执行。屏幕会打印以下信息：

Cannot open the input file. The program terminates.

然后 `return` 语句通过向操作系统返回值 `1` 来终止程序。

现在，让我们在第3章的 *编程示例：学生成绩* 中包含这些功能，使用响应输入失败的代码。回想一下，该程序根据输入文件中的数据计算平均测试分数，然后将结果输出到另一个文件。以下编程代码与第3章中的代码相同，不同之处在于它包含了一旦输入文件不存在就退出程序的语句。

```cpp
//计算平均测试分数的程序。

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;

int main()
{
    ifstream inFile;    //输入文件流变量
    ofstream outFile;   //输出文件流变量

    double test1, test2, test3, test4, test5;
    double average;

    string firstName;
    string lastName;
```


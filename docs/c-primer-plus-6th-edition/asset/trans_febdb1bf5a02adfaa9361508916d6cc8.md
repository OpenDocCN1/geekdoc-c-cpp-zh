

## 294 第 6 章 分支语句与逻辑运算符

你可以这样使用这些对象：

```cpp
double wt;
inFile >> wt; // 从 bowling.txt 读取一个数字
char line[81];
fin.getline(line, 81); // 读取一行文本
```

重要的一点是，在你声明了一个 `ifstream` 对象并将其与文件关联后，你可以完全像使用 `cin` 一样使用它。所有适用于 `cin` 的可用操作和方法也适用于 `ifstream` 对象，例如前面示例中的 `inFile` 和 `fin`。

如果尝试打开一个不存在的文件进行输入会发生什么？此错误会导致后续使用 `ifstream` 进行输入的尝试失败。检查文件是否成功打开的首选方法是使用 `is_open()` 方法。你可以使用如下代码：

```cpp
inFile.open("bowling.txt");
if (!inFile.is_open())
    exit(EXIT_FAILURE);
```

如果文件成功打开，`is_open()` 方法返回 `true`，因此如果尝试失败，表达式 `!inFile.is_open()` 则为 `true`。`exit()` 函数在 `cstdlib` 头文件中定义，该头文件还定义了 `EXIT_FAILURE` 作为用于与操作系统通信的参数。`exit()` 函数会终止程序。

`is_open()` 方法对于 C++ 来说较新。如果你的编译器不支持它，你可以使用旧的 `good()` 方法。正如第 17 章讨论，`good()` 对可能问题的检查没有 `is_open()` 那么详尽。

列表 6.16 中的程序打开用户指定的文件，从文件中读取数字并报告它们的总和及平均值。正确设计输入循环至关重要，接下来的“程序说明”部分将详细讨论这一点。请注意，该程序极大受益于语句的使用。

## 列表 6.16 sumfile.cpp

```cpp
// sumfile.cpp -- 带有数组参数的函数
#include <iostream>
#include <fstream>
#include <cstdlib>      // 文件 I/O 支持
                      // exit() 支持
const int SIZE = 60;
int main() {
    using namespace std;
    char filename[SIZE];
    ifstream inFile;      // 处理文件输入的对象

    cout << "Enter name of data file: ";
    cin.getline(filename, SIZE);
    inFile.open(filename); // 将 inFile 与文件关联
    if (!inFile.is_open()) // 打开文件失败
    {
        cout << "Could not open the file " << filename << " " << endl;
        cout << "Program terminating.\n";
        exit(EXIT_FAILURE);
    }
    double value;
    double sum = 0.0;
    int count = 0; // 读取的项数

    inFile >> value; // 获取第一个值
    while (inFile.good()) // 当输入状态良好且未到文件末尾时
    {
        count++;
        sum += value; // 计算运行总和
        inFile >> value; // 获取下一个值
    }
    if (inFile.eof())
        cout << "End of file reached.\n";
    else if (inFile.fail())
        cout << "Input terminated by data mismatch.\n";
    else
        cout << "Input terminated for unknown reason.\n";
    if (count == 0)
        cout << "No data processed.\n";
    else
    {
        cout << "Items read: " << count << endl;
        cout << "Sum: " << sum << endl;
        cout << "Average: " << sum / count << endl;
    }
    inFile.close(); // 完成文件处理
    return 0;
}
return 0;
```

要使用列表 6.16 中的程序，你必须先创建一个包含数字的文本文件。你可以使用文本编辑器（例如你编写源码时使用的编辑器）来创建此文件。假设文件名为 `scores.txt` 且内容如下：

18 19 18.5 13.5 14
16 19.5 20 18 12 18.5
17.5

程序必须能够找到该文件。通常情况下，除非你的输入包含文件路径，否则程序将在包含可执行文件的相同文件夹或目录中查找。

> 注意
> Windows 文本文件使用回车符紧随换行符来结束一行文本。（通常的 C++ 文本在读取文件时会将此组合转换为换行符，并在写入文件时反转该转换。）某些文本编辑器（如 Metroworks CodeWarrior IDE 编辑器）不会在最后一行自动添加此组合。因此，如果你使用此类编辑器，需要在退出文件前输入最后一次编辑时按下 Enter 键。

以下是列表 6.16 程序的示例运行：

+ Enter name of data file: `scores.txt`
End of file reached.
Items read: 12
Sum: 204.5
Average: 17.0417

## 程序说明

列表 6.16 中的程序没有硬编码文件名，而是将用户提供的名称存储在字符数组 `filename` 中。然后该数组被作为 `open()` 的参数使用：`inFile.open(filename);`

正如本章早期讨论的那样，测试打开文件的尝试是否成功至关重要。以下是一些可能出现的问题：
- 文件可能不存在。
- 程序可能没有读取该文件的权限。
- 文件可能损坏。
- 输入可能包含非数字数据。
- 文件可能意外结束。


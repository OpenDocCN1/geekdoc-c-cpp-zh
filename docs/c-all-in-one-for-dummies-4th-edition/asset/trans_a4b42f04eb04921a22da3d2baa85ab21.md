

## 使用输出流写入

对于宽度操纵器 `setw()`，你也可以添加 `#include <iomanip>`，然后使用该操纵器：

```cpp
cout << setw(10);
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_727_0.png)

由于库中的一些古怪行为，当你设置宽度后，它只在下一次输出操作中保持该设置。你可以说它健忘。因此，假设你有如下代码：

```cpp
cout.width(10);
cout << 20 << 30 << endl;
```

只有第一个输出 20 具有 10 的字段宽度。30 只占用它所需的空间。因此，这些代码行产生如下输出，这很可能不是大多数人想要的结果：

```text
        2030
```

这就是为什么更推荐使用操纵器形式：你在每个输出项之前指定宽度。改为试试这个：

```cpp
cout << setw(10) << 20 << setw(10) << 30 << endl;
```

这会将以下内容写入 cout：

```text
        20        30
```

清单 2-4 中的 `WidthFunction` 示例展示了设置宽度后可以实现的出色效果。

**清单 2-4：使用 setw 操纵器或 Width 函数设置字段宽度**

```cpp
#include <iostream>
#include <iomanip>
#include <fstream>

using namespace std;

int main() {
    ofstream sals("..\\salaries.txt");

    sals << setprecision(2) << fixed << left;
    sals << setw(20) << "Name" << setw(10) << "Salary";
    sals << endl;

    // 19 hyphens, one space
    sals << "------------------- ";

    // 10 hyphens
    sals << "----------" << endl;

    sals << setw(20) << "Hank Williams";
    sals << setw(10) << 28422.82 << endl;
    sals << setw(20) << "Buddy Holly";
    sals << setw(10) << 39292.22 << endl;
    sals << setw(20) << "Otis Redding";
    sals << setw(10) << 43838.55 << endl;
    sals.close();

    cout << "File Written" << endl;
    return 0;
}
```

运行清单 2-4 时，你会得到一个名为 salaries.txt 的文件，如下所示：

| 名称 | 薪资 |
| --- | --- |
| Hank Williams | 28422.82 |
| Buddy Holly | 39292.22 |
| Otis Redding | 43838.55 |

第一个字段“名称”宽 20 个字符。你只使用 19 个连字符，以在两个字之间呈现出空格的外观。实际上，这两个字段紧挨在一起，中间没有空格。

![](img/128ab511de4e7360e167e3b15cdd5dd0_728_0.png)

如果你想运行清单 2-4，但以科学计数法格式显示每个薪资，例如 2.8e+04，则需要在移除 `fixed` 修饰符后使用 `sals.setf(ios::scientific);` 和 `sals.setf(ios::left);`。

**提示**

![](img/128ab511de4e7360e167e3b15cdd5dd0_728_1.png)

该示例使用 `left` 格式标志，使每个字段中的数据对齐到字段左端。默认情况下，每个字段右对齐。

![](img/128ab511de4e7360e167e3b15cdd5dd0_729_0.png)

尽管你可以指定字段宽度，但实际上指定的是最小值。如果输出中的字符少于字段宽度，运行时库会用空格填充，使其达到该最小大小。如果字符多于该宽度，库不会将其截断以使其适应。如果你在清单 2-4 的 Hank Williams 行中添加字母（像这样：`sals << setw(20) << "Hank WilliamsABCDEFGHIJ";`），输出反而会像下面这个示例。Hank Williams 行会超出 20 个字符并进入下一个字段。

| 名称 | 薪资 |
| --- | --- |
| Hank WilliamsABCDEFGHIJ | 28422.82 |
| Buddy Holly | 39292.22 |
| Otis Redding | 43838.55 |

## 使用运算符提取

从文件读取时，可以使用提取运算符 `>>`。这个运算符很容易使用，只要你明白使用提取运算符确实有一些注意事项。例如，假设你有一个名为 `Numbers.txt` 的文件，其中一行包含以下文本（你需要 `Numbers.txt` 文件来运行本章的示例代码）：

```
100 50 30 25
```

你可以使用清单 3-1 中所示的 `FileRead01` 示例代码，轻松将这些数字读入内存。

**清单 3-1：使用提取运算符将文件读入内存**

```cpp
#include <iostream>
#include <fstream>
#include <string.h>

using namespace std;

int main() {
    string weight;
    string height;
    string width;
    string depth;

    ifstream MyFile("../Numbers.txt");
    if (!MyFile) {
        cerr << "File couldn't be opened!" << endl;
        cerr << "Error Code: " << strerror(errno) << endl;
        return -1;
    }

    MyFile >> weight;
    MyFile >> height;
    MyFile >> width;
    MyFile >> depth;

    cout << "Weight = " << weight << "\r\n";
    cout << "Height = " << height << "\r\n";
    cout << "Width = " << width << "\r\n";
    cout << "Depth = " << depth;

    MyFile.close();
    return 0;
}
```

每个变量只保存一个字符串元素。要读取全部四个数字，需要提取数据四次。输入文件 Numbers.txt 中的数字用空格分隔。你也可以用换行符分隔它们，像这样：

```
100
50
30
25
```

应用程序不在乎。它会查找空白字符，即任意数量的空格、制表符和换行符。你可以将数据格式化成如下示例的样子，应用程序仍能正确读取它们。

```
100    50
       30
   25
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_732_0.png)

处理标准输入对象 `cin` 时，同样的空白字符规则也适用：如果你像下面示例那样读取四个数字，`cin` 对象会像 `ifstream` 对象一样，根据空白字符分隔数字。

![](img/128ab511de4e7360e167e3b15cdd5dd0_732_1.png)

用户常犯的错误可能导致应用程序失败，或可能显示不正确信息：

- 如果用户意外地在输入流中插入空格，无论来自控制台还是文件，计算机都会将该空格视为新字符串的开头。
- 有时用户忘记添加空白字符，这意味着两个值会挤在一起，计算机将它们视为一个整体。
- 用户可能尝试使用逗号、分号或其他非空白字符来分隔值。
- 缺少值，即用户直接遗漏数据，也是一个问题。

因此，当输入数据出现问题时，检查多余的空白字符、缺失的空白字符或缺失的值是一个很好的起点。

![](img/128ab511de4e7360e167e3b15cdd5dd0_733_0.png)

从文件读取信息时，请确保清楚定义信息顺序。换句话说，确保你们已就信息的协议达成一致。否则，你很可能会最终遇到错误和失误。

这个示例包含打开文件时的错误捕获。此错误捕获需要添加 `#include <string.h>`（注意包含了 `.h`）。在创建 `MyFile` 并用构造函数打开文件后，代码会检查 `MyFile` 中是否有文件句柄。如果 `MyFile` 为空，代码会向标准错误输出 `cerr` 输出错误信息，并提供一个人类可读的输出错误，例如 `No such file or directory`。

如果文件打开过程成功，代码会使用提取运算符读取每个数据值。然后以格式良好的形式输出这些值，并关闭文件。运行应用程序时，你会看到读取文件的结果：

```
Weight = 100
Height = 50
Width = 30
Depth = 25
```

### 什么是协议？

你有一个数字列表：1600 20500 1849 20240。无论你怎么看这些数字，它们都没有任何意义。你需要一个协议。如本章所定义，*协议* 只是一条关于如何格式化和排序数据的规则。它描述数据流所需的内容。一般来说，协议定义了计算机之间交换任何类型信息的规则（可以把它想象成一种外交角色）。两个系统基于标准化规则协商数据交换。

碰巧的是，这组数字中的第一个数字是华盛顿特区白宫的街道地址，第二个数字是白宫的邮政编码。第三个数字是国家公园管理局总部主办公室的街道地址，第四个是国家公园管理局的邮政编码。

此外，协议还规定了接收数据后如何响应。你可以回传单个数字 1，表示你已正确接收数据；另一方可以回传单个 0，表示你不会再接收更多信息。这就是协议，协议在读取数据时很有用，无论数据来自文件还是来自互联网。


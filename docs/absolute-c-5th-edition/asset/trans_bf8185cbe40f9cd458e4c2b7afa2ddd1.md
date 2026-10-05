
`close` 会自动调用 `flush`，因此你很少需要使用 `flush`。`flush` 的语法如下例所示：

```
outStream.flush();
```

## 陷阱：流变量的限制

你按照通常的方式声明流变量（类型为 `ifstream` 或 `ofstream` 之一），但这些变量不能像其他变量那样用于某些方式。你不能使用赋值语句给流变量赋值。你可以拥有一个流类型的参数（`ifstream`、`ofstream` 或任何其他流类型），但它必须是引用传递参数（call-by-reference）。它不能是值传递（call-by-value）。

## 追加到文件

向文件中输出内容时，你的代码必须首先使用成员函数 `open` 打开文件并将其连接到 `ofstream` 流。我们到目前采用的方法（仅使用一个文件名作为参数）总是产生一个空文件。如果已存在同名文件，其旧内容将会丢失。还有另一种打开文件的方法，使得程序的输出内容可以追加到文件中已有任何数据之后。

要将输出内容追加到名为 "important.txt" 的文件中，你需要使用带有两个参数的 `open` 版本，如下所示：

```
outStream;
outStream.open("important.txt", ios::app);
```

如果文件 "important.txt" 不存在，这将会创建一个同名的空文件以接收程序的输出；如果文件已存在，则程序的所有输出都将追加到文件末尾，这样文件中的旧数据就不会丢失。这在显示 12.2 中所示。

第二个参数 `ios::app` 定义在 `ios` 类中。`ios` 类定义在 `<iostream>` 库中（也在其他一些流库中）。`ios` 类的定义放在 `std` 命名空间中，因此以下任一代码都能让你的程序可以使用 `ios::app`：

```cpp
#include <iostream>
using namespace std;
```

```cpp
#include <iostream>
using std::ios;
```

或者

## 显示 12.2 追加到文件

```cpp
// 将数据追加到 data.txt 的末尾。
#include <fstream>
#include <iostream>
using std::ofstream;
using std::cout;
using std::ios;

int main() 
{
    cout << "Opening data.txt for appending.\n";
    ofstream fout;
    fout.open("data.txt", ios::app);
    fout << "5 6 pick up sticks.\n";
    fout << "7 8 ain't C++ great!\n";
    cout << "End of appending to file.\n";
    return 0;
}
```

示例对话

### Data.txt
（程序运行前）

### Data.txt
（程序运行后）

| 1 buckle my shoe. |
| 3 shut the door. |

| 1 2 buckle my shoe. |
| 3 shut the door. |
| 5 6 pick up sticks. |
| 7 8 ain't C++ great! |

## 屏幕输出

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_552_0.png)

## 追加到文件

如果你想将数据追加到文件中，使其位于文件中任何现有内容之后，请按如下方式打开文件。

语法

```
Output_Stream.open(File_Name, ios::app);
```

示例

```cpp
ofstream outStream;
outStream.open("important.txt", ios::app);
```

### 提示：打开文件的另一种语法

`ifstream` 和 `ofstream` 每个类都拥有构造函数，允许你指定文件名，有时还有打开文件的其他参数。几个示例将使变得清晰。

以下两个语句

```cpp
ifstream inStream;
inStream.open("infile.txt");
```

可以用以下等价行替换：

```cpp
ifstream inStream("infile.txt");
```

以下两个语句

```cpp
ofstream outStream;
outStream.open("outfile.txt");
```

可以用以下等价行替换：

```cpp
ofstream outStream("outfile.txt");
```

作为最后一个示例，以下两行代码

```cpp
ofstream outStream;
outStream.open("important.txt", ios::app);
```

等同于以下：

```cpp
ofstream outStream("important.txt", ios::app);
```

## I/O 流 525

显示 12.3 带有打开检查的文件 I/O

```cpp
// 从文件 infile.txt 读取三个数字，并将和写入
// 文件 outfile.txt。
#include <fstream>
#include <iostream>
#include <cstdlib> //for exit
using std::ifstream;
using std::ofstream;
using std::cout;
using std::endl;

int main ( {
{
    ifstream inStream;
    ofstream outStream;

    inStream.open("infile.txt");
    if (inStream.fail()) {
        exit(1);
    }

    outStream.open("outfile.txt");
    if (outStream.fail()) {
        cout << "Input file opening failed.\n";
        exit(1);
    }

    int first, second, third;
    inStream >> first >> second >> third;
    outStream << "The sum of the first 3\n"
              << "numbers in infile.txt\n"
              << "is " << (first + second + third) << endl;

    inStream.close();
    outStream.close();
    return 0;
}
``` 
示例对话（如果文件 infile.txt 不存在）：Input file opening failed.

### 提示：检查文件是否成功打开

`open` 调用失败可能出于多种原因。例如，如果你尝试打开一个不存在的指定输入文件，那么 `open` 调用将失败。另一个例子是，尝试打开输出文件可能会因为文件已存在但你的程序（即你的账户）没有写入权限。当此类情况发生时，你可能不会收到错误消息，而程序可能会执行意外的操作。你应该在调用 `open` 后紧跟一个测试来检查打开是否成功，并结束程序。

（注：原文后续部分存在大量重复文本，此处已根据要求仅翻译核心内容。）

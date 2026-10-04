

## 446 I/O 流与数据文件

## 程序 8.2

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib> // needed for exit()
using namespace std;

int main() {
    ifstream inFile;
    ofstream outFile;

    inFile.open("prices.dat"); // 尝试打开文件进行输入

    char response;

    if (!inFile.fail()) // 如果没有失败，则文件存在 {
        cout << "A file by the name prices.dat exists.\n"
             << "  Do you want to continue and overwrite it\n"
             << "  with the new data (y or n): ";
        cin >> response;
        if (tolower(response) == 'n') {
            cout << "The existing file will not be overwritten." << endl;
            exit(1);
        }
    }

    outFile.open("prices.dat"); // 现在打开文件进行写入

    if (inFile.fail()) // 检查是否打开成功
    {
        cout << "\nThe file was not successfully opened\n"
             << endl;
        exit(1);
    }

    cout << "  The file has been successfully opened for output.\n" << endl;

    // 写入文件的语句将放在这里

    return 0;
}
```

## 第 8 章

## 447 I/O 流对象与方法

以下是程序 8.2 的两次运行结果：

A file by the name prices.dat exists.
Do you want to continue and overwrite it
with the new data (y or n): n
The existing file will not be overwritten.

and

A file by the name prices.dat exists.
Do you want to continue and overwrite it
with the new data (y or n): y
The file has been successfully opened for output.

它们可以合并为一条语句：

```cpp
ifstream inFile("prices.dat");
```

## 嵌入式与交互式文件名

程序 8.1 和 8.2 有两个问题：

- 外部文件名嵌入在程序代码中。
- 没有提供让用户在程序运行时输入文件名的机制。

编写程序时，如果需要更改文件名，程序员必须修改 `open()` 调用中的外部文件名并重新编译程序。这两个问题都可以通过将文件名赋值给字符串变量来避免。

本书使用的字符串变量是一个可以存储字符串值的变量，字符串是包含在双引号中的零个或多个字符的序列，例如 `"Hello World"` 和 `""`。请记住，引号界定了字符串的开始和结束，但不会作为字符串的一部分存储。

在为 `open()` 方法声明并初始化字符串变量时，该字符串被视为 C 字符串。（有关使用 C 字符串的注意事项，请参阅信息点“将 C 字符串作为文件名”）。一种更安全的替代方案，也是书中处处使用的方法，是使用 `string` 类对象并使用 `c_str()` 方法将其转换为 C 字符串。

## I/O 流与数据文件

### 关于 C 字符串作为文件名的说明

### 使用 C 字符串作为文件名
如果你使用 C 字符串（本质上是一个一维字符数组）来存储外部文件名，必须在声明后立即用方括号指定该 C 字符串的最大长度。例如，查看以下声明：

```c
char filename[21] = "prices.dat";
```
括号中的数字 (21) 比赋值给变量 `filename` 的最大字符数多一个，因为编译器会添加一个结束字符串字符来终止字符串。因此，由 10 个字符组成的字符串 `"prices.dat"` 实际上存储为 11 个字符。在这个示例中，赋值给变量 `filename` 的最大值是一个由 20 个字符组成的字符串值。

在声明用于存储文件名的字符串变量后，可以用两种方式之一使用。首先，如程序 8.3a 所示，它可以被放在程序顶部，以清晰地标识文件名，而不是将其嵌入 `open()` 方法中。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_467_0.png)

## 程序 8.3a

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib> // needed for exit()
#include <string>
using namespace std;
int main()
{
    string filename = "prices.dat"; // 将文件名放在前面
    ifstream infile;
    infile.open(filename.c_str()); // 打开文件
    if (infile.fail()) // 检查是否打开成功
    {
        cout << "\nThe file named *" << filename << "*\n";
        cout << " was not successfully opened";
        cout << "\nnPlease check that the file currently exists.";
        cout << endl;
        exit(1);
    }

    cout << "\nThe file has been successfully opened for reading.\n";
    return 0;
}
```

## 第 8 章

## I/O 流对象与方法

在程序 8.3a 中，字符串对象以 `filename` 命名声明并初始化。该名字被放在 `main()` 对象的顶部，以便识别文件。当使用字符串对象 own字符串字面量时，`open()` 方法调用中的变量名不需要包含在引号内。此时，通过表达式 `filename.c_str()` 提供了字符串对象的值（一个 C 字符串）。

字符串对象的另一个有用作用是允许用户在程序执行时输入文件名。例如，以下代码：

```cpp
string filename;

cout << "Enter the name of the file you wish to open: ";
cin >> filename;
```

该代码允许用户在运行时输入文件的外部名。这段代码的唯一限制是用户不能将输入的字符串值包含在引号内，且输入的字符串值不能包含任何空格。不包含空格的原因是当使用 `cin` 时，编译器在遇到空格时会终止字符串。程序 8.3b 在完整程序使用了这段代码。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_468_0.png)

## 程序 8.3b

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib> // needed for exit()
#include <string>
using namespace std;
int main()
{
    string filename;
    ifstream inputFile;
    cout << "Enter the name of the file you wish to open: ";
    cin >> filename;
    inputFile.open(filename.c_str()); // 打开文件
    if (inputFile.fail()) // 检查是否打开成功
    {
        cout << "\nThe file named *" << filename << "*\n";
        cout << " was not successfully opened";
        cout << "\nnPlease check that the file currently exists.";
        cout << endl;
        exit(1);
    }

    cout << "\nThe file has been successfully opened for reading.\n";
    return 0;
}
```

## 469

### 信息点

### 使用 fstream 对象

在 `fstream` 和 `ofstream` 对象中，输入或输出模式由对象指示。因此，`fstream` 对象必须用于输入，`ofstream` 对象必须用于输出。创建文件流另一种方法是使用用于输入或输出的 `fstream` 对象，但这种方法需要显式指定模式。使用以下语法声明 fstream 对象：

```cpp
fstream objectName;
```

使用 fstream 类的 `open()` 方法时，需要两个参数：文件名和模式指示。以下是允许的模式指示：

| 指示符 | 说明 |
| --- | --- |
| ios:: | 以输入模式打开文件 |
| ios:: | 以输出模式打开文件 |
| ios::app | 以追加模式打开文件 |
| ios::ate | 打开后跳转到文件末尾 |
| ios::binary | 以二进制模式打开文件（默认是文本文件） |
| ios::trunc | 如果文件存在则删除内容 |
| ios::ncreate | 如果文件不存在，则打开失败 |
| ios::noreplace | 如果文件存在，则打开失败 |

与 `ofstream` 对象一样，输出模式下的 `fstream` 对象会创建一个新文件并使其可写入。如果存在与打开文件同名的文件，旧文件将被擦除。例如，以下语句将 `file1` 声明为 fstream 对象：

```cpp
fstream file1;
```

以下语句尝试以输出模式打开 `prices.dat` 文件：

```cpp
file1.open("prices.dat",ios::out);
```

文件打开后，程序通过内部名称 `file1` 访问文件，计算机以外部名称 `prices.dat` 保存文件。




# 518 第 12 章 流与文件 I/O

（上上）。使用这种方法，你的程序不允许对文件进行回溯并第二次读取任何内容。这正是当你的程序从键盘获取输入时发生的情况，因此这看起来并不新奇或奇怪。（正如我们将要所示的，你的程序可以从文件的开头开始读取文件，但这是重新开始，而不是回溯）。同样，对于这里介绍的方法，你的程序是从文件的开头开始向文件写入输出并向前进行。你的程序不允许回溯或更改已经写入文件的输出。这正是当你的程序将输出发送到屏幕时发生的情况：你可以向屏幕发送更多内容，但你不能回溯并更改屏幕输出。你将文件内容输入到你的程序或将程序中的输出发送到文件的方法，是通过流（stream）将你的程序与文件连接起来。

要发送文件，你的程序必须先将文件连接到 `ofstream` 类的（流）对象。要从文件中读取内容，你的程序必须先将文件连接到 `ifstream` 类的（流）对象。`ifstream` 和 `ofstream` 类定义在 `<fstream>` 库中，并位于 `std` 命名空间下。因此，为了同时进行文件输入和输出，你的程序将包含：

```cpp
#include <fstream>
using namespace std;
```

或者

```cpp
#include <fstream>
using std::ifstream;
using std::ofstream;
```

声明流的方式就像声明任何其他类变量一样。因此，你可以这样声明 `inStream` 为一个文件的输入流，将 `outStream` 为另一个文件的输出流：

```cpp
ifstream inStream;
ofstream outStream;
```

之前声明的流变量（如 `inStream` 和 `outStream`）必须分别连接到一个文件。这被称为“打开文件”，并通过成员函数 `open` 完成。例如，假设你想让输入流 `inputStream` 连接到名为 `infile.txt` 的文件。在从该文件读取任何输入之前，你的程序必须包含以下内容：

```cpp
inStream.open("infile.txt");
```

在提供文件名时，你可以指定路径名（目录或文件夹）。指定路径名的细节在不同系统中略有不同，请咨询当地专家了解细节（或进行一些试错编程）。在我们的示例中，我们将使用简单的文件名，这假设文件与运行程序的程序处于同一个目录（文件夹）中。

## 声明流

## 连接流到文件

## open

## 路径名

## I/O 流

# 519

一旦你声明了输入流变量并使用 `open` 函数将其连接到文件，你的程序就可以使用提取运算符 `>>` 从文件中获取输入，输入流的使用方法与 `cin` 相同。例如，以下代码从连接到 `inStream` 的文件中读取两个输入数字，并将它们存放在变量 `oneNumber` 和 `anotherNumber` 中：

```cpp
int oneNumber, anotherNumber;
inStream >> oneNumber >> anotherNumber;
```

输出流的打开（连接到文件）方式与上述描述输出流的方式方式相同。例如，以下代码声明了输出流 `outStream` 并将其连接到文件 `outfile.txt`：

```cpp
ofstream outStream;
outStream.open("outfile.txt");
```

当与 `ofstream` 类型的流一起使用时，成员函数 `open` 会在文件不存在创建该输出文件。该成员函数将丢弃文件的内容，以便在调用 `open` 后输出文件为空。我们将在本章稍后部分讨论打开文件的其他方法。

在调用 `open` 将文件连接到 `outStream` 后，程序可以使用插入运算符 `<<` 向字符串发送输出。例如，以下代码将两个字符串以及变量 `oneNumber` 和 `anotherNumber` 的内容写入连接到流 `outStream` 的文件（在本示例中是名为 `outfile.txt` 的文件）；

```cpp
outStream << "oneNumber = " << oneNumber << "anotherNumber = " << anotherNumber;
```

| >> 和 << 的重载适用于文件 |
| :--- |
| 正如我们在第 8 章中中所指出的，如果你重载了 `>>` 和 `<<`，那么这些重载应用于文件输入输出流的方式与它们应用于 `cin` 和 `cout` 的方式相同。（如果你还没有读第 8 章，可以忽略此注释。它将在第 8 章中再次为你重复。） |

注意，当你的程序处理文件时，该文件就像有两个名字一样。一个是操作系统使用的文件通常名称，即**外部名称**。在我们的示例代码中，外部名称是 `infile.txt` 和 `outfile.txt`。在某种意义上，外部名称是文件的“真实名称”。拼写这些外部文件名的约定在不同系统之间有所不同。我们在示例中使用的 `infile.txt` 和 `outfile.txt` 名称可能看起来不像你系统上的文件名。你应该遵循你操作系统上所使用的任何约定来命名你的文件。虽然外部文件名是文件的真实名称，但它通常在程序中只使用一次。外部文件名作为 `open` 函数的参数给出，但在文件打开后，始终通过命名连接到该文件的流来引用该文件。因此，在你的程序内部，流名充当了文件的第二个名字。

# 第 12 章 流与文件 I/O

## 文件有两个名字

你的程序使用的每个输入和输出文件都有两个名字。外部文件名是文件的真实名称，但它只在调用 `open` 函数时使用。`open` 将文件连接到流。在调用 `open` 后，你总是通过命名连接到该文件的流来引用该文件。因此，在你的程序内部，流名充当了文件的第二个名字。

你的程序在从文件中获取输入或向文件发送输出完成后，应该关闭文件。文件是通过调用 `close` 函数来关闭的。以下代码展示了如何使用 `close` 函数：

```cpp
inStream.close();
outStream.close();
```

注意 `close` 函数不接受参数。如果你的程序正常结束，系统会自动关闭文件。然而，养成关闭文件的习惯至少有两个理由。第一，如果你的程序由于错误异常结束，文件将不会关闭并可能处于损坏状态。第二，如果程序在完成任务后立即关闭文件，文件损坏的可能性会降低。你可能希望程序向文件发送输出并将其读回程序。为了做到，你的程序在写入完成后关闭文件，然后用输入流重新打开。（可以同时打开文件进行输入输出，但方法略有不同。）

常用的但你最终可能需要的成员函数是 `flush`，它是输出流的成员函数。出于效率考虑，输出在实际写入文件之前通常会被缓冲——即临时存储在某处。`flush` 成员函数刷新输出流，以便所有可能缓冲的内容被物理写入文件。调用

550

# 显示 12.1 简单文件输入输出

```cpp
// 从文件 infile.txt 读取三个数字，求和，
// 并将和写入文件 outfile.txt。
#include <fstream>
using std::ifstream;
using std::ofstream;
using std::endl;

int main() {
    ifstream inputStream;
    ofstream outputStream;

    inputStream.open("infile.txt");
    outputStream.open("outfile.txt");

    int first, second, third;
    inputStream >> first >> second >> third;
    outputStream << "The sum of the first 3\n";
    outputStream << "is " << (first + second + third) << endl;

    inputStream.close();
    outputStream.close();

    return 0;
}
```

> 该程序的更好版本在显示 12.3 中。

示例对话

> 屏幕没有输出，键盘没有输入。

Infile.txt
（未被程序修改）

Outfile.txt
（程序运行后）

| 1 |
| 2 |
| 3 | The sum of the first 3 numbers in infile.txt
 is 6 |
| 4 |


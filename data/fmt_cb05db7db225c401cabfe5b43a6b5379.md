
```cpp
int main(int nNumberOfArgs, char* pszArgs[])
{
    MyContainer mc(100, "Original");
    mc = fn(100, "Created in fn()");

    // 等待用户准备好后再终止程序
    cout << "Press Enter to continue..." << endl;
    cin.ignore(10, '\n');
    cin.get();
    return 0;
}
```

该程序的输出如下：

```
Created in fn()
Press Enter to continue...
```

函数`fn()`返回了一个临时对象，该对象通过赋值运算符`operator=(MyContainer&)`移动到`mc`对象上。`move()`函数的执行速度比`copy()`函数快得多——它没有分配堆内存，也没有复制任何内容。`move()`函数直接从`src`对象中获取内存块，而该对象正是`fn()`返回的临时对象。

![](img/c6a7aed193f785f4098546695e53f585_329_0.png)

确保你将`src`对象中的指针置零；否则，析构函数会将内存块返回给堆，导致目标对象指向未分配的内存。

# 第 23 章 使用流 I/O

## 本章内容

- 执行输入/输出
- 重新发现作为重载运算符的流 I/O
- 检查文件类的其他方法
- 使用流缓冲区 I/O

本章之前出现的程序从`cin`输入对象读取，并通过`cout`输出对象输出。也许你还没有真正仔细考虑过它，但这种输入/输出技术被称为流 I/O。

在本章中，我将更详细地描述 I/O。我必须警告你，流 I/O 是一个巨大的课题，无法在一个章节内完全涵盖——整整一本书都致力于这个主题。幸运的是对我们双方来说，要编写绝大多数程序，你并不需要了解关于流 I/O 的全部。

## 流 I/O 的工作原理

流 I/O 基于重载版本的`operator>>()`和`operator<<()`。这些重载运算符的声明可以在头文件`iostream`中找到，本书从第 1 章开始的所有程序都包含了该头文件。这些函数的代码包含在标准库中，你的 C++ 程序会与之进行链接。

以下代码显示了`iostream`中出现的几个原型：

```cpp
// 对于输入，我们有
istream& operator>>(istream& source, char *pDest);
istream& operator>>(istream& source, string &sDest);
istream& operator>>(istream& source, int &dDest);
istream& operator>>(istream& source, double &dDest);
//...以此类推...
```

```cpp
// 对于输出，我们有：
ostream& operator<< (ostream& dest, char *pSource);
ostream& operator<< (ostream& dest, string &sDest);
ostream& operator<< (ostream& dest, int source);
ostream& operator<< (ostream& dest, double source);
//...以此类推。
```

当重载用于处理 I/O 时，`operator>>()`被称为提取器（extractor），`operator<<()`被称为插入器（inserter）。`istream`类是从文件或设备（如键盘）进行输入的基本基类。C++ 在程序启动时会打开`istream`对象。同样，`ostream`是输出的基类。这些原型是用于指向空终止字符串（如`""`）、字符串对象、`int`和`double`的插入器和提取器。

## 默认流对象

C++ 在你的程序开头添加了一段代码，在`main()`获取控制权之前执行。除了其他之外，这段代码创建了表 23-1 所示的默认输入/输出对象。

| 表 23-1 标准 I/O 对象 | 对象 | 类 | 目的 |
| :--- | :--- | :--- | :--- |
| `cin` | `istream` | 标准输入 |
| `wcin` | `istream` | 宽字符输入 |
| `cout` | `ostream` | 标准输出 |
| `wcout` | `ostream` | 宽字符输出 |
| `cerr` | `istream` | 标准错误 |
| `wcerr` | `ostream` | 宽字符错误 |
| `clog` | `istream` | 标准日志 |
| `wlog` | `ostream` | 宽字符日志 |

## 输入/输出

`istream`和`ostream`类用于文件输入输出。`ifstream`和`ofstream`分别是它们的类的子类。

例如，简单的输出到文件：

```cpp
// 简单的输出到文件
#include <fstream>
using namespace std;

int main(int nNumberOfArgs, char* pszArgs[])
{
    ofstream my("MyName.txt");
    my << "Stephen Davis is suave and handsome\n";
    my << "and definitely not balding prematurely\n";
    my << endl;
    return 0;
}
```

文件流类的析构函数会自动关闭关联的文件。在我的简单示例中，`MyName.txt`文件在对象从`main()`函数返回并超出作用域时被关闭。全局对象在程序终止时也会被关闭。

## 打开模式

表 23-2 显示了打开文件时可能使用的不同模式。然而，每当你打开文件时，你都需要回答三个基本问题：

- 你想从文件中读取还是向其写入？使用`ifstream`读取，使用`ofstream`写入。如果你打算对同一个文件同时进行读和写，请使用`ifstream`并将模式设置为`inout`，但祝你好运——更好的做法是完全写入一个文件，然后关闭它并作为一个独立的对象重新打开进行读取。
- 如果你正在写入的文件且该文件已存在，你是想添加现有内容（这种情况下使用设置`ate`模式打开），还是截断文件并重新开始（这种情况下使用`trunc`）。
- 你是在读取或写入二进制数据吗？`ifstream`和`ofstream`默认都使用文本模式。如果你正在读取或写入原始的非文本数据，请使用二进制模式。

二进制模式和文本模式之间的主要区别在于处理换行符的方式。Unix 系统编写于打字机仍然流行的时代（当时被称为“typing”而不是“keyboarding”）。Unix 以换行符后紧跟一个回车符来结束句子。

随后的系统认为没有必要继续用两个字符表示一个句子，但它们对于使用哪种字符无法达成共识。有些使用回车符，另一些使用换行符（重命名为 newline）。C++ 标准使用的是简单的换行符。

当文件以文本模式打开时，C++ 库会将换行字符转换为适用于你操作系统的格式，无论是回车加换行符、单个回车、换行符还是完全不同的内容。在读取文件时，它会执行相反的操作。对于以二进制模式打开的文件，C++ 库不会进行此类转换。

![](img/c6a7aed193f785f4098546695e53f585_334_0.png)

在操作非人类可读格式的文件时请使用二进制模式。否则，如果数据流中的某个字节恰好等于回车符或换行符，文件 I/O 库将修改它。

## 嘿，文件，你处于什么状态？

一个构造好的`istream`对象（包括`istream`和`ofstream`）成为它所关联文件的代理。例如，流对象维护有关 I/O 过程的状态信息。成员函数`bad()`在发生某些“坏”情况时返回`true`。这个模糊的术语意味着文件无法打开、某些内部对象被损坏，或者东西直接丢失了。较轻的错误`fail()`表示要么发生了`bad()`情况，要么上一次读取失败了——例如，如果你尝试读取一个`int`但程序只能找到一个触发`fail()`而非`bad()`的字符。成员函数`good()`在`bad()`和`fail()`都为`false`时返回`true`。

对已设置错误的流对象进行输入或输出的尝试将被忽略。成员函数`clear()`会将`fail`标志置零，为暂时的错误提供再次机会——通常情况下，`clear`清除“fails”但不会清除“bad”。对已错误的`ofstream`对象的所有输出尝试都不会产生影响。

最后一段话是字面意思——只要流对象的内部错误状态不为零，就不可能进行输入或输出。如果错误是暂时的且你可以清除它，那么在你调用`clear()`清除错误标志之前，程序甚至不会尝试。

## 你能给我看个例子吗？

下面的示例程序演示了如何使用`istream`类来提取一系列整数：

```cpp
// StreamInput - 使用 fstream 从文件进行简单输入
#include <iostream>
#include <cstdlib>
#include <fstream>
using namespace std;

istream& openFile()
{
    istream* pFileStream = 0;
    for(;;) {
        // 打开用户指定的文件
        string sFileName;
        cout << "Enter the name of a file with integers:";
        cin >> sFileName;

        // 打开文件进行读取
        pFileStream = new istream(sFileName.c_str());

        if (pFileStream->good()) {
            pFileStream->seekg(0);
            cout << "Successfully opened " << sFileName << endl;
            break;
        }
        cerr << "Couldn't open " << sFileName << endl;
        delete pFileStream;
    }
    return *pFileStream;
}

int main(int argc, char* argv[]) {
    // 获取一个引用
    ifstream& fileStream = openFile();

    // 当没有更多数据输入时停止
    while (!fileStream.eof()) {
        // 读取一个值
        int nValue = 0;
        fileStream >> nValue;

        // 如果程序
        if (fileStream.fail()) {
            break;
        }

        // 输出值
        cout << nValue << endl;
    }

    cout << "Press Enter to continue..." << endl;
    cin.get();
    return 0;
}
```

该程序的输出如下（我对输入内容加了粗体）：

```
Enter the name of a file with integers:chicken
Couldn't open chicken
Enter the name of a file with integers:integers.txt
Successfully opened integers.txt
1
2
3
4
5
6
Press Enter to continue...
```

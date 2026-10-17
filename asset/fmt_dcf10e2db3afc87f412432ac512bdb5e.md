
`fn()` 函数通过赋值运算符 `operator=(MyContainer&&)` 返回一个移动到 `mc` 对象的临时对象。`move()` 函数执行比 `copy()` 函数快得多——它不在堆上分配内存或拷贝任何内容。`move()` 函数只是从 `src` 对象获取内存块，确保 `src` 对象中的指针置零；否则析构函数将返回堆上的内存。

## 使用流 I/O

在本章中：
- 执行输入/输出
- 作为重载运算符的流 I/O
- 文件的其他方法
- 使用缓冲区 I/O

在本章之前的程序从 `cin` 输入对象读取并通过 `cout` 输出对象输出。也许你还没有真正考虑过它，但这种输入/输出技术被称为流 I/O。我必须警告你，流 I/O 是一个巨大的话题，无法在一个章节中涵盖——整本书都致力于这个主题。幸运的是，我们不需要在编写时详细描述流 I/O。

### 流 I/O 如何工作

流 I/O 基于重载版本的 `operator>>` 和 `operator<<`。这些重载运算符的声明在所有程序都包含的 `iostream` 头文件中。这些函数的代码在 C++ 连接的标准库中。以下代码显示了 `iostream` 中的原型：

```cpp
// 输入：
istream& operator>>(istream& source, char* pDest);
istream& operator>>(istream& source, string& dDest);
istream& operator>>(istream& source, int& dDest);
istream& operator>>(istream& source, double& dDest);
// ... 等此类推
// 输出：
ostream& operator<<(ostream& dest, char* pSource);
ostream& operator<<(ostream& dest, string& sDest);
ostream& operator<<(ostream& dest, int& source);
ostream& operator<<(ostream& dest, double& source);
// ... 等此类推
```

当重载用于 I/O 时，`operator>>` 称为提取，`operator<<` 称为插入。`istream` 类是从文件或键盘等设备输入的基本类。C++ 在程序启动时打开 `istream` 对象。同样，`ostream` 是输出的基本类。这些原型用于处理空终止字符字符串、字符串对象、整数和双精度浮点数的提取器。

C++ 在程序开头添加了一段在 `main()` 获取控制权之前执行的代码。此外，代码创建了表 23-1 所示的默认输入/输出对象。

表 23-1
| 对象 | 类 | 目的 |
|---|---|---|
| `cin` | `istream` | 标准 char 输入 |
| `wcin` | `wstream` | 标准 wchar_t 输入 |
| `cout` | `ostream` | 标准 char 输出 |
| `wcout` | `wstream` | 标准 wchar_t 输出 |
| `cerr` | `ostream` | 标准错误输出 |
| `wcerr` | `wstream` | 标准错误 wchar_t 输出 |
| `clog` | `ostream` | 标准日志 |
| `wlog` | `ostream` | 标准 wchar_t 输出 |

你见过 `cin` 和 `cout` 从键盘输入并输出显示器：

```
C:>MyProgram <InputFile.txt >DefaultOut.txt
```

## 第 23 章：使用流 I/O

在这里，运算符的意思是“执行 `MyProgram`”，但从 `InputFile.txt` 读取标准输入，并将本该发送到标准输出的内容发送到 `DefaultOut.txt`。

重定向输入输出来自 Windows 中的 DOS 提示符以及所有版本的 Unix 和 Linux。当你尝试快速编写一些内容时，这是执行文件输入/输出最简单的方法。

默认情况下，`cerr` 对象像 `cout` 一样输出到显示器，但重定向 `cout` 默认输出到文件不会重定向 `cerr` 输出。这允许程序即使 `cerr` 已重定向到文件，也能向运算符显示错误消息。

错误消息应该发送到 `cerr` 而不是 `cout`，以防运算符重定向了标准输出。

`wcin`、`wcout` 和 `wcerr` 分别是标准输入、输出和错误的宽版本。这些设计用于处理 Unicode 符号：

```cpp
cout << "this is narrow output" << endl;
wcout << L"Is this is wide output" << endl;
```

### 流输入/输出

在 `fstream` 中定义的 `ifstream` 和 `ostream`（可能是 `ofstream`）类是 `istream` 和 `ostream` 的子类，用于执行到磁盘文件的流输入输出。你可以使用像在 `cin` 和 `cout` 上使用的相同的提取器和插入器用于 `ifstream` 和 `ofstream` 对象。

`ifstream` 实际上是模板类 `basic_istream<T>` 的实例化，其中 `T` 设置为 `char`。在第 26 章。`basic_istream<T>` 模板类也用其他类型实例化，以提供不同类型的输入类。例如，宽流文件 `ifstream` 基于相同的 `basic_istream<T>`，其中 `T` 设置为 `wchar_t`。`ostream` 等同于 `basic_ostream<char>`。

# 318 第五部分：安全

第一个参数是指向要打开的文件名的指针。第二个参数指定模式。`openmode` 类型是定义在 `ios_base` 中的一个整数类型。在 `ios_base` 中还定义了表 23-2 中列出的模式的可能值。这些是程序员通过位或（OR）操作组合在一起的字段。（有关位域或操作的解释，请参见第 4 章。）`istream` 的默认模式是以输入方式打开文件，并将指针指向文件开头（这很符合逻辑）。

| 表 23-2 | 控制文件打开方式的常量 |
| --- | --- |
| 标志位 | 含义 |
| `ios_base::app` | 在每次写入之前跳转到文件尾。 |
| `ios_base::ate` | 如果文件存在，在打开文件后立即跳转到文件尾。 |
| `ios_base::binary` | 以二进制模式打开文件（另一种是文本模式）。 |
| `ios_base::in` | 以输入模式打开文件（`istream` 默认）。 |
| `ios_base::out` | 以输出模式打开文件（`ostream` 默认）。 |
| `ios_base::trunc` | 如果文件存在，则截断文件（`ostream` 默认）。 |

`ostream` 的默认值是以输出模式打开，如果文件已存在则将其截断。截断的替代方案是 `ios_base::app`，这意味着如果文件存在，则将新输出追加到文件末尾。这两个选项可以在文件不存在时创建一个文件。

例如，`StreamOutput` 程序打开了 `MyName.txt` 文件，然后向该文件写入了一些重要且绝对真实的信息：

```cpp
// simple output to a file
#include <fstream>
using namespace std;
int main(int nNumberOfArgs, char* pszArgs[]) {
	ofstream my("MyName.txt");
	my << "Stephen Davis is suave and handsome\n";
		 << "and definitely not balding prematurely";
		 << endl;
	return 0;
}
```

# 第 23 章：使用流输入输出

文件类的析构函数会自动关闭关联的文件。在我的简单示例中，当 `my` 对象从 `main()` 返回并离开作用域时，`MyName.txt` 文件被关闭了。全局对象在程序终止时会被关闭。

### 打开模式

表 23-2 显示了打开文件时可能的各种不同模式。然而，每当你打开一个文件时，都需要回答三个基本问题：
- 你是想从文件中读取还是向文件中写入？使用 `ifstream` 读取，使用 `ofstream` 写入。如果你打算对同一个文件同时进行读和写，请使用 `ifstream` 并将模式设置为 `inout`，但运气不错的话——更好的做法是完全写入文件并关闭它，然后作为一个独立的对象重新打开进行读取。
- 你是否打算向文件写入且该文件已存在？你是想在现有内容上进行添加（这种情况下，使用 `ate` 打开），还是截断文件并重新开始（这种情况下，使用 `trunc`）？
- 你读取的是文本数据还是二进制数据？`ifstream` 和 `ofstream` 默认都使用文本模式。如果你正在读取或写入原始的非文本数据，请使用二进制模式。

二进制模式和文本模式的主要区别在于处理换行符的方式。Unix 操作系统编写于打字机仍然流行的时代（那时被称为“打字”而不是“键盘输入”）。Unix 以换行符后跟回车符结束句子。

随后的系统认为没有必要继续使用两个字符来结束一行，但它们对使用哪种字符无法达成一致。有些使用回车符，另一些使用换行符（现在重命名为 newline）。C++ 标准是唯一的标准。

当文件以文本模式打开时，C++ 库会在输出时将换行符转换为适用于你操作系统的格式，无论是回车符加换行符、回车符还是其他内容。在读取时，它会执行相反的转换。对于以二进制模式打开的文件，C++ 库不进行任何转换。

在处理非人类可读格式的文件时，始终使用二进制模式。否则，如果数据中的某个字节必须与回车符或换行符相同，文件 I/O 库将修改它。

## 第 23 章：使用流 I/O

| 方法 | 含义 |
| --- | --- |
| `istream& seekp(pos_type position)` | 返回写指针。 |
| `istream& seekp(off_type offset, ios_base::seekdir) set(fmtflags)` | 设置特定的格式标志。返回旧值。 |
| `pos_type tellg()` | 返回读指针的位置。 |
| `pos_type tellp()` | 返回写指针的位置。 |
| `fmtflags unsetf(fmtflags)` | 清除特定的格式标志。返回旧值。 |
| `int width() width(int w)` | 读取或设置下一个格式化输出语句要显示的字符数。 |
| `ostream& write(const char* buffer, streamsize num)` | 向输出文件写入块块数据。 |

### 直接读写流

插入运算符（inserter）和提取运算符（extractor）为格式化输入提供了一种方便的机制。然而，有时你只是想说：“给我吧；我不在乎格式是什么。”在这种情况下，几个方法非常有用。

最简单的函数 `get()` 只是返回输入文件中的下一个字符。它的输出等价物是 `put()`。`getline()` 函数返回一个字符字符串，直到遇到终止符为止——默认是换行符。`getline()` 会剥离终止符，但不会尝试对输入进行折射或其他形式的解释。

`read()` 函数甚至更基础。该函数读取你指定的字符数，如果程序遇到文件结束符（EOF），则读取少于该数的字符。`gcount()` 函数始终返回实际读取的字符数。输出等价物是 `write()`。

下面的示例程序使用 `read()` 和 `write()` 函数，为你提供的任何文件创建备份，方法是通过在名称末尾附加 "backup" 字符串来创建一个副本：

```cpp
// FileCopy - 为传递程序的文件创建备份副本
#include <cstdio>
#include <cstdlib>
#include <fstream>
#include <iostream>
using namespace std;
int main(int NNumberOfArgs, char* szArgs[]) {
    for (int n = 1; n < NNumberOfArgs; n++)
    {
        string szSource(szArgs[n]);
        string szTarget = szSource + ".backup";
        ifstream input(szSource.c_str(), ios_base::ios_base::binary);
        ofstream output(szTarget.c_str(), ios_base::ios_out|ios_base::binary|ios_base::trunc);
        if (input.good() && output.good())
        {
            cout << "Backing up " << szSource << " ...\n";
            while (!input.eof() && input.good())
            {
                char buffer[4096];
                input.read(buffer, 4096);
                output.write(buffer, input.gcount());
            }
            cout << "finished" << endl;
        }
        else
        {
            cerr << "Couldn't copy " << szSource << endl;
        }
    }
    cout << "Press Enter to continue..." << endl;
    cin.ignore(10, '\n');
    cin.get();
    return 0;
}
```

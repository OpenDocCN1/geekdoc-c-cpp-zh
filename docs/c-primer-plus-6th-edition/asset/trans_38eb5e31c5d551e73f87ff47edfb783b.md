

# Listing 17.17 count.cpp

```cpp
// count.cpp -- counting characters in a list of files
#include <iostream>
#include <fstream>
#include <cstdlib> // for exit()
int main(int argc, char * argv[])
{
    using namespace std;
    if (argc == 1) { // quit if no arguments
        cerr << "Usage: " << argv[0] << " filename[s]\n";
        exit(EXIT_FAILURE);
    }

    ifstream fin; // open stream
    long count;
    long total = 0;
    char ch;

    for (int i = 1; i < argc; i++) {
        fin.open(argv[i]); // connect stream to argv[i]
        if (!fin.is_open()) {
            cerr << "Could not open " << argv[i] << endl;
            fin.clear();
            continue;
        }
        count = 0;
        while (fin.get(ch)) {
            count++;
        }
        cout << count << " characters in " << argv[i] << endl;
        total += count;
        fin.clear(); // needed for some implementations
        fin.close(); // disconnect file
    }
    cout << total << " characters in all files\n";

    return 0;
}
```

## Note

某些 C++ 实现要求在程序结束时使用 `fin.clear()`，而另一些则不需要。这取决于与 `ifstream` 对象关联新文件时是否会自动重置状态。即使不需要，使用 `fin.clear()` 也没有什么大错。

例如，在 Linux 系统上，你可以将 Listing 17.17 编译为名为 `a.out` 的可执行文件。那么，示例运行可能如下：

```bash
$ a.out
Usage: a.out filename[s]
$ a.out paris rome
3580 characters in paris
4886 characters in rome
8466 characters in all files
$
```

注意该程序使用 `cerr` 来输出错误信息。微小的一点是，信息使用了 `argv[0]` 而不是 `a.out`。

这样，如果你更改了可执行文件的名称，程序将自动使用新名称。程序使用 `is_open()` 方法来验证其是否能够打开请求的文件。让我们进一步探讨这个问题。

## 文件模式

文件模式描述了如何使用文件：读取、写入、追加等。当你通过用文件名初始化文件流对象，或使用 `open()` 方法将流与文件关联时，你可以提供第二个参数来指定文件模式。

```cpp
ifstream fin("banjo", mode); // 带有 mode 参数的构造函数
ofstream fout;
fout.open("harp", mode2); // 带有带有 mode 参数的 open()
```

`ios_base` 类定义了打开模式来表示文件：类似于 `mflags` 和 `iost` 类型，它是一个位掩码类型（在以前，它是 `int` 类型）。你可以从 `ios_base` 类定义的多个常量中选择指定模式。表 17.7 列出了这些常量及其含义。C++ 文件 I/O 经过了更改，以兼容 ANSI C I/O。

### 表 17.7 文件模式常量

| 常量 | 含义 |
| --- | --- |
| ios_base::in | 打开文件进行读取。 |
| ios_base::out | 打开文件进行写入。 |
| ios_base::ate | 打开时移动到文件末尾。 |
| ios_base::app | 追加到文件末尾。 |
| ios_base::trunc | 如果文件存在，则截断文件。 |
| ios_base::binary | 二进制文件。 |

## 文件输入和输出

如果 `ifstream` 和 `ofstream` 的构造函数以及 `open()` 方法接受两个参数，那么我们在之前的示例中是如何只使用一个参数的呢？正如你可能猜到的，这些类成员函数的原型为第二个参数（文件模式参数）提供了默认值。例如，`ifstream` 的 `open()` 方法和构造函数使用 `ios_base::in`（用于读取）作为模式参数的默认值，而 `ofstream` 的 `open()` 方法和构造函数使用 `ios_base::out | ios_base::trunc`（写入并截断文件）作为默认值。位或运算符 `|` 用于将两个位合并为一个可用于设置位的单个值。`fstream` 类不提供默认模式，因此在创建该类的对象时必须显式提供模式。

注意 `ios_base::trunc` 标志意味着当打开文件以接收程序输出时，现有文件会被截断；即其之前的内容会被丢弃。这种行为极地减少了磁盘空间耗尽的危险，你可以想象在某些情况下你不想打开一个的文件。当然，C++ 提供了其他选项。例如，如果你想保留文件内容并在末尾添加（追加）新材料，你可以使用 `ios_base::app` 模式：

```cpp
ofstream fout("bags", ios_base::out | ios_base::app);
```

再次，代码使用 `|` 运算符来组合模式。因此 `ios_base::out | ios_base::app` 同时调用了 `out` 模式和 `app` 模式（见图 17.6）。你可能会在其他 C++ 实现中发现一些差异。例如，它们允许在之前的示例中省略 `ios_base::out`。


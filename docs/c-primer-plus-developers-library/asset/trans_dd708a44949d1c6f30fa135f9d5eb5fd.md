

**注意**

过去，判断文件是否成功打开的常用测试方法如下：

```cpp
if(fin.fail()) ... // 打开失败
if(!fin.good()) ... // 打开失败
if (!fin) ... // 打开失败
```

当 `fin` 对象用于测试条件时，如果 `fin.good()` 为 `false`，则被转换为 `false`，否则转换为 `true`，因此这两种形式是等价的。然而，这些测试无法检测一种情况，即尝试使用不适当的文件模式打开文件（参见本章后面的“文件模式”一节）。`is_open()` 方法能够捕获这种形式的错误，以及 `good()` 方法捕获的那些错误。不过，较旧的 C++ 实现没有 `is_open()`。

## 打开多个文件

你可能需要程序打开多个文件。打开多个文件的策略取决于它们的使用方式。如果你需要同时打开两个文件，则必须为每个文件创建单独的流。例如，一个将两个已排序文件合并到第三个文件的程序，会为两个输入文件创建两个 `ifstream` 对象，并为输出文件创建一个 `ofstream` 对象。你可以同时打开的文件数量取决于操作系统。

然而，你可能计划按顺序处理一组文件。例如，你可能想统计一个名字在一组 10 个文件中出现的次数。在这种情况下，你可以打开单个流并依次将其与每个文件关联。这比每个文件打开单独的流更有效地节省计算机资源。要使用这种方法，你可以声明一个未初始化的 `ifstream` 对象，然后使用 `open()` 方法将流与文件关联。例如，以下是你如何处理连续读取两个文件的方式：

```cpp
ifstream fin;                 // 使用默认构造函数创建流
fin.open("fat.txt");          // 将流与 fat.txt 文件关联
...
fin.close();                  // 终止与 fat.txt 的关联
fin.clear();                  // 重置 fin（可能不需要）
fin.open("rat.txt");          // 将流与 rat.txt 文件关联
...
fin.close();
```

我们很快会看一个示例，但首先，让我们研究一种将文件列表馈送给程序的技术，使程序能够使用循环来处理它们。

## 命令行处理

文件处理程序通常使用命令行参数来标识文件。*命令行参数* 是在命令行中键入命令时出现在命令行上的参数。例如，要在 Unix 或 Linux 系统上统计某些文件中的单词数，你需要在命令行提示符下键入以下命令：

```text
wc report1 report2 report3
```

这里 `wc` 是程序名，`report1`、`report2` 和 `report3` 是作为命令行参数传递给程序的文件名。

C++ 有一种机制，允许在命令行环境中运行的程序访问命令行参数。你可以将以下替代函数头用于 `main()`：

```cpp
int main(int argc, char *argv[])
```

`argc` 参数表示命令行上的参数数量。该计数包括命令名本身。`argv` 变量是一个指向 `char` 指针的指针。这听起来有点抽象，但你可以将 `argv` 视为指向命令行参数的指针数组，其中 `argv[0]` 是指向字符串第一个字符的指针，该字符串包含命令名，`argv[1]` 是指向字符串第一个字符的指针，该字符串包含第一个命令行参数，以此类推。也就是说，`argv[0]` 是命令行的第一个字符串，依此类推。例如，假设你有以下命令行：

```text
wc report1 report2 report3
```

在这种情况下，`argc` 将为 4，`argv[0]` 将是 `wc`，`argv[1]` 将是 `report1`，依此类推。以下循环将在单独一行上打印每个命令行参数：

```cpp
for (int i = 1; i < argc; i++)
    cout << argv[i] << endl;
```

从 `i = 1` 开始只打印命令行参数；从 `i = 0` 开始也会打印命令名。

当然，命令行参数与命令行操作系统（如 Windows 命令提示符模式、Unix 和 Linux）密不可分。其他设置可能仍允许你使用命令行参数：

- 许多 Windows IDE（集成开发环境）都有提供命令行参数的选项。通常，你需要通过一系列菜单选择，进入一个可以键入命令行参数的框。具体步骤因供应商和升级版本而异，因此请查阅你的文档。
- 许多 Windows IDE 可以生成可在 Windows 命令提示符模式下运行的可执行文件。

清单 17.17 将命令行技术与文件流技术相结合，用于统计命令行中列出的文件中的字符数。

### 清单 17.17 count.cpp

```cpp
// count.cpp -- counting characters in a list of files
#include <iostream>
#include <fstream>
#include <cstdlib>        // for exit()
int main(int argc, char * argv[])
{
    using namespace std;
    if (argc == 1)        // quit if no arguments
    {
        cerr << "Usage: " << argv[0] << " filename[s]\n";
        exit(EXIT_FAILURE);
    }

    ifstream fin;         // open stream
    long count;
    long total = 0;
    char ch;

    for (int file = 1; file < argc; file++)
    {
        fin.open(argv[file]);  // connect stream to argv[file]
        if (!fin.is_open())
        {
            cerr << "Could not open " << argv[file] << endl;
            fin.clear();
            continue;
        }
        count = 0;
        while (fin.get(ch))
            count++;
        cout << count << " characters in " << argv[file] << endl;
        total += count;
        fin.clear();          // needed for some implementations
        fin.close();          // disconnect file
    }
    cout << total << " characters in all files\n";

    return 0;
}
```

> **注意**
>
> 某些 C++ 实现要求在程序末尾使用 `fin.clear()`，而其他实现则不需要。这取决于将新文件与 `ifstream` 对象关联时是否自动重置流状态。即使不需要，使用 `fin.clear()` 也无害。

例如，在 Linux 系统上，你可以将清单 17.17 编译为名为 `a.out` 的可执行文件。然后示例运行可能如下所示：

```text
$ a.out
Usage: a.out filename[s]
$ a.out paris rome
3580 characters in paris
4886 characters in rome
8466 characters in all files
$
```

请注意，程序使用 `cerr` 输出错误消息。一个小细节是，消息使用 `argv[0]` 而不是 `a.out`：

```cpp
cerr << "Usage: " << argv[0] << " filename[s]\n";
```

这样，如果你更改可执行文件的名称，程序将自动使用新名称。

程序使用 `is_open()` 方法来验证是否能够打开请求的文件。让我们进一步探讨这个问题。

## 文件模式

文件模式描述了文件的使用方式：读取、写入、追加等。当你将流与文件关联时，无论是通过文件名初始化文件流对象，还是使用 `open()` 方法，你都可以提供指定文件模式的第二个参数：

```cpp
ifstream fin("banjo", mode1);   // 带模式参数的构造函数
ofstream fout;
fout.open("harp", mode2);        // 带模式参数的 open()
```

`ios_base` 类定义了一个 `openmode` 类型来表示模式；与 `fmtflags` 和 `iostate` 类型一样，它是一种位掩码类型。（在早期，它是 `int` 类型。）你可以从 `ios_base` 类中定义的几个常量中选择来指定模式。表 17.7 列出了这些常量及其含义。C++ 文件 I/O 经历了几次更改，以使其与 ANSI C 文件 I/O 兼容。

**表 17.7 — 文件模式常量**

| 常量 | 含义 |
|---|---|
| `ios_base::in` | 以读取方式打开文件。 |
| `ios_base::out` | 以写入方式打开文件。 |
| `ios_base::ate` | 打开文件后定位到文件末尾。 |
| `ios_base::app` | 追加到文件末尾。 |
| `ios_base::trunc` | 如果文件存在则截断文件。 |
| `ios_base::binary` | 二进制文件。 |


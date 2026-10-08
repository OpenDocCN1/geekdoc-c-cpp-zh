
- **流对象（Stream object）。** 作为字节的源和目的地。流对象操作的是一组有序的线性字节序列。这系列字节可以代表屏幕、文件或程序员想去的任何其他地方。你可以在几个库文件中找到处理流的类：`<fstream>`、`<iomanip>` `<ios>`、`<iosfwd>` `<iostream>`、`<istream>` `<ostream>`、`<streambuf>` 和 `<strstream>`。

- **操纵符（Manipulator）。** 以某种方式操作流中的数据。例如，操纵符可以将所有字符转换为大写，或者将使用十进制表示法的数字转换为十六进制表示。

- **插入（Insertion）。** 将字节放入流中。执行插入的方法被称为 `inserted`（插入符）。

- **提取（Extraction）。** 从流中取出字节。执行提取的方法被称为 `extractors`（提取器）。

# 理解头文件

在上一节关于流对象的项目符号中，我们列出了几个头文件。这些头文件中的每一个都封装了整个 C++ 流架构的某部分内容。所有这些文件共同构成了 C++ 提供的完整 I/O 支持。每一个文件都完成了其特定任务，使 C++ 拥有了任何编程语言中最多样化的 I/O 功能。每个头文件的目的如下：

- `<fstream>`。 包含了几个模板类的定义，这些类支持 `iostream` 头文件对存储在外部文件中序列的操作。

- `<iomanip>`。 包含了若干个单参数操纵符。

- `<ios>`。 包含了 `iostream` 头文件类的大部分格式操纵符。

- `<iosfwd>`。 包含了 `iostream` 头文件类的前置声明。

- `<iostream>`。 包含了标准全局流对象（如 `cin` 和 `cout`）的声明。

# 第 9 章 • 使用流和文件

- `<iostream>`。 包含了从流中输入数据的提取器，并包含了模板类 `basic_istream`。换句话说，`<iostream>` 提供了 I/O 中的 I（输入）。

- `<ostream>`。 包含了用于放入系列字节的插入器，并包含了模板类 `basic_ostream`。基本上，`<ostream>` 提供了 I/O 中的 O（输出）。

- `<sstream>`。 支持在字符串对象上定义的流。

- `<streambuf>`。 定义了 `basic_streambuf` 模板类。

- `<str>`。 支持在数组上定义的流。

除了 `ios_base` 类外，每个模板类都有一个针对字符的特化类。图 9.1 显示了最常用的类及其特化类。然而，这并不是一个完整的列表，因为几个流类超出了本书的范围。

图 9.1

| `<ios>` | `<ostream>` | `<iostream>` | `<fstream>` | `<sstream>` |

| --- | --- | --- | --- | --- |

| `ios_base` | | | | |

| | `ostream` | | | | |

| | | `cout`, `cerr`, `clog` | | | |

| | `<ostream>` | | `fstream` | | | |

| | `istream` | | | | `ostringstream` |

| | `istream` | | | | `istream` |

| | | `streambuf` | | | | `filebuf` | | |

| | `<streambuf>` | | | | `stringbuf` |

# IOS_BASE 类

`ios_base` 类包含了所有流通用的字节存储以及不依赖于模板参数的方法。这些字节存储存储了字节。

`ios_base` 类包含了所有流通用的字节存储以及不依赖于模板参数的方法。以下列表列出了 `ios_base` 中几种类型的目的：

- **event。** 使用 `event` 存储流。

- **fmtflags。** 使用 `fmtflags` 存储状态。

- **iostate。** 使用 `iostate` 跟踪 I/O。

- **openmode。** 使用 `openmode` 打开文件。

- **seekdir。** 使用 `seekdir` 访问。

- **flags()。** 存储标志位信息。

- **getloc()。** 获取本地化信息。

- **imbue()。** 浸入对象。

- **ios_bas()。** 构造函数。

- **operator =（赋值运算符）。** 复制一切。

- **precision()。** 精度。

- **pword()。** 回调流的引用。

- **register_callback()。** 注册回调函数。

- **setf()。** 设置标志。

- **unsetf()。** 清除标志。

- **width()。** 宽度。

- **xalloc()。** 唯一静态变量。

关于 `ios_base` 类还可以编写更多内容。然而，为了保持书籍的趣味性并控制篇幅，我们决定关注流的最常用用法。然而，如果你是那些无法充分学习流的奇人，你可以在库部分扩展你的知识：http://www.microsoft.com。

# 文件流

通常，你对文件流对象（例如派自 `ofstream`、`ifstream` 或 `fstream` 的类）的第一个操作是将其与要操作的文件关联。你使用 `open()` 方法或每个类的构造函数建立这种关联。

`open()` 方法的原型如下：

```
void open(const char * filename, openmode mode);
```

`filename` 是代表文件名的字符字符串，`mode` 是表 9.1 所示标志的组合。

标志使用位或运算符 (`|`) 连接。假设你想以二进制模式打开 *level1.map*。打开函数可能如下：

```
ofstream file:
file.open("level1.map", ios::out | ios::binary);
```

每个文件类都包含 `open()` 方法；然而，每个流都有指定其用途的默认标志。然而，只有在调用方法时不提供标志时，才会应用默认值。默认标志见表 9.2。

| 表 9.2 打开文件的标志 |

| 标志 | 功能 |

| ios::in | 打开读取。 |

| ios::out | 打开写入。 |

| ios::ate | 初始位置在文件末尾。 |

| ios::app | 将每次输出追加到文件末尾。 |

| ios::trunc | 如果文件已存在，则将其擦除。 |

| ios::binary | 以二进制模式访问文件。 |

# 表格 9.2 文件类的默认标志

| 类 (Class) | 标志 (Flags) |

| --- | --- |

| `ofstream` | `ios::out` | `ios::trunc` |

| `ifstream` | `ios::in` |

| `fstream` | `ios::in` | `ios::trunc` |

你也可以通过在构造函数包含文件名来打开文件。类构造函数使用的参数与 `open()` 方法相同。例如，如果你使用 `ifstream` 类，构造函数的原型看起来如下：

```cpp
ifstream::ifstream(const char * filename, openmode mode);
```

在这里 `filename` 和 `mode` 的含义与 `open()` 方法中相同。

你可以通过调用 `is_open()` 方法来检查文件是否正确打开：

```cpp
bool is_open()
```

如果文件正确打开，`is_open()` 返回 `true`，否则返回 `false`。

以下是文件无法正确打开的常见原因：

- 文件名错误——例如，一个不存在的文件名。

- 文件损坏——例如，位于硬盘坏道上的文件。

- 其他程序正在独占访问——这意味着具有独占访问权的程序可以访问该文件。因此，在相应程序释放独占权限之前，其他程序无法使用它。

- Windows 保护文件——Windows 有时会自动保护特定文件夹或特定类型的文件。如果发生这种情况，请联系你的系统管理员。

# 关闭文件

为了让其他程序能够访问文件，你必须关闭文件。要一次关闭一个文件，请使用 `close` 方法。对于这三个类中的每一个，都使用 `close` 成员来关闭文件，如下：

```cpp
void close();
```

如果文件流对象被销毁，它的析构函数会自动关闭与对象关联的文件。

# 处理文本文件

向文件输入和输出与向屏幕的输入输出完全相同，因为 `cin` 和 `ifstream` 类都派自于 `istream` 类（如图 9.1 所示）。同样，`cout` 和 `ofstream` 都派自于 `ostream` 类。它们都使用重载的插入运算符 `<<`。

以下代码阐释了这一点：

```cpp
// 9.1 - 输出文本 - Dirk Henkemans
#include <fstream>
using namespace std;
int main(void) {
    // 默认标志 ios::out | ios::trunc
    ofstream streams("dragons.txt");
    if(dragons.is_open()) {
        dragons << "Copper Dragon" << "\n"
        << "Bronze Dragon" << "\n"
        << "Silver Dragon" << "\n"
        << "Gold Dragon" << "\n";
    }
    dragons.close();
    return 0;
}
```

输出：

Copper Dragon

Bronze Dragon

Silver Dragon

Gold Dragon

`"dragons.txt"` 通常位于你项目所在的文件夹中。但是，如果你没有找到它，请前往 Windows 任务栏，点击“开始 > 查找（或搜索） > 文件或文件夹”。会出现一个标题类似于“查找：所有文件”的窗口。输入文件名并选择其存储所在的驱动器。点击“立即查找”，Windows 将为你查找到该文件。（注意：你的程序名称可能略有不同）

如果你运行程序，你会发现文本文件始终包含相同的信息。这是因为如果你没有指定 `mode` 参数，隐含的 `ios::trunc` 会使用 `ostream` 类。记住，`ios::trunc` 在文件已存在时会重新启动文件。

# 初学者 C++ 编程，第二版

虽然你可以使用重载的移位运算符 `(>>)` 从文件输入，但你无法知道何时到达文件末尾。从文本文件输入最简单的方法是使用 `istream::getline()` 方法按行输入数据。这也是最有用的方法，因为大多数数据是按行存储的，所以你输入整行，然后将数据分解为各个字段。

使用 `istream::getline()` 方法有三种选择：

```cpp
istream& getline(char* pch, int nCount, char delim = '\n');
istream& getline(unsigned char* puch, int nCount, char delim = '\n');
istream& getline(signed char* psch, int nCount, char delim = '\n');
```

参数占位符含义如下：

- `pch`, `puch`, `psch`：指向字符数组的指针。记住 `getline` 方法会覆盖存储在数组中的数据。

- `nCount`：`getline` 方法应该存储的最大数量，包括终止空字符。

- `delim`：`getline()` 停止的边界符。

最后，你可能想读取到文件末尾，但如何知道末尾在哪里？你可以使用 `eof()` 方法：

```cpp
int eof();
```

当到达文件末尾时，`eof()` 返回一个非零整数。

现在你可以将其整合起来并从 `"dragon.txt"` 文件读取。这里有一个示例实现：

```cpp
// 9.2 - 输入龙 - Dirk Henkemans
#include <fstream>
#include <iostream>
using namespace std;

int main(void)
{
    // 默认标志 ios::in
    ifstream dragons("dragons.txt");
    char buffer[50];
    if(!dragons.is_open())
    {
        cout << "Error opening file\n";
        // 非 0退出表示错误
        exit(1);
    }
    while(!dragons.eof()) {
      dragons.getline(buffer, 49);
      cout << buffer << "\n";
    }
    dragons.close();
    return 0;
}
```

输出：

Copper Dragon

Bronze Dragon

Silver Dragon

Gold Dragon

# 零基础 C++ 编程，第二版

| 方向 | 描述 |

| --- | --- |

| `ios::beg` | 偏移量从流的开始指定。 |

| `ios::cur` | 偏移量从指针当前位置向前指定。 |

| `ios::end` | 偏移量从流的末尾向前指定。 |

以下示例使用了刚刚讨论的几种方法来确定文件的大小：

```cpp
//9.3 - Binary File Size - Dirk Henkemans
#include <iostream>
#include <fstream>
using namespace std;
int main(void)
{
    int n1, n2;
    ifstream dragons("dragons.txt", ios::binary);
    n1 = dragons.tellg();
    dragons.seekg(0, ios::end);
    n2 = dragons.tellg();
    cout << "The size of dragons.txt is " << n2 - n1 << "\n";
    return 0;
}
```

输出:

The size of dragons.txt is 58

# 写入和读取二进制流

文件流引入了两个专门为数据顺序输入输出设计的方法：`ostream::write()` 和 `istream::read()`。这两个文件的原型如下：

```cpp
write(char * buffer, streamsize size);
read(char * buffer, streamsize size);
```

`write()` 将 `size` 指定的字节数放在 put 指针之后，从而将其写入文件。

`read()` 从 get 指针获取 `size` 指定的字节数，并将这些字节放置在 buffer 指针参数之后。

为了说明这两个方法，请查看以下程序，该程序读取 `"dragons.txt"` 文件并将其复制到名为 `"dragons2.txt"` 的文件中。

```cpp
//9.4 - File Copier - Dirk Henkemans
#include <iostream>
#include <fstream>
using namespace std;

int main(void)
{
    char buffer;
    int index = 0;

    // 文件名
    const char filename1[] = "dragons.txt";
    const char filename2[] = "dragons2.txt";

    // 打开文件
    fstream file1(filename1, ios::in);
    fstream file2(filename2, ios::out);

    // 指向文件开头
    file1.seekg(0, ios::beg);
    file2.seekp(0, ios::beg);

    // 读取第一个字符
    file1.read(&buffer, 1);

    // 写入剩余字符
    while(file1.good() && file2.good())
    {
        file2.write(&buffer, 1);
        index++;
        file1.seekp(index);
        file2.seekg(index);
        file1.read(&buffer, 1);
    }

    // 关闭文件
    file1.close();
    file2.close();

    return 0;
}
```

当你打开 `"dragons2.txt"` 时，它应该和 `"dragons.txt"` 相同。

## 使用常用的操作符

操作符用于操作流中的数据。例如，你可以使用某些操作符将所有小写字母转换为大写字母，或调整数字显示方式。大多数操作符包含在 `ios` 头文件中。在下一节中，你将只使用在 `ios` 头文件中常见的操作符。

虽然我们无法在书中列出所有的操作符，但表 9.5 列出了几个常用的操作符及其功能。

| 标记 | 功能 |

| --- | --- |

| `dec()` | 以十进制系统显示。 |

| `hex()` | 以十六进制系统显示。 |

| `oct()` | 以八进制系统显示。 |

| `fixed()` | 插入浮点值。 |

| `scientific()` | 使用科学计数法（指数）格式插入浮点值。 |

| `internal()` | 通过在内部插入空白来根据需要填充字段宽度。 |

| `left()` | 通过在右侧填充空白使字符左对齐。 |

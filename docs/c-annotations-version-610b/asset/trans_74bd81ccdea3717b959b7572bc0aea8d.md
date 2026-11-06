
流已打开。另请参见第 [6.4.2](#) 节的示例。

下面的示例演示了从二进制文件读取（另见第 [6.5.1.1](#) 节）：

```cpp
#include <fstream>
using namespace std;

int main(int argc, char **argv)
{
    ifstream in(argv[1]);
    double   value;

    // reads double in raw, binary form from file.
    in.read(reinterpret_cast<char *>(&value), sizeof(double));
}
```

### 6.5.3 从内存输入：类 'istringstream'

要使用流设施从内存读取信息，应使用 std::istringstream 对象。由于 istringstream 类派生自 istream 类，istream 的所有设施同样可用于 istringstream 对象。要使用和定义 istringstream 对象，必须包含头文件 sstream。此外，istringstream 类提供以下构造器和成员：

- `istringstream istr(string const &init, ios::openmode mode = ios::in);`
  
  该对象用 init 的内容初始化。
- `istringstream istr(ios::openmode mode = ios::in)` (此构造器通常用作默认构造器。示例：
  
    ```cpp
    std::istringstream in;
    ```
- `void str(std::string const &str);`
  
  当前对象使用新的初始内容重新初始化。

下面的示例演示了 istringstream 类的使用：从对象中提取若干值。这类 istringstream 对象最常用于进行“字符串到类型”的转换，例如将文本转换为 int 值（参见 C 的 atoi 函数）。格式化标志也可以与 istringstream 一起使用，因为它们是 iostream 类的一部分。在示例中，请特别注意成员 seekg 的使用：

```cpp
#include <iostream>
#include <sstream>
using namespace std;

int main()
{
        istringstream istr("123 345");  // store some text.
        int x;

        istr.seekg(2);                 // skip "12"
        istr >> x;                     // extract int
        cout << x << '\n';             // write it out
        istr.seekg(0);                 // retry from the beginning
        istr >> x;                     // extract int
        cout << x << '\n';             // write it out
        istr.str("666");       // store another text
        istr >> x;             // extract it
        cout << x << '\n';     // write it out
}
/*
   output of this program:
3
123
666
*/
```

### 6.5.4 复制流

通常，文件是通过逐字符或逐行读取源文件来复制的。处理流的基本模式如下：

- *持续循环：*
  - 1. 从流中读取
  - 2. 如果读取未成功（即 `fail` 返回 `true`），则跳出循环
  - 3. 处理所读取的信息

请注意，读取必须*先于*测试进行，因为只有在实际尝试从文件读取之后，才能知道读取是否成功。当然，也存在变体：`getline(istream &, string &)`（见第 6.5.1.1 节）返回一个 `istream &`，因此在这里读取和测试可以合并为一个表达式。尽管如此，上述模式代表了一般情况。因此，下面的程序可用于将 `cin` 复制到 `cout`：

```cpp
#include <iostream>
using namespace std;

int main()
{
    while (true)
    {
        char c;

        cin.get(c);
        if (cin.fail())
            break;
        cout << c;
    }
}
```

这里可以通过将 `get` 与 `if` 语句合并来简写，结果如下：

```cpp
if (!cin.get(c))
    break;
```

即便如此，这仍然遵循基本规则：“先读取，后测试”。

仅仅复制文件并不常见。更常见的情况是，文件先被处理到某一点，然后直接复制文件的其余信息。下面的程序说明了这一点。使用 `ignore` 跳过第一行（为了示例，假定第一行最多 80 个字符），第二条语句使用了 `<<` 运算符的另一个重载版本，其中将一个 `streambuf` 指针插入到流中。作为成员

```cpp
#include <iostream>
using namespace std;

int main()
{
    cin.ignore(80, '\n');   // skip the first line and...
    cout << cin.rdbuf();    // copy the rest through the streambuf *
}
```

这种复制流的方式仅假定存在一个 `streambuf` 对象。因此，它可以用于 `streambuf` 类的所有特化。

### 6.5.5 耦合流

Ostream 对象可以通过 `tie` 成员函数与 `ios` 对象*耦合*。耦合的结果是，每当对 `ios` 对象（该 `ostream` 对象被绑定到它）执行输入或输出操作时，都会刷新 `ostream` 的缓冲区。默认情况下，`cout` 绑定到 `cin`（使用 `cin.tie(cout)`）。这意味着每当请求对 `cin` 进行操作时，会首先刷新 `cout`。要解除绑定，可以调用 `ios::tie(0)`。在示例中：`cin.tie(0)`。

另一种有用的流耦合方式是 `cerr` 和 `cout` 之间的绑定。由于这种绑定，写到屏幕的标准输出和错误消息会与它们生成的时间同步显示：

```cpp
#include <iostream>
using namespace std;

int main()
{
    cerr.tie(0);        // untie
    cout << "first (buffered) line to cout ";
    cerr << "first (unbuffered) line to cerr\n";
    cout << "\n";

    cerr.tie(&cout);    // tie cout to cerr
    cout << "second (buffered) line to cout ";
    cerr << "second (unbuffered) line to cerr\n";
    cout << "\n";
}
/*
    Generated output:

    first (unbuffered) line to cerr
    first (buffered) line to cout
    second (buffered) line to cout second (unbuffered) line to cerr
*/
```

另一种耦合流的方式是让流使用一个公共的 `streambuf` 对象。这可以通过 `ios::rdbuf(streambuf *)` 成员函数来实现。这样，两个流可以使用例如各自的格式化，一个流可用于输入，另一个用于输出，并且可以实现使用流库而不是操作系统调用的重定向。参见以下各节的示例。

## 6.6 高级主题

### 6.6.1 重定向流

使用 `ios::rdbuf`，可以强制流共享它们的 `streambuf` 对象。因此，写入一个流的信息实际上会被写入另一个流；这种现象通常称为*重定向*。重定向通常在操作系统级别实现，有时这仍然是必要的（参见第 23.2.3 节）。

重定向有用的一种常见情况是，错误消息应写入文件而不是标准错误流（通常由其文件描述符编号 2 表示）。在使用 bash shell 的 Unix 操作系统中，可以如下实现：

```
program 2>/tmp/error.log
```

执行此命令后，由 `program` 写入的任何错误消息都会保存到文件 `/tmp/error.log` 中，而不是显示在屏幕上。

下面的示例展示了如何使用 `streambuf` 对象实现这一点。假设 `program` 期望一个参数来指定写入错误消息的文件名。它可以如下调用：

```
program /tmp/error.log
```

程序如下所示，在程序源代码之后提供了说明：

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main(int argc, char **argv)
{
    ofstream errlog;                              // 1
    streambuf *cerr_buffer = 0;                   // 2

    if (argc == 2)
    {
        errlog.open(argv[1]);                     // 3
        cerr_buffer = cerr.rdbuf(errlog.rdbuf()); // 4
    }
    else
    {
        cerr << "Missing log filename\n";
        return 1;
    }

    cerr << "Several messages to stderr, msg 1\n";
    cerr << "Several messages to stderr, msg 2\n";

    cout << "Now inspect the contents of " <<
        argv[1] << "... [Enter] ";
    cin.get();                                    // 5

    cerr << "Several messages to stderr, msg 3\n";

    cerr.rdbuf(cerr_buffer);                      // 6
    cerr << "Done\n";                             // 7
}
```



```cpp
:
    d_width(width),
    d_newWidth(true)
{}

inline field::field()
:
    d_newWidth(false)
{}
```

由于 field 将 Fistream 声明为其友元，因此 setField 可以直接检查 field 的成员。

现在回到 setField。该函数期望一个 field 对象的引用，该对象可以通过以下三种不同方式之一进行初始化：

- `field()`：当 setField 的参数是由其默认构造函数构造的 field 对象时，下一次提取将使用与上一次提取相同的字段宽度。
- `field(0)`：当此 field 对象用作 setField 的参数时，固定大小的字段提取停止，Fistream 再次像任何标准 istream 对象一样工作。
- `field(x)`：当 field 对象本身由非零的 size_t 值 x 初始化时，则下一次字段宽度为 x 个字符宽。此类 field 的准备工作留给 setBuffer，它是 Fistream 唯一的私有成员。

以下是 setField 的实现：

```cpp
std::istream & Fistream::setField(field const &params)
{
    if (params.d_newWidth)                         // new field size requested
        d_width = params.d_width;                  // set new width

    if (!d_width)                                  // no width?
        rdbuf(d_streambuf);                        // return to the old buffer
    else
        setBuffer();                               // define the extraction buffer

    return *this;
}
```

私有成员 setBuffer 定义一个包含 d_width + 1 个字符的缓冲区，并使用 read 将缓冲区填充为 d_width 个字符。该缓冲区以 ASCII-Z 字符终止。该缓冲区用于初始化 d_iss 成员。Fistream 的 rdbuf 成员用于通过 Fistream 对象本身提取 d_str 的数据：

```cpp
void Fistream::setBuffer()
{
    char *buffer = new char[d_width + 1];

    rdbuf(d_streambuf);                           // use istream’s buffer to
    buffer[read(buffer, d_width).gcount()] = 0;   // read d_width chars,
                                                 // terminated by ascii-Z
    d_iss.str(buffer);
    delete[] buffer;

    rdbuf(d_iss.rdbuf());                         // switch buffers
}
```

## 23.1. 将文件描述符与 FSTREAMBUF 类一起使用

尽管可以使用 setField 来配置 Fistream 使用或不使用固定大小的字段提取，但使用操纵器可能更可取。为了允许 field 对象用作操纵器，定义了一个重载的提取运算符。该提取运算符接受 istream & 和一个 field const & 对象。使用该提取运算符，类似以下语句

```cpp
fis >> field(2) >> x >> field(0);
```

是可能的（假设 fis 是一个 Fistream 对象）。以下是重载的 operator>> 及其声明：

```cpp
istream &std::operator>>(istream &str, field const &params)
{
    return reinterpret_cast<Fistream *>(&str)->setField(params);
}
```

声明：

```cpp
namespace std
{
    istream &operator>>(istream &str, FBB::field const &params);
}
```

最后是一个示例。以下程序使用 Fistream 对象对出现在其标准输入中的 URL 编码信息进行 URL 解码：

```cpp
int main()
{
    Fistream fis(cin);

    fis >> hex;
    while (true)
    {
        size_t x;
        switch (x = fis.get())
        {
            case '\n':
                cout << '\n';
                break;
            case '+':
                cout << ' ';
                break;
            case '%':
                fis >> field(2) >> x >> field(0);
                // FALLING THROUGH
            default:
                cout << static_cast<char>(x);
                break;
            case EOF:
                return 0;
        }
    }
}
/*
    Generated output after:
        echo My+name+is+%60Ed%27 | a.out

    My name is ‘Ed’
*/
```

## 23.2 ‘fork’ 系统调用

在 C 编程语言中，fork 系统调用广为人知。当程序需要启动一个新进程时，可以使用 system。fork 系统要求程序等待 *子进程* 终止。生成子进程的更通用方式是使用 `fork`。

在本节中，我们研究如何使用 C++ 围绕像 `fork` 这样的复杂系统调用包装类。本节后续的许多内容直接适用于 Unix 操作系统，因此讨论集中在该操作系统上。其他系统通常提供类似的功能。后续内容与 *模板设计模式* 密切相关（参见 *Gamma 等人*（1995）《设计模式》，Addison-Wesley）

当调用 fork 时，当前程序在内存中被复制，从而创建一个新进程。复制之后，两个进程都在 fork 系统调用之后继续执行。这两个进程可以检查 fork 的返回值：原进程（称为 *父进程*）中的返回值与新创建的进程（称为 *子进程*）中的返回值不同：

- 在 *父进程* 中，`fork` 返回由 `fork` 系统调用创建的（子）进程的 *进程 ID*。这是一个正整数值。
- 在 *子进程* 中，`fork` 返回 0。
- 如果 `fork` 失败，则返回 -1。

### 23.2.1 一个基本的 Fork 类

一个基本的 `Fork` 类应向用户隐藏像 `fork` 这样的系统调用的所有簿记细节。这里开发的 `Fork` 类正是这样做的。该类本身只确保 `fork` 系统调用的正确执行。通常，调用 `fork` 是为了启动一个子进程，这通常归结为执行一个单独的进程。该子进程可能期望从其标准输入流获得输入，和/或可能向其标准输出和/或标准错误流生成输出。`Fork` 并不知道所有这些，也不必知道子进程将做什么。`Fork` 对象应能够启动其子进程。

Fork 的构造函数无法知道其子进程应执行什么操作。同样，它也无法知道父进程应执行什么操作。针对这类情况，开发了 *模板方法设计模式*。根据 Gamma 等人，*模板方法设计模式*

> “在一个操作中定义算法的骨架，将一些步骤延迟到子类中。[模板方法]（设计模式）允许子类重新定义算法的某些步骤，而不改变算法的结构。”

这种设计模式允许我们定义一个 *抽象基类*，它已经提供与 `fork` 系统调用相关的基本步骤，并将 `fork` 系统调用其他部分的实现延迟到子类。

`Fork` 抽象基类具有以下特征：

- 它定义了一个数据成员 `d_pid`。在父进程中，该数据成员包含子进程的 *进程 ID*，而在子进程中其值为 0。其公共接口只声明两个成员：
  - 一个 `fork` 成员函数，负责实际的分叉（即创建（新的）子进程）；
  - 一个 `virtual` 析构函数 `~Fork`（函数体为空）。

以下是 Fork 的接口：

```cpp
class Fork
{
        int d_pid;

        public:
                virtual ~Fork();
                void fork();

        protected:
                int pid() const;
                int waitForChild();                 // returns the status

        private:
                virtual void childRedirections();
                virtual void parentRedirections();

                virtual void childProcess() = 0;    // pure virtual members
                virtual void parentProcess() = 0;
};
```

- 所有其他非虚成员函数都声明在类的受保护部分中，因此**只能**由派生类使用。它们是：

  - `pid()`：成员函数 `pid` 允许派生类访问系统 fork 的返回值：

```cpp
inline int Fork::pid() const
{
        return d_pid;
}
```

  - `waitForChild()`：成员 `int waitForChild` 可由父进程调用，以等待其子进程完成（如下所述）。该成员在类接口中声明。其实现为：

```cpp
#include "fork.hh"

int Fork::waitForChild()
{
        int status;

        waitpid(d_pid, &status, 0);

        return WEXITSTATUS(status);
}
```

这个简单的实现将子进程的 *退出状态* 返回给父进程。被调用的系统函数 `waitpid` 会 *阻塞*，直到子进程终止。

- 当使用 fork 系统调用时，必须始终区分 *父进程* 和 *子进程*。这些进程之间的主要区别在于：在父进程中，`d_pid` 成为子进程的进程 ID；而在子进程本身中，`d_pid` 变为 0。由于这两个进程必须始终被区分（并且存在），Fork 的接口强制要求由 `Fork` 派生的类实现它们：定义子进程操作的成员 `childProcess` 和定义父进程操作的成员 `parentProcess` 被定义为纯虚函数。

- 父进程与子进程之间的通信可以使用标准流或其他设施，例如 *管道*（参见第 23.2.5 节）。为便于这种进程间通信，派生类 *可以* 实现：

  - `childRedirections()`：如果必须在 *子* 进程中重定向任何标准流（`cin`、`cout` 或 `cerr`），则派生类应重写该成员（参见第 23.2.3 节）。默认情况下，它有一个空实现；


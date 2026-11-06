
- parentRedirections()：如果需要在父进程中重定向任何标准流（cin、cout 或 cerr），派生类应重写该成员。默认情况下，它有一个空实现。

如果父进程和子进程必须通过标准流相互通信，那么标准流的重定向就是必要的。下面是它们的默认定义。由于这些函数是虚函数，因此不应内联实现，而应在它们自己的源文件中实现：

```cpp
void Fork::childRedirections()
{}
void Fork::parentRedirections()
{}
```

### 23.2.2 父进程与子进程

成员函数 fork 调用系统函数 fork（注意：由于系统函数 fork 是由一个同名成员函数调用的，因此必须使用 `::` 作用域解析运算符来防止成员函数自身被递归调用）。函数 ::fork 的返回值决定调用 parentProcess 还是 childProcess。可能需要重定向。Fork::fork 的实现会在调用 childProcess 之前调用 childRedirections，并在调用 parentProcess 之前调用 parentRedirections：

```cpp
#include "fork.ih"

void Fork::fork()
{
    if ((d_pid = ::fork()) < 0)
        throw "Fork::fork() failed";

    if (d_pid == 0)            // child process has pid == 0
    {
        childRedirections();
        childProcess();
        exit(1);               // we shouldn't come here:
    }                          // childProcess() should exit

    parentRedirections();
    parentProcess();
}
```

在 fork.cc 中包含了类的内部头文件 fork.ih。这个头文件负责包含必要的系统头文件，以及包含 fork.h 本身。其实现为：

```cpp
#include "fork.h"
#include <cstdlib>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
```

子进程不应返回：一旦完成其任务，它们就应当终止。当子进程调用 exec... 家族中的成员时，这会自动发生；但如果子进程自身仍保持活动，那么它必须确保正确终止。子进程通常使用 exit 来终止自身，但要注意，exit 会阻止激活那些在与调用 exit 的层级相同或更浅的嵌套层级中定义的对象析构函数。全局定义对象的析构函数会在使用 exit 时被激活。当使用 exit 终止 childProcess 时，它要么应自身调用一个支持成员函数来定义它所需的所有嵌套对象，要么应在复合语句（例如，使用 `throw` 块）中定义其所有对象，并在该复合语句之外调用 `exit`。

父进程通常应等待其子进程完成。正在终止的子进程通过发送一个*信号*来通知其父进程它们即将终止，父进程应捕获该信号。如果子进程终止而其父进程没有捕获这些信号，那么这些子进程会作为所谓的*僵尸*进程继续可见。

如果父进程必须等待其子进程完成，它们可以调用成员 `waitForChild`。该成员会将子进程的退出状态返回给其父进程。

存在一种情况：*子*进程*继续*存活，但*父*进程死亡。这是相当自然的事件：父进程往往先于其子进程死亡。在我们的语境中（即 C++），这被称为*守护进程*程序。在守护进程中，父进程死亡，子程序继续作为基本 init 进程的子进程运行。同样，当子进程最终死亡时，会向其“继父”`init` 发送一个信号。这不会产生僵尸进程，因为 `init` 会捕获其所有（继）子进程的终止信号。鉴于 Fork 类的可用性，守护进程的构造非常简单（参见第 [23.2.4](23.2.4) 节）。

### 23.2.3 重定向再探

前面在第 [6.6.1](6.6.1) 节中，流是使用 `ios::rdbuf` 成员函数重定向的。通过将一个流的 `streambuf` 赋给另一个流，两个流对象访问同一个 `streambuf`，从而在编程语言本身层面实现重定向。

这在 C++ 程序的语境中可能没问题，但一旦离开该语境，重定向就会终止。操作系统并不知道流对象。例如，当程序使用系统调用启动子程序时就会遇到这种情况。本节末尾的示例程序使用 C++ 重定向将插入到 `cout` 的信息重定向到文件，然后调用

```cpp
system("echo hello world");
```

来输出一行众所周知的文本。由于 `echo` 将其信息写入标准输出，如果操作系统能识别 C++ 的重定向，这就会是程序对文件的重定向。

但重定向并没有发生。相反，`hello world` 仍然出现在程序的标准输出上，而被重定向的文件保持不变。要将 `hello world` 写入被重定向的文件，必须在操作系统层面实现重定向。一些操作系统（例如 Unix 及其同类系统）提供 `dup` 和 `dup2` 之类的系统调用来实现这一点。这些系统调用的使用示例见第 [23.2.5](23.2.5) 节。

下面是使用 `streambuf` 重定向进行 C++ 重定向之后，在系统层面*失败的重定向*示例：

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
using namespace std;

int main()
{
    ofstream of("outfile");

    streambuf *buf = cout.rdbuf(of.rdbuf());
    cout << "To the of the stream\n";
    system("echo hello world");
    cout << "To the of the stream\n";
    cout.rdbuf(buf);
}

/*
    Generated output: on the file 'outfile'

    To the of stream
    To the of stream

    On standard output:

    hello world
*/
```

### 23.2.4 ‘守护进程’程序

有些应用只把 `fork` 用于启动子进程。父进程在生成子进程后立即终止。如果发生这种情况，子进程会继续作为 `init` 的子进程运行，而 `init` 是 Unix 系统上始终运行的第一个进程。这样的进程通常被称为*守护进程*，作为后台进程运行。

尽管下一个示例可以很容易地写成普通 C 程序，但它仍被收录在 C++ Annotations 中，因为它与当前对 `Fork` 类的讨论密切相关。我曾考虑给该类添加一个 `daemon` 成员，但最终决定不这样做，因为守护进程程序的构造非常简单，并且除了 `Fork` 类当前提供的功能之外不需要任何其他特性。下面是一个说明如何构造此类守护进程程序的示例。它的子进程不执行 `exit`，而是执行 `throw 0`，该异常由子进程 `main` 函数的 `catch` 子句捕获。这样做可确保子进程定义的所有对象都被正确销毁：

```cpp
#include <iostream>
#include <unistd.h>
#include "fork.h"

class Daemon: public Fork
{
    virtual void parentProcess()        // the parent does nothing.
    {}
    virtual void childProcess()         // actions by the child
    {
        sleep(3);

        std::cout << "Hello from the child process\n"; // just a message...
        throw 0;                        // The child process ends
    }
};

int main()
try
{
    Daemon().fork();
}
catch(...)
{}

/*
    Generated output:

The next command prompt, then after 3 seconds:
Hello from the child process
*/
```

### 23.2.5 ‘Pipe’类

系统层面的重定向需要使用由 pipe 系统调用创建的*文件描述符*。当两个进程希望使用这样的文件描述符进行通信时，会发生以下情况：

- 该进程使用 pipe 系统调用构造两个*关联的文件描述符*。其中一个文件描述符用于写入，另一个文件描述符用于读取。

- 进行 fork（即调用系统 fork 函数），复制这些文件描述符。现在我们有四个文件描述符，因为子进程和父进程都拥有由 pipe 创建的两个文件描述符各自的副本。

- 一个进程（例如父进程）使用这些文件描述符进行*读取*。它应关闭其用于*写入*的文件描述符。

- 另一个进程（例如子进程）使用这些文件描述符进行*写入*。因此它应关闭其用于*读取*的文件描述符。

- 子进程写入用于写入的文件描述符的所有信息，现在都可以由父进程从对应的用于读取的文件描述符中读取，从而在子进程和父进程之间建立通信通道。

尽管这基本上很简单，但错误很容易混入。两个进程（子进程或父进程）可用的文件描述符的功能很容易被混淆。为防止簿记错误，可以先将簿记正确设置一次，然后将其隐藏在像这里开发的 `Pipe` 类这样的类中。让我们看一下它的特征（在使用 pipe 和 dup 之类的函数之前，编译器必须已经读取了 `<unistd.h>` 头文件）：

- pipe 系统调用期望一个指向两个 int 值的指针，这两个值分别表示用于读取的文件描述符和用于写入的文件描述符。为避免混淆，`Pipe` 类定义了一个 enum，其值将 2 个 int 数组的索引与符号常量关联起来。这两个文件描述符本身存储在数据成员 `d_fd` 中。下面是该类接口的起始部分：

```cpp
class Pipe
{
    enum  RW  { READ, WRITE };
    int      d_fd[2];
```

- 该类只需要一个默认构造函数。该构造函数调用 `pipe` 创建一组关联的文件描述符，用于访问管道两端：

```cpp
Pipe::Pipe()
{
    if (pipe(d_fd))
        throw "Pipe::Pipe(): pipe() failed";
}
```

- 成员 `readOnly` 和 `readFrom` 用于配置管道的读取端。后一个函数在使用重定向时使用。它会获得一个备用文件描述符，用于从管道读取。通常这个备用文件描述符是 `STDIN_FILENO`，允许 `cin` 从管道提取信息。前一个函数仅用于配置管道的读取端。它关闭匹配的写入端，并返回一个可用于从管道读取的文件描述符：

```cpp
int Pipe::readOnly()
{
    close(d_fd[WRITE]);
    return d_fd[READ];
}
```

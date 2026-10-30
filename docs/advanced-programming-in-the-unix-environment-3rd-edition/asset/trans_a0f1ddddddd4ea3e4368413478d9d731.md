

请注意，有些处理文件描述符标志的现有程序并不使用常量 FD_CLOEXEC。相反，这些程序将标志设置为 0（不关闭-on-exec，默认值）或 1（执行关闭-on-exec）。

## F_GETFL

返回 fd 的文件状态标志作为函数的值。我们在描述 open 函数时描述了文件状态标志。它们列在图 3.10 中。

| 文件状态标志 | 描述 |
|---|---|
| O_RDONLY | 仅用于读取打开 |
| O_WRONLY | 仅用于写入打开 |
| O_RDWR | 用于读写打开 |
| O_EXEC | 仅用于执行打开 |
| O_SEARCH | 仅用于搜索打开目录 |
| O_APPEND | 每次写入时追加 |
| O_NONBLOCK | 非阻塞模式 |
| O_SYNC | 等待写入完成（数据和属性） |
| O_DSYNC | 等待写入完成（仅数据） |
| O_RSYNC | 同步读写 |
| O_FSYNC | 等待写入完成（仅 FreeBSD 和 Mac OS X） |
| O_ASYNC | 异步 I/O（仅 FreeBSD 和 Mac OS X） |

图 3.10 fcntl 的文件状态标志

不幸的是，五个访问模式标志——O_RDONLY、O_WRONLY、O_RDWR、O_EXEC 和 O_SEARCH——并不是可以测试的独立位。（正如我们之前提到的，出于历史原因，前三个通常分别具有值 0、1 和 2。此外，这五个值是互斥的；一个文件只能启用其中一个。）因此，我们必须首先使用 O_ACCMODE 掩码获得访问模式位，然后将结果与五个值中的任何一个进行比较。

## F_SETFL

将文件状态标志设置为第三个参数的值（作为整数）。唯一可以更改的标志是 O_APPEND、O_NONBLOCK、O_SYNC、O_DSYNC、O_RSYNC、O_FSYNC 和 O_ASYNC。

## F_GETOWN

获取当前接收 SIGIO 和 SIGURG 信号的进程 ID 或进程组 ID。我们在第 14.5.2 节中描述了这些异步 I/O 信号。

## F_SETOWN

设置接收 SIGIO 和 SIGURG 信号的进程 ID 或进程组 ID。positive arg 指定进程 ID。negative arg 意味着进程组 ID 等于 arg 的绝对值。

fcntl 的返回值取决于命令。所有命令在出错时返回 –1，或在正常时返回其他值。以下四个命令具有特殊的返回值：F_DUPFD、F_GETFD、F_GETFL 和 F_GETOWN。第一个命令返回新的文件描述符，接下来的两个返回相应的标志，最后一个命令返回正的进程 ID 或负的进程组 ID。

## 示例

图 3.11 中的程序接受一个命令行参数，指定一个文件描述符，并打印该描述符的所选文件标志的描述。

```
#include "apue.h"
#include <fcntl.h>
int
main(int argc, char *argv[])
{
    int     val;
    if (argc != 2)
        err_quit("usage: a.out <descriptor#>");
    if ((val = fcntl(atoi(argv[1]), F_GETFL, 0)) < 0)
        err_sys("fcntl error for fd %d", atoi(argv[1]));
    switch (val & O_ACCMODE) {
    case O_RDONLY:
        printf("read only");
        break;
    case O_WRONLY:
        printf("write only");
        break;
    case O_RDWR:
        printf("read write");
        break;
    default:
        err_dump("unknown access mode");
    }
    if (val & O_APPEND)
        printf(", append");
    if (val & O_NONBLOCK)
        printf(", nonblocking");
    if (val & O_SYNC)
        printf(", synchronous writes");
#if !defined(_POSIX_C_SOURCE) && defined(O_FSYNC) && (O_FSYNC != O_SYNC)
    if (val & O_FSYNC)
        printf(", synchronous writes");
#endif
    putchar('\n');
    exit(0);
}
```

图 3.11 打印指定描述符的文件标志

请注意，我们使用特性测试宏 _POSIX_C_SOURCE 并有条件地编译不是 POSIX.1 部分的文件访问标志。以下脚本显示了从 bash（Bourne-again shell）调用程序时的操作。结果会根据使用的 shell 而有所不同。

```
$ ./a.out 0 < /dev/tty
read only
$ ./a.out 1 > temp.foo
$ cat temp.foo
write only
$ ./a.out 2 2>>temp.foo
write only, append
$ ./a.out 5 5<>temp.foo
read write
```

子句 5<>temp.foo 在文件描述符 5 上以读写方式打开文件 temp.foo。

## 示例

当我们修改文件描述符标志或文件状态标志时，我们必须小心地获取现有标志值，按需修改它，然后设置新的标志值。我们不能简单地发出 F_SETFD 或 F_SETFL 命令，因为这可能会关闭之前设置的标志位。

图 3.12 显示了一个设置描述符的一个或多个文件状态标志的函数。

```
#include "apue.h"
#include <fcntl.h>

void
set_fl(int fd, int flags) /* flags are file status flags to turn on */
{
    int val;

    if ((val = fcntl(fd, F_GETFL, 0)) < 0)
        err_sys("fcntl F_GETFL error");

    val |= flags;        /* turn on flags */
    if (fcntl(fd, F_SETFL, val) < 0)
        err_sys("fcntl F_SETFL error");
}
```

图 3.12 打开描述符的一个或多个文件状态标志

如果我们将中间语句改为

```
val &= ~flags;    /* turn flags off */
```

我们就有一个名为 clr_fl 的函数，我们将在一些后面的示例中使用它。该语句将 flags 的 one's complement 与当前的 val 进行逻辑 AND。

如果我们在图 3.5 所示程序的开头添加行

```
set_fl(STDOUT_FILENO, O_SYNC);
```

我们将打开同步写入标志。这会导致每次写入等待数据写入磁盘后才返回。通常在 UNIX 系统中，写入只是将数据排队以供写入；实际的磁盘写入操作可能在稍后进行。数据库系统是使用 O_SYNC 的可能候选者，以便在写入返回时知道数据是否已实际写入磁盘，以防发生异常系统故障。

我们预计 O_SYNC 标志会增加程序运行时系统的 CPU 时间和时钟时间。为了测试这一点，我们可以运行图 3.5 中的程序，从磁盘上的一个文件复制 492.6 MB 的数据到另一个文件，并将其与使用 O_SYNC 标志设置相同操作的版本进行比较。Linux 系统使用 ext4 文件系统的结果显示在图 3.13 中。

| 操作 | 用户 CPU（秒） | 系统 CPU（秒） | 时钟时间（秒） |
|---|---|---|---|
| 图 3.6 中 BUFFSIZE = 4,096 的读取时间 | 0.03 | 0.58 | 8.62 |
| 正常写入磁盘文件 | 0.00 | 1.05 | 9.70 |
| 设置 O_SYNC 写入磁盘文件 | 0.02 | 1.09 | 10.28 |
| 写入磁盘后跟 fdatasync | 0.02 | 1.14 | 17.93 |
| 写入磁盘后跟 fsync | 0.00 | 1.19 | 18.17 |
| 设置 O_SYNC 写入磁盘后跟 fsync | 0.02 | 1.15 | 17.88 |

图 3.13 使用各种同步机制的 Linux ext4 定时结果

图 3.13 中的六行都是使用 BUFFSIZE 为 4,096 字节测量的。图 3.6 中的结果是在读取磁盘文件并写入 /dev/null 时测量的，因此没有磁盘输出。图 3.13 中的第二行对应于读取磁盘文件并写入另一个磁盘文件。这就是为什么图 3.13 中的第一行和第二行不同。当我们写入磁盘文件时，系统时间会增加，因为内核现在从我们的进程复制数据并将数据排队以供磁盘驱动程序写入。我们预计当我们写入磁盘文件时，时钟时间也会增加。

当我们启用同步写入时，系统和时钟时间应该显著增加。正如第三行所示，同步写入的系统时间并没有比使用延迟写入时更昂贵。这意味着 Linux 操作系统对延迟写入和同步写入所做的工作量相同（这不太可能），或者 O_SYNC 标志没有产生预期的效果。在这种情况下，Linux 操作系统不允许我们使用 fcntl 设置 O_SYNC 标志，而是失败但不返回错误（但如果我们能够在打开文件时指定该标志，它就会遵守该标志）。

最后三行中的时钟时间反映了等待所有写入提交到磁盘所需的额外时间。同步写入文件后，我们预计对 fsync 的调用将没有效果。这种情况应该由最后


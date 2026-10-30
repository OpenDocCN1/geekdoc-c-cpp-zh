

```c
printf("pw_passwd = %s\n", ptr->pw_passwd == NULL || ptr->pw_passwd[0] == 0 ? "(null)" : ptr->pw_passwd);
exit(0);
}
```

## 图 C.6 在 FreeBSD 和 Mac OS X 下打印加密密码

## 6.5

图 C.7 所示的程序以类似于 `date` 命令的格式打印日期。

```c
#include "apue.h"
#include <time.h>

int
main(void)
{
    time_t      caltime;
    struct tm   *tm;
    char        line[MAXLINE];

    if ((caltime = time(NULL)) == -1)
        err_sys("time error");
    if ((tm = localtime(&caltime)) == NULL)
        err_sys("localtime error");
    if (strftime(line, MAXLINE, "%a %b %d %X %Z %Y\n", tm) == 0)
        err_sys("strftime error");
    fputs(line, stdout);
    exit(0);
}
```

## 图 C.7 以类似于 date(1) 的格式打印时间和日期

运行此程序得到：

```text
$ ./a.out
Wed Jul 25 22:58:32 EDT 2012
$ TZ=US/Mountain ./a.out
Wed Jul 25 20:58:32 MDT 2012
$ TZ=Japan ./a.out
Thu Jul 26 11:58:32 JST 2012
```

作者的默认时区是美国东部时区。

美国山区时区。

日本。

## 第 7 章

## 7.1

`printf` 的返回值（输出的字符数）似乎成为了 `main` 的返回值。为了验证这一理论，可以更改所打印字符串的长度，看看新的长度是否与返回值匹配。请注意，并非所有系统都表现出这一特性。此外还要注意，如果在 gcc 中启用 ISO C 扩展，那么按照标准要求，返回值始终为 0。

## 7.2

以交互方式运行程序时，标准输出通常是行缓冲的，因此实际输出会在每个换行符输出时发生。但是，如果将标准输出重定向到文件，它可能会采用全缓冲方式，实际输出要等到标准 I/O 清理完成后才会发生。

## 7.3

在大多数 UNIX 系统中，无法做到这一点。`argc` 和 `argv` 的副本不会像 `environ` 那样保存在全局变量中。

## 7.4

当进程尝试解引用空指针这一常见的 C 编程错误时，这提供了一种终止进程的方法。

## 7.5

定义如下：

```c
typedef void Exitfunc(void);
int atexit(Exitfunc *func);
```

## 7.6

`calloc` 会将其分配的内存初始化为全 0 位。ISO C 并不保证这与浮点数 0 或空指针相同。

## 7.7

堆和栈直到程序被 `exec` 函数之一执行时才会分配（参见第 8.10 节）。

## 7.8

可执行文件（`a.out`）包含符号表信息，这些信息有助于调试 core 文件。要移除这些信息，请使用 `strip(1)` 命令。剥离两个 `a.out` 文件后，其大小分别减少为 798,760 字节和 6,200 字节。

## 7.9

不使用共享库时，可执行文件中很大一部分空间由标准 I/O 库占用。

## 7.10

该代码是错误的，因为它在自动变量已经不存在之后，仍通过指针引用自动整型变量 `val`。在复合语句起始左花括号之后声明的自动变量，会在匹配的右花括号之后消失。

## 第 8 章

## 8.1

为了模拟子进程退出时关闭标准输出的行为，可以在子进程调用 `exit` 之前添加以下代码行：

```c
fclose(stdout);
```

要查看这样做的影响，请将对 `printf` 的调用替换为以下代码行：

```c
i = printf("pid = %ld, glob = %d, var = %d\n", (long)getpid(), glob, var);
sprintf(buf, "%d\n", i);
write(STDOUT_FILENO, buf, strlen(buf));
```

还需要定义变量 `i` 和 `buf`。

这里假设子进程调用 `exit` 时关闭的是标准 I/O 流 `stdout`，而不是文件描述符 `STDOUT_FILENO`。某些版本的标准 I/O 库会关闭与标准输出关联的文件描述符，这会导致向标准输出的 `write` 操作也失败。在这种情况下，应将标准输出 `dup` 到另一个描述符，并使用这个新描述符进行写操作。

## 8.2

请考虑图 C.8。

```c
#include "apue.h"

static void f1(void), f2(void);

int
main(void)
{
    f1();
    f2();
    _exit(0);
}

static void
f1(void)
{
    pid_t pid;

    if ((pid = vfork()) < 0)
        err_sys("vfork error");
    /* child and parent both return */
}

static void
f2(void)
{
    char buf[1000];      /* automatic variables */
    int i;
    for (i = 0; i < sizeof(buf); i++)
        buf[i] = 0;
}
```

**图 C.8 `vfork` 的错误用法**

调用 `vfork` 时，父进程的栈指针指向调用 `vfork` 的 `f1` 函数的栈帧。图 C.9 展示了这一点。`vfork` 会使子进程先执行，子进程从 `f1` 返回。随后，子进程调用 `f2`，其栈帧会覆盖之前 `f1` 的栈帧。接着，子进程将自动变量 `buf` 清零，把栈帧中的 1,000 个字节设置为 0。子进程从 `f2` 返回，然后调用 `_exit`，但 `main` 的栈帧下方的栈内容已经发生改变。之后父进程在 `vfork` 调用之后恢复执行，并从 `f1` 返回。返回信息通常存储在栈帧中，而这些信息很可能已被子进程修改。父进程恢复执行后，此示例会发生什么取决于 UNIX 系统的许多实现细节（返回信息存储在栈帧中的位置、修改自动变量时栈帧中的哪些信息被覆盖，等等）。通常的结果是生成一个 core 文件，但你的结果可能不同。

![](img/244bf0c3b6d0288ae397336907e37851_955_0.png)

## 8.4

在图 8.13 中，我们让父进程先写出其输出。父进程完成后，子进程写出自己的输出，但我们让父进程终止。父进程终止还是子进程先完成输出，取决于内核如何调度这两个进程（这是另一个竞态条件）。当父进程终止时，shell 会启动下一个程序，而这个程序可能会干扰前一个子进程的输出。

我们可以让父进程等到子进程也完成输出后再终止，从而防止这种情况发生。将 `fork` 后面的代码替换为以下内容：

```c
else if (pid == 0) {
    WAIT_PARENT();          /* parent goes first */
    charatime("output from child\n");
    TELL_PARENT(getppid()); /* tell parent we're done */
} else {
    charatime("output from parent\n");
    TELL_CHILD(pid);        /* tell child we're done */
    WAIT_CHILD();           /* wait for child to finish */
}
```

如果让子进程先执行，就不会看到这种情况，因为 shell 要等到父进程终止后才会启动下一个程序。

## 8.5

对于 `argv[2]`，打印出的值相同（`/home/sar/bin/testinterp`）。原因是，`execvp` 最终会使用与直接调用 `exec1` 时相同的路径名调用 `execve`。回顾图 8.15。

## 8.6

图 C.10 中的程序会创建一个僵尸进程。

```c
#include "apue.h"

#ifdef SOLARIS
#define PSCMD "ps -a -o pid,ppid,s,tty,comm"
#else
#define PSCMD "ps -o pid,ppid,state,tty,command"
#endif

int
main(void)
{
    pid_t pid;

    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid == 0)    /* child */
        exit(0);

    /* parent */
    sleep(4);
    system(PSCMD);

    exit(0);
}
```

**图 C.10 创建僵尸进程并使用 `ps` 查看其状态**

通常，`ps(1)` 会将僵尸进程的状态标记为 Z：

```text
$ ./a.out
PID PPID S TT     COMMAND
2369 2208 S pts/2  -bash
7230 2369 S pts/2  ./a.out
7231 7230 Z pts/2  [a.out] <defunct>
7232 7230 S pts/2  sh -c ps -o pid,ppid,state,tty,command
7233 7232 R pts/2  ps -o pid,ppid,state,tty,command
```

## 第 9 章

## 9.1

`init` 进程能够得知终端用户何时注销，因为 `init` 是登录 shell 的父进程，并且会在登录 shell 终止时接收到 `SIGCHLD` 信号。

然而，对于网络登录，`init` 并不参与其中。相反，`utmp` 和 `wtmp` 文件中的登录条目及其对应的注销条目，通常由处理登录并检测注销的进程写入（在我们的示例中是 `telnetd`）。


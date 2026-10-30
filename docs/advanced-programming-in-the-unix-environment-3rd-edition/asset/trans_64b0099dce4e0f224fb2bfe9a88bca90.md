
```c
#include <stdio.h>
FILE *
open_data(void)
{
    FILE *fp;
    char databuf[BUFSIZ]; /* setvbuf makes this the stdio buffer */
    if ((fp = fopen("datafile", "r")) == NULL)
        return(NULL);
    if (setvbuf(fp, databuf, _IOLBF, BUFSIZ) != 0)
        return(NULL);
    return(fp);    /* error */
}
```

## 图 7.14 自动变量的不正确使用

问题是当 open_data 返回时，它在栈上使用的空间将被下一个被调用函数的栈帧所使用。但标准 I/O 库仍将使用该部分内存作为其流缓冲区。这必然导致混乱。要修正这个问题，数组 databuf 需要从全局内存中分配，要么静态分配（static 或 extern），要么动态分配（某个 alloc 函数）。

## 7.11 getrlimit 和 setrlimit 函数

每个进程都有一组资源限制，其中一些可以通过 getrlimit 和 setrlimit 函数进行查询和更改。

```c
#include <sys/resource.h>

int getrlimit(int resource, struct rlimit *rlptr);

int setrlimit(int resource, const struct rlimit *rlptr);

Both return: 0 if OK, -1 on error
```

这两个函数在单一 UNIX 规范中被定义在 XSI 选项中。进程的资源限制通常由进程 0 在系统初始化时建立，然后由每个后续进程继承。每种实现都有自己的方式来调整各种限制。

每次调用这两个函数时，需要指定一个资源以及指向以下结构的指针：

```c
struct rlimit {
    rlim_t rlim_cur;  /* soft limit: current limit */
    rlim_t rlim_max;  /* hard limit: maximum value for rlim_cur */
};
```

有三条规则支配资源限制的更改。

- 1. 进程可以将其软限制更改为小于或等于硬限制的值。
- 2. 进程可以将其硬限制降低为大于或等于软限制的值。对于普通用户而言，降低硬限制是不可逆的。
- 3. 只有超级用户进程才能提高硬限制。

无限限制由常量 RLIM_INFINITY 指定。

resource 参数取以下值之一。图 7.15 显示了单一 UNIX 规范定义了哪些限制，以及每种实现支持哪些限制。

RLIMIT_AS    进程总可用内存的最大字节数。这会影响 sbrk 函数（第 1.11 节）和 mmap 函数（第 14.8 节）。

RLIMIT_CORE   核心文件的最大字节数。限制为 0 会阻止创建核心文件。

RLIMIT_CPU    CPU 时间的最大秒数。当超过软限制时，会向进程发送 SIGXCPU 信号。

RLIMIT_DATA    数据段的最大字节数：即图 7.6 中初始化数据、未初始化数据和堆的总和。

RLIMIT_FSIZE    可创建文件的最大字节数。当超过软限制时，会向进程发送 SIGXFSZ 信号。

RLIMIT_MEMLOCK    进程可以使用 mlock(2) 锁定到内存中的最大内存字节数。

RLIMIT_RSS  最大驻留集大小（RSS），以字节为单位。如果可用物理内存不足，内核会从超过其 RSS 的进程中回收内存。

RLIMIT_SBSIZE  用户在任意给定时间可以消耗的套接字缓冲区最大字节数。

RLIMIT_SIGPENDING  可以为进程排队的最大信号数。此限制由 sigqueue 函数（第 10.20 节）强制执行。

RLIMIT_STACK  栈的最大字节数。参见图 7.6。

RLIMIT_SWAP  用户可以消耗的最大交换空间字节数。

RLIMIT_VMEM  这是 RLIMIT_AS 的同义词。

| 限制 | XSI | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|---|
| RLIMIT_AS | • | • |  |  | • |
| RLIMIT_CORE | • | • | • | • | • |
| RLIMIT_CPU | • | • | • | • | • |
| RLIMIT_DATA | • | • | • | • | • |
| RLIMIT_FSIZE | • | • | • | • | • |
| RLIMIT_MEMLOCK |  | • | • | • |  |
| RLIMIT_MSGQUEUE |  |  | • |  |  |
| RLIMIT_NICE |  |  | • |  |  |
| RLIMIT_NOFILE | • | • | • | • | • |
| RLIMIT_NPROC |  | • | • | • |  |
| RLIMIT_NPTS |  | • |  |  |  |
| RLIMIT_RSS |  | • | • | • |  |
| RLIMIT_SBSIZE |  | • |  |  |  |
| RLIMIT_SIGPENDING |  |  | • |  |  |
| RLIMIT_STACK | • | • | • | • | • |
| RLIMIT_SWAP |  | • |  |  |  |
| RLIMIT_VMEM |  |  |  |  | • |

图 7.15 资源限制的支持

资源限制影响调用进程，并被其所有子进程继承。这意味着资源限制的设置需要内建到 shell 中，才能影响我们未来的所有进程。确实，Bourne shell、GNU Bourne-again shell 和 Korn shell 都有内建的 ulimit 命令，而 C shell 有内建的 limit 命令。（umask 和 chdir 函数也必须作为 shell 内建命令来处理。）

## 示例

图 7.16 中的程序会打印系统支持的所有资源限制的当前软限制和硬限制。为了在各种实现上编译此程序，我们有条件地包含了那些不同的资源名称。请注意，某些系统将 rlim_t 定义为 unsigned long long 而不是 unsigned long。这个定义甚至可能在同一个系统上发生变化，具体取决于我们是否编译程序以支持 64 位文件。某些限制适用于文件大小，因此 rlim_t 类型必须足够大，以表示文件大小限制。为了避免使用错误格式说明符导致编译器警告，我们先将限制复制到一个 64 位整数中，这样只需处理一种格式。

```c
#include "apue.h"
#include <sys/resource.h>

#define doit(name) pr_limits(#name, name)

static void pr_limits(char *, int);

int
main(void)
{
#ifdef RLIMIT_AS
    doit(RLIMIT_AS);
#endif

    doit(RLIMIT_CORE);
    doit(RLIMIT_CPU);
    doit(RLIMIT_DATA);
    doit(RLIMIT_FSIZE);

#ifdef RLIMIT_MEMLOCK
    doit(RLIMIT_MEMLOCK);
#endif

#ifdef RLIMIT_MSGQUEUE
    doit(RLIMIT_MSGQUEUE);
#endif

#ifdef RLIMIT_NICE
    doit(RLIMIT_NICE);
#endif

    doit(RLIMIT_NOFILE);

#ifdef RLIMIT_NPROC
    doit(RLIMIT_NPROC);
#endif

#ifdef RLIMIT_NPTS
    doit(RLIMIT_NPTS);
#endif

#ifdef RLIMIT_RSS
    doit(RLIMIT_RSS);
#endif

#ifdef RLIMIT_SBSIZE
    doit(RLIMIT_SBSIZE);
#endif

#ifdef RLIMIT_SIGPENDING
    doit(RLIMIT_SIGPENDING);
#endif

    doit(RLIMIT_STACK);

#ifdef RLIMIT_SWAP
    doit(RLIMIT_SWAP);
#endif

#ifdef RLIMIT_VMEM
    doit(RLIMIT_VMEM);
#endif
}
    exit(0);
}
static void
pr_limits(char *name, int resource)
{
    struct rlimit  limit;
    unsigned long  long lim;
    if (getrlimit(resource, &limit) < 0)
        err_sys("getrlimit error for %s", name);
    printf("%-14s", name);
    if (limit.rlim_cur == RLIM_INFINITY) {
        printf("(infinite) ");
    } else {
        lim = limit.rlim_cur;
        printf("%10lld ", lim);
    }
    if (limit.rlim_max == RLIM_INFINITY) {
        printf("(infinite)");
    } else {
        lim = limit.rlim_max;
        printf("%10lld", lim);
    }
    putchar((int)'\n');
}
```

## 图 7.16 打印当前资源限制

注意，我们在 doit 宏中使用了 ISO C 的字符串创建运算符（#），为每个资源名生成字符串值。当我们写

```
doit(RLIMIT_CORE);
```

C 预处理器会将其扩展为

```
pr_limits("RLIMIT_CORE", RLIMIT_CORE);
```

在 FreeBSD 下运行此程序，我们得到以下输出：

```
$ ./a.out
RLIMIT_AS      (infinite)    (infinite)
RLIMIT_CORE    (infinite)    (infinite)
RLIMIT_CPU     (infinite)    (infinite)
RLIMIT_DATA    536870912     536870912
RLIMIT_FSIZE   (infinite)    (infinite)
RLIMIT_MEMLOCK (infinite)    (infinite)
RLIMIT_NOFILE  3520          3520
RLIMIT_NPROC   1760          1760
RLIMIT_NPTS    (infinite)    (infinite)
RLIMIT_RSS     (infinite)    (infinite)
RLIMIT_SBSIZE  (infinite)    (infinite)
RLIMIT_STACK   67108864      67108864
RLIMIT_SWAP    (infinite)    (infinite)
RLIMIT_VMEM    (infinite)    (infinite)
```

Solaris 给出以下结果：

```
$ ./a.out
RLIMIT_AS      (infinite)    (infinite)
RLIMIT_CORE    (infinite)    (infinite)
RLIMIT_CPU     (infinite)    (infinite)
RLIMIT_DATA    (infinite)    (infinite)
RLIMIT_FSIZE   (infinite)    (infinite)
RLIMIT_NOFILE  256           65536
RLIMIT_STACK   8388608       (infinite)
RLIMIT_VMEM    (infinite)    (infinite)
```

习题 10.11 将在我们介绍完信号后继续讨论资源限制。

## 7.12 小结

理解 UNIX 系统环境中 C 程序的环境，是理解 UNIX 系统进程控制特性的先决条件。在本章中，我们了解了进程如何启动、如何终止，以及如何向进程传递参数列表和环境。虽然参数列表和环境都不由内核解释，但正是内核将这两者从 exec 的调用者传递给新进程。

我们还检查了 C 程序的典型内存布局，并了解了进程如何动态分配和释放内存。详细研究可用于操作环境的函数是值得的，因为它们涉及内存分配。我们还介绍了 setjmp 和 longjmp 函数，它们提供了一种在进程内执行非局部跳转的方法。本章最后描述了各种实现提供的资源限制。


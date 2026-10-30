

可选命令参数。运行 10 秒后，两个进程打印其计数器的值并退出。通过比较不同 nice 值下的计数器值，我们可以了解 nice 值如何影响进程调度。

```
#include "apue.h"
#include <errno.h>
#include <sys/time.h>

#if defined(MACOS)
#include <sys/syslimits.h>
#elif defined(SOLARIS)
#include <limits.h>
#elif defined(BSD)
#include <sys/param.h>
#endif

unsigned long long count;
struct timeval end;

void
checktime(char *str)
{
        struct timeval tv;

        gettimeofday(&tv, NULL);
        if (tv.tv_sec >= end.tv_sec && tv.tv_usec >= end.tv_usec) {
                printf("%s count = %lld\n", str, count);
                exit(0);
        }
}

int
main(int argc, char *argv[])
{
        pid_t   pid;
        char    *s;
        int     nzero, ret;
        int     adj = 0;

        setbuf(stdout, NULL);
#if defined(NZERO)
        nzero = NZERO;
#elif defined(_SC_NZERO)
        nzero = sysconf(_SC_NZERO);
#else
#error NZERO undefined
#endif

        printf("NZERO = %d\n", nzero);
        if (argc == 2)
                adj = strtol(argv[1], NULL, 10);
        gettimeofday(&end, NULL);
        end.tv_sec += 10;   /* run for 10 seconds */
        if ((pid = fork()) < 0) {
err_sys("fork failed");
} else if (pid == 0) {  /* child */
    s = "child";
    printf("current nice value in child is %d, adjusting by %d\n", nice(0)+nzero, adj);
    errno = 0;
    if ((ret = nice(adj)) == -1 && errno != 0)
        err_sys("child set scheduling priority");
    printf("now child nice value is %d\n", ret+nzero);
} else {  /* parent */
    s = "parent";
    printf("current nice value in parent is %d\n", nice(0)+nzero);
}
for(;;) {
    if (++count == 0)
        err_quit("%s counter wrap", s);
    checktime(s);
}
```

## 图 8.30 评估更改 nice 值的影响

我们运行该程序两次：一次使用默认的 nice 值，一次使用最高的合法 nice 值（最低调度优先级）。我们在单处理器 Linux 系统上运行此程序，以展示调度程序如何在具有不同 nice 值的进程之间共享 CPU。在系统基本空闲的情况下，多处理器系统（或多核 CPU）将允许两个进程同时运行，而无需共享 CPU，我们就不会在具有不同 nice 值的两个进程之间看到太多差异。

```
$ ./a.out
NZERO = 20
current nice value in parent is 20
current nice value in child is 20, adjusting by 0
now child nice value is 20
child count = 1859362
parent count = 1845338
$ ./a.out 20
NZERO = 20
current nice value in parent is 20
current nice value in child is 20, adjusting by 20
now child nice value is 39
parent count = 3595709
child count = 52111
```

当两个进程具有相同的 nice 值时，父进程获得 50.2% 的 CPU，子进程获得 49.8% 的 CPU。注意，两个进程在效果上被平等对待。百分比并不完全相等，因为进程调度并不精确，而且由于在计算结束时间和处理循环开始时间之间，子进程和父进程执行的处理量不同。

相比之下，当子进程具有最高可能的 nice 值（最低优先级）时，我们看到父进程获得 98.5% 的 CPU，而子进程仅获得 1.5% 的 CPU。这些值会根据进程调度程序如何使用 nice 值而变化，因此不同的 UNIX 系统会产生不同的比例。

## 8.17 进程时间

在第 1.10 节中，我们描述了可以测量的三种时间：挂钟时间、用户 CPU 时间和系统 CPU 时间。任何进程都可以调用 times 函数来获取其自身以及任何已终止子进程的这些值。

```
#include <sys/times.h>

clock_t times(struct tms *buf);

Returns: elapsed wall clock time in clock ticks if OK, -1 on error
```

此函数填充 buf 指向的 tms 结构：

```
struct tms {
    clock_t tms_utime;  /* user CPU time */
    clock_t tms_stime;  /* system CPU time */
    clock_t tms_cutime; /* user CPU time, terminated children */
    clock_t tms_cstime; /* system CPU time, terminated children */
};
```

请注意，该结构不包含挂钟时间的任何测量。相反，函数返回挂钟时间作为函数的值，每次调用时都如此。该值是从过去某个任意点开始测量的，因此我们不能使用其绝对值；相反，我们使用其相对值。例如，我们调用 times 并保存返回值。在稍后的某个时间，我们再次调用 times 并从新的返回值中减去较早的返回值。差值就是挂钟时间。 （对于长时间运行的进程来说，挂钟时间溢出的可能性很小，但并非不可能；请参阅练习 1.5。）

此函数返回的子进程的两个结构字段仅包含我们已使用本章前面讨论的 wait 函数之一等待的子进程的值。

此函数返回的所有 clock_t 值都使用每秒时钟滴答数——sysconf 返回的 _SC_CLK_TCK 值（第 2.5.4 节）转换为秒。

大多数实现都提供 getrusage(2) 函数。此函数返回 CPU 时间和 14 个其他指示资源使用情况的值。历史上，该函数起源于 BSD 操作系统，因此基于 BSD 的实现通常支持的字段比其他实现更多。

### 示例

图 8.31 中的程序将每个命令行参数作为 shell 命令字符串执行，计时命令并打印 tms 结构中的值。

```
#include "apue.h"
#include <sys/times.h>

static void pr_times(clock_t, struct tms *, struct tms *);
static void do_cmd(char *);

int
main(int argc, char *argv[])
{
    int     i;

    setbuf(stdout, NULL);
    for (i = 1; i < argc; i++)
        do_cmd(argv[i]);    /* once for each command-line arg */
    exit(0);
}
static void
do_cmd(char *cmd)      /* execute and time the "cmd" */
{
    struct tms tmsstart, tmsend;
    clock_t start, end;
    int     status;

    printf("\ncommand: %s\n", cmd);

    if ((start = times(&tmsstart)) == -1)    /* starting values */
        err_sys("times error");
    if ((status = system(cmd)) < 0)          /* execute command */
        err_sys("system() error");
    if ((end = times(&tmsend)) == -1)        /* ending values */
        err_sys("times error");

    pr_times(end-start, &tmsstart, &tmsend);
    pr_exit(status);
}

static void
pr_times(clock_t real, struct tms *tmsstart, struct tms *tmsend)
{
    static long clktck = 0;

    if (clktck == 0)    /* fetch clock ticks per second first time */
        if ((clktck = sysconf(_SC_CLK_TCK)) < 0)
            err_sys("sysconf error");

    printf(" real: %7.2f\n", real / (double) clktck);
    printf(" user: %7.2f\n", (tmsend->tms_utime - tmsstart->tms_utime) / (double) clktck);
    printf(" sys: %7.2f\n", (tmsend->tms_stime - tmsstart->tms_stime) / (double) clktck);
    printf(" child user: %7.2f\n",
(tmsend->tms_cutime - tmsstart->tms_cutime) / (double) clktck);
printf(" child sys: %7.2f\n",
    (tmsend->tms_cstime - tmsstart->tms_cstime) / (double) clktck);
}
```

图 8.31 计时并执行所有命令行参数

如果我们运行此程序，我们得到

```
$ ./a.out "sleep 5" "date" "man bash >/dev/null"

command: sleep 5
real:    5.01
user:    0.00
sys:     0.00
child user:  0.00
child sys:   0.00
normal termination, exit status = 0

command: date
Sun Feb 26 18:39:23 EST 2012
real:    0.00
user:    0.00
sys:     0.00
child user:  0.00
child sys:   0.00
normal termination, exit status = 0

command: man bash >/dev/null
real:    1.46
user:    0.00
sys:     0.00
child user:  1.32
child sys:   0.07
normal termination, exit status = 0
```

在前两个命令中，执行速度足够快，以至于在报告的分辨率下无法记录任何 CPU 时间。但是，在第三个命令中，我们运行一个需要足够处理时间的命令，可以注意到所有的 CPU 时间都出现在子进程中，即 shell 和命令执行的位置。

## 8.18 摘要

对 UNIX 系统进程控制的透彻理解对于高级编程至关重要。只有少数几个函数需要掌握：fork、exec 系列、_exit、wait 和 waitpid。这些原语在许多应用程序中使用。fork 函数还给了我们一个机会来查看竞争条件。

我们对 system 函数和进程记账的检查让我们再次了解了所有这些进程控制函数。我们还查看了另一种变体


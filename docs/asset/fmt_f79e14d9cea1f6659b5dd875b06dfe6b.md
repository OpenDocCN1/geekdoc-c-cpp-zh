
结果，`/etc`目录的内容列在屏幕上。注意，调用`execcl()`函数下方的`printf()`不会被执行。这是因为`exec`系列函数用要执行程序的代码和数据覆盖调用进程的映像。在我们的情况下，子进程的内存被`ls`程序的代码和数据覆盖了。因此，`printf()`的调用没有实现。

在`fork()`之前调用`exec()`没什么意义。因为这不会创建一个子进程，且`execcl()`将直接覆盖主进程本身。结果是调用`execcl()`之后的语句将永远不会执行。因此`fork()`和`execcl()`通常是配套使用的。

## 僵尸进程与孤进程

我们知道`ps -A`命令列出了所有运行的进程。但`ps`程序从哪里获取这些信息呢？Linux维护着一个包含所有进程信息的表。这个表被称为“进程表”。除了其他信息外，进程表还包含进程的“退出码”条目。这个整数值表示进程被终止的原因。即使进程结束了，它的条目仍将留在进程表中，直到终止进程的父进程查询退出码为止。这种查询行为

第19章：与硬件交互 661 将从进程表中删除已终止进程的条目，并将退出码返回给提出查询的父进程。

当我们派生一个新的子进程且子进程继续执行时，有两种可能——子进程先结束，或者父进程先结束。让我们讨论这两种可能性。

- (a) 子进程早于父进程终止

在这种情况下，在父进程查询已终止的子进程条目之前，子进程将一直存在。在Linux术语中，这种进程被称为“僵尸”`Zombie`进程。`Zombie`的意思是鬼，或者在印地语中称为“Bhoot”。教训是，父进程在子进程终止后应立即查询进程表。这将防止僵尸进程的产生。

如果父进程在没有查询的情况下终止了呢？在这种情况下，僵尸子进程被视为“孤进程”`Orphan`。立即，所有进程之父——`init`——会收养这个孤进程。随后，`init`查询进程表，从而从进程表中删除该子进程条目。

- (b) 父进程早于子进程终止

由于父进程都是从`shell`启动的，父进程的父进程是`shell`进程。当我们的父进程终止时，`shell`查询进程表。然而，仍在运行的子进程变成了孤进程。`init`进程立即会收养它，当它的执行结束时，`init`会查询进程表以清理子进程。注意，在这种情况下子进程不会变成僵尸。

662 # 让我们学习C语言 因此，当产生僵尸或孤进程时，操作系统会接管并确保进行适当清理。然而，作为良好的编程习惯，我们的程序应该获取已终止进程的退出码，从而确保适当清理。注意这里清理是重要的（无论如何都会发生）。获取已终止进程的退出码很重要，是因为退出码会指示分配给的任务是否成功完成。以下程序展示了如何实现。

```c
#include <unistd.h>
#include <sys/types.h>
int main()
{
    unsigned int i = 0;
    int pid, status;
    pid = fork();
    if (pid == 0)
    {
        while (i < 4294967295U)
            i++;
        printf("The child is now terminating\n");
    }
    else
    {
        waitpid(pid, &status, 0);
        if (WIFEXITED(status))
            printf("Parent: Child terminated normally\n");
        else
            printf("Parent: Child terminated abnormally\n");
    }
    return 0;
}
```

在程序程序中，我们在子进程中应用了一个大循环。这个循环确保了子进程不会立即终止。在父进程内部，我们调用了`waitpid()`函数。该函数让父进程等待，直到子进程的执行结束。这确保了子进程永远不会变成孤进程。

# 664
# Let Us C

## 总结

- (a) Linux是一个免费操作系统，其内核由Linus Torvalds及其朋友构建。
- (b) 一个Linux发行版由带有源代码的内核以及大量的应用程序、库、脚本等组成。
- (c) Linux下的C程序可以使用流行的`gcc`编译器进行编译。
- (d) Linux中的基本调度单位是“进程”`Process`。进程由一个名为“调度器”`Scheduler`的特殊程序调度。
- (e) `fork()`库函数可创建子进程。
- (f) Init进程是所有进程的父进程。
- (g) `exec()`库函数用于从运行中的程序内部执行另一个程序。
- (h) `exec()`函数会覆盖调用进程的映像（代码和数据）。
- (i) `exec()`和`fork()`通常是成对使用的。
- (j) `ps`命令可以获取所有进程列表。
- (k) `kill`命令可以终止进程。
- (l) “僵尸进程”`Zombie`是指终止的子进程，其父进程正在运行但尚未调用函数获取子进程的退出状态。
- (m) “孤儿进程”`Orphan`是指父进程已终止的子进程。
- (n) 孤儿进程会自动被`init`进程收养。
- (o) 父进程可以使用`waitpid()`函数避免僵尸进程和孤儿进程的产生。

## 练习题

[A] 判断对错：

- (a) 我们可以修改Linux操作系统的内核。
- (b) 所有Linux发行版都包含相同的应用程序、库和安装脚本。
- (c) Linux中的基本调度单位是文件。
- (d) `execl()`库函数可以创建一个新的子进程。
- (e) 调度器进程是所有进程的父进程。
- (f) 提供系列`fork()`和`exec()`函数，它们的功能基本上相同相同，仅有细微差异。
- (g) `fork()`将父进程的代码和数据完全复制到子进程。
- (h) `fork()`覆盖调用进程的映像（代码和数据）。
- (i) `fork()`被调用两次但只执行了一次。
- (j) 每个僵尸进程本质上都是孤儿进程。每个孤儿进程本质上都是孤儿进程。

## [B] 回答以下问题：

- (a) 如果一个程序连续调用了四次`fork()`，总共会创建多少进程？
- (b) 僵尸进程和孤儿进程之间的区别是什么？
- (c) 编写一个程序，打印它接收到的命令行参数。如果命令行参数是*?*，程序的输出是什么？
- (d) `getpid()`、`getppid()`、`getppid()`函数的作用是什么？
- (e) 重写“僵尸进程与孤儿进程”部分中的程序，将`while`循环替换为调用`sleep()`函数。你是否观察到程序输出有任何变化？
- (f) `waitpid()`如何防止僵尸进程或孤儿进程的产生？

# 21 更多 Linux 编程

- 使用信号进行通信
- 处理多个信号
- 注册公共处理程序
- 阻塞信号
- 事件驱动编程
- 接下来去哪里
- 总结
- 练习题

# 668
# Let Us C

通信是所有进步的本质。这在现实生活中编程中也是如此。一个孤立运行的程序作用有限。在当今世界，程序通常必须与外部世界通信，特别是与操作系统通信。在第16和17章中，我们看到了基于Windows的程序如何与Windows通信。在本章中，让我们探索这种通信如何在Linux下发生。

## 使用信号通信

在上一节中，我们使用`fork()`和`exec()`库函数分别创建子进程并执行新程序。这些库函数通过与Linux操作系统的通信完成了任务。因此，通信方向是从程序到操作系统。反向通信——从操作系统到程序——是通过一种名为“信号”`Signal`的机制实现的。

```c
int main()
{
    printf("Program Running");
    while ( 1 );
}
```

当上述程序运行时，如果我们按下`Ctrl+C`，内核会向该进程发送一个`SIGINT`信号。默认操作是终止。然而，信号也可以被忽略、捕获或由自定义函数处理。要处理信号，我们使用`signal()`库函数。第一个参数指定我们想要注册的信号ID。第二个参数是应该调用的函数地址。该地址必须强制转换为`void (*)`。

# 692
# 第21章：更多 Linux 编程 669

现在我们已经知道如何处理一个信号，让我们尝试处理多个信号。这里是实现此目的的程序

# 670
# Let Us C

```c
#include <signal.h>
void sighhandler (int signum)
{
    printf("\nSIGINT received.\n"); }
int main ()
{
    signal (SIGINT, (void*)sighhandler);
    while ( 1 )
    {
        printf("Program Running ");
    }
    return 0;
}
```

在这个程序中，我们为`SIGINT`注册了一个处理程序。当我们按下`Ctrl+C`时，注册的处理程序（即`sighhandler()`）就会被调用。

与默认处理程序不同，我们的处理程序不会终止执行。因此，终止它的唯一方法是从另一个终端杀死运行中的进程。

```bash
# kill 3276
```

在我的情况下，执行`a.out`的终端是`tty1`，其进程ID变为3276。在你的情况下，终端名称和进程ID可能是不同的数字。

如果我们愿意，可以在处理程序中的`printf()`之后使用`exit( 0 )`来终止程序的执行。

注意信号是异步工作的。也就是说，当接收到信号时，无论程序正在做什么，信号处理程序都会立即被调用。一旦信号处理程序的执行结束，程序将从接收信号的地方继续执行。

# 处理多个信号

```c
#include <unistd.h>
#include <sys/types.h>
#include <signal.h>
void inandler (int signum)
{
    printf("\nSIGINT\n");
}
void termhandler (int signum)
{
    printf("\nSIGTERM\n");
}
void conhandler (int signum)
{
    printf("\nSIGCONT\n");
}
int main ()
{
    signal (SIGINT, inandler);
    signal (SIGTERM, termhandler);
    signal (SIGCONT, conhandler);
    while ( 1 )
    {
        printf("\rProgram Running ");
    }
    return 0;
}
```

在这个程序中，除了`SIGINT`之外，我们额外注册了两个新信号，即`SIGTERM`和`SIGCONT`。`signal()`函数被调用三次，为这三个信号分别注册了不同的处理器。注册信号后，我们进入一个无限的`while`循环，在屏幕上打印“Program running”信息。

与上一个程序一样，在这里当我们按下`Ctrl + C`时，`SIGINT`的处理器（即`inhandler()`）会被调用。然而，当我们尝试从第二个终端使用`kill`命令杀掉程序时，程序并没有终止。这是因为当使用`kill`命令时，它会向运行中的程序发送一个`SIGTERM`信号。由于我们自己处理了该信号，`SIGTERM`的处理器（即`termhandler()`）会被调用。结果是，`termhandler()`函数中的`printf()`语句被执行，屏幕上显示了“SIGTERM Received”消息。一旦`termhandler()`函数的执行完成，程序将恢复执行并继续打印“Program Running”。那么，我们该如何终止程序呢？很简单。在另一个终端上使用以下命令：

```
kill -SIGKILL 3276
```

如命令所示，我们正尝试向我们的程序发送一个`SIGKILL`信号。`SIGKILL`信号会终止程序。

大多数信号可以被进程捕获，但有少数信号是进程无法捕获的，它们会导致进程终止。这些信号通常被称为不可捕获信号`un-catchable signals`。`SIGKILL`信号就是不可捕获信号，它可以强制终止进程的执行。

请注意，即使进程尝试通过注册处理器来处理`SIGKILL`信号，控制权始终会回到默认的`SIGKILL`处理器，该处理器将终止程序。

# 第21章：更多 Linux 编程

`SIGKILL`信号应作为最后的手段，用于终止失去控制的程序。使用这种信号的一个进程是系统关机进程。它首先向所有进程发送`SIGTERM`信号，等待一段时间，从而为所有运行中的进程留出“宽限期”。然而，在宽限期结束后，它使用`SIGKILL`信号强制终止所有剩余进程。

这只剩下一个问题——进程何时接收到`SIGCONT`信号呢？让我尝试回答这个问题。

在Linux下，可以使用`Ctrl + Z`命令挂起进程。进程被停止但没有终止，即被挂起。这产生了不可捕获的`SIGSTOP`信号。要恢复挂起进程的执行，我们可以使用`fg`（前台）命令。结果是，挂起的程序恢复执行并接收`SIGCONT`信号（`CONT`意味着继续执行）。

## 注册通用处理器

与其为每个信号注册单独的处理器，我们可能决定使用一个通用信号处理器来处理所有信号。如下程序所示：

```c
## include <unistd.h>
#include<sys/types.h>
#include<signal.h>
```

```c
void sighandler ( int signum )
{
    switch ( signum)
    {
        case SIGINT :
```

```c
printf ("SIGINT Received\n" );
            break;
```

```c
        case SIGTERM:
            printf ("SIGTERM Received\n" );
            break;
```

```c
        case SIGCONT:
            printf ("SIGCONT Received\n" );
            break;
    }
}
```

```c
int main()
{
    signal ( SIGINT, handler);
    signal ( SIGTERM, handler);
    signal ( SIGCONT, handler);
    while ( 1 )
        printf ("\rProgram running\n" );
    return 0; }
```

在这个程序中，每次调用`signal()`函数时，我们都指定了名为`sighandler()`的通用信号处理器的地址。因此，当接收到三个信号中的任何一个时都会调用同一个信号处理器函数。这不会导致问题，因为我们可以通过函数的第一个参数在信号ID内部确定`sighandler()`的具体逻辑。在我们的程序中，我们使用了`switch-case`结构为三个信号中的每一个信号打印不同的消息。

请注意，我们可以很容易地在程序中混合这两种注册信号的方法。也就是说，我们可以为某些信号注册单独的信号处理器，为其他信号注册通用处理器。如果我们希望以完全相同的方式响应不同的信号，那么注册通用处理器是有意义的。

## 阻塞信号

有时，我们可能希望程序中关键/时间敏感部分的执行流不被一个或多个信号的发生所干扰。在这种情况下，我们可能决定阻塞该信号。一旦我们完成了关键/时间敏感代码，就可以解锁信号。请注意，如果信号在被阻塞时到达，它会被简单地放入信号队列中。当信号被取消阻塞时，进程会一个接一个地接收所有等待的信号。因此，阻塞信号会延迟信号向进程的传递，直到某些关键/时间敏感代码的执行完成。与其忽略信号或让信号中断执行，不如暂时阻塞信号并在稍后传递它们。现在让我们写一个程序来理解信号阻塞。这里是该程序……

```c
#include <unistd.h>
#include <sys/types.h>
#include <signal.h>
#include <stdio.h>
void sighhandler ( int signum )
{
    switch ( signum )
    {
        case SIGTERM :
            printf ("SIGTERM Received\n" );
            break;
        case SIGINT :
            printf ("SIGINT Received\n" );
            break;
        case SIGCONT :
            printf ("SIGCONT Received\n" );
            break;
    }
}
int main()
{
    char buffer [80] = "\0";
    sigset_t block;
    signal (SIGTERM, handler);
    signal (SIGINT, handler);
    signal (SIGCONT, handler);
    sigemptyset(&block);
    sigaddset(&block, SIGTERM);
    sigaddset(&block, SIGINT);
```

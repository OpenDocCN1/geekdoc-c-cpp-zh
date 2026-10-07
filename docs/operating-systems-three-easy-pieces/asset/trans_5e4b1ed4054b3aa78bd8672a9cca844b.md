
# 42
间插录：进程 API

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    printf("hello world (pid:%d)\n", getpid());
    int rc = fork();
    if (rc < 0) {
        // fork 失败
        fprintf(stderr, "fork failed\n");
        exit(1);
    } else if (rc == 0) {
        // 子进程（新进程）
        printf("hello, I am child (pid:%d)\n", (int) getpid());
    } else {
        // 父进程进入此路径（main）
        printf("hello, I am parent of %d (pid:%d)\n", rc, (int) getpid());
    }
    return 0;
}

fork()
```

图 5.1：调用 fork() pl.c

当你运行这个程序（称为 pl.c）时，你会看到以下内容：

```
prompt> ./pl
hello world (pid:29146)
hello, I am parent of 29147 (pid:29146)
hello, I am child (pid:29147)
prompt>
```

让我们详细了解 pl.c 中发生了什么。在首次运行时，进程打印了一条 hello world 消息；消息中包含了它的进程标识符，也称为 PID。该进程的 PID 为 29146；在 UNIX 中，如果想对进程进行某些操作（例如停止它的运行），PID 用于命名进程。到目前为止一切顺利。

有趣的部分开始了。进程调用了 `fork()` 系统调用，操作系统通过此作为创建新进程的方法。创建的另一个部分是调用进程的（几乎）相同的副本。这意味着对于操作系统来说，现在似乎有两个程序的副本在运行，并且它们都能从 `fork()` 系统调用返回。新创建的进程（与父进程相对称为子进程）并没有在 `main()` 中启动，正如你预期的那样（注意，“hello world”消息只被打印了一次）；而是它像是自己调用了 `fork()` 一样产生的。

操作系统
[版本 1.01]

WWW.OSTEP.ORG

#间插录：进程 API

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("hello world (pid:%d)\n", getpid());
    int rc;
    rc = fork();
    if (rc < 0) { // fork 失败；退出
        fprintf(stderr, "fork failed\n");
        exit(1);
    } else if (rc == 0) { // 子进程（新进程）
        printf("hello, I am child (pid:%d)\n", (int) getpid());
    } else {
        int rc_wait = wait(NULL);
        printf("hello, I am parent of %d (rc_wait:%d) (pid:%d)\n", rc_wait, (int) getpid());
    }
    return 0;
}
```

图 5.2：调用 fork() 和 Wait() (p2.c)

你可能已经注意到：子进程并不是完全副本。具体来说，尽管它有自己的地址空间（即它的私有内存），但它有自己的寄存器（通常是 PC），因此它返回给 `fork()` 调用者的值是不同的。具体而言，父进程接收到新创建子进程的 PID，而子进程接收到的返回值为零。这种区分是有用的，因为编写处理两种不同情况的代码（如上所示）很简单。

你可能还会注意到：输出（pl.c 的输出）不是确定性的。当子进程被创建时，系统中现在有两个活动进程，我们称之为：父进程和子进程。假设我们运行在一个具有单 CPU 的系统上（为了简单起见），在这一点，子进程或父进程可能会运行。在我们的示例中（上文），父进程运行并首先打印了它的消息。在其他情况下，可能会发生相反的情况，正如我们在输出跟踪中所示：

```
prompt> ./pl
hello world (pid:29146)
hello, I am child (pid:29147)
hello, I am parent of 29147 (pid:29146)
prompt>
```

CPU 调度器（我们将很快详细讨论的话题）决定在给定时刻运行哪个进程；因为调度器是复杂的，我们通常无法对它将选择做什么以及因此哪个进程将先运行做出强有力的假设。这种**不确定性**事实会导致一些有趣的问题，特别是在**多线程程序**中；因此，当我们在书的第二部分学习**并发**时，我们将看到很多不确定性。

# 5.2 wait() 系统调用

到目前为止，我们还没做什么：只是创建了一个打印消息并退出的子进程。事实证明，父进程等待孩子完成它正在做是非常非常有用的。任务通过 `wait()` 系统调用（或更完整的 `waitpid()`）完成，详见图 5.2。

在示例（p2.c）中，父进程调用 `wait()` 来延迟其执行，直到子进程完成执行。当子进程完成后，`wait()` 返回给父进程。

在代码中添加 `wait()` 使得输出具有确定性。你知道为什么吗？继续想一想。

（等待你思考……完成）

现在你已经思考了一会儿，这里是输出：

```
prompt> ./p2
hello world (pid:29266)
hello, I am child (pid:29267)
hello, I am parent of 29267 (rc_wait:29267) (pid:29266)
prompt>
```

通过这段代码，我们现在知道子进程会先运行。我们为什么不知道呢？嗯，它可能只是先运行，因为 `wait()` 直到子进程退出才返回。因此，父进程等待孩子。

# 5.3 最后，exec() 系统调用

进程创建最后最后是 `exec()` 系统调用。当你想要运行与调用进程不同的程序时，该系统非常有用。例如，调用 `fork()` 让“子进程先运行”。在 Linux 上，`exec()` 有六种变体：`execcl()`、`execp()`、`execle()`、`execve()` 和 `execv()`。阅读页面更多。

`fork()` 系统调用很奇怪；它的伙伴 `exec()` 并不那么普通。它的作用是：给定一个可执行文件的名称（例如 wc）和一些参数（例如 p3.c），它从那里加载代码（和静态数据）。

# 间插录：进程 API

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("hello world\n", (pid:%d), getpid());
    int rc = fork();
    if (rc < 0) { // fork 失败：退出
        fprintf(stderr, "fork failed\n");
        exit(1);
    } else if (rc == 0) { // 子进程（新进程）
        printf("hello, I am child (pid:%d)\n", (int) getpid());
        char *myargs[3] = strdup("wc"); // 程序："wc"
        myargs[1] = strdup("p3.c"); // 参数：计数的文件
        myargs[2] = NULL; // 数组结束
        execvp(myargs, myargs); // 运行 wc
        printf("this shouldn't print out");
    } else { // 进入此路径（main）
        int rc_wait = wait(NULL);
        printf("hello, I am parent of %d (rc_wait:%d) (pid:%d)\n", (int)rc, rc_wait, (int)getpid());
    }
    return 0;
}
```

图 5.3：调用 fork(), wait() 和 exec() (p3.c)

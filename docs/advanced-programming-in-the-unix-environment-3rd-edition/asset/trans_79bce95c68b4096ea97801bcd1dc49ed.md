
意味着竞争条件不存在；它只是意味着我们在这个特定系统上看不到它。）以下实际输出显示了结果如何变化：

```
$ ./a.out
ooutput from child
utput from parent
$ ./a.out
ooutput from child
utput from parent
$ ./a.out
output from child
output from parent
```

我们需要修改图8.12中的程序，以使用TELL和WAIT函数。图8.13中的程序完成了这一点。前面带有加号的行是新行。

```
#include "apue.h"
static void charatatime(char *);

int
main(void)
{
    pid_t  pid;

+   TELL_WAIT();
+
    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) {  /* parent goes first */
+       WAIT_PARENT();
        charatatime("output from child\n");
    } else {
        charatatime("output from parent\n");
+       TELL_CHILD(pid);
    }
    exit(0);
}

static void
charatatime(char *str)
{
    char  *ptr;
    int   c;
    setbuf(stdout, NULL);      /* set unbuffered */
    for (ptr = str; (c = *ptr++) != 0; )
        putc(c, stdout);
}
```

## 图8.13 修改图8.12以避免竞争条件

当我们运行这个程序时，输出正如我们所预期；两个进程的输出没有交错。

在图8.13所示的程序中，父进程先执行。如果我们将fork之后的代码行改为以下形式，则子进程先执行：

```
} else if (pid == 0) {
    charatatime("output from child\n");
    TELL_PARENT(getppid());
} else {
    WAIT_CHILD();        /* child goes first */
    charatatime("output from parent\n");
}
```

练习8.4继续这个例子。

## 8.10 exec 函数

我们在8.3节中提到，fork函数的一个用途是创建一个新进程（子进程），然后该进程通过调用某个exec函数来执行另一个程序。当进程调用某个exec函数时，该进程会被新程序完全替换，新程序从其main函数开始执行。进程ID在exec过程中不会改变，因为并没有创建新进程；exec只是用磁盘上一个全新的程序替换当前进程的文本、数据、堆和栈段。

有七个不同的exec函数，但我们通常只说“exec函数”，意思是我们可以使用这七个函数中的任意一个。这七个函数完善了UNIX系统的进程控制原语。通过fork，我们可以创建新进程；通过exec函数，我们可以启动新程序。exit函数和wait函数处理终止和等待终止。这些就是我们需要的全部进程控制原语。在后面的章节中，我们将使用这些原语来构建其他函数，如popen和system。

```
#include <unistd.h>

int execl(const char *pathname, const char *arg0, ... /* (char *)0 */ );
int execv(const char *pathname, char *const argv[]);
int execle(const char *pathname, const char *arg0, ...
    /* (char *)0, char *const envp[] */ );
int execve(const char *pathname, char *const argv[], char *const envp[]);
int execlp(const char *filename, const char *arg0, ... /* (char *)0 */ );
int execvp(const char *filename, char *const argv[]);
int fexecve(int fd, char *const argv[], char *const envp[]);

All seven return: -1 on error, no return on success
```

这些函数的第一个区别是，前四个以路径名（pathname）作为参数，接下来两个以文件名（filename）作为参数，最后一个以文件描述符作为参数。当指定文件名参数时：
- 如果*filename*包含斜杠，则将其视为路径名。
- 否则，在`PATH`环境变量指定的目录中搜索可执行文件。

`PATH`变量包含一个目录列表，这些目录称为路径前缀（path prefixes），以冒号分隔。例如，*name=value*环境字符串

```
PATH=/bin:/usr/bin:/usr/local/bin/:
```

指定了四个要搜索的目录。最后一个路径前缀指定当前目录。（零长度的前缀也表示当前目录。它可以指定为值的开头的冒号、连续两个冒号，或值的末尾的冒号。）

> 出于安全原因，*永远不要*将当前目录包含在搜索路径中。参见Garfinkel等人[2003]。

如果`execl`或`execvp`使用某个路径前缀找到了可执行文件，但该文件不是由链接编辑器生成的机器可执行文件，则函数会假定该文件是一个shell脚本，并尝试将*filename*作为shell的输入来调用`/bin/sh`。

使用`execve`，我们完全避免了查找正确可执行文件的问题，而依靠调用者来完成。通过使用文件描述符，调用者可以验证文件确实是有意为之的文件，并在无竞争的情况下执行它。否则，拥有适当权限的恶意用户可以在可执行文件（或指向可执行文件的路径的一部分）被定位和验证之后、但在调用者执行它之前替换它（回想3.3节中关于TOCTTOU错误的讨论）。

下一个区别涉及参数列表的传递（l代表列表list，v代表向量vector）。函数`execl`、`execlp`和`execle`要求将新程序的每个命令行参数指定为单独的参数。我们用空指针标记参数的结束。对于其他四个函数（`execv`、`execvp`、`execve`和`fexecve`），我们必须构建一个指向参数的指针数组，这个数组的地址就是这三个函数的参数。

在使用ISO C原型之前，显示`execl`、`execle`和`execlp`这三个函数命令行参数的通常方式是

```
char *arg0, char *arg1, ..., char *argn, (char *)0
```

这种语法明确显示最后一个命令行参数后面跟着一个空指针。如果这个空指针用常量0指定，我们必须将其强制转换为指针；如果不这样做，它会被解释为一个整数参数。如果整数的大小与char *的大小不同，exec函数的实际参数将是错误的。

最后一个区别是将环境列表传递给新程序。三个名字以e结尾的函数（`execle`、`execve`和`fexecve`）允许我们传递一个指向环境字符串指针数组的指针。然而，其他四个函数使用调用进程中的environ变量来为新程序复制现有环境。（回想我们在7.9节和图7.8中关于环境字符串的讨论。我们提到，如果系统支持setenv和putenv这样的函数，我们可以更改当前环境以及任何后续子进程的环境，但我们无法影响父进程的环境。）通常，进程允许其环境传播给子进程，但在某些情况下，进程希望为子进程指定特定的环境。后者的一个例子是当启动新的登录shell时的login程序。通常，login会创建一个只定义了少量变量的特定环境，并让我们在登录时通过shell启动文件向环境中添加变量。

在使用ISO C原型之前，execle的参数显示为

```
char *pathname, char *arg0, ..., char *argv, (char *)0, char *envp[]
```

这种语法特别显示了最后一个参数是指向环境字符串的字符指针数组的地址。ISO C原型没有显示这一点，因为所有命令行参数、空指针和envp指针都用省略号（...）表示。

这七个exec函数的参数很难记住。函数名中的字母有所帮助。字母p表示该函数接受文件名参数，并使用PATH环境变量来查找可执行文件。字母l表示该函数接受一个参数列表，并且与字母v互斥，v表示它接受argv[]向量。最后，字母e表示该函数接受envp[]数组而不是使用当前环境。图8.14显示了这七个函数之间的区别。

| 函数 | 路径名 | 文件名 | fd | 参数列表 | argv[] | environ | envp[] |
|---|---|---|---|---|---|---|---|
| execl | • |  |  | • |  | • |  |
| execlp |  | • |  | • |  | • |  |
| execle | • |  |  | • |  |  | • |
| execv | • |  |  |  | • | • |  |
| execvp |  | • |  |  | • | • |  |
| execve | • |  |  |  | • |  | • |
| fexecve |  |  | • |  | • |  | • |
| （名称中的字母） |  | p | f | l | v |  | e |

## 图8.14 七个exec函数之间的区别

每个系统对参数列表和环境列表的总大小都有限制。根据2.5.2节和图2.8，这个限制由ARG_MAX给出。在POSIX.1系统上，该值必须至少为4,096字节。当使用shell的文件名展开功能生成文件名列表时，我们有时会遇到这个限制。例如，在某些系统上，命令

```
grep getrlimit /usr/share/man/*/*
```

会生成如下形式的shell错误：

```
Argument list too long
```




```
sleep(10);
/* Parent process does not wait for the child */
/* process and child becomes a zombie process */
exit(0);
}
$ gcc -w create_zombie.c -o create_zombie
$ create_zombie
Parent's PID = 15831
Child's PID  = 15832
^Z
[1]+  Stopped                 create_zombie
$ ps -o pid,tt,stat,cmd
  PID TT     STAT CMD
15691 pts/2  Ss   -bash
15831 pts/2  T    create_zombie
15832 pts/2  Z    [create_zombie] <defunct>
15836 pts/2  R+   ps -o pid,tt,stat,cmd
$ fg
create_zombie
$
```

您也可以使用 ps -al 命令来显示僵尸进程的状态。

当 systemd 进程的一个子进程终止时，systemd 会调用 wait() 系列系统调用之一来收集子进程的退出状态。因此，systemd 的子进程永远不会变成僵尸进程。该子进程可能是一个由 systemd 直接创建的进程，也可能是因为其父进程在进程终止时已经死亡（或未等待）而被 systemd 继承的进程。

### 练习 16.11

在自己的系统上复现前面的会话。create_zombie.c 程序是否按预期工作？

### 16.3.7 终止进程

进程可以使用 kill() 系统调用来终止一个它有权终止的进程。超级用户拥有的进程可以终止任何进程。我们将在第 16.5.4 节详细讨论这个系统调用。

## 16.4 进程与文件描述符表

我们现在讨论 PPFDT 在进程间文件共享、I/O 重定向以及使用不同通道（包括管道、FIFO 和套接字）进行进程间通信方面的重要性。我们将在第 16.4.1 节讨论文件共享的概念，并在第 16.4.2 节讨论 I/O 重定向。第 20 章详细描述了 Linux 进程间通信。

### 16.4.1 进程间的文件共享

如前所述，子进程会获得其父进程 PPFDT 的一份副本。这意味着，如果进程在创建子进程之前打开了一个文件，那么父进程和子进程都可以访问该打开文件的文件描述符。因此，任一进程对打开文件执行的 I/O 操作对另一个进程都是可见的。

两个进程中 I/O 后的文件指针，验证两个进程确实使用同一个文件执行 I/O。nbytes 参数可以在 0 到 512 之间变化，因为读/写缓冲区的大小已设置为 512 字节。我们在父进程中使用 sleep(1) 调用，以确保子进程在父进程之前执行 I/O。这样做的目的是确保两个进程中的文件指针值都能正确显示。程序清单之后提供了几个示例运行，以验证文件共享概念确实如所述工作。请注意，foo 是一个现有文件的名称。我们使用 man bash > foo 命令创建了这个文件。

```
$ cat file_sharing.c
/* file_sharing.c: fileshare filename nbytes */

#include <fcntl.h>
#include <unistd.h>
#include <sys/wait.h>

#define SIZE 512

int main(int argc, char *argv[])
{
    int fd, n, nr, nbytes, pid, status;
    char buf[SIZE];

    /* Open file */
    if (argc != 3) {
        printf("%s filename nbytes\n", argv[1]);
        exit(1);
    }
    nbytes = atoi(argv[2]);
    if ((fd = open(argv[1], O_RDWR)) == -1) {
        perror("File opening");
        exit(1);
    }
    /* Create a child */
    pid = fork();
    /* Child process */
    if (pid == 0) {
        /* Read and display on stdout */
        if ((nr = read(fd, buf, nbytes)) == -1) {
            perror("Read failed");
            exit(1);
        }
        write(1, buf, nr); /* Write on standard output */
        n = lseek(fd, 0L, SEEK_CUR);
        printf("\n\nCHILD: position of the file pointer after I/O is %d\n\n", n);
        close(fd);
        exit(0);
    }
    /* Parent process */
    sleep(1); /* Allow the child process to do I/O first. */
    /* Read and display on stdout */
    if ((nr = read(fd, buf, nbytes)) == -1) {
        perror("Read failed");
        exit(1);
    }
    write(1, buf, nr); /* Write on standard output */
    n = lseek(fd, 0L, SEEK_CUR);
    printf("\n\nPARENT: position of the file pointer after I/O is %d\n\n", n);
    close(fd);
    while (wait3(&status, WNOHANG, 0) >= 0)
        ;
    exit(0);
}
```

```
$ gcc -w file_sharing.c -o fileshare
$ fileshare foo 32
BASH(1) Gene
CHILD: position of the file pointer after I/O is 32
ral Commands Manual
PARENT: position of the file pointer after I/O is 64
```

```
$ fileshare foo 64
BASH(1) General Commands Manual
CHILD: position of the file pointer after I/O is 64
BASH(1)
NAME
bash - GNU Bourne-Again SHell
SYNOP
PARENT: position of the file pointer after I/O is 128
```

```
$ fileshare foo 256
BASH(1) General Commands Manual BASH(1)
NAME
bash - GNU Bourne-Again SHell
SYNOPSIS
bash [options] [command_string | file]
COPYRIGHT
Bash is Copyright (C) 1989-2013 by the Free Software Foundat
CHILD: position of the file pointer after I/O is 256
ion, Inc.
DESCRIPTION
Bash is an sh-compatible command language interpreter that executes commands read from the standard input or from a file. Bash also incorporates useful features from the Korn and C shells (ksh and csh).
PARENT: position of the file pointer after I/O is 512
$
```

### 练习 16.12

在自己的系统上复现前面的会话。file_sharing.c 程序是否按预期工作？

### 练习 16.13

修改 file_sharing.c 程序，使其将要读取的字节数作为第一个命令行参数，文件名作为第二个参数。编译并运行该程序，使用不同的文件和要读取的字节数作为命令行参数。

表 16.7  dup() 和 dup2() 系统调用失败的原因

| 失败原因 | errno 的值 |
|---|---|
| olddes 中指定的描述符不是有效的活动描述符（即尚未通过诸如 open() 之类的系统调用分配），或者 newdes 中指定的描述符大于 PPFDT 的大小，或者是负数 | EBADF |
| 进程已经使用了最大数量的描述符（即 PPFDT 已被完全占用） | EMFILE |

### 16.4.2 复制文件描述符

你可以使用 dup() 和 dup2() 系统调用来复制文件描述符。Linux shell 使用这些系统调用来实现 I/O 重定向。以下是这些调用的简要说明：

```
#include <unistd.h>
int dup(int olddes);
int dup2(int olddes, int newdes);

Success: A newly allocated file descriptor
Failure: -1 and kernel variable errno set to indicate the type of error
```

dup() 调用复制 PPFDT 中现有的文件描述符 olddes，并返回复制的文件描述符。如前所述，新文件描述符是 PPFDT 中最小的未使用描述符。旧文件描述符和新文件描述符指向 SFT 中的同一个条目。因此，读/写文件指针、文件内容和文件属性的更改通过这两个描述符都是可见的。无论描述符指向的文件类型是普通文件、管道、套接字还是 FIFO，这一点都成立。

dup2() 调用与 dup() 类似，不同之处在于新分配的描述符被明确指定为第二个参数。如果 olddes 是有效描述符且等于 newdes，则调用成功并执行空操作；也就是说，它不执行任何操作。如果 olddes 是有效描述符但不等于 newdes，则 dup2() 调用首先释放 newdes，然后执行复制操作。如果 olddes 不是有效描述符，则调用失败，且不执行复制操作。

这些调用可能因表 16.7 中指定的原因而失败。

这些调用通常用于实现进程的输入、输出和错误重定向（参见第 9 章）。你可以通过关闭进程的标准输入、打开需要重定向输入的文件，以及将文件描述符复制到 PPFDT 中用于标准输入的槽位，从而将标准输入附加到该文件。类似地，你也可以对进程进行输出和错误重定向。

以下程序展示了 dup() 系统调用的示例用法。该程序将一个文件作为命令行参数，以写入方式打开该文件，并将该文件的文件描述符保存在 fd 中。如果文件不存在，程序会创建它并设置其访问权限为可读可写。然后，程序使用 close(1) 系统调用关闭标准输出的文件描述符。标准文件描述符关闭后，PPFDT 的 1 号槽位变为空闲，dup(fd) 系统调用会将 PPFDT 中 fd 的条目复制到 1 号槽位。完成此操作后，所有发送到标准输出的内容都会被发送到打开的文件。因此，printf() 调用的输出被重定向到作为命令行参数传入的文件。在下面的会话中，我们将 foo 作为命令行参数传递给程序。cat foo 命令的输出验证了标准输出已被重定向到 foo。

```
$ cat dup.c
#include <fcntl.h>
#include <sys/stat.h>

int main(int argc, char *argv[])
{
    int fd;
```


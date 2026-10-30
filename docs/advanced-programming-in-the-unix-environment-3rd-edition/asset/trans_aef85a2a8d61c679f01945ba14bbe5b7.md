

struct flock    lock;

lock.l_type = type;       /* F_RDLCK or F_WRLCK */
lock.l_start = offset;    /* byte offset, relative to l_whence */
lock.l_whence = whence;   /* SEEK_SET, SEEK_CUR, SEEK_END */
lock.l_len = len;         /* #bytes (0 means to EOF) */

if (fcntl(fd, F_GETLK, &lock) < 0)
    err_sys("fcntl error");

if (lock.l_type == F_UNLCK)
    return(0);             /* false, region isn't locked by another proc */
return(lock.l_pid);        /* true, return pid of lock owner */
}

图 14.6 测试锁定条件的函数

如果存在会阻止所请求参数的锁，此函数返回持有该锁的进程 ID。否则，函数返回 0（假）。我们通常从以下两个宏（在 apue.h 中定义）调用此函数：

```
#define is_read_lockable(fd, offset, whence, len) \
        (lock_test((fd), F_RDLCK, (offset), (whence), (len)) == 0)
#define is_write_lockable(fd, offset, whence, len) \
        (lock_test((fd), F_WRLCK, (offset), (whence), (len)) == 0)
```

请注意，lock_test 函数不能由进程用来查看它当前是否持有文件的一部分的锁。F_GETLK 命令的定义指出，返回的信息适用于会阻止我们创建自己的锁的现有锁。由于 F_SETLK 和 F_SETLKW 命令总是在存在时替换进程的现有锁，我们永远不会因自己的锁而被阻塞；因此，F_GETLK 命令永远不会报告我们自己的锁。

## 示例—死锁

当两个进程各自等待对方锁定的资源时，就会发生死锁。如果控制了锁定区域的进程在尝试锁定由另一个进程控制的另一个区域时被挂起，则存在死锁的可能性。

图 14.7 显示了死锁的示例。子进程锁定字节 0，父进程锁定字节 1。随后各自尝试锁定对方已锁定的字节。我们使用第 8.9 节中的父子同步例程（TELL_xxx 和 WAIT_xxx），以便每个进程都能等待另一个进程获得其锁。

```
#include "apue.h"
#include <fcntl.h>

static void
lockabyte(const char *name, int fd, off_t offset)
{
    if (writew_lock(fd, offset, SEEK_SET, 1) < 0)
        err_sys("%s: writew_lock error", name);
    printf("%s: got the lock, byte %lld\n", name, (long long)offset);
}
int
main(void)
{
    int     fd;
    pid_t   pid;

    /*
     * Create a file and write two bytes to it.
     */
    if ((fd = creat("templock", FILE_MODE)) < 0)
        err_sys("create error");
    if (write(fd, "ab", 2) != 2)
        err_sys("write error");

    TELL_WAIT();
    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) {    /* child */
        lockabyte("child", fd, 0);
        TELL_PARENT(getppid());
        WAIT_PARENT();
        lockabyte("child", fd, 1);
    } else {                /* parent */
        lockabyte("parent", fd, 1);
        TELL_CHILD(pid);
        WAIT_CHILD();
        lockabyte("parent", fd, 0);
    }
    exit(0);
}
```

# 图 14.7 死锁检测示例

运行图 14.7 中的程序，我们得到

```
$ ./a.out
parent: got the lock, byte 1
child: got the lock, byte 0
parent: writew_lock error: Resource deadlock avoided
child: got the lock, byte 1
```

当检测到死锁时，内核必须选择一个进程返回错误。在此示例中，父进程被选中，但这是实现细节。在某些系统上，子进程总是收到错误。在其他系统上，父进程总是收到错误。在某些系统上，随着多次锁定尝试，你甚至可能会看到错误在子进程和父进程之间分配。

## 锁的隐式继承与释放

自动继承和释放记录锁遵循三条规则。

- 1. 锁与进程和文件相关联。这有两个含义。第一个很明显：当进程终止时，其所有锁都会被释放。第二个则不那么明显：每当关闭一个描述符时，该进程对该描述符引用的文件的所有锁都会被释放。这意味着如果我们进行如下调用

```
fd1 = open(pathname, ...);
read_lock(fd1, ...);
fd2 = dup(fd1);
close(fd2);
```

在 close(fd2) 之后，在 fd1 上获得的锁将被释放。如果我们用 open 替换 dup，如下所示

```
fd1 = open(pathname, ...);
read_lock(fd1, ...);
fd2 = open(pathname, ...);
close(fd2);
```

以在另一个描述符上打开同一文件，也会发生同样的情况。

- 2. 锁永远不会通过 fork 继承给子进程。这意味着如果进程获得锁然后调用 fork，子进程在锁方面被视为与父进程获得的锁不同的另一个进程。子进程必须调用 fcntl 在 fork 跨越继承的任何描述符上获得自己的锁。此限制是有意义的，因为锁的目的是防止多个进程同时写入同一文件。如果子进程在 fork 后继承锁，父进程和子进程都可能同时写入同一文件。

- 3. 锁会被新程序在 exec 时继承。需要注意的是，如果为文件描述符设置了 close-on-exec 标志，则在 exec 期间关闭描述符时，所有底层文件的锁都会被释放。

## FreeBSD 实现

让我们简要查看 FreeBSD 实现中使用的数据结构。这有助于阐明规则 1，即锁与进程和文件相关联。

考虑一个执行以下语句的进程（忽略错误返回）：

```
fd1 = open(pathname, ...);
write_lock(fd1, 0, SEEK_SET, 1);    /* parent write locks byte 0 */
if (pid = fork()) {                   /* parent */
    fd2 = dup(fd1);
    fd3 = open(pathname, ...);
} else if (pid == 0) {                 /* child */
    read_lock(fd1, 1, SEEK_SET, 1);   /* child read locks byte 1 */
}
pause();
```

图 14.8 显示了父进程和子进程都暂停后得到的结果数据结构。

![](img/244bf0c3b6d0288ae397336907e37851_526_0.png)

**图 14.8** FreeBSD 记录锁的数据结构

我们展示了 open、fork 和 dup 调用产生的数据结构（图 3.9 和 8.2）。这里新的是从 i-node 结构链接起来的锁结构。每个锁结构描述给定进程的一个锁定区域（由偏移量和长度定义）。我们展示了两个这样的结构：一个用于父进程对 write_lock 的调用，一个用于子进程对 read_lock 的调用。每个结构都包含相应的进程 ID。

在父进程中，关闭 fd1、fd2 或 fd3 中的任何一个都会导致父进程的锁被释放。当关闭这三个文件描述符中的任何一个时，内核会遍历对应 i-node 的锁链表并释放调用进程持有的锁。内核无法分辨（也不关心）父进程使用这三个描述符中的哪一个获得了锁。

## 示例

在图 13.6 的程序中，我们看到守护进程如何使用文件上的锁来确保只有一个副本在运行。图 14.9 显示了守护进程用于在文件上放置写锁的 lockfile 函数的实现。

```
#include <unistd.h>
#include <fcntl.h>
int
lockfile(int fd)
{
    struct flock fl;
    fl.l_type = F_WRLCK;
    fl.l_start = 0;
    fl.l_whence = SEEK_SET;
    fl.l_len = 0;
    return(fcntl(fd, F_SETLK, &fl));
}
```

图 14.9 在整个文件上放置写锁

或者，我们也可以用 write_lock 函数来定义 lockfile 函数：

```
#define lockfile(fd) write_lock((fd), 0, SEEK_SET, 0)
```

## 文件末尾的锁

在相对于文件末尾锁定或解锁字节范围时，我们需要谨慎。大多数实现会将 l_whence 值 SEEK_CUR 或 SEEK_END 转换为绝对文件偏移量，使用 l_start 和文件的当前位置或当前长度。然而，通常我们需要相对于文件当前长度指定锁，但我们不能调用 fstat 来获取当前文件大小，因为我们没有对文件的锁。（在调用 fstat 和锁调用之间，另一个进程可能会更改文件的长度。）


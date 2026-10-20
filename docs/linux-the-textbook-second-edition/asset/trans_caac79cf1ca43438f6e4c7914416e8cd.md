
`open()` 系统调用会跟随符号链接，并访问该链接所指向文件的数据或属性。如果你想读取符号链接本身的数据或属性，则必须使用 `readlink()` 系统调用。类似地，`creat()` 系统调用只能创建普通文件。如果你想创建符号链接，应使用 `symlink()` 系统调用。你可以浏览这些调用的手册页以了解更多信息。

## 练习 15.6

给出 `symlink()` 和 `readlink()` 系统调用的原型，并简要描述这些调用的每个参数。

## 15.8.2 关闭文件

可以使用 `close()` 系统调用关闭文件，它接受一个文件描述符作为参数，并释放与给定描述符对应的 PPFDT 槽位。下面是对该调用的简要描述：

```
#include <unistd.h>
int close(int fd);

Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

`close()` 系统调用可能因多种原因失败。表 15.5 列出了两个常见原因，以及这些错误对应的 `errno` 变量符号值。

如果一个打开的文件正在被多个进程引用——也就是说，如果多个 PPFDT 中的条目指向 SFT 中的某个条目——那么关闭该文件只会释放相关 PPFDT 中的条目，并将引用计数减 1。只有当这个引用计数变为 0 时，文件才被关闭。当进程终止时，内核会自动关闭其所有打开的文件。

在下面的示例中，我们打开作为唯一命令行参数传入的文件，显示该文件的文件描述符，然后关闭该文件。示例程序的编译和执行结果显示在程序输出中。我们使用带有 -w 选项的编译命令来抑制警告信息。

```
$ cat open_close.c
#include <fcntl.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
    int fd;

        /* Open file */
        if (argc == 1) {
                printf("No file specified as command line argument.\n");
                exit(1);
        }
        if ((fd = open(argv[1], O_RDWR)) == -1) {
                perror("File opening");
```

**表 15.5**  
`close()` 系统调用失败的常见原因

| 失败原因 | `errno` 的值 |
|---|---|
| `fd` 不是活动描述符，即不对应打开的文件 | `EBADF` |
| 关闭文件的操作被信号中断 | `EINTR` |

```
exit(1);
} else
        printf("The file descriptor is %d.\n",fd);
/* Close file */
if (close(fd) == -1) {
        perror("File closing");
        exit(1);
}
else
        printf("File closed successfully.\n");
exit(0);
}
$ gcc open_close.c -w
$ man talk > foobar
$ a.out foobar
The file descriptor is 3.
File closed successfully.
$
```

注意，这是该进程打开的第一个（也是唯一一个）文件。由于内核已经为该进程打开了标准文件，当程序打开 **foobar** 时，内核分配了文件描述符 3。

现在我们稍微修改程序，使它先关闭标准输入，然后打开作为命令行参数传入的文件。为此，我们只需在 open() 系统调用之前插入下面一行：

```
close(0);
```

以下是更新后的程序：

```
$ cat open_close_new.c
#include <fcntl.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
        int fd;

        /* Open file */
        if (argc == 1) {
                printf("No file specified as command line argument.\n");
                exit(1);
        }
        close(0); /* Close standard input */
        if ((fd = open(argv[1], O_RDWR)) == -1) {
                perror("File opening");
                exit(1);
        } else
                printf("The file descriptor is %d.\n",fd);
        /* Close file */
        if (close(fd) == -1) {
                perror("File closing");
                exit(1);
        }
        else
                printf("File closed successfully.\n");
        exit(0);
}
$ gcc open_close_new.c -w
$ a.out foobar
The file descriptor is 0.
```

```
File closed successfully.
$
```

如你所见，正如预期的那样，内核将文件描述符 0 分配给了新打开的文件 **foobar**。

## 练习 15.7

编译并运行 15.8.1 和 15.8.2 节中给出的程序。它们是否能按预期工作？

## 15.8.3 从文件读取

一旦使用 open() 系统调用打开了文件，就可以使用 read() 系统调用读取其内容。下面是对 read() 调用的简要描述：

```
#include <sys/types.h>
#include <unistd.h>
ssize_t read(int fd, void *buf, size_t nbytes);

Success: 0

Failure: -1 and kernel variable errno set to indicate the type of error
```

该调用尝试从文件描述符 fd 对应的文件中读取 nbytes 字节到 buf 所指向的主内存区域。数据从读写文件指针的当前位置开始读取。完成后，read() 调用返回实际读取的字节数，该值可能小于 nbytes。文件指针会按实际读取的字节数前进。对于普通文件，如果文件中在 EOF 之前还剩余这么多字节，该调用保证读取 nbytes 字节。但是，对于其他文件（如管道或套接字，见第 16、W20 和 W21 章），则不保证。当 read() 系统调用遇到 EOF 时返回 0。

失败时，read() 返回 -1，并设置 errno 以指示失败原因。表 15.6 显示了 read() 调用对普通文件失败的一些常见原因。

# 表 15.6

read() 系统调用失败的一些常见原因

| 失败原因 | errno 的值 |
|---|---|
| fd 参数不是有效的读取描述符 | EBADF |
| buf 参数指向进程地址空间之外的内存位置 | EFAULT |
| 从文件系统读取时发生 I/O 错误 | EIO |
| 文件读取操作被中断 | EINTR |
| 与 fd 参数关联的指针为负数 | EINVAL |
| nbytes 值大于 INT_MAX，即整数的最大值 | EINVAL |

## 15.8.4 写入文件

一旦使用 open() 或 creat() 系统调用打开了文件，就可以使用 write() 系统调用向其中写入数据。下面是对 write() 调用的简要描述：

```
#include <sys/types.h>
#include <unistd.h>
ssize_t write(int fd, const void *buf, size_t nbytes);

Success: 0

Failure: -1 and kernel variable errno set to indicate the type of error
```

# 表 15.7

write() 系统调用失败的一些常见原因

| 失败原因 | errno 的值 |
|---|---|
| fd 参数不是有效的写入描述符 | EBADF |
| fd 参数与负指针关联 | EINVAL |
| 已超出进程文件大小限制或最大文件大小限制 | EFBIG |
| 包含该文件的文件系统已满 | ENOSPC |
| 用户在该文件系统上的磁盘块配额已耗尽 | EDQUOT |
| 从文件系统读取时发生 I/O 错误 | EIO |
| 文件读取操作被中断 | EINTR |
| nbytes 值大于 INT_MAX，即整数的最大值 | EINVAL |

该调用尝试将 buf 指向的主内存区域中的 nbytes 字节写入文件描述符 fd 对应的文件。数据从读写文件指针的当前位置开始写入。完成后，write() 调用返回实际写入的字节数，该值可能小于 nbytes。文件指针会按实际写入的字节数前进。对于普通文件，如果磁盘未满或文件大小未超过 Linux 系统支持的最大文件大小，该调用保证写入 nbytes 字节。但是，对于其他文件（如套接字，见第 W20 章），则不保证。

失败时，write() 返回 -1，并设置 errno 以指示失败原因。表 15.7 显示了 read() 调用对普通文件失败的一些常见原因。

现在我们增强 open_close.c 程序，将其转换为一个文件复制程序 cpy，语法如下：

```
cpy source target
```

该程序将源文件（一个已存在的文件）复制到目标文件（一个不存在的文件）。示例程序的编译和执行结果显示在程序输出中。

```
$ cat cpy.c
#include <fcntl.h>
#include <unistd.h>

#define SIZE 512

void closefd(int);

int main(int argc, char *argv[])
{
    int rfd, wfd, nr, nw;
    char buf[SIZE];

    if (argc != 3) {
        printf("Inappropriate number of command line arguments.\n");
        exit(0);
    }
    /* Open the source file for reading */
    if ((rfd = open(argv[1], O_RDONLY)) == -1) {
        perror("Source file opening");
        exit(1);
    }
    /* Open the destination file for writing */
    if ((wfd = open(argv[2], O_CREAT | O_WRONLY | O_TRUNC, 0666)) == -1) {
        perror("Creation and opening of destination file");
        exit(1);
    }
}
```


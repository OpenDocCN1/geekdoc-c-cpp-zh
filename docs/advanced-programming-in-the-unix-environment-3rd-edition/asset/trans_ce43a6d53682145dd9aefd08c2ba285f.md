

3.6 如果使用追加标志以读写方式打开一个文件，是否仍能使用 lseek 从文件的任意位置读取？能否使用 lseek 替换文件中的现有数据？编写一个程序来验证这一点。

## 4 文件和目录

### 4.1 引言

在上一章中我们介绍了执行 I/O 的基本函数。讨论集中于对普通文件的 I/O——打开文件，以及读写文件。现在我们将研究文件系统的附加特性以及文件的属性。我们将从 stat 函数开始，并遍历 stat 结构体的每个成员，查看文件的全部属性。在此过程中，我们还将描述修改这些属性的每个函数：更改所有者、更改权限等等。我们还将更详细地研究 UNIX 文件系统的结构和符号链接。本章最后介绍操作目录的函数，并开发一个遍历目录层次结构的函数。

### 4.2 stat、fstat、fstatat 和 lstat 函数

本章的讨论集中于四个 stat 函数及其返回的信息。

```
#include <sys/stat.h>

int stat(const char *restrict pathname, struct stat *restrict buf);
int fstat(int fd, struct stat *buf);
int lstat(const char *restrict pathname, struct stat *restrict buf);
int fstatat(int fd, const char *restrict pathname,
    struct stat *restrict buf, int flag);

All four return: 0 if OK, -1 on error
```

给定一个路径名，stat 函数返回有关命名文件的信息结构。fstat 函数获取已在描述符 fd 上打开的文件的信息。lstat 函数与 stat 类似，但当命名文件是符号链接时，lstat 返回有关符号链接本身的信息，而不是符号链接引用的文件的信息。（我们在第 4.22 节遍历目录层次结构时需要 lstat。我们将在第 4.17 节更详细地描述符号链接。）

fstatat 函数提供了一种根据 fd 参数表示的打开目录返回相对于该目录的路径名的文件统计信息的方法。flag 控制是否跟随符号链接；当设置 AT_SYMLINK_NOFOLLOW 标志时，fstatat 不会跟随符号链接，而是返回链接本身的信息。否则，默认行为是跟随符号链接，返回符号链接指向的文件的信息。如果 fd 参数的值为 AT_FDCWD 且路径名参数是相对路径名，则 fstatat 将相对于当前目录计算路径名参数。如果路径名参数是绝对路径名，则 fd 参数将被忽略。在这两种情况下，fstatat 的行为类似于 stat 或 lstat，具体取决于 flag 的值。

buf 参数是指向我们必须提供的结构体的指针。函数会填充该结构体。结构体的定义在不同实现中可能有所不同，但它可能如下所示

```
struct stat {
    mode_t      st_mode;     /* file type & mode (permissions) */
    ino_t       st_ino;      /* i-node number (serial number) */
    dev_t       st_dev;      /* device number (file system) */
    dev_t       st_rdev;     /* device number for special files */
    nlink_t     st_nlink;    /* number of links */
    uid_t       st_uid;      /* user ID of owner */
    gid_t       st_gid;      /* group ID of owner */
    off_t       st_size;     /* size in bytes, for regular files */
    struct timespec st_atim; /* time of last access */
    struct timespec st_mtim; /* time of last modification */
    struct timespec st_ctim; /* time of last file status change */
    blksize_t   st_blksize;  /* best I/O block size */
    blkcnt_t    st_blocks;   /* number of disk blocks allocated */
};
```

st_rdev、st_blksize 和 st_blocks 字段不是 POSIX.1 所要求的。它们作为 Single UNIX Specification 中的 XSI 选项的一部分定义。

timespec 结构类型以秒和纳秒为单位定义时间。它至少包含以下字段：

```
time_t tv_sec;
long  tv_nsec;
```

在 2008 年版标准之前，时间字段命名为 st_atime、st_mtime 和 st_ctime，且类型为 time_t（以秒表示）。timespec 结构使时间戳具有更高分辨率。为了兼容，旧名称可以用 tv_sec 成员定义。例如，st_atime 可以定义为 st_atim.tv_sec。

请注意，stat 结构的大多数成员由原始系统数据类型指定（参见第 2.8 节）。我们将遍历该结构体的每个成员以检查文件的属性。

stat 函数的最大使用者可能是 ls -l 命令，用于了解有关文件的所有信息。

### 4.3 文件类型

到目前为止，我们谈到了两种不同的文件类型：普通文件和目录。大多数 UNIX 系统上的文件都是普通文件或目录，但还有其他类型的文件。类型如下

- 1. 普通文件。最常见的文件类型，包含某种形式的数据。UNIX 内核不会区分此数据是文本还是二进制。对普通文件内容的任何解释都留给处理该文件的应用程序。

  > 一个值得注意的例外是二进制可执行文件。要执行程序，内核必须理解其格式。所有二进制可执行文件都符合一种格式，允许内核识别程序的文本和数据应加载的位置。

- 2. 目录文件。包含其他文件名称以及这些文件信息的指针的文件。任何对目录文件具有读权限的进程都可以读取目录的内容，但只有内核可以直接写入目录文件。进程必须使用本章描述的函数来更改目录。

- 3. 块特殊文件。一种提供对磁盘驱动器等设备进行缓冲的固定大小单元 I/O 访问的文件类型。

  > 请注意，FreeBSD 不再支持块特殊文件。所有对设备的访问都通过字符特殊接口进行。

- 4. 字符特殊文件。一种提供对设备进行无缓冲的变长单元 I/O 访问的文件类型。系统上的所有设备都是块特殊文件或字符特殊文件。

- 5. FIFO。用于进程间通信的文件类型。有时称为命名管道。我们在第 15.5 节描述 FIFO。

- 6. 套接字。用于进程间网络通信的文件类型。套接字也可以用于单台主机上进程之间的非网络通信。我们在第 16 章使用套接字进行进程间通信。

- 7. 符号链接。指向另一个文件的文件类型。我们在第 4.17 节更详细地讨论符号链接。

文件的类型编码在 stat 结构体的 st_mode 成员中。我们可以使用图 4.1 所示的宏确定文件类型。这些宏的参数是来自 stat 结构体的 st_mode 成员。

| Macro | Type of file |
|---|---|
| S_ISREG() | regular file |
| S_ISDIR() | directory file |
| S_ISCHR() | character special file |
| S_ISBLK() | block special file |
| S_ISFIFO() | pipe or FIFO |
| S_ISLNK() | symbolic link |
| S_ISSOCK() | socket |

Figure 4.1 File type macros in <sys/stat.h>

POSIX.1 允许实现将进程间通信（IPC）对象，如消息队列和信号量，表示为文件。图 4.2 所示的宏允许我们从 stat 结构确定 IPC 对象的类型。与图 4.1 中的宏不同，这些宏的参数不是 st_mode 成员，而是指向 stat 结构的指针。

| Macro | Type of object |
|---|---|
| S_TYPEISMQ() | message queue |
| S_TYPEISSEM() | semaphore |
| S_TYPEISSHM() | shared memory object |

Figure 4.2 IPC type macros in <sys/stat.h>

消息队列、信号量和共享内存对象在第 15 章中讨论。然而，本书中讨论的各种 UNIX 系统实现都不将这些对象表示为文件。

Example

图 4.3 中的程序打印每个命令行参数的文件类型。

```
#include "apue.h"
int
main(int argc, char *argv[])
{
    int i;
    struct stat buf;
    char *ptr;
    for (i = 1; i < argc; i++) {
        printf("%s: ", argv[i]);
        if (lstat(argv[i], &buf) < 0) {
            err_ret("lstat error");
            continue;
        }
        if (S_ISREG(buf.st_mode))
            ptr = "regular";
        else if (S_ISDIR(buf.st_mode))
```



fullpath[n] = 0;

if ((dp = opendir(fullpath)) == NULL)  /* 无法读取目录 */
    return(func(fullpath, &statbuf, FTW_DNR));

while (((dirp = readdir(dp)) != NULL)) {
    if (strcmp(dirp->d_name, ".") == 0 ||
        strcmp(dirp->d_name, "..") == 0)
        continue;        /* 忽略点和点点 */
    strcpy(&fullpath[n], dirp->d_name); /* 在“/”后追加名称 */
    if ((ret = dopath(func)) != 0)      /* 递归 */
        break;   /* 退出时机 */
    }
    fullpath[n-1] = 0;  /* 擦除从斜杠开始的所有内容 */
    if (closeddir(dp) < 0)
        err_ret("无法关闭目录 %s", fullpath);
    return(ret);
}

static int
myfunc(const char *pathname, const struct stat *statptr, int type)
{
    switch (type) {
    case FTW_F:
        switch (statptr->st_mode & S_IFMT) {
        case S_IFREG:  nreg++;  break;
        case S_IFBLK:  nblk++;  break;
        case S_IFCHR:  nchr++;  break;
        case S_IFIFO:  nifo++;  break;
        case S_IFLNK:  nslink++; break;
        case S_IFSOCK: nsock++; break;
        case S_IFDIR:  /* 目录的类型应为 FTW_D */
            err_dump("对于 %s，类型为 S_IFDIR", pathname);
        }
        break;
    case FTW_D:
        ndir++;
        break;
    case FTW_DNR:
        err_ret("无法读取目录 %s", pathname);
        break;
    case FTW_NS:
        err_ret("%s 的 stat 错误", pathname);
        break;
    default:
        err_dump("路径名 %s 的未知类型 %d", pathname, type);
    }
    return(0);
}

为了说明 ftw 和 nftw 函数，本程序提供了比实际需要更多的通用性。例如，函数 myfunc 始终返回 0，尽管调用它的函数已经准备好处理非零返回值。

有关遍历文件系统，以及在许多标准 UNIX 系统命令（如 find、ls、tar 等）中使用这种技术的更多信息，请参阅 Fowler、Korn 和 Vo [1989]。

## 4.23 chdir、fchdir 和 getcwd 函数

每个进程都有一个当前工作目录。所有相对路径名的搜索都从该目录开始（即所有不以斜杠开头的路径名）。当用户登录 UNIX 系统时，当前工作目录通常从 `/etc/passwd` 文件的第六个字段所指定的目录开始，即用户的主目录。当前工作目录是进程的属性；主目录是登录名的属性。

我们可以通过调用 chdir 或 fchdir 函数来更改调用进程的当前工作目录。

```
#include <unistd.h>
int chdir(const char *pathname);
int fchdir(int fd);

两者均返回：成功返回 0，出错返回 -1
```

我们既可以将路径名指定为新的当前工作目录，也可以通过打开的文件描述符指定。

### 示例

由于当前工作目录是进程的属性，因此执行 chdir 的进程所调用的进程不会受到当前工作目录变化的影响。（我们将在第 8 章中更详细地介绍进程之间的关系。）因此，图 4.23 中的程序并不会执行我们所预期的操作。

```
#include "apue.h"
int
main(void)
{
    if (chdir("/tmp") < 0)
        err_sys("chdir failed");
    printf("chdir to /tmp succeeded\n");
    exit(0);
}
```

图 4.23 chdir 函数示例

如果我们编译此程序，将可执行文件命名为 mycd，然后运行它，会得到以下结果：

```
$ pwd
/usr/lib
$ mycd
chdir to /tmp succeeded
$ pwd
/usr/lib
```

执行 mycd 程序的 shell 的当前工作目录并没有改变。这是 shell 执行程序方式所产生的副作用。每个程序都在独立的进程中运行，因此 shell 的当前工作目录不会受到程序中 chdir 调用的影响。正因为如此，chdir 函数必须直接由 shell 调用，所以 cd 命令被内置在 shell 中。

由于内核必须维护当前工作目录的信息，因此我们应该能够获取它的当前值。遗憾的是，内核并不维护目录的完整路径名。相反，内核保存有关该目录的信息，例如指向目录 v-node 的指针。

> Linux 内核能够确定完整路径名。路径名的各个组成部分分散在挂载表和 dcache 表中；例如，当读取 `/proc/self/cwd` 符号链接时，内核会重新组装这些组成部分。

我们需要一个从当前工作目录（点）开始，沿目录层次结构向上移动的函数，并使用点点来向上移动一级。在每一级中，该函数读取目录项，直到找到与刚刚离开的目录的 i-node 对应的名称。重复此过程，直到遇到根目录，就能得到当前工作目录的完整绝对路径名。幸运的是，已经存在一个函数可以替我们完成这项工作。

```
#include <unistd.h>

char *getcwd(char *buf, size_t size);

返回：成功返回 buf，出错返回 NULL
```

我们必须将缓冲区 buf 的地址及其大小（以字节为单位）传递给该函数。缓冲区必须足够容纳绝对路径名以及结尾的空字节，否则将返回错误。（回顾第 2.5.5 节关于为最大长度路径名分配空间的讨论。）

> 某些较旧的 getcwd 实现允许第一个参数 buf 为 NULL。在这种情况下，函数会调用 malloc 动态分配 size 个字节。这并不是 POSIX.1 或 Single UNIX Specification 的一部分，因此应避免使用这种方式。

### 示例

图 4.24 中的程序切换到一个特定目录，然后调用 getcwd 打印工作目录。如果运行该程序，会得到：

```
$ ./a.out
cwd = /var/spool/uucppublic
$ ls -l /usr/spool
lrwxrwxrwx 1 root 12 Jan 31 07:57 /usr/spool -> ../var/spool
```

```
#include "apue.h"
int
main(void)
{
    char    *ptr;
    size_t   size;
    if (chdir("/usr/spool/uucppublic") < 0)
        err_sys("chdir failed");
    ptr = path_alloc(&size);    /* 我们自己的函数 */
    if (getcwd(ptr, size) == NULL)
        err_sys("getcwd failed");
    printf("cwd = %s\n", ptr);
    exit(0);
}
```

# 图 4.24 getcwd 函数示例

请注意，chdir 会跟随符号链接——正如我们从图 4.17 中所预期的那样；但是，当沿目录树向上移动时，getcwd 并不知道到达 `/var/spool` 目录时，该目录是由符号链接 `/usr/spool` 指向的。这是符号链接的一个特性。

当应用程序需要返回文件系统中最初启动的位置时，getcwd 函数非常有用。我们可以在更改工作目录之前调用 getcwd，保存起始位置。处理完成后，可以将 getcwd 获得的路径名传递给 chdir，从而返回文件系统中的起始位置。

fchdir 函数为完成此任务提供了一种简便方法。我们不必调用 getcwd，而是可以在切换到文件系统中的其他位置之前打开当前目录，并保存文件描述符。当希望返回起始位置时，只需将该文件描述符传递给 fchdir 即可。

## 4.24 设备特殊文件

st_dev 和 st_rdev 这两个字段经常被混淆。在第 18.9 节编写 ttyname 函数时，我们需要使用这些字段。它们的使用规则很简单。

- 每个文件系统都由其主设备号和次设备号标识，这两个号码编码在基本系统数据类型 dev_t 中。主设备号用于标识设备驱动程序，有时还编码需要通信的外设板；次设备号用于标识具体的子设备。回顾图 4.13，磁盘驱动器通常包含多个文件系统。同一磁盘驱动器上的每个文件系统通常具有相同的主设备号，但具有不同的次设备号。

- 我们通常可以通过大多数实现定义的两个宏 major 和 minor 来访问主设备号和次设备号。因此，我们不必关心这两个号码在 dev_t 对象中的存储方式。

早期系统将设备号存储在 16 位整数中，其中主设备号占 8 位，次设备号占 8 位。FreeBSD 8.0 和 Mac OS X 10.6.8 使用 32 位整数，其中主设备号占 8 位，次设备号占 24 位。在 32 位系统中，Solaris 10 使用 32 位整数表示 dev_t，其中主设备号占 14 位，次设备号占 18 位。在 64 位系统中，Solaris 10 将 dev_t 表示为 64 位整数，两个号码各占 32 位。在 Linux 3.2.0 中，虽然 dev_t 是 64 位整数，但主设备号仅使用 12 位，次设备号使用 20 位。

POSIX.1 规定存在 dev_t 类型，但没有定义它包含什么内容，也没有定义如何访问其内容。大多数实现都定义了 major 和 minor 宏。它们定义所在的头文件取决于系统。在基于 BSD 的系统中，它们位于 `<sys/types.h>` 中。Solaris 在 `<sys/mkdev.h>` 中定义了这两个宏的函数原型，因为 Solaris 中 `<sys/sysmacros.h>` 内的宏定义已被视为过时。Linux 在 `<sys/sysmacros.h>` 中定义这些宏，而 `<sys/types.h>` 会包含该文件。

- 系统中每个文件名的 st_dev 值，都是包含该文件名及其对应 i-node 的文件系统的设备号。

- 只有字符特殊文件和块特殊文件具有 st_rdev 值。该值包含实际设备的设备号。

### 示例

图 4.25 中的程序打印每个命令行参数的设备号。此外，如果参数指向字符特殊文件或块特殊文件，还会打印该特殊文件的 st_rdev 值。

```
#include "apue.h"
#ifdef SOLARIS
#include <sys/mkdev.h>
#endif

int
main(int argc, char *argv[])
{
    int         i;
    struct stat buf;

    for (i = 1; i < argc; i++) {
        printf("%s: ", argv[i]);
        if (stat(argv[i], &buf) < 0) {
            err_ret("stat error");
            continue;
        }

        printf("dev = %d/%d", major(buf.st_dev),  minor(buf.st_dev));
```


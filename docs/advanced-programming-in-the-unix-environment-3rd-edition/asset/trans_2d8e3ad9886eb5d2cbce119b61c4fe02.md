

```
#include <unistd.h>
int rmdir(const char *pathname);

Returns: 0 if OK, -1 on error
```

如果通过此调用目录的链接计数变为 0，并且如果没有其他进程打开该目录，则目录占用的空间将被释放。如果在链接计数达到 0 时有一个或多个进程打开该目录，则在该函数返回之前会删除最后一个链接并删除点和点点条目。此外，不能在该目录中创建新文件。目录不会被释放，直到最后一个进程关闭它为止。（即使有其他进程打开了该目录，它也无法在目录中做太多事情，因为 rmdir 函数成功的前提是目录必须为空。）

## 4.22 读取目录

任何具有读取目录访问权限的人都可以读取目录。但只有内核可以写入目录，以保持文件系统的一致性。回顾第 4.5 节，目录的写权限位和执行权限位决定了我们是否可以在目录中创建新文件以及从目录中删除文件——它们并不指定我们是否可以写入目录本身。

目录的实际格式取决于 UNIX 系统的实现和文件系统的设计。早期系统，如 Version 7，具有简单的结构：每个目录条目为 16 字节，其中 14 字节用于文件名，2 字节用于 i-node 编号。当在 4.2BSD 中添加更长的文件名时，每个条目变为变长，这意味着读取目录的任何程序现在都依赖于系统。为了简化读取目录的过程，开发了一组目录例程，并且是 POSIX.1 的一部分。许多实现阻止应用程序使用 read 函数访问目录的内容，从而进一步将应用程序与目录格式的实现特定细节隔离开来。

```
#include <dirent.h>

DIR *opendir(const char *pathname);
DIR *fdopendir(int fd);

Both return: pointer if OK, NULL on error

struct dirent *readdir(DIR *dp);
Returns: pointer if OK, NULL at end of directory or error

void rewinddir(DIR *dp);
int closedir(DIR *dp);

Returns: 0 if OK, -1 on error

long telldir(DIR *dp);
Returns: current location in directory associated with dp

void seekdir(DIR *dp, long loc);
```

fdopendir 函数首次出现在 Single UNIX Specification 的第 4 版中。它提供了一种将打开的文件描述符转换为用于目录处理函数的 DIR 结构的方法。

telldir 和 seekdir 函数不是 POSIX.1 基础标准的一部分。它们包含在 Single UNIX Specification 的 XSI 选项中，因此所有符合的 UNIX 系统实现都预计提供它们。

回顾我们在图 1.3 中所示的程序中使用了其中几个函数，我们的 ls 命令的简易实现。

在 <dirent.h> 中定义的 dirent 结构依赖于实现。实现定义该结构至少包含以下两个成员：

```
ino_t d_ino;        /* i-node number */
char * d_name[];    /* null-terminated filename */
```

d_ino 条目未由 POSIX.1 定义，因为它是实现特性，但它作为 POSIX.1 中的 XSI 选项的一部分而定义。POSIX.1 仅在此结构中定义 d_name 条目。

请注意，d_name 条目的大小未指定，但保证至少容纳 NAME_MAX 个字符，不包括终止空字节（回顾图 2.15。）由于文件名以 null 结尾，因此 d_name 在头文件中如何定义并不重要，因为数组大小并不表示文件名的长度。

DIR 结构是这些七个函数使用的内部结构，用于维护有关正在读取的目录的信息。DIR 结构的目的类似于标准 I/O 库维护的 FILE 结构，我们将在第 5 章中描述它。

opendir 和 fdopendir 返回的指向 DIR 结构的指针随后与另外五个函数一起使用。opendir 函数初始化事物，以便第一次 readdir 返回目录中的第一个条目。当 DIR 结构由 fdopendir 创建时，readdir 返回的第一个条目取决于传递给 fdopendir 的文件描述符关联的文件偏移量。请注意，目录内条目的顺序依赖于实现，通常不是按字母顺序排列的。

### 示例

我们将使用这些目录例程编写一个遍历文件层次结构的程序。目标是生成图 4.4 中所示的各种文件类型的计数。图 4.22 中所示的程序接受单个参数——起始路径名——并从该点递归下降层次结构。Solaris 提供了一个函数 ftw(3)，它执行层次结构的实际遍历，为每个文件调用用户定义的函数。该函数的问题在于它为每个文件调用 stat 函数，这会导致程序跟随符号链接。例如，如果我们从根目录开始并且有一个名为 /lib 的符号链接指向 /usr/lib，则 /usr/lib 目录中的所有文件将被计算两次。为了解决这个问题，Solaris 提供了一个额外的函数 nftw(3)，它有一个选项可以阻止它跟随符号链接。虽然我们可以使用 nftw，但我们将编写自己的简单文件遍历器以展示目录例程的使用。

在 SUSv4 中，nftw 作为 XSI 选项的一部分包含在内。实现包含在 FreeBSD 8.0、Linux 3.2.0、Mac OS X 10.6.8 和 Solaris 10 中。（在 SUSv4 中，ftw 函数已被标记为过时。）基于 BSD 的系统有一个不同的函数 fts(3)，它提供类似的功能。它在 FreeBSD 8.0、Linux 3.2.0 和 Mac OS X 10.6.8 中可用。

```
#include "apue.h"
#include <dirent.h>
#include <limits.h>

/* function type that is called for each filename */
typedef int Myfunc(const char *, const struct stat *, int);

static Myfunc myfunc;
static int myftw(char *, Myfunc *);
static int dopath(Myfunc *);

static long nreg, ndir, nblk, nchr, nfifo, nslink, nsock, ntot;

int
main(int argc, char *argv[])
{
    int ret;

    if (argc != 2)
        err_quit("usage: ftw <starting-pathname>");

    ret = myftw(argv[1], myfunc);      /* does it all */
    ntot = nreg + ndir + nblk + nchr + nfifo + nslink + nsock;
    if (ntot == 0)
        ntot = 1;      /* avoid divide by 0; print 0 for all counts */
    printf("regular files  = %7ld, %5.2f %%\n", nreg,
        nreg*100/ntot);
    printf("directories    = %7ld, %5.2f %%\n", ndir,
        ndir*100/ntot);
    printf("block special  = %7ld, %5.2f %%\n", nblk,
        nblk*100/ntot);
    printf("char special   = %7ld, %5.2f %%\n", nchr,
        nchr*100/ntot);
    printf("FIFOs          = %7ld, %5.2f %%\n", nfifo,
        nfifo*100/ntot);
    printf("symbolic links = %7ld, %5.2f %%\n", nslink,
        nslink*100/ntot);
    printf("sockets        = %7ld, %5.2f %%\n", nsock,
        nsock*100/ntot);
    exit(ret);
}

/*
 * Descend through the hierarchy, starting at "pathname".
 * The caller's func() is called for every file.
 */
#define FTW_F 1      /* file other than directory */
#define FTW_D 2      /* directory */
```

```
#define FTW_DNR 3      /* directory that can't be read */
#define FTW_NS  4      /* file that we can't stat */

static char *fullpath;      /* contains full pathname for every file */
static size_t pathlen;

static int                 /* we return whatever func() returns */
myftw(char *pathname, Myfunc *func)
{
    fullpath = path_alloc(&pathlen);      /* malloc PATH_MAX+1 bytes */
                                     /* (Figure 2.16) */
    if (pathlen <= strlen(pathname)) {
        pathlen = strlen(pathname) * 2;
        if ((fullpath = realloc(fullpath, pathlen)) == NULL)
            err_sys("realloc failed");
    }
    strcpy(fullpath, pathname);
    return(dopath(func));
}
/*
 * Descend through the hierarchy, starting at "fullpath".
 * If "fullpath" is anything other than a directory, we lstat() it,
 * call func(), and return.  For a directory, we call ourselves
 * recursively for each name in the directory.
 */
static int                 /* we return whatever func() returns */
dopath(Myfunc* func)
{
    struct stat     statbuf;
    struct dirent   *dirp;
    DIR             *dp;
    int             ret, n;
    if (lstat(fullpath, &statbuf) < 0)  /* stat error */
        return(func(fullpath, &statbuf, FTW_NS));
    if (S_ISDIR(statbuf.st_mode) == 0)  /* not a directory */
        return(func(fullpath, &statbuf, FTW_F));

    /*
     * It's a directory. First call func() for the directory,
     * then process each filename in the directory.
     */
    if ((ret = func(fullpath, &statbuf, FTW_D)) != 0)
        return(ret);
    n = strlen(fullpath);
    if (n + NAME_MAX + 2 > pathlen) {   /* expand path buffer */
        pathlen *= 2;
        if ((fullpath = realloc(fullpath, pathlen)) == NULL)
            err_sys("realloc failed");
    }
    fullpath[n++] = '/';
```

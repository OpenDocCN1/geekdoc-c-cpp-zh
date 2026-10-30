

超级用户可以在文件系统支持的情况下使用 *pathname* 指定一个目录来调用 `unlink`，但应使用 `rmdir` 函数来解除链接目录。我们在第 4.21 节中描述了 `rmdir` 函数。

我们也可以使用 `remove` 函数来解除链接文件或目录。对于文件，`remove` 与 `unlink` 相同。对于目录，`remove` 与 `rmdir` 相同。

```c
#include <stdio.h>

int remove(const char *pathname);
                             Returns: 0 if OK, −1 on error
```

ISO C 指定 `remove` 函数来删除文件。名称从历史上的 UNIX 名称 `unlink` 更改，因为在当时，大多数实现 C 标准的非 UNIX 系统并不支持向文件创建链接的概念。

## 4.16 rename 和 renameat 函数

文件或目录的改名可通过 `rename` 或 `renameat` 函数完成。

```c
#include <stdio.h>

int rename(const char *oldname, const char *newname);

int renameat(int oldfd, const char *oldname, int newfd,
             const char *newname);

                                  Both return: 0 if OK, −1 on error
```

`rename` 函数由 ISO C 为文件定义。 （C 标准不处理目录。）POSIX.1 将定义扩展到包括目录和符号链接。

这些函数的条件有多种，取决于 *oldname* 是否引用文件、目录或符号链接。我们还必须描述如果 *newname* 已存在会发生什么。

- 1. 如果 *oldname* 指定一个不是目录的文件，则我们是在重命名文件或符号链接。在这种情况下，如果 *newname* 存在，它不能引用目录。如果 *newname* 存在且不是目录，则将其删除，并将 *oldname* 重命名为 *newname*。我们必须对包含 *oldname* 的目录和包含 *newname* 的目录具有写权限，因为我们正在更改这两个目录。
- 2. 如果 *oldname* 指定一个目录，则我们是在重命名目录。如果 *newname* 存在，它必须引用一个目录，并且该目录必须为空。 （当我们说一个目录为空时，我们的意思是目录中唯一的条目是点和点点。）如果 *newname* 存在且是一个空目录，则将其删除，并将 *oldname* 重命名为 *newname*。此外，在重命名目录时，*newname* 不能包含命名 *oldname* 的路径前缀。例如，我们不能将 `/usr/foo` 重命名为 `/usr/foo/testdir`，因为旧名称（`/usr/foo`）是新名称的前缀路径，不能被删除。
- 3. 如果 oldname 或 newname 引用符号链接，则处理链接本身，而不是它解析到的文件。
- 4. 我们不能重命名点或点点。更准确地说，点或点点不能作为 oldname 或 newname 的最后一个组件出现。
- 5. 作为特例，如果 oldname 和 newname 引用同一个文件，函数将成功返回而不做任何更改。

如果 newname 已存在，我们需要如同删除它一样的权限。此外，因为我们正在删除 oldname 的目录条目并可能创建 newname 的目录条目，所以我们需要在包含 oldname 的目录和包含 newname 的目录中具有写权限和执行权限。

`renameat` 函数提供的功能与 `rename` 函数相同，只是当 oldname 或 newname 引用相对路径名时除外。如果 oldname 指定相对路径名，则它相对于 oldfd 引用的目录进行求值。类似地，如果 newname 指定相对路径名，则 newname 相对于 newfd 引用的目录进行求值。oldfd 或 newfd 参数（或两者）都可以设置为 AT_FDCWD，以使相应的路径名相对于当前目录进行求值。

## 4.17 符号链接

符号链接是对文件的间接指针，与上一节中描述的硬链接不同，后者直接指向文件的 i-节点。符号链接被引入是为了克服硬链接的限制。

- 硬链接通常要求链接和文件位于同一文件系统。
- 只有超级用户才能创建指向目录的硬链接（当底层文件系统支持时）。

符号链接对其指向的内容没有文件系统限制，任何人都可以创建指向目录的符号链接。符号链接通常用于将文件或整个目录层次结构“移动”到系统上的另一个位置。

在使用按名称引用文件的函数时，我们始终需要知道函数是否会跟随符号链接。如果函数跟随符号链接，则函数中的路径名参数引用符号链接指向的文件。否则，路径名参数引用链接本身，而不是链接指向的文件。图 4.17 总结了本章中描述的函数是否跟随符号链接。函数 mkdir、mkfifo、mknod 和 rmdir 未出现在该图中，因为当路径名为符号链接时它们会返回错误。此外，接受文件描述符参数的函数，如 fstat 和 fchmod，未列出，因为返回文件描述符的函数（通常是 open）处理符号链接。历史上，实现在 chown 是否跟随符号链接方面存在差异。然而，在所有现代系统中，chown 都跟随符号链接。

符号链接随 4.2BSD 引入。最初，chown 不会跟随符号链接，但该行为在 4.4BSD 中发生了变化。System V 在 SVR4 中包含了对符号链接的支持，但偏离了原始的 BSD 行为，通过实现 chown 来跟随符号链接。在旧版本的 Linux（2.1.81 之前的版本）中，chown 不会跟随符号链接。从版本 2.1.81 开始，chown 跟随符号链接。在 FreeBSD 8.0、Mac OS X 10.6.8 和 Solaris 10 中，chown 跟随符号链接。所有这些平台都提供了 lchown 的实现来更改符号链接本身的所有权。

| 函数 | 不跟随符号链接 | 跟随符号链接 |
|---|---|---|
| access |  | • |
| chdir |  | • |
| chmod |  | • |
| chown |  | • |
| creat |  | • |
| exec |  | • |
| lchown | • |  |
| link |  | • |
| lstat | • |  |
| open |  | • |
| opendir |  | • |
| pathconf |  | • |
| readlink | • |  |
| remove | • |  |
| rename | • |  |
| stat |  | • |
| truncate |  | • |
| unlink | • |  |

图 4.17 各函数对符号链接的处理

图 4.17 总结的行为有一个例外，当 open 函数同时设置了 O_CREAT 和 O_EXCL 时。在这种情况下，如果路径名引用符号链接，open 将失败并将 errno 设置为 EEXIST。这种行为旨在关闭一个安全漏洞，以防止特权进程被欺骗写入错误的文件。

### 示例

使用符号链接，可以在文件系统中引入循环。大多数查找路径名的函数在发生这种情况时会返回 ELOOP 的 errno。考虑以下命令：

```
$ mkdir foo                  make a new directory
$ touch foo/a                create a 0-length file
$ ln -s ../foo foo/testdir   create a symbolic link
$ ls -l foo
total 0
-rw-r--r-- 1 sar 0 Jan 22 00:16 a
lrwxrwxrwx 1 sar 6 Jan 22 00:16 testdir -> ../foo
```

这创建了一个目录 foo，其中包含文件 a 和一个指向 foo 的符号链接。我们在图 4.18 中展示了这种安排，将目录画成圆圈，文件画成正方形。

![](img/244bf0c3b6d0288ae397336907e37851_155_0.png)

图 4.18 创建循环的符号链接 testdir

如果我们编写一个简单的程序，使用 Solaris 上的标准函数 ftw(3) 遍历文件层次结构并打印遇到的每个路径名，输出为

```
foo
foo/a
foo/testdir
foo/testdir/a
foo/testdir/testdir
foo/testdir/testdir/a
foo/testdir/testdir/testdir
foo/testdir/testdir/testdir/a
(many more lines until we encounter an ELOOP error)
```

在第 4.22 节中，我们提供了自己的 ftw 函数版本，该版本使用 lstat 而不是 stat，以防止它跟随符号链接。

> 请注意，在 Linux 上，ftw 和 nftw 函数会记录所有看到的目录并避免多次处理同一个目录，因此它们不会显示这种行为。

这种形式的循环很容易删除。我们可以解除链接文件 foo/testdir，因为 unlink 不会跟随符号链接。但如果我们创建形成这种类型循环的硬链接，其删除会困难得多。这就是为什么 link 函数只有在进程具有超级用户权限时才会形成指向目录的硬链接。

> 确实，Rich Stevens 在撰写本节的原始版本时，在自己的系统上进行了这样的实验。文件系统损坏了，正常的 fsck(1) 实用程序无法修复。已弃用的工具 clri(8) 和 decheck(8) 才得以修复文件系统。

对目录的硬链接的需求早已过去。有了符号链接和 mkdir 函数，用户不再需要创建指向目录的硬链接。

当我们打开一个文件时，如果传递给 open 的路径名指定了符号链接，open 会跟随链接到指定的文件。如果符号链接指向的文件不存在，open 会返回错误，说明它无法打开文件。这种响应会让不熟悉符号链接的用户感到困惑。例如，


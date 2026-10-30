

如果我们运行这个程序，可以看到权限位是如何设置的。

```
$ umask
002
$ ./a.out
$ ls -l foo bar
-rw------ 1 sar 0 Dec 7 21:20 bar
-rw-rw-rw- 1 sar 0 Dec 7 21:20 foo
$ umask
002
```

首先打印当前的文件模式创建掩码

查看文件模式创建掩码是否发生了变化

大多数 UNIX 系统的用户从不处理他们的 umask 值。它通常在登录时由 shell 的启动文件设置一次，并且从不更改。尽管如此，当编写创建新文件的程序时，如果我们想确保启用特定的访问权限位，我们必须在进程运行时修改 umask 值。例如，如果我们想确保任何人都可以读取一个文件，我们应该将 umask 设置为 0。否则，在我们的进程运行时生效的 umask 值可能会导致权限位被关闭。

在前面的示例中，我们使用 shell 的 umask 命令在运行程序之前和完成后打印文件模式创建掩码。这向我们展示了更改进程的文件模式创建掩码不会影响其父进程（通常是 shell）的掩码。所有 shell 都有一个内置的 umask 命令，我们可以用它来设置或打印当前的文件模式创建掩码。

用户可以设置 umask 值来控制他们创建的文件的默认权限。该值以八进制表示，一个位代表一个要屏蔽的权限，如图 4.10 所示。可以通过设置相应的位来拒绝权限。一些常见的 umask 值是 002 以防止其他人写入你的文件，022 以防止组成员和其他人写入你的文件，以及 027 以防止组成员写入你的文件并防止其他人读取、写入或执行你的文件。

| Mask bit | Meaning |
|---|---|
| 0400 | user-read |
| 0200 | user-write |
| 0100 | user-execute |
| 0040 | group-read |
| 0020 | group-write |
| 0010 | group-execute |
| 0004 | other-read |
| 0002 | other-write |
| 0001 | other-execute |

图 4.10 umask 文件访问权限位

Single UNIX Specification 要求 umask 命令支持符号模式操作。与八进制格式不同，符号格式指定要允许的权限（即在文件创建掩码中清除），而不是要拒绝的权限（即在文件创建掩码中设置）。比较下面命令的两种形式。

请注意，图 4.11 中的九个条目是图 4.6 中的九个文件访问权限位。我们添加了两个 set-ID 常量（S_ISUID 和 S_ISGID）、保存文本常量（S_ISTVTX）以及三个组合常量（S_IRWXU、S_IRWXG 和 S_IRWXO）。

保存文本位（S_ISTVTX）不是 POSIX.1 的一部分。它在 Single UNIX Specification 中 XSI 选项中定义。我们将在下一节描述其用途。

### Example

回顾我们在图 4.9 中运行程序以演示 umask 函数时文件 foo 和 bar 的最终状态：

```
$ ls -l foo bar
-rw------- 1 sar       0 Dec  7 21:20 bar
-rw-rw-rw- 1 sar       0 Dec  7 21:20 foo
```

图 4.12 所示的程序修改了这两个文件的模式。

```
#include "apue.h"
int
main(void)
{
    struct stat     statbuf;
    /* turn on set-group-ID and turn off group-execute */
    if (stat("foo", &statbuf) < 0)
        err_sys("stat error for foo");
    if (chmod("foo", (statbuf.st_mode & ~S_IXGRP) | S_ISGID) < 0)
        err_sys("chmod error for foo");
    /* set absolute mode to "rw-r--r--" */
    if (chmod("bar", S_IRUSR | S_IWUSR | S_IRGRP | S_IROTH) < 0)
        err_sys("chmod error for bar");
    exit(0);
}
```

图 4.12 chmod 函数示例

运行图 4.12 中的程序后，我们看到两个文件的最终状态为

```
$ ls -l foo bar
-rw-r--r-- 1 sar       0 Dec  7 21:20 bar
-rw-rwSrwx 1 sar       0 Dec  7 21:20 foo
```

在这个示例中，我们将文件 bar 的权限设置为绝对值，而不管当前的权限位。对于文件 foo，我们将其权限相对于当前状态进行设置。为此，我们首先调用 stat 获取当前权限，然后对其进行修改。我们已明确打开 set-group-ID 位并关闭 group-execute 位。请注意，ls 命令将 group-execute 权限列为 S，以表示 set-group-ID 位已设置而 group-execute 位未设置。

在 Solaris 上，ls 命令显示 l 而不是 S 来指示该文件的强制文件和记录锁定已启用。此行为仅适用于常规文件，但我们将在第 14.3 节中更详细地讨论这一点。

最后，请注意，ls 命令列出的时间和日期在我们运行图 4.12 中的程序后没有改变。我们将在第 4.19 节看到 chmod 函数仅更新 i-node 最后更改的时间。默认情况下，ls -l 列出的是文件内容最后修改的时间。

chmod 函数在以下条件下会自动清除两个权限位：

- 在 Solaris 等将粘滞位用于常规文件时赋予其特殊含义的系统上，如果我们尝试在没有超级用户权限的情况下在常规文件上设置粘滞位（S_ISVTX），则模式中的粘滞位会自动关闭。（我们将在下一节描述粘滞位。）为了防止恶意用户设置粘滞位并对系统性能产生不利影响，只有超级用户才能在常规文件上设置粘滞位。

在 FreeBSD 8.0 和 Solaris 10 中，只有超级用户才能在常规文件上设置粘滞位。Linux 3.2.0 和 Mac OS X 10.6.8 对粘滞位的设置没有此类限制，因为在这些系统上应用于常规文件时该位没有意义。虽然该位在应用于 FreeBSD 上的常规文件时也没有意义，但除超级用户外的所有人都被禁止在常规文件上设置它。

- 新创建的文件的组 ID 可能是调用进程不属于的组。回顾第 4.6 节，新文件的组 ID 可能是父目录的组 ID。具体来说，如果新文件的组 ID 不等于进程的有效组 ID 或进程的任何补充组 ID，并且进程没有超级用户权限，则 set-group-ID 位会自动关闭。这可以防止用户创建由用户不属于的组拥有的 set-group-ID 文件。

FreeBSD 8.0 在这种情况下会失败设置 set-group-ID 的尝试。其他系统会静默关闭该位，但不会失败更改文件访问权限的尝试。

FreeBSD 8.0、Linux 3.2.0、Mac OS X 10.6.8 和 Solaris 10 添加了另一项安全功能，以防止滥用某些保护位。如果没有超级用户权限的进程写入文件，则 set-user-ID 和 set-group-ID 位会自动关闭。如果恶意用户找到他们可以写入的 set-group-ID 或 set-user-ID 文件，即使他们可以修改文件，他们也会失去文件的特殊权限。

## 4.10 Sticky Bit

S_ISVTX 位有一个有趣的历史。在早于按需分页的 UNIX 系统版本中，该位被称为粘滞位。如果为可执行程序文件设置，则程序第一次执行时，程序文本的副本会在进程终止时保存在交换区中。（程序的文本部分是机器指令。）程序下次执行时加载到内存的速度会更快，因为交换区被处理为连续的文件，而与正常 UNIX 文件系统中数据块的可能随机位置相比。粘滞位通常为常见的应用程序程序设置，例如文本编辑器和 C 编译器的各个阶段。自然地，在用完交换空间之前，交换区中可以容纳的粘滞文件数量是有限的，但这是一种有用的技术。名称 sticky 的由来是因为文件文本部分在系统重新启动之前一直保留在交换区中。后来版本的 UNIX 系统将其称为保存文本位；因此常量为 S_ISVTX。随着当今大多数具有虚拟内存系统和更快文件系统的较新 UNIX 系统的出现，这种技术的需求已经消失。

在当代系统上，粘滞位的使用已得到扩展。Single UNIX Specification 允许为目录设置粘滞位。如果为目录设置了该位，则目录中的文件只能在用户对目录具有写权限并且满足以下条件之一时被删除或重命名：

- 拥有该文件
- 拥有该目录
- 是超级用户

目录 /tmp 和 /var/tmp 通常是粘滞位的候选目录——它们是任何用户通常可以创建文件的目录。这两个目录的权限通常对每个人（用户、组和其他）都是读、写和执行。但用户不应能够删除或重命名他人拥有的文件。

> 保存文本位不是 POSIX.1 的一部分。它是 Single UNIX Specification 中定义 XSI 选项的一部分，并由 FreeBSD 8.0、Linux 3.2.0、Mac OS X 10.6.8 和 Solaris 10 支持。
> 
> Solaris 10 如果在常规文件上设置了粘滞位，则会赋予其特殊含义。在这种情况下，如果未设置任何执行位，操作系统将不会缓存文件的内容。

## 4.11 chown, fchown, fchownat, and lchown Functions

chown 函数允许我们更改文件的用户 ID 和组 ID，但如果 owner 或 group 两个参数中的任一个为 -1，则对应的 ID 保持不变。

```
#include <unistd.h>

int chown(const char *pathname, uid_t owner, gid_t group);
int fchown(int fd, uid_t owner, gid_t group);
int fchownat(int fd, const char *pathname, uid_t owner, gid_t group, int flag);
int lchown(const char *pathname, uid_t owner, gid_t group);

All four return: 0 if OK, -1 on error
```


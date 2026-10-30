

## Example

要了解保存的 set-user-ID 功能的用途，让我们检查使用它的程序的运行情况。我们来看 at(1) 程序，我们可以用它来安排在未来某个时间运行的命令。

在 Linux 3.2.0 上，at 程序被安装为 set-user-ID 到用户 daemon。在 FreeBSD 8.0、Mac OS X 10.6.8 和 Solaris 10 上，at 程序被安装为 set-user-ID 到用户 root。这允许 at 命令写入由 daemon 拥有的特权文件，该 daemon 将代表运行 at 命令的用户运行命令。在 Linux 3.2.0 上，程序由 atd(8) daemon 运行。在 FreeBSD 8.0 和 Solaris 10 上，程序由 cron(1M) daemon 运行。在 Mac OS X 10.6.8 上，程序由 launchd(8) daemon 运行。

为了防止被 trick 去运行我们无权运行的命令，或读取/写入我们无权访问的文件，at 命令和最终代表我们运行命令的 daemon 必须在权限集之间切换：我们的权限和 daemon 的权限。以下步骤会发生。

- 1. 假设 at 程序文件由 root 拥有并且设置了 set-user-ID 位，当我们运行它时，我们有
  real user ID = 我们的用户 ID（未改变）
  effective user ID = root
  saved set-user-ID = root

- 2. at 命令做的第一件事是降低其权限，使其以我们的权限运行。它调用 seteuid 函数将 effective user ID 设置为我们的 real user ID。之后，我们有
  real user ID = 我们的用户 ID（未改变）
  effective user ID = 我们的用户 ID
  saved set-user-ID = root（未改变）

- 3. at 程序以我们的权限运行，直到它需要访问控制要运行哪些命令以及何时运行的配置文件。这些文件由将为我们运行命令的 daemon 拥有。at 命令调用 seteuid 将 effective user ID 设置为 root。此调用是允许的，因为 seteuid 的参数等于 saved set-user-ID。（这就是我们需要 saved set-user-ID 的原因。）之后，我们有
  real user ID = 我们的用户 ID（未改变）
  effective user ID = root
  saved set-user-ID = root（未改变）
  
  因为 effective user ID 是 root，文件访问是允许的。

- 4. 在修改文件以记录要运行的命令和运行时间后，at 命令通过调用

## Example

让我们看一个例子，看看内核如何处理 exec 函数的参数，当被执行的文件是解释器文件并且解释器文件的第一行上有可选参数时。图 8.20 中的程序 exec 一个解释器文件。

```
#include "apue.h"
#include <sys/wait.h>

int
main(void)
{
    pid_t pid;

    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) {       /* child */
        if (execl("/home/sar/bin/testinterp",
                  "testinterp", "myarg1", "MY ARG2", (char *)0) < 0)
            err_sys("execl error");
    }
    if (waitpid(pid, NULL, 0) < 0)   /* parent */
        err_sys("waitpid error");
    exit(0);
}
```

图 8.20  一个 exec 解释器文件的程序

下面显示了被执行的一行解释器文件的内容以及运行图 8.20 中程序的结果：

```
$ cat /home/sar/bin/testinterp
#!/home/sar/bin/echoarg foo
$ ./a.out
argv[0]: /home/sar/bin/echoarg
argv[1]: foo
argv[2]: /home/sar/bin/testinterp
argv[3]: myarg1
argv[4]: MY ARG2
```

程序 echoarg（解释器）只是回显其命令行参数。（这是图 7.4 中的程序。）注意，当内核 exec 解释器（/home/sar/bin/echoarg）时，argv[0] 是解释器的路径名，argv[1] 是来自解释器文件的可选参数，其余参数是路径名（/home/sar/bin/testinterp）和来自图 8.20 中程序对 execl 的调用的第二个和第三个参数（myarg1 和 MY ARG2）。来自 execl 调用的 argv[1] 和 argv[2] 都向右移动了两个位置。注意内核采用来自 execl 调用的路径名而不是第一个参数（testinterp），假设路径名可能包含比第一个参数更多的信息。

## Example

在解释器路径名之后使用可选参数的一个常见用途是为支持此选项的程序指定 -f 选项。例如，awk(1) 程序可以作为

```
awk -f myfile
```

执行，这告诉 awk 从文件 myfile 读取 awk 程序。

源自 UNIX System V 的系统通常包含两种版本的 awk 语言。在这些系统上，awk 通常被称为“旧 awk”，对应于随 V7 分发的原始版本。相比之下，nawk（新 awk）包含许多增强功能，对应于 Aho、Kernighan 和 Weinberger [1988] 中描述的语言。此更新版本提供了访问命令行参数的功能，我们在下面的示例中需要它。Solaris 10 提供了两个版本。

awk 程序是 POSIX 在其 1003.2 标准中包含的实用程序之一，该标准现在是 Single UNIX Specification 中基础 POSIX.1 规范的一部分。此实用程序还基于 Aho、Kernighan 和 Weinberger [1988] 中描述的语言。

Mac OS X 10.6.8 中的 awk 版本基于 Bell Laboratories 版本，该版本已置于公共领域。FreeBSD 8.0 和一些 Linux 发行版随附 GNU awk，称为 gawk，链接到名称 awk。gawk 符合 POSIX 标准，但还包括其他扩展。由于 gawk 和来自 Bell Laboratories 的 awk 版本更 up-to-date，它们优于 nawk 或旧 awk。（Bell Labs 版本的 awk 可在 ../../../../cm.bell-labs.com/cm/cs/awkbook/index.html 获得。）

使用解释器文件中的 -f 选项让我们可以编写

```
#!/bin/awk -f
(awk 程序随后在解释器文件中)
```

例如，图 8.21 显示了 /usr/local/bin/awkexample（一个解释器文件）。

```
#!/usr/bin/awk -f
# Note: on Solaris, use nawk instead
BEGIN {
    for (i = 0; i < ARGC; i++)
        printf "ARGV[%d] = %s\n", i, ARGV[i]
    exit
}
```

# 图 8.21 一个作为解释器文件的 awk 程序

如果其中一个路径前缀是 /usr/local/bin，我们可以执行图 8.21 中的程序（假设我们已为文件打开了执行位）作为

```
$ awkexample file1 FILENAME2 f3
ARGV[0] = awk
ARGV[1] = file1
ARGV[2] = FILENAME2
ARGV[3] = f3
```

而不是需要知道该程序实际上是一个 awk 脚本，我们否则必须作为

```
awk -f awkexample optional-arguments
```

执行。

- 2. 解释器脚本提供了效率提升。再次考虑之前的示例。我们仍然可以通过将其包装在 shell 脚本中来隐藏该程序是 awk 脚本：

```
awk 'BEGIN {
    for (i = 0; i < ARGC; i++)
        printf "ARGV[$i] = %s\n", i, ARGV[i]
    exit
}' $*
```

这个解决方案的问题是需要更多的工作。首先，shell 读取命令并尝试 execvp 文件名。因为 shell 脚本是可执行文件但不是机器可执行文件，返回错误并且 execvp 假设文件是 shell 脚本（确实是）。然后使用 shell 脚本的路径名作为其参数执行 /bin/sh。shell 正确运行我们的脚本，但要运行 awk 程序，shell 会进行 fork、exec 和 wait。因此，用 shell 脚本替换解释器脚本涉及更多开销。

- 3. 解释器脚本让我们可以使用 /bin/sh 以外的 shell 编写 shell 脚本。当它找到一个不是机器可执行的可执行文件时，execvp 必须选择要调用的 shell，并且它总是使用 /bin/sh。然而，使用解释器脚本，我们可以简单地编写

```
#!/bin/csh
(C shell 脚本随后在解释器文件中)
```

同样，我们可以将其包装在调用 C shell 的 /bin/sh 脚本中，如我们之前所述，但需要更多开销。

如果这三个 shell 和 awk 不使用井号作为注释字符，以上所有内容都不会按我们所示的方式工作。

## 8.13 system Function

从程序内部执行命令字符串很方便。例如，假设我们想把时间-日期戳放入某个文件中。我们可以使用第 6.10 节中描述的函数来做到这一点：调用 time 获取当前日历时间，然后调用 localtime 将其转换为分解时间，然后调用 strftime 格式化结果，最后将结果写入文件。然而，更容易说

```
system("date > file");
```

ISO C 定义了 system 函数，但其操作强烈依赖于系统。POSIX.1 包含 system 接口，在 ISO C 定义的基础上扩展了其在 POSIX 环境中的行为描述。


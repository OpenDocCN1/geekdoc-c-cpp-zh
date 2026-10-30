

这些最小值不会因系统而异。它们指定了这些特性的最严格值。符合 POSIX.1 的实现必须提供至少这么大的值。这就是为什么它们被称为最小值，尽管它们的名称都包含 MAX。此外，为了确保可移植性，严格符合规范的应用程序不得要求更大的值。我们在文中逐步介绍时会说明这些常量各自的含义。

> 严格符合 POSIX 的应用程序与仅仅符合 POSIX 的应用程序不同。符合 POSIX 的应用程序仅使用 IEEE 标准 1003.1-2008 中定义的接口。严格符合 POSIX 的应用程序必须满足进一步的限制，例如不依赖任何未定义行为、不使用任何已废弃的接口，并且不得要求常量的值大于图 2.8 中所示的最小值。

| Name | Description | Minimum acceptable value |
|---|---|---|
| `ARG_MAX` | maximum length of arguments to exec functions | `POSIX_ARG_MAX` |
| `ATEXIT_MAX` | maximum number of functions that can be registered with the atexit function | 32 |
| `CHILD_MAX` | maximum number of child processes per real user ID | `_POSIX_CHILD_MAX` |
| `DELAYTIMER_MAX` | maximum number of timer expiration overruns | `_POSIX_DELAYTIMER_MAX` |
| `HOST_NAME_MAX` | maximum length of a host name as returned by gethostname | `_POSIX_HOST_NAME_MAX` |
| `LOGIN_NAME_MAX` | maximum length of a login name | `_POSIX_LOGIN_NAME_MAX` |
| `OPEN_MAX` | one more than the maximum value assigned to a newly created file descriptor | `_POSIX_OPEN_MAX` |
| `PAGESIZE` | system memory page size, in bytes | 1 |
| `RTSIG_MAX` | maximum number of real-time signal queues reserved for application use | `_POSIX_RTSIG_MAX` |
| `SEM_NSEMS_MAX` | maximum number of semaphores a process can use | `_POSIX_SEM_NSEMS_MAX` |
| `SEM_VALUE_MAX` | maximum value of a semaphore | `_POSIX_SEM_VALUE_MAX` |
| `SIGQUEUE_MAX` | maximum number of signals that can be queued for a process | `_POSIX_SIGQUEUE_MAX` |
| `STREAM_MAX` | maximum number of standard I/O streams a process can have open at once | `_POSIX_STREAM_MAX` |
| `SYMLOOP_MAX` | number of symbolic links that can be traversed during pathname resolution | `_POSIX_SYMLOOP_MAX` |
| `TIMER_MAX` | maximum number of timers per process | `_POSIX_TIMER_MAX` |
| `TTY_NAME_MAX` | length of a terminal device name, including the terminating null | `_POSIX_TTY_NAME_MAX` |
| `TZNAME_MAX` | number of bytes for the name of a time zone | `_POSIX_TZNAME_MAX` |

*Figure 2.9* POSIX.1 runtime invariant values from `<limits.h>`

不幸的是，其中一些不变的最小值太小而无法实际使用。例如，今天大多数 UNIX 系统为每个进程提供的打开文件数远不止 20 个。此外，`_POSIX_PATH_MAX` 的最小限制 256 也太小。路径名可能超过此限制。这意味着我们不能在编译时将两个常量 `_POSIX_OPEN_MAX` 和 `_POSIX_PATH_MAX` 用作数组大小。

图 2.8 中的每个 25 个不变最小值都有一个关联的实现值，其名称是通过从图 2.8 中的名称中去掉 _POSIX_ 前缀形成的。去掉前导 _POSIX_ 的名称本意是给定实现所支持的实际值。 （这 25 个实现值来自我们本节前面列出的项目 1、4、5 和 7 中的：2 个运行时可增加值、15 个运行时不变值和 7 个路径名可变值，以及来自数值值的 SSIZE_MAX。）问题是，并非所有 25 个实现值都保证在 `<limits.h>` 头文件中定义。

例如，如果给定进程的实际值取决于系统上的内存量，则该特定值可能不会包含在头文件中。如果值未在头文件中定义，我们就不能在编译时将它们用作数组边界。为了在运行时确定实际的实现值，POSIX.1 决定为我们提供三个可调用的函数——sysconf、pathconf 和 fpathconf。然而仍然存在一个问题，因为 POSIX.1 将其中的一些值定义为可能“不确定” （逻辑上无限）。这意味着该值没有实际的上限。例如，在 Solaris 上，您可以用 atexit 注册以便在进程结束时运行的函数数量仅受系统内存量的限制。因此在 Solaris 上 ATEXIT_MAX 被认为是未确定的。我们将在第 2.5.5 节中回到这个不确定运行时限制的问题。

## 2.5.3 XSI Limits

XSI 选项还定义了表示实现限制的常量。它们包括：

- 1. 最小值：图 2.10 中的五个常量
- 2. 运行时不变值，可能不确定：IOV_MAX 和 PAGE_SIZE

最小值列在图 2.10 中。后两个说明了 POSIX.1 最小值太小的情况—— presumably 为了允许嵌入式 POSIX.1 实现，因此为 XSI 符合系统添加了具有更大最小值的符号。

| Name | Description | Minimum acceptable value | Typical value |
|---|---|---|---|
| NL_LANGMAX | maximum number of bytes in LANG environment variable | 14 | 14 |
| NZERO | default process priority | 20 | 20 |
| _XOPEN_IOV_MAX | maximum number of iovec structures that can be used with readv or writev | 16 | 16 |
| _XOPEN_NAME_MAX | number of bytes in a filename | 255 | 255 |
| _XOPEN_PATH_MAX | number of bytes in a pathname | 1,024 | 1,024 |

Figure 2.10 XSI minimum values from <limits.h>

```
printf("\n")
printf("\tif (argc != 2)\n")
printf("\t\t_err_quit(\"usage: a.out <dirname>\");\n\n")
FS="+t"
while (getline <"sysconf.sym" > 0) {
    printf("#ifdef %s\n", $1)
    printf("\tprintf(\"%s defined to be %%ld\\n\", (long)%s+0);\n",
           $1, $1)
    printf("#else\n")
    printf("\tprintf(\"no symbol for %s\\n\");\n", $1)
    printf("#endif\n")
    printf("#ifdef %s\n", $2)
    printf("\tpr_sysconf(\"%s =\", %s);\n", $1, $2)
    printf("#else\n")
    printf("\tprintf(\"no symbol for %s\\n\");\n", $2)
    printf("#endif\n")
}
close("sysconf.sym")
while (getline <"pathconf.sym" > 0) {
    printf("#ifdef %s\n", $1)
    printf("\tprintf(\"%s defined to be %%ld\\n\", (long)%s+0);\n",
           $1, $1)
    printf("#else\n")
    printf("\tprintf(\"no symbol for %s\\n\");\n", $1)
    printf("#endif\n")
    printf("#ifdef %s\n", $2)
    printf("\tpr_pathconf(\"%s =\", argv[1], %s);\n", $1, $2)
    printf("#else\n")
    printf("\tprintf(\"no symbol for %s\\n\");\n", $2)
    printf("#endif\n")
}
close("pathconf.sym")
exit
}
END {
printf("\texit(0);\n")
printf("\n\n")
printf("static void\n")
printf("pr_sysconf(char *mesg, int name)\n")
printf("{\n")
printf("\tlong val;\n\n")
printf("\tfputs(mesg, stdout);\n")
printf("\terrno = 0;\n")
printf("\tif (val = sysconf(name)) < 0) {\n")
printf("\t\tif (errno != 0) {\n")
printf("\t\t\tif (errno == EINVAL)\n")
printf("\t\t\t\tfputs(\" (not supported)\\n\", stdout);\n")
printf("\t\t\telse\n")
printf("\t\t\t\t_err_sys(\"sysconf error\");\n")
printf("\t\t} else {\n")
printf("\t\t\tfputs(\" (no limit)\\n\", stdout);\n")
```

```
printf("\t\t}\\n")
printf("\t) else {\\n")
printf("\t\tprintf(\" %%ld\\n\\", val);\\n")
printf("\t}\\n")
printf("}\\n")
printf("static void\\n")
printf("pr_pathconf(char *mesg, char *path, int name)\\n")
printf("{\\n")
printf("\tlong val;\\n")
printf("\\n")
printf("\ttfputs(mesg, stdout);\\n")
printf("\terrno = 0;\\n")
printf("\tif (val = pathconf(path, name)) < 0) {\\n")
printf("\t\tif (errno != 0) {\\n")
printf("\t\t\tif (errno == EINVAL)\\n")
printf("\t\t\t\ttfputs(\" (not supported)\\n\\", stdout);\\n")
printf("\t\t} else\\n")
printf("\t\t\tterr_sys(\"pathconf error, path = %%s\\", path);\\n")
printf("\t} else\\n")
printf("\t\ttfputs(\" (no limit)\\n\\", stdout);\\n")
printf("\t} else {\\n")
printf("\t\tprintf(\" %%ld\\n\\", val);\\n")
printf("\t}\\n")
printf("}\\n")
```

# Figure 2.13 Build C program to print all supported configuration limits

awk 程序读取两个输入文件——pathconf.sym 和 sysconf.sym——其中包含由制表符分隔的限制名称和符号。并非所有符号都在每个平台上定义，因此 awk 程序用必要的 #ifdef 语句将每次对 pathconf 和 sysconf 的调用包围起来。

例如，awk 程序将输入文件中的一行

```
NAME_MAX          _PC_NAME_MAX
```

转换为以下 C 代码：

```
#ifdef NAME_MAX
printf("NAME_MAX is defined to be %d\n", NAME_MAX+0);
#else
printf("no symbol for NAME_MAX\n");
#endif
#ifdef _PC_NAME_MAX
pr_pathconf("NAME_MAX =", argv[1], _PC_NAME_MAX);
#else
printf("no symbol for _PC_NAME_MAX\n");
#endif
```

图 2.14 中由 awk 程序生成的程序打印所有这些限制，并处理限制未定义的情况。



第 7.8 节)。与 sfio 包一样，ASI 试图通过使用指针来最大限度地减少数据复制量。

在为内存占用小的系统设计的 C 库中，有几种标准 I/O 库的实现，例如嵌入式系统。这些实现强调适中的内存需求，而非可移植性、速度或功能。其中两个实现是 uClibc C 库（参见 ../.../../.../www.uclibc.org/...）和 Newlib C 库（../.../../.../sources.redhat.com/newlib）。

## 5.16 总结

标准 I/O 库被大多数 UNIX 应用程序使用。在本章中，我们查看了该库提供的许多函数，以及一些实现细节和效率考虑。要意识到该库中发生的缓冲，因为这是产生最多问题和困惑的区域。

## 练习

- 5.1 使用 setvbuf 实现 setbuf。
- 5.2 输入使用逐行 I/O（fgets 和 fputs）复制文件的程序，如图 5.5 所示，但使用 4 的 MAXLINE。复制超过此长度的行时会发生什么？解释发生了什么。
- 5.3 printf 返回值为 0 表示什么？
- 5.4 以下代码在某些机器上工作正常，但在其他机器上不工作。可能是什么问题？

```
#include <stdio.h>
int
main(void)
{
    char c;
    while ((c = getchar()) != EOF)
        putchar(c);
}
```

- 5.5 你将如何使用 fsync 函数（第 3.13 节）与标准 I/O 流一起使用？
- 5.6 在图 1.7 和 1.10 中的程序中，打印的提示符不包含换行符，我们也没有调用 fflush。是什么导致提示符被输出？
- 5.7 基于 BSD 的系统提供了一个名为 funopen 的函数，允许我们在流上拦截 read、write、seek 和 close 调用。使用此函数为 FreeBSD 和 Mac OS X 实现 fmemopen。

本页特意留空

## 系统数据文件和信息

### 6.1 引言

UNIX 系统需要大量数据文件来正常运行：密码文件 /etc/passwd 和组文件 /etc/group 就是各种程序经常使用的两个文件。例如，每当用户登录到 UNIX 系统以及每当有人执行 ls -l 命令时，都会使用密码文件。

历史上，这些数据文件一直是 ASCII 文本文件，并使用标准 I/O 库读取。但对于较大的系统，顺序扫描密码文件会变得耗时。我们希望能够以 ASCII 文本以外的格式存储这些数据文件，但仍然为应用程序提供一个与任何文件格式都兼容的接口。这些数据文件的可移植接口是本章的主题。我们还涵盖系统识别函数以及时间和日期函数。

### 6.2 密码文件

UNIX 系统的密码文件，由 POSIX.1 称为用户数据库，包含图 6.1 所示的字段。这些字段包含在 <pwd.h> 中定义的 passwd 结构中。

请注意，POSIX.1 仅指定了 passwd 结构中 10 个字段中的 5 个。大多数平台至少支持 7 个字段。派生自 BSD 的平台支持全部 10 个。

| 描述 | struct passwd 成员 | POSIX.1 | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|---|---|
| 用户名 | char *pw_name | • | • | • | • | • |
| 加密密码 | char *pw_passwd |  | • | • | • | • |
| 数值用户 ID | uid_t pw_uid | • | • | • | • | • |
| 数值组 ID | gid_t pw_gid | • | • | • | • | • |
| 注释字段 | char *pw_gecos |  | • | • | • | • |
| 初始工作目录 | char *pw_dir | • | • | • | • | • |
| 初始 shell（用户程序） | char *pw_shell | • | • | • | • | • |
| 用户访问类 | char *pw_class |  | • |  | • |  |
| 下次更改密码时间 | time_t pw_change |  | • |  | • |  |
| 账户过期时间 | time_t pw_expire |  | • |  | • |  |

# 图 6.1 /etc/passwd 文件中的字段

历史上，密码文件存储在 /etc/passwd 中，并且是一个 ASCII 文件。每行包含图 6.1 中描述的字段，以冒号分隔。例如，Linux 上 /etc/passwd 文件中的四行可能是

```
root:x:0:0:root:/root:/bin/bash
squid:x:23:23::/var/spool/squid:/dev/null
nobody:x:65534:65534:Nobody:/home:/bin/sh
sar:x:205:105:Stephen Rago:/home/sar:/bin/bash
```

注意这些条目的以下几点。

- 通常有一个用户名为 root 的条目。该条目的用户 ID 为 0（超级用户）。
- 加密密码字段包含一个字符作为占位符，旧版本的 UNIX 系统曾在此存储加密密码。由于将加密密码存储在人人可读的文件中是一个安全漏洞，因此加密密码现在保存在其他地方。我们将在下一节讨论密码时更详细地介绍这个问题。
- 密码文件条目中的某些字段可以为空。如果加密密码字段为空，通常意味着用户没有密码。（不推荐这样做。）squid 条目有一个空白字段：注释字段。空注释字段没有影响。
- shell 字段包含用作用户登录 shell 的可执行程序的名称。空 shell 字段的默认值通常为 /bin/sh。注意，squid 条目的登录 shell 为 /dev/null。显然，这是一个设备，不能执行，因此在此处使用是为了防止任何人以用户 squid 登录到我们的系统。

许多服务为帮助实现该服务的守护进程（第 13 章）提供了单独的用户 ID。squid 条目用于实现 squid 代理缓存服务的进程。

- 有几种替代使用 /dev/null 来防止特定用户登录到系统的方法。例如，/bin/false 通常用作登录 shell。它仅以不成功（非零）状态退出；shell 将退出状态评估为 false。/bin/true 用于禁用账户也很常见；它仅以成功（零）状态退出。一些系统提供 nologin 命令，它打印可定制的错误消息并以非零退出状态退出。
- nobody 用户名可用于允许人们登录到系统，但使用用户 ID（65534）和组 ID（65534）提供无特权。唯一可以访问的文件是那些可被世界读取或写入的文件。（这种方法假设没有文件专门属于用户 ID 65534 或组 ID 65534，这应该是正确的。）
- 一些提供 finger(1) 命令的系统在注释字段中支持额外信息。这些字段中的每一个都以逗号分隔：用户的姓名、办公室位置、办公室电话号码和家庭电话号码。此外，一些实用程序会将注释字段中的与号替换为登录名（大写）。例如，我们可以有 sar:xi205:105:Steve Rago, SF 5-121, 555-1111, 555-2222:/home/sar:/bin/sh 然后我们可以使用 finger 打印有关 Steve Rago 的信息。$ finger -p sar Login: sar Name: Steve Rago Directory: /home/sar Shell: /bin/sh Office: SF 5-121, 555-1111 Home Phone: 555-2222 On since Mon Jan 19 03:57 (EST) on ttyv0 (messages off) No Mail. 即使你的系统不支持 finger 命令，这些字段仍可放入注释字段中，因为该字段只是一个注释，不会被系统实用程序解释。

一些系统提供 vipw 命令以允许管理员编辑密码文件。vipw 命令序列化对密码文件的更改，并确保任何附加文件与所做的更改一致。系统通常还通过图形用户界面提供类似的功能。

POSIX.1 定义了两个用于从密码文件获取条目的函数。这些函数允许我们根据用户的登录名或数值用户 ID 查找条目。

```
#include <pwd.h>

struct passwd *getpwuid(uid_t uid);
struct passwd *getpwnam(const char *name);

Both return: pointer if OK, NULL on error
```

getpwuid 函数由 ls(1) 程序使用，将 i-node 中包含的数值用户 ID 映射为用户的登录名。getpwnam 函数由 login(1) 程序在我们输入登录名时使用。


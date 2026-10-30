
这两个函数都返回一个指向passwd结构的指针，该结构由函数填充。这个结构通常是函数内的一个静态变量，因此每次调用这两个函数中的任何一个时，其内容都会被覆盖。

如果我们只想查找登录名或用户ID，这两个POSIX.1函数就足够了，但有些程序需要遍历整个口令文件。为此可以使用三个函数：getpwent、setpwent和endpwent。

```
#include <pwd.h>

struct passwd *getpwent(void);

Returns: pointer if OK, NULL on error or end of file

void setpwent(void);
void endpwent(void);
```

这三个函数不属于基础POSIX.1标准的一部分。它们在Single UNIX Specification中被定义为XSI选项的一部分。因此，所有UNIX系统都应提供它们。

我们调用getpwent返回口令文件中的下一个条目。与那两个POSIX.1函数一样，getpwent返回一个指向它已填充的结构的指针。每次调用此函数时，该结构通常都会被覆盖。如果这是对该函数的第一次调用，它会打开其使用的任何文件。使用此函数时不保证任何顺序；条目可以按任意顺序排列，因为某些系统使用文件/etc/passwd的散列版本。

函数setpwent会回绕它使用的任何文件，而endpwent则关闭这些文件。使用getpwent时，我们必须始终确保在结束后调用endpwent来关闭这些文件。尽管getpwent足够聪明，知道何时需要打开其文件（即我们第一次调用它时），但它永远不知道我们何时结束。

### 示例

图6.2展示了函数getpwnam的一个实现。

```
#include <pwd.h>
#include <stddef.h>
#include <string.h>

struct passwd *
getpwnam(const char *name)
{
    struct passwd *ptr;
    setpwent();
    while (((ptr = getpwent()) != NULL))
        if (strcmp(name, ptr->pw_name) == 0)
            break;      /* found a match */
    endpwent();
    return(ptr);    /* ptr is NULL if no match found */
}
```

图6.2 getpwnam函数

此函数开头调用setpwent是一种自我保护：我们确保文件被回绕，以防调用者已经通过调用getpwent打开了它们。我们在完成后调用endpwent，因为getpwnam和getpwuid都不应让任何文件保持打开状态。

## 6.3 阴影口令

加密口令是用户口令经过单向加密算法处理后的副本。由于该算法是单向的，我们无法从加密版本中猜出原始口令。

历史上，所使用的算法总是从64个字符的字符集[a-zA-Z0-9./]生成13个可打印字符（参见Morris和Thompson [1979]）。一些较新的系统使用其他算法，如MD5或SHA-1，来生成更长的加密口令字符串。（用于存储加密口令的字符越多，组合就越多，通过尝试所有可能的变体来猜测口令就越困难。）当我们在加密口令字段中放置单个字符时，我们确保加密口令永远不会匹配此值。

给定一个加密口令，我们无法应用一种算法将其反转并返回明文口令。（明文口令就是我们在Password:提示符下输入的内容。）但是我们可以猜测一个口令，通过单向算法运行它，并将结果与加密口令进行比较。如果用户口令是随机选择的，这种暴力破解方法就不会太成功。然而，用户倾向于选择非随机口令，例如配偶的名字、街道名或宠物名。常见的实验是有人获取口令文件的副本并尝试猜测口令。（Garfinkel等人[2003]的第4章包含有关口令以及UNIX系统上使用的口令加密方案的更多细节和历史。）

为了增加获取原始材料（加密口令）的难度，系统现在将加密口令存储在另一个文件中，通常称为阴影口令文件。该文件至少必须包含用户名和加密口令。与口令相关的其他信息也存储在此处（图6.3）。

| 描述 | struct spwd成员 |
|---|---|
| 用户登录名 | char *sp_namp |
| 加密口令 | char *sp_pwdp |
| 自上次修改口令以来经过的Epoch天数 | int sp_lstchg |
| 允许更改前的天数 | int sp_min |
| 必须更改前的天数 | int sp_max |
| 到期前警告的天数 | int sp_warn |
| 账户不活跃前的天数 | int sp_inact |
| 账户到期时自Epoch以来的天数 | int sp_expire |
| 保留 | unsigned int sp_flag |

图6.3 /etc/shadow文件中的字段

仅有的两个必填字段是用户登录名和加密口令。其他字段控制口令更改的频率（称为“口令老化”）以及账户允许保持活跃的时间。

阴影口令文件不应让所有用户可读。只有少数程序需要访问加密口令——例如login(1)和passwd(1)——这些程序通常设置为set-user-ID root。使用阴影口令后，普通口令文件/etc/passwd可以保持对所有用户可读。

在Linux 3.2.0和Solaris 10上，有一套单独的函数可用于访问阴影口令文件，类似于用于访问口令文件的函数集。

```
#include <shadow.h>
struct spwd *getspnam(const char *name);
struct spwd *getspent(void);

Both return: pointer if OK, NULL on error

void setspent(void);
void endspent(void);
```

在FreeBSD 8.0和Mac OS X 10.6.8上，没有阴影口令结构。额外的账户信息存储在口令文件中（参见图6.1）。

## 6.4 组文件

UNIX系统的组文件（POSIX.1称之为组数据库）包含图6.4所示的字段。这些字段包含在定义于<grp.h>中的group结构中。

| 描述 | struct group成员 | POSIX.1 | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|---|---|
| 组名 | char *gr_name | • | • | • | • | • |
| 加密口令 | char *gr_passwd |  | • | • | • | • |
| 数字组ID | int gr_gid | • | • | • | • | • |
| 指向各个用户名的指针数组 | char **gr_mem | • | • | • | • | • |

图6.4 /etc/group文件中的字段

字段gr_mem是指向属于此组的用户名的指针数组。该数组以空指针结尾。

我们可以使用以下两个函数来查找组名或数字组ID，这两个函数由POSIX.1定义。

```
#include <grp.h>
struct group *getgrgid(gid_t gid);
struct group *getgrnam(const char *name);

Both return: pointer if OK, NULL on error
```

与口令文件函数一样，这两个函数通常返回指向静态变量的指针，该变量在每次调用时被覆盖。

如果要搜索整个组文件，我们需要一些额外的函数。以下三个函数类似于口令文件对应的函数。

```
#include <grp.h>

struct group *getgrent(void);

Returns: pointer if OK, NULL on error or end of file

void setgrent(void);

void endgrent(void);
```

这三个函数不属于基础POSIX.1标准的一部分。它们在单一UNIX规范中被定义为XSI选项的一部分。所有UNIX系统都提供它们。

setgrent函数打开组文件（如果它尚未打开）并回绕它。getgrent函数从组文件读取下一个条目，如果文件尚未打开，则先打开它。endgrent函数关闭组文件。

## 6.5 辅助组ID

UNIX系统中组的使用随着时间的推移发生了变化。在Version 7中，每个用户在任一时刻只属于一个组。当我们登录时，会被分配一个真实组ID，该ID对应于口令文件条目中的数字组ID。我们可以随时通过执行newgrp(1)来更改这一点。如果newgrp命令成功（有关权限规则请参考手册页），我们的真实组ID将更改为新组的ID，并且此值将用于所有后续的文件访问权限检查。我们可以随时通过不带任何参数执行newgrp来回到原来的组。

这种组成员身份形式一直持续到4.2BSD（约1983年）才发生变化。4.2BSD引入了辅助组ID的概念。我们不仅属于口令文件条目中组ID对应的组，还可以属于多达16个附加组。文件访问权限检查被修改，除了将文件的组ID与进程的有效组ID进行比较外，还要与所有辅助组ID进行比较。

> 辅助组ID是POSIX.1的必需特性。（在较早版本的POSIX.1中，它们是可选的。）常量NGROUPS_MAX（图2.11）指定辅助组ID的数量。常见的值是16（图2.15）。

使用辅助组ID的好处是我们不再需要显式地更改组。同时属于多个组（即参与多个项目）并不罕见。

提供了三个函数来获取和设置辅助组ID中的数字组ID。

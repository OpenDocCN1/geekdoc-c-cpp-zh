
SELinux 带有并将 `Targeted` 策略设置为默认。因此，默认情况下，SELinux 仅针对少数守护进程。

## MLS (多级安全) 策略

`MLS` 策略的主要目的是强制 Bell-LaPadula 模型。它根据角色的安全密级和对象的分类级别授予对其他主体和对象的访问权限。

在 `MLS` 策略中，安全上下文的 `MLS` 属性至关重要。否则，策略规则将不知道如何执行访问限制。

## Minimum 策略

这种策略正如其名——最小的。它最初是为低内存机器或设备（如智能手机）设计的。

`Minimum` 策略本质与 `Targeted` 策略相同，但只使用基础策略规则包。这种“空壳”策略可以用于测试 SELinux 对单个指定守护进程的影响。对于低内存设备，`Minimum` 策略允许 SELinux 在不消耗大量资源的情况下运行。

## 理解 SELinux 策略规则包

策略规则也称为允许规则（`allow rules`），是 SELinux 用于确定主体是否有权访问某个对象的规则。策略规则随 SELinux 安装并分组成包，也称为模块（`modules`）。每个特定的策略文件都以 `.pp` 结尾。

`/etc/selinux/policy_type/modules/active/modules` 目录包含许多策略包 (`*.pp`) 文件。接下来的示例显示了实现 `Targeted` 策略的 Linux 策略规则包：

```bash
# ls /etc/selinux/targeted/modules/active/*.pp
/etc/selinux/targeted/modules/active/abrt.pp
/etc/selinux/targeted/modules/active/accountsd.pp
/etc/selinux/targeted/modules/active/acct.pp
/etc/selinux/targeted/modules/active/ada.pp
/etc/selinux/targeted/modules/active/afs.pp
/etc/selinux/targeted/modules/active/server.pp
/etc/selinux/targeted/modules/active/system.pp
/etc/selinux/targeted/modules/active/targeted.pp
/etc/selinux/targeted/modules/active/var.pp
/etc/selinux/targeted/modules/active/variant.pp
/etc/selinux/targeted/modules/active/zebra.pp
```

你的发行版中提供的策略类型可能与此处列出的不匹配。例如，在旧的 Linux 发行版中，`strict` 策略可用。在较新的发行版中，`strict` 策略已合并到 `targeted` 策略中，并默认使用 `targeted`。

`/etc/selinux/policy_type/modules/active/modules` 目录包含许多策略包 (`*.pp`) 文件。接下来的示例显示了实现 `Targeted` 策略的 Linux 系统策略规则包（注意：此处的 OCR 文本列表已根据标准路径重构）。

这些安全上下文可以更改以管理你组织的安全上下文需求。然而，在学习如何更改这些安全上下文的设置之前，你需要了解 SELinux 拼图的另一部分：SELinux 策略类型。

理解 SELinux 策略类型直接决定了使用哪些策略规则集来规定对象可以访问什么。策略类型还决定了哪些特定的安全上下文属性需要的。这取决于你从何处开始查看通过 SELinux 实现细粒度访问控制。

你的发行版中提供的策略类型可能与此处列出的不匹配。例如，在旧的 Linux 发行版中，`strict` 策略可用。在较新的发行版中，`strict` 策略已合并到 `targeted` 策略中，并默认使用 `targeted`。

SELinux 有不同的策略供选择：

- `Targeted`
- `MLS`
- `Minimum`

每种策略都实现了不同的访问控制以匹配你组织的需求。理解这些策略类型至关重要，以便根据你特定的安全需求选择正确的策略。

## Targeted 策略

为了满足你的特定需求，位于 `/etc/selinux/` 目录下的配置文件控制着 SELinux 状态。主配置文件是 `config`，其显示内容如下：

```bash
# cat /etc/selinux/config
# getforcing
# sestatus
SELinux status:
SELinuxfs mount: /sys/fs/selinux
SELinux root directory: /etc/selinux
Loaded policy name: targeted
Current mode: enforcing
Mode from config file: enforcing
Policy MLS status: enabled
Policy deny unknown status: allowed
Max kernel version: 28
```

要更改模式设置，使用 `setforce newsetting`，其中 `newsetting` 或是：

- `enforcing` `1`
- `permissive` `0`

```bash
# setforce 0
# getforce
```

# 第 24 章：使用 SELinux 增强 Linux 安全

```
Permissive
# sestatus
SELinux status: enabled
SELinux-fs mount: /sys/fs/selinux
Loaded policy name: targeted
Current mode: permissive
Mode from config file: enforcing
```

## 注意事项

最好通过修改配置文件从 `disabled` 切换到 `enforcing` 并重启。通过 `setforce` 命令从 `disabled` 切换到 `enforcing` 可能会因为文件标签错误而导致系统挂起。请记住，在更改 `disabled` 模式重启后，文件系统可能需要等待，直到系统以 `permissive` 或 `enforcing` 模式启动。

要禁用 SELinux，必须编辑 SELinux 配置文件。重启系统始终会将模式改回配置文件中设置的值。更改 SELinux 模式优优方法是修改配置文件并重启系统。

从 `disabled` 切换到 `enforcing` 或 `permissive` 模式时，SELinux 在重启后会对文件系统进行重新标记。这意味着 SELinux 会检查并更改任何具有错误安全上下文（例如，标签错误的文件）的安全上下文，这些文件可能会在新模式下引起问题。此外，还包括任何未标记上下文的文件。此重新标记过程可能需要很长时间，因为每个文件的上下文都会被检查。以下是系统在重启后进行重新标记过程时收到的消息：

> *** 警告 - 需要重新标记 SELinux targeted 策略。
> *** 重新标记可能需要很长时间，取决于文件系统的大小和硬盘的速度。

若要修改 `/etc/selinux/config` 文件，请将 `SELINUX=` 行更改为以下值之一：

- `disabled`
- `enforcing`
- `permissive`

下面的 SELinux 配置文件示例显示了模式已设置为 `permissive`。现在，当系统重启时，模式就会发生变化。

```
# /etc/selinux/config
# 此文件控制系统上 SELinux 的状态。
# SELINUX= 可以取以下三个值之一：
# enforcing - 强制 SELinux 安全策略。
# permissive - SELinux 打印警告而不是强制。
# disabled - SELinux 已完全禁用。
SELINUX=permissive
```

SELinux 配置文件不仅包含模式设置，它还指定了将执行的策略类型。

## 设置 SELinux 策略类型

你选择的策略类型决定了 SELinux 强制 TE、MLS 还是基础包。该类型直接决定了用于规定对象可以访问内容的规则集。

默认情况下，策略类型设置为 `targeted`。要更改默认策略类型，请编辑 `/etc/selinux/config` 文件。将 `SELINUXYPE=` 行更改为以下值之一：

- `targeted`
- `mls`
- `minimum`

如果你选择 SELinux 类型为 `mls` 或 `minimum`，你需要确保已安装了相应的策略包。通过输入以下命令检查：`yum list selinux-policy-mls` 或 `yum list selinux-policy-minimum`。

> 注意：在 Ubuntu 上检查 SELinux 策略包，请使用命令 `sudo apt-cache policy package_name`。

接下来的 SELinux 配置文件示例显示类型已设置为 `mls`。当系统重启时，策略类型会发生变化。

```
# cat /etc/selinux/config
# 此文件控制系统上 SELinux 的状态。
# SELINUXTYPE= 使用的策略类型。可能的值有：
# targeted 仅保护网络守护进程。
# strict 全 SELinux 保护。
SELINUXTYPE=mls
```

> 警告：不要被 SELinux 配置文件中过时的注释误导。在较新的 Linux 发行版中，你无法将 `SELINUXTYPE` 设置为 `strict`。如果系统挂起，你必须使用 grub 命令来修复此问题。`strict` 策略类型现在是 `targeted` 策略类型的一部分。

# 第 24 章：使用 SELinux 增强 Linux 安全

## 管理 SELinux 安全上下文

SELinux 安全上下文允许 SELinux 为主体访问对象执行策略规则。你的 Linux 系统已经分配了安全上下文。

要查看当前的 SELinux 文件和进程的安全上下文，请使用 `secon` 命令。表 24.1 列出了 `secon` 命令的可用选项。

### 表 24.1 secon 命令选项

| 选项 |  |
| :--- | :--- |
| `-u` | 使用此选项显示安全上下文的用户。 |
| `-r` | 使用此选项显示安全上下文的角色。 |
| `-t` | 使用此选项显示安全上下文的类型。 |
| `-s` | 使用此选项显示安全上下文的敏感性级别。 |
| `-c` | 使用此选项显示安全上下文的权限。 |
| `-m` | 使用此选项以 MLS 范围的形式显示安全上下文的敏感性和权限级别 |

如果你不带任何参数使用 `secon` 命令，它将向你显示当前进程的安全上下文。要查看另一个进程的安全上下文，请使用 `-p` 选项。下面的示例演示了如何使用 `secon` 查看当前和系统进程的安全上下文。

```
# secon -urt
user: unconfined_u
role: unconfined_r
type: unconfined_t
# secon -urt -p 1
user: system_u
```

注：原文中存在大量重复内容，此处已根据逻辑对核心内容进行了整合翻译。

由专门为该守护进程编写的 SELinux 策略。如果某个进程不存在策略，则会被分配一个默认类型 `unconfined_t`。

对于由用户（父进程）运行的程序或应用程序，新进程（子进程）会继承用户的安全上下文。当然，这只有在用户被允许运行程序时才会发生。一个进程也可以运行程序，在这种情况下，子进程会继承其父进程的安全上下文。因此，子进程在相同的域中运行。

因此，进程的安全上下文在程序运行之前就已经设置，并取决于启动它的谁。你可以使用几个命令来更改程序运行的安全上下文：

- `runcon`——使用选项来确定用户、角色和类型（即域）。
- `sandbox`——在严格控制的域内运行程序（沙箱）。

使用 `runcon` 可能会导致许多问题，因此请谨慎使用。然而，`sandbox` 提供了大量的保护。它允许在你的 Linux 系统上灵活地测试新程序。

## 编写 SELinux 策略包

策略规则用于 SELinux 确定主体是否对对象具有访问权限。它们被分组为包（也称为模块），并使用 SELinux 安装。在你的系统上查看模块的简单方法是使用 `semodule` 命令。它可以让你看到所有的策略模块及其当前版本号。`semodule` 命令的示例是：

```bash
# module -1
abrt 1.2.0
accountsd 1.0.6
acct 1.5.1
...
vserver 3.8.4
zabbix 1.5.3
zarafa 1.1.0
zebra 1.2.0
zoneminder 1.1.1
```

几个工具可以帮助你管理甚至创建自己的策略模块。表 24.3 显示了 Fedora 系统上提供的各种策略包工具。

### 表 24.3 SELinux 策略包工具

| 策略工具 | 说明 |
| --- | --- |
| `audit2allow` | 从拒绝的操作日志中生成策略允许/审计规则 |
| `audit2why` | 从拒绝的操作日志中生成访问被拒绝的原因描述 |
| `checkmodule` | 编译策略模块 |
| `checkpolicy` | 编译 SELinux 策略 |
| `load_policy` | 将新策略加载到内核 |
| `semodule` | 管理策略模块 |
| `semodule_deps` | 列出策略包之间的依赖关系 |
| `semodule_expand` | 扩展策略模块包 |
| `semodule_link` | 将策略模块包链接 |
| `semodule_package` | 创建策略模块包 |

以下是一个用用创建本地策略规则框架的示例策略。示例策略非常长，因此只显示了部分。

```bash
# cat /usr/share/selinux/dev/example.te
policy_module(myapp,1.0.0)
####################################
#
# 声明
#
type myapp_t;
type myapp_exec_t;
domain_type(myapp)
domain_entry_file(myapp_t, myapp_exec_t)
type myapp_log_t;
logging_log_file(myapp_log_t)
type myapp_tmp_t;
files_tmp_file(myapp_tmp_t)
...
```

```bash
allow myapp_t myapp_tmp_t:file manage_file_tmp_perms;
files_tmp_fileletrans(myapp_t,myapp_tmp_t,file)
```

前面的示例代码显示策略代码中使用了特殊的语法。要创建和修改策略规则，你需要学习这种策略语言语法，学习如何使用 SELinux 策略编译器，以及如何将策略规则链接在一起形成模块；你可能需要参加几个为期一天的课程。在这一点，你可能会想要放弃 SELinux。然而，使用布尔值（Booleans）修改策略要简单得多。

## 通过布尔值管理 SELinux

SELinux 策略编写和模块创建是一项复杂且耗时的活动。创建错误的策略规则可能会损害你 Linux 系统的安全性。诚实地说，SELinux 提供了布尔值。

布尔值是一个开启或关闭设置的开关。布尔开关允许你在不需要具备策略编写知识的情况下更改 SELinux 规则的一部分。这些更改也可以无需重启系统完成！

要列出 SELinux 中使用的所有布尔值，请使用 `getsebool -a` 命令。以下是 Fedora Linux 系统上带有布尔值的 SELinux 策略示例：

```bash
getsebool -a
abrt_anon_write --> off
abrt_handle_event --> off

xserver_object_manager --> off
zabbix_can_network --> off
```

要查看可以通过布尔值修改的特定策略，再次使用 `getsebool` 命令。这次将策略传递给它，如下所示：

```bash
getsebool httpd_can_connect_ftp
httpd_can_connect_ftp --> off
```

要切换策略，你可以使用 `setboolean` 命令或 `toggleboolean` 命令。这两个命令都会更改策略。

## 第 24 章：使用 SELinux 增强 Linux 安全性

目录 `/home/chris/Music`。要查看完整的 SELinux 消息：

运行 `sealert -1 8f52dd56-8025-4208-af41-7d29dbaaa46b`

从示例中，你可以看到 SELinux 用户尝试以特定用户的身份登录 FTP 服务 (`vsftpd`)。由于 FTP 使用明文密码，该操作被认为是不安全的，因此被 SELinux 拒绝。请注意，AVC 拒绝信息会提示你，可以运行 `sealert -1` 命令来获取更多信息。

`sealert` 工具允许你获取有关特定 AVC 拒绝消息的更多信息。`sealert` 的信息格式允许你诊断问题。示例显示了 `sealert` 提供的上一个示例中显示的 AVC 拒绝的信息。注意使用的命令与之前的消息日志文件中的命令完全相同。`sealert` 命令中使用的长数字是 AVC 拒绝 ID。

```bash
# sealert -1 8f52dd56-8025-4208-af41-7d29dbaaa46b
```

SELinux 阻止了 `/usr/bin/vsftpd` 访问目录 `/home/chris/Music`。

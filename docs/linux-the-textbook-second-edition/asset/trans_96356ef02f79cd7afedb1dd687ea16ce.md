

![](img/2a18e06cd9c6395e451f26126ecba1fd_636_0.png)

图18.2 systemd 引导目标。

## 18.2.3 systemd 控制的关机

如第17章2.3.2节所介绍，systemd 控制的关机可以遵循多条路径，具体取决于“引入”哪些目标单元来实现所需的系统关机或重启方式。参见图18.3，这些路径从 shutdown.target 和 umount.target 流向 poweroff.target。沿这些路径启动过程的具体 systemctl 命令见表17.1。

图18.3显示了关机、重启和断电过程中涉及的常见目标和服务。对于 kexec，它使你能够从当前运行的内核加载并引导至另一个内核，重启过程非常快，无需等待整个 BIOS 引导过程完成。

我们在本书网站的 W27 章第4和第5节中提供了关于关机目标的更多信息。

![](img/2a18e06cd9c6395e451f26126ecba1fd_637_0.png)

图18.3 systemd 关机路径。

## 18.3 使用 systemctl 命令的 systemd 系统服务管理基础

当引导和启动过程结束，系统进入稳定状态（其正常运行状态）后，systemd 的主要目的是通过高效、迅捷地管理系统服务与进程来维持该稳定状态。本节详细介绍这一操作，并给出系统服务管理中最重要工具命令 systemctl 的几个用例。

systemctl 命令的一般形式如下：

```
Syntax:
    systemctl [OPTIONS...] COMMAND [Name...]
Purpose: systemctl is the controlling command for the state of the “systemd” system and service manager
Output: Modified system state control
Commonly used options/features:
  -t, --type=argument    where argument should be a comma-separated list of unit types, such as service and socket
  -a, --all              used with the list-units command, to show inactive units and units which are following other units
  --after                used with list-dependencies, to show the units that are ordered before the specified unit
```

**常用命令及用法：**

| 命令 | 描述 |
|---|---|
| `systemctl` | 列出所有服务单元文件及其他单元 |
| `systemctl start` | 启动服务（非持久） |
| `systemctl stop Name` | 停止服务（非持久） |
| `systemctl restart Name` | 停止然后重新启动服务 |
| `systemctl reload Name` | 重新加载配置文件，不中断正在进行的操作 |
| `systemctl restart Name` | 如果服务已在运行则重新启动 |
| `systemctl status Name` | 说明服务当前是否正在运行 |
| `systemctl enable Name` | 启用服务，以便下次引导时或其他触发器时启动 |
| `systemctl disable Name` | 禁用服务，使其在下次重启或任何其他触发器时不启动 |
| `systemctl is-enabled Name` | 检查服务是否配置为启动 |
| `systemctl list-unit-files` | 列出单元文件 |
| `systemctl daemon-reload` | 重新启动 systemd 管理程序本身 |

### 练习 18.6

在你的 Linux 系统上使用 systemctl 命令，确定已加载多少个单元。其中有多少单元处于非活动状态？你使用什么命令来查看所有已加载但处于非活动状态的单元的名称？

在后续章节以及本书网站的 W27 章的许多插图中，我们展示了 systemctl 命令的一般或通用格式，连同其可能的选项和子命令。你可以通过以下方式识别这些通用格式：命令行提示符缺失，且命令参数是通用的 name.service。例如：

```
sudo systemctl start name.service
```

我们还展示了许多 systemctl 命令，并在前面加上 Bash 的 $ 命令行提示符，其中包含我们在代表性 Linux 系统上看到的具体选项和参数。例如：

```
$ sudo systemctl set-default multi-user.target
```

还要注意，我们都是以普通用户身份使用 sudo 来执行所有 systemctl 命令！这是因为我们后面演示的许多 systemctl 命令都会改变系统状态，要求你在 Linux 系统上拥有 sudo 权限。因此，为了避免区分需要或不需要该权限的命令，我们一概使用 sudo 命令。

### 18.3.1 如何使用 systemctl 管理 systemd 服务和单元

作为用户可直接使用的命令（即位于图18.1的顶部），以下各节将说明 systemctl 命令的一些重要用途。这些节将进一步扩展你对 systemd 在维护内核以及构成 Linux 计算机的整个软件/硬件系统稳定状态方面有多广泛、多普遍的理解。

表18.1汇总了最常用的 systemctl 子命令及每个命令的简要说明。

#### 18.3.1.1 服务管理

诸如 systemd 之类的初始化和启动系统的基本目的之一，是初始化 Linux 内核引导后必须启动的组件。这些组件传统上被称为“用户态”组件。初始化系统还用于管理服务和服务守护进程

# 表18.1

# systemctl 命令

| 命令与参数 | 描述 |
| --- | --- |
| list-units [Pattern] | 列出单元[根据模式]。如果指定了多个模式，仅显示与其中一个模式匹配的单元 |
| list-unit-files [Pattern] | 列出已安装的单元文件[根据模式]及其状态 |
| list-timers [Pattern] | 列出定时器单元，并显示它们下次到期的时间 |
| list-dependencies [Name] | 递归列出单元[Name]所需（required）和期望（wanted）的单元 |
| set-default Name | 设置系统引导进入的默认目标 |
| start Pattern | 启动模式单元 |
| stop Pattern | 停止模式单元 |
| daemon-reload | 重新加载 systemd 管理器配置 |
| restart Pattern | 重新启动模式中指定的单元。如果这些单元尚未运行，则启动它们 |
| isolate Name | 启动单元 Name 及其依赖项，并停止所有其他单元 |
| get-default | 列出系统引导进入的默认目标。即列出 default.target 所符号链接到的目标单元名称 |
| is-active Pattern | 检查模式指定的任何单元是否处于活动（运行）状态 |
| status [Pattern] | 显示一个或多个单元的运行时状态信息，以及日志中最近的日志数据 |
| enable Name | 单元将在下次重启时自动启动 |
| reenable Name | 重置符号链接，以便你可以先禁用再启用某个单元 |
| disable Name | 禁用 Name 单元。从单元配置目录中移除所有指向 Name 单元文件的符号链接。单元将不会在下次重启时自动启动 |
| is-enabled Name | 给出 Name 的启用状态 |
| emergency | 进入紧急目标状态 |
| rescue | 进入救援目标状态 |
| poweroff | 关闭系统并切断电源 |
| reboot | 关闭并重新启动计算机 |
| halt | 关闭并停止系统 |

注：凡以 [ ] 括起来的内容都是可选的。

此外，在系统正常运行的任何时刻，该服务管理功能还扩展为涵盖优雅有序的重启或关机。

在 systemd 中，要管理的对象是“单元”（units），即 systemd 最自然地设计用于管理的资源。单元按其代表的资源类型进行分类，并通过称为单元文件的文件加以定义。每个单元的类型可以从该单元文件名末尾的后缀推断出来。

对于服务管理任务，该单元将是服务单元，其单元文件的后缀为 .service。然而，对于你执行的大多数服务管理命令，实际上可以省略 .service 后缀，因为 systemd 在使用服务管理命令时默认操作的就是服务。

若要启动系统服务，请通过执行服务单元文件中的指令，使用 start 命令，如下所示。如果你是以非 root 用户身份运行，则必须使用 sudo，因为正如前面提到的，启动服务会改变操作系统的状态：

```
sudo systemctl start name.service
```


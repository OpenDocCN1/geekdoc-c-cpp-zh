

| VLAN | 名称 | 状态 |
|---|---|---|
| 2 | Freds-vlan | active |
| 3 | VLAN0003 | active |
| 1002 | fddi-default | act/unsup |
| 1003 | token-ring-default | act/unsup |
| 1004 | fddinet-default | act/unsup |
| 1005 | trnet-default | act/unsup |

## 存储 VTP 及相关配置

有趣的是，尽管 VTP 会同步 VLAN 和 VTP 配置，你却不能直接通过输入 `show running-config` 命令来发现交换机是否已同步其 VLAN 配置数据库。VTP 不会将配置命令放入 VTP 服务器或客户端的 running-config 或 startup-config 文件中。相反，VTP 服务器和客户端模式的交换机会将 `vtp` 配置命令以及一些 VLAN 配置命令存储在闪存中的 `vlan.dat` 文件里。要验证这些配置命令及其设置，请使用 `show vtp status` 和 `show vlan` 命令。

图 5-9 显示了一个示例。它展示了三个关键的 VTP 命令（`vtp mode`、`vtp domain` 和 `vtp password`），以及一个创建 VLAN 10 的 `vlan 10` 命令。图中还展示了 `switchport access vlan 10` 接口子命令以作对比。其中，在 VTP 服务器或客户端上，只有 `switchport access vlan 10` 命令会出现在 running-config 或 startup-config 文件中。

![](img/79473ea15699e01619d2aa789f5bd43b_189_0.png)

*图 5-9* VTP 存储配置的位置：VTP 客户端与服务器

没有与 `show running-config` 等效的命令来显示 `vlan.dat` 文件的内容。相反，你必须使用各种 `show vtp` 和 `show vlan` 命令来查看有关 VLAN 和 VTP 的信息。作为参考，表 5-3 列出了与 VLAN 相关的配置命令、VTP 服务器或客户端存储这些命令的位置，以及如何查看这些命令的设置。

**表 5-3 VTP 客户端和服务器存储 VLAN 相关配置的位置**

| 配置命令 | 存储位置 | 查看方式 |
|---|---|---|
| `vtp domain` | vlan.dat | `show vtp status` |
| `vtp mode` | vlan.dat | `show vtp status` |
| `vtp password` | vlan.dat | `show vtp password` |
| `vtp pruning` | vlan.dat | `show vtp status` |

- 对于任意组合的 VTP 服务器和客户端，相邻交换机之间的 VTP 版本不必匹配即可进行同步。
- 在判断 VTP 是否已同步时，请注意 VLAN 的管理状态（根据全局配置命令 **shutdown vlan vlan-id** 以及 VLAN 配置模式下的 **shutdown** 命令）不会通过 VTP 进行通信。因此，两个相邻交换机可以知道同一个 VLAN，但该 VLAN 在一台交换机上处于关闭状态，而在另一台交换机上处于活动状态。

## 配置 VTP 时常见的拒绝情况

VTP 客户端根本无法配置 VLAN，无论是添加、删除还是命名。VTP 服务器（使用 VTP 版本 1 和 2 时）仅限于操作标准范围的 VLAN。接下来的简短主题将展示当您尝试添加这些 VLAN 时出现的错误消息，尽管本章声称允许这样做，只是为了让你了解错误消息的样子。

### 示例 5-4 *在 VTP 客户端和服务器上尝试 vlan 命令*

```
SW3# configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW3(config)# vlan 200
VTP VLAN configuration not allowed when device is in CLIENT mode.
SW3(config)# vlan 2000
SW3(config-vlan)# exit
% Failed to create VLANs 2000
Extended VLAN(s) not allowed in current VTP mode.
%Failed to commit extended VLAN(s) changes.
SW3(config)#
```

示例的后半部分展示了一些奇怪的现象。首先，`vlan 200` 命令立即被拒绝。其次，`vlan 2000` 命令也被拒绝，但不是立即——IOS 的逻辑有些奇怪，直到用户退出 VLAN 配置模式时，IOS 才真正尝试添加扩展模式 VLAN 的配置。一旦发出 `exit` 命令，IOS 就发出了三条高亮错误消息——所有这些消息都以某种方式确认 VLAN 2000 并未被创建。

请注意，在 VTP 服务器上，`vlan 200` 命令会被接受，但 `vlan 2000` 命令会被拒绝，其过程与示例中所示相同。

## 向网络中添加交换机时的问题

VTP 可能导致前面段落所描述的那种普遍的局域网问题，因此在使用 VTP 时你必须格外小心。当一台新的交换机连接到现有网络时，就可能发生这类问题。无论这种问题是偶然发生还是作为拒绝服务（DoS）攻击，根本原因都是：

当两台相邻交换机首次通过中继链路连接，并且它们也满足通过 VTP 进行同步的所有要求时，修订号较低的交换机会接受来自修订号较高的邻居的 VLAN 数据库。

请特别注意，前面的陈述完全没有提到哪台交换机是服务器或客户端，也没有提到哪台是较旧的生产交换机，哪台是新添加的交换机。也就是说，无论服务器具有较高的修订号还是客户端具有较高的修订号，两台交换机最终都会统一使用具有较高修订号的 VLAN 数据库。其中没有任何关于哪台交换机是客户端或服务器、哪台是新交换机、哪台是既有旧交换机的逻辑。

这种在连接新交换机时使用较高修订号的 VTP 行为具有一些相当强大的含义。例如，考虑以下场景：有人正在为 CCNA R&S 考试学习，使用公司小实验室里的设备。实验室里有几台与生产网络隔离的局域网交换机——也就是说，这些交换机甚至没有线缆连接到生产网络。但由于工程师知道生产环境中使用的 VTP 域名和密码，在实验室配置时，工程师使用了相同的 VTP 域名和密码。这（暂时）不会造成问题，因为实验室交换机甚至没有连接到生产网络。（在现实生活中，请在实验室设备中使用不同的 VTP 域名和密码！）

同一位工程师继续在实验室进行 CCNA 学习和测试，对 VLAN 配置做了大量更改。每次更改都会使 VLAN 配置数据库的修订号增加 1。最终，实验室交换机的 VTP 配置修订号变得很高，高到超过了生产交换机的修订号。但实验室仍然隔离，所以仍然没有问题。

你看到危险了吗？现在只需要有人将一根链路从实验室交换机连接到生产交换机并使其成为中继。例如，想象现在另一位工程师决定在实验室进行一些测试，却没有想到检查实验室交换机与生产交换机的 VTP 状态。这第二位工程师走进实验室，将实验室交换机连接到生产网络。链路协商为中继…VTP 在实验室交换机和生产交换机之间同步…然后这两台交换机发现实验室交换机的配置数据库具有更高的修订号。此时，VTP 正在愉快地履行职责，同步 VLAN 配置数据库，但不幸的是，VTP 正在分发实验室的 VLAN 配置，从而删除了生产 VLAN。

在现实生活中，当将新交换机安装到现有 VTP 域时，有几种方法可以帮助减少此类问题的发生。特别是，在将新交换机连接到现有 VTP 域之前，请通过以下任一方法将新交换机的 VTP 修订号重置为 0：

- 将新交换机配置为 VTP 透明模式，然后再切换回 VTP 客户端或服务器模式。
- 擦除新交换机闪存中的 `vlan.dat` 文件并重新加载交换机。（`vlan.dat` 文件包含交换机的 VLAN 数据库，包括修订号。）


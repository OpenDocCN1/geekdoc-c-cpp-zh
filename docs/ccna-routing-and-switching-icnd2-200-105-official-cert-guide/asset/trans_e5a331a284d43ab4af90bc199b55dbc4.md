
最后请注意，示例 11-12 中的 **show ip ospf** 命令还显示了一个常见误报，它看似是 OSPF 邻居问题的一个根本原因。OSPF PID——即 **router ospf** 命令中的编号——不必匹配。请注意，在示例 11-12 中，同一输出的第一行显示 R3 使用 **router ospf 3** 命令，依据是短语 “Process ospf 3”，而 R1 使用 **router ospf 1** 命令，如短语 “Process ospf 1” 所示。这些不匹配的编号并不是问题。

### 发现 OSPF Hello 和 Dead 计时器不匹配

最后，考虑 R4 上产生的问题：其配置的 Hello 计时器和 Dead 计时器与 R1、R2 和 R3 上的默认设置不同。EIGRP 允许邻居使用不同的 Hello 计时器，而 OSPF 不允许，因此这种不匹配导致 R4 无法与其他三台 OSPF 路由器中的任何一台成为邻居。

示例 11-13 展示了查找该不匹配的最简单方法，即在 R1 和 R4 上都使用 **show ip ospf interface** 命令。该命令列出每个接口的 Hello 和 Dead 计时器，如示例中高亮所示。请注意，R1 使用 10 和 40（Hello 和 Dead），而 R4 使用 5 和 20。

**示例 11-13** 查找不匹配的 Hello/Dead 计时器

```text
R1# show ip ospf interface G0/0
GigabitEthernet0/0 is up, line protocol is up
  Internet Address 10.1.1.1/24, Area 0, Attached via Network Statement
  Process ID 1, Router ID 1.1.1.1, Network Type BROADCAST, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1         no          no            Base
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router (ID) 1.1.1.1, Interface address 10.1.1.1
  No backup designated router on this network
  Timer intervals configured, Hello 10, Dead 40, Wait 40, Retransmit 5
    Hello due in 00:00:00
  ! lines omitted for brevity

! Moving on to R4 next
!
R4# show ip ospf interface Gi0/0
GigabitEthernet0/0 is up, line protocol is up
  Internet Address 10.1.1.4/24, Area 0, Attached via Network Statement
  Process ID 4, Router ID 10.1.44.4, Network Type BROADCAST, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1         no          no            Base
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router (ID) 10.1.44.4, Interface address 10.1.1.4
  No backup designated router on this network
  Timer intervals configured, Hello 5, Dead 20, Wait 20, Retransmit 5
    Hello due in 00:00:00
  ! lines omitted for brevity
```

**debug ip ospf hello** 命令也可以发现此问题，因为它会为每个 Hello 列出一条消息，从而揭示 Hello/Dead 计时器不匹配，如示例 11-14 所示。

| 命令 | 描述 |
|---|---|
| show ip ospf interface brief | 列出启用了 OSPF 协议的接口（基于 **network** 命令），包括被动接口 |
| show ip ospf interface [type number] | 列出所有接口或所列接口的详细 OSPF 设置，包括 Hello 和 Dead 计时器以及 OSPF 区域 |
| show ip route ospf | 列出路由表中由 OSPF 学习到的路由 |
| show ip ospf neighbor | 按接口列出邻居及与邻居的当前状态 |
| show ip ospf | 列出一组关于 OSPF 进程本身的消息，并在第一行列出 OSPF Router ID |
| show interfaces | 按接口列出一长组消息，其中列出配置、状态和计数器信息 |
| show interfaces description | 为每个接口列出一行输出，包含简要状态信息 |

**表 11-9** 第 11 章 `debug` 命令参考

| 命令 | 描述 |
|---|---|
| debug eigrp packets | 列出进出路由器的 EIGRP 数据包的日志消息 |
| debug ip ospf adj | 为邻接事件（即与路由器成为邻居相关的事件）发出日志消息 |
| debug ip ospf events | 为 OSPF 采取的每个操作发出日志消息，包括接收消息 |
| debug ip ospf packet | 发出描述所有 OSPF 数据包内容的日志消息 |
| debug ip ospf hello | 发出描述 Hello 和 Hello 失败的日志消息 |
| undebug all | 用于禁用所有当前调试的 EXEC 命令 |

## 实施外部 BGP

**本章涵盖以下考试主题：**

- 3.0 WAN 技术
- 3.4 描述 WAN 拓扑选项
  - 3.4.d 单归属与双归属
- 3.6 使用 eBGP IPv4 配置并验证单归属分支机构连通性（仅限使用 Network 命令进行对等和路由通告）

在 Cisco CCNA Routing & Switching 认证的悠久历史中，Cisco 首次为最新的 ICND2 和 CCNA R&S 考试将边界网关协议（BGP）纳入其中。过去，BGP 可能只是作为当前用于在公司（就 BGP 而言称为自治系统）之间交换路由的一种路由协议而被提及。现在，在 Cisco CCNA R&S 考试历史上，考试主题首次包含 BGP 配置和验证主题。

然而，唯一的 BGP 考试主题只涵盖 BGP 的一小部分，这使得 BGP 的讨论仅限于本章。BGP 是一种长期存在且灵活的协议，具有许多核心特性，多年来还增加了许多特性。本章介绍 Cisco 选择引入 CCNA 的这一小部分内容：在企业与 ISP 之间，仅使用单条互联网链路，将 BGP 用于 IPv4。

### “我已经掌握了吗？”测验

如果你想用分数帮助决定花多少时间学习本章，请参加测验（可以在这里进行，也可以使用 PCPT 软件）。答案在测验后页面底部，解析在 DVD 附录 C 和 PCPT 软件中。

**表 12-1** “我已经掌握了吗？”基础主题部分与问题对应关系

| 基础主题部分 | 问题 |
|---|---|
| BGP 概念 | 1–3 |
| eBGP 配置与验证 | 4–6 |

1. 以下哪些互联网边缘设计包含到两个 ISP 的连接？（选择两个答案。）
   - a. 单归属
   - b. 单多归属
   - c. 双归属
   - d. 双多归属

为了让你了解互联网核心路由器中 IP 路由表的规模，请查看网站 http://bgp.potaroo.net，这是 Geoff Huston 的网站，他几十年来一直在发布有关互联网的统计数据。在编写本章时查看该网站显示，互联网中 BGP 表的规模——它表示这些路由器中预计存在的 IPv4 路由数量——略高于 600,000 条条目。BGP 要做的工作很多。

### 使用 BGP 通告路由

BGP 使用与 IGP 相同的一般过程来交换路由信息，但当然也有一些差异。要启动 BGP 进程，一台路由器必须了解某个 IPv4 前缀。然后，它使用 BGP 协议消息（BGP 更新消息）与另一台路由器交换路由信息，如图 12-1 所示。在 BGP 中，另一台路由器称为 BGP 邻居或 BGP 对等体。

![](img/79473ea15699e01619d2aa789f5bd43b_358_0.png)

**图 12-1** *在自治系统之间使用 BGP*

与 IGP 相比，BGP 的一个重大区别是，BGP 将路由通告给其他公司中的其他路由器，图中表示为其他 ISP。按照定义，IGP 将路由通告给同一公司内部的其他路由器。

> **注意** 虽然 IGP 通告的地址块通常称为*子网*，但在 BGP 中，我们将这些地址块称为*前缀*、*地址块*，甚至正式 BGP 名称*网络层可达性信息（NLRI）*。不使用*子网*一词的原因是，在实践中，BGP 很少通告小到单个子网的地址块。

BGP 与 IGP 在用途上不同，其中包括：对于企业而言，BGP 可用于向本地 ISP 通告企业的公共 IPv4 前缀。在图 12-1 中，企业位于最左侧，并与企业的 ISP（本例中为 ISP1）建立 BGP 对等关系。然后，企业将其公共前缀（C 类网络 192.0.2.0/24）通告到 ISP1 中。为了构建全球互联网，ISP 之间相互连接，因此 ISP1 随后如图所示将该前缀（192.0.2.0/24）通告给其他 ISP，以便互联网各部分都知道如何将数据包转发到 192.0.2.0/24 中的地址。

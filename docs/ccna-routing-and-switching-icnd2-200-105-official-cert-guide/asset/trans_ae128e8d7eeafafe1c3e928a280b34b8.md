
VLAN位于12位系统ID扩展字段中。网络工程师唯一可配置的部分是4位优先级字段。

然而，配置优先级字段中的数字是Cisco路由器或交换机上最奇怪的配置之一。如图3-3顶部所示，优先级字段最初是一个16位数字，表示从0到65,535的十进制数。由于这段历史，当前的配置命令（`spanning-tree vlan vlan-id priority x`）要求一个介于0和65,535之间的十进制数。但并非该范围内的任何数字都有效——它必须是4096的倍数：0、4096、8192、12288，依此类推，直到61,440。

交换机根据配置的值设置BID的前4位。事实证明，在从0到61,440的16个允许的4096倍数中，每个倍数的前4位都有不同的二进制值：0000、0001、0010，依此类推，直到1111。交换机根据配置值的前4位设置真正的4位优先级。

尽管历史和配置可能使BID优先级的概念显得有点复杂，但在BID中增加一个12位字段在实践中效果很好，因为它可用于识别VLAN ID。VLAN ID的范围为1到4094，需要12位。Cisco交换机将VLAN ID放入系统ID扩展字段中，因此每台交换机在每个VLAN中都有唯一的BID。

例如，一台配置了VLAN 1到4的交换机，默认基础优先级为32,768，在VLAN 1中的默认STP优先级为32,769，VLAN 2中为32,770，VLAN 3中为32,771，依此类推。因此，你可以将16位优先级视为基础优先级（如`spanning-tree vlan *vlan-id* priority x`命令中所配置的）加上VLAN ID。

> **注意** Cisco交换机必须使用系统ID扩展版本的网桥ID；无法禁用。

## 每VLAN端口成本

每个交换机接口根据第2章表2-6中列出的IEEE建议，默认设置其每VLAN STP成本。在支持多种速率的接口上，Cisco交换机基于当前实际速率来计算成本。因此，如果接口协商使用较低速率，默认STP成本将反映该较低速率。如果接口协商使用不同速率，交换机也会动态更改STP端口成本。

或者，你可以使用**spanning-tree [vlan vlan-id] cost**接口子命令配置交换机的STP端口成本。你最常见到该命令用于中继端口，因为在中继端口上设置成本会影响交换机的根成本，而在接入端口上设置STP成本则不会。

对于命令本身，它可以包含VLAN ID，也可以不包含。该命令仅在中继端口上需要vlan参数来设置每个VLAN的成本。在中继端口上，如果命令省略了VLAN参数，它会为所有未通过`spanning-tree vlan x cost`命令设置成本的VLAN设置STP成本。

## STP配置选项摘要

表3-2总结了BID和端口成本的默认设置，并列出了本章涵盖的可选配置命令。

## 关键主题

### 表3-2 STP默认值和配置选项

| 设置 | 默认值 | 更改默认值的命令 |
|---|---|---|
| BID优先级 | 基础：32,768 | `spanning-tree vlan vlan-id root [primary \| secondary]`<br>`spanning-tree vlan vlan-id priority priority` |
| 接口成本 | 10 Mbps 为 100<br>100 Mbps 为 19<br>1 Gbps 为 4<br>10 Gbps 为 2 | `spanning-tree vlan vlan-id cost cost` |
| PortFast | 未启用 | `spanning-tree portfast` |
| BPDU Guard | 未启用 | `spanning-tree bpduguard enable` |

接下来，配置部分展示了如何在简单网络中检查STP的运行，以及如何更改这些可选设置。

## 验证STP运行

在查看如何更改配置之前，首先考虑几个STP验证命令。先查看这些命令有助于加深对默认STP设置的理解。特别是，本节中的示例使用图3-4所示的网络。

![](img/79473ea15699e01619d2aa789f5bd43b_130_0.png)

**图3-4** *用于STP配置和验证示例的示例LAN*

示例3-1以一个有用的STP命令开始讨论：`show spanning-tree vlan 10`命令。该命令识别根交换机，并在本地交换机上列出其设置。示例3-1列出了该命令在SW1和SW2上的输出，如下所述。

甚至有一条明确的语句“此网桥是根”，确认SW1现在是VLAN 10 STP拓扑的根。

接下来，比较示例下半部分中在SW2上相同命令的高亮行。SW2列出了SW1的BID详细信息作为根；换句话说，SW2同意SW1赢得了根选举。SW2没有列出“此网桥是根”这个短语。然后SW2在有关根BID详情的行之后，列出了自己的（不同的）BID详情。

输出还确认了一些默认值。首先，每台交换机将BID的优先级部分列为一个单独的数字：32778。该值来自默认优先级32768，加上VLAN 10，总计32778。输出还显示了一些快速以太网和千兆以太网接口的接口成本，默认分别为19和4。

最后，**show spanning-tree**命令输出的底部列出了VLAN中的每个接口，包括中继端口，以及STP端口角色和端口状态。例如，在交换机SW1上，输出列出了三个接口，角色为Desg（指定端口，DP），状态为FWD（转发）。SW2列出了三个接口，两个DP和一个根端口，因此这三个接口都处于FWD或转发状态。

示例3-1展示了许多有用的STP信息，但示例3-2中显示的两个其他命令更适合以更简短的形式列出BID信息。第一个命令**show spanning-tree root**列出了每个VLAN的根BID。该命令还列出了其他详细信息，如本地交换机的根成本和根端口。另一个命令**show spanning-tree vlan 10 bridge**将BID分解为其组成部分。在本示例中，它显示SW2的优先级为默认值32768，VLAN ID为10，以及MAC地址。

### 示例3-2 在交换机SW2上列出根交换机和本地交换机的BID

```
SW2# show spanning-tree root

                                                Root    Hello Max Fwd
Vlan                    Root ID                 Cost    Time  Age Dly  Root Port
------------------- ------------------------- --------- ----- ---- --- ----------
VLAN0001                 32769 1833.9d5d.c900        23    2   20  15   Gi0/1
VLAN0010                 32778 1833.9d7b.0e80         4    2   20  15   Gi0/2
VLAN0020                 32788 1833.9d7b.0e80         4    2   20  15   Gi0/2
VLAN0030                 32798 1833.9d7b.0e80         4    2   20  15   Gi0/2
VLAN0040                 32808 1833.9d7b.0e80         4    2   20  15   Gi0/2

SW2# show spanning-tree vlan 10 bridge

                                                Hello Max Fwd
Vlan                    Bridge ID               Time  Age Dly  Protocol
------------------- ------------------------- ----- ---- --- --------
VLAN0010                 32778 (32768,  10) 1833.9d7b.1380       2   20  15  ieee
```

请注意，示例3-2中的两个命令都有一个VLAN选项：**show spanning-tree [vlan x] root**和**show spanning-tree [vlan x] bridge**。如果不列出VLAN，每个命令将每个VLAN列出一行；如果指定VLAN，则输出相同的信息，但仅针对该VLAN。

本示例以在SW3上执行**debug spanning-tree events**命令开始。该命令告诉交换机，每当STP对接口的角色或状态进行更改时，就发出调试日志消息。这些消息在示例中作为配置的结果出现。

接下来，示例展示了使用**spanning-tree vlan 10 cost 30**接口子命令将SW3在VLAN 10中的端口成本更改为30的配置。根据图，通过SW3的G0/1到达根的根成本现在将是30，而不是4。因此，SW3到达根的最佳成本为8，SW3的G0/2作为其根端口。

调试消息带有时间戳，告诉我们SW3上的STP在幕后是如何思考的。请注意，在这种情况下，用户退出配置模式后立即显示的前五条调试消息都发生在同一时间（精确到同一毫秒）。值得注意的是，之前处于转发状态的G0/1立即移动到阻塞状态。之前处于阻塞状态的接口G0/2并未进入转发状态，而是移动到侦听状态（至少根据此消息是这样）。

现在查找列出G0/2转换为学习状态的调试消息，然后查找下一条显示它最终达到转发状态的消息。消息之间相隔多长时间？在每种情况下，消息的时间戳显示已过去15秒。在本实验中，交换机使用默认的转发延迟设置（15秒）。因此，这些调试消息确认了STP将接口从阻塞状态转换到转发状态所采取的步骤。

如果你在配置成本时恰好没有启用调试，之后使用**show**命令也可以确认SW3做出的相同选择，即现在使用其G0/2端口作为根端口（RP）。示例3-4使用**show spanning-tree vlan 10**命令显示了SW3上新的STP端口成本设置，以及新的根端口和根成本。注意，G0/2现在被列为根端口。输出顶部将SW3的根成本列为8，与图3-5所示的分析一致。

### 示例3-4 SW3上新的STP状态和设置

```
SW3# show spanning-tree vlan 10

VLAN0010
  Spanning tree enabled protocol ieee
  Root ID    Priority    32778
             Address     1833.9d7b.0e80
             Cost        8
             Port        26 (GigabitEthernet0/2)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32778  (priority 32768 sys-id-ext 10)
             Address     f47f.35cb.d780
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- ----------------
Fa0/23           Desg FWD 19        128.23   P2p
Gi0/1            Altn BLK 30        128.25   P2p
Gi0/2            Root FWD 4         128.26   P2p
```


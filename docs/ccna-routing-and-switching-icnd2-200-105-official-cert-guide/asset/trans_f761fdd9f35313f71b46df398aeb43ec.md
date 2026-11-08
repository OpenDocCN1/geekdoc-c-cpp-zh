
如示例所示，**show ipv6 protocols** 命令的输出列出了路由器 R1 上的全部五个 OSPFv3 接口，包括被动接口 G0/0.11。

## 排除 OSPFv3 接口故障

大多数关于 OSPFv3 的故障排除讨论都围绕两个 OSPFv3 邻居之间可能出现的问题展开。然而，接口子命令的配置错误实际上可能导致许多此类 OSPF 邻居问题。为了开始讨论，只需考虑本章到目前为止提到的接口子命令可能出现的问题：

![](img/79473ea15699e01619d2aa789f5bd43b_686_0.png)

- 使用 `ipv6 ospf process-id area area-id` 接口子命令配置了错误的区域，会阻止邻居关系在该接口上建立。
- 使接口对 OSPFv3 进程处于被动状态，会阻止本地路由器在该接口上建立邻居关系。

对于列表中的第一项，请注意同一数据链路中的所有 OSPFv3 路由器都需要被分配到同一区域。在考试中，你需要检查有关预期区域设计的任何信息。要查明哪些接口被分配到哪个区域，请使用 **show ipv6 ospf interface** 和 **show ipv6 ospf interface brief** 命令。

至于将接口设置为对 OSPFv3 被动的问题，当需要通过该接口建立邻居关系时，路由器不应将该接口设置为对 OSPFv3 被动。请注意，只有 **show ipv6 ospf interface** 命令会提及哪些 OSPFv3 接口恰好是被动的。

示例 23-6 列出了两条有助于发现这两个问题的命令。两者都会列出区域信息，但只有第二条会提及接口处于被动状态。

**示例 23-6** *在 R1 上查找 OSPFv3 被动接口*

```
R1# show ipv6 ospf interface brief
Interface          PID  Area       Intf ID  Cost  State  Nbrs F/C
Gi0/0.12           1    0          16       1     DR     0/0
Gi0/0.11           1    0          17       1     DR     0/0
Gi0/1              1    4          4        1     DR     1/1
Se0/0/0/1          1    23         7        64    P2P    1/1
Se0/0/0/0          1    23         6        64    P2P    1/1

R1# show ipv6 ospf interface G0/0.11
GigabitEthernet0/0.11 is up, line protocol is up
  Link-local address FE80::FE00:1, Interface ID 17
  Area 0, Process ID 1, Instance ID 0, Router ID 1.1.1.1
  Network Type BROADCAST, Cost: 1
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router (ID) 1.1.1.1, local address FE80::FF:FE00:1
  No backup designated router on this network
  Timer intervals configured, Hello 10, Dead 40, Wait 40, Retransmit 5
  No Hellos (Passive interface)
! remaining lines omitted for brevity
```

最后，为了查看其中一个问题的示例，请再来看一下路由器 R4 的配置。在示例 23-3 中的正确配置中，工程师将 LAN 接口 G0/1 设置为被动，因为该 LAN 上不存在其他路由器。但是请注意，R4 使用一个以太网接口作为其 WAN 接口（G0/0），另一个作为其 LAN 接口（G0/1）。假设工程师犯了一个简单的错误，将 R4 的 G0/0 设置为被动，而不是 G0/1。为了说明会发生什么，示例 23-7 将 R4 的 G0/0 接口改为对 OSPFv3 被动；请注意，在发出 passive-interface 命令后，R4 与 R1 的邻居关系几乎立即失效。

**示例 23-7** *R4 与 R1 的邻居关系因被动而失效*

```
R4# configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R4(config)# ipv6 router ospf 4
R4(config-rtr)# passive-interface GigabitEthernet 0/0
R4(config-rtr)# ^Z
R4#

Jan 17 23:49:56.379: %OSPFv3-5-ADJCHG: Process 4, Nbr 1.1.1.1 on GigabitEthernet0/0 from FULL to DOWN, Neighbor Down: Interface down or detached
```

## OSPFv3 邻居

与往常一样，OSPFv3 沿用了 OSPFv2 关于邻居工作方式的约定。OSPFv3 使用许多相同的协议消息名称、邻居状态以及用于建立邻居关系和交换 LSDB 的概念。接下来的主题既会展示一些过程样本，更重要的是，会讨论查找 OSPF 问题的首要位置：阻止路由器成为邻居的问题。

### 验证 OSPFv3 邻居

接下来，示例 23-8 展示了 OSPFv3 与 OSPFv2 在消息名称和邻居状态方面的一些相似之处。在阅读示例中的调试输出时，不必担心所有细节；相反，请重点关注突出显示的部分。突出显示的内容列出了 OSPFv2 中一些熟悉的邻居状态，如 2-way、exstart、exchange、loading 和 full，在本例中 full 是最终的期望状态。

该示例首先展示了 debug ipv6 ospf adj 命令的输出，该命令列出了 OSPFv3“邻接”事件的消息——即邻居在其状态间转换时发生的情况。示例末尾显示了 R2 的 show ipv6 ospf neighbor 命令输出，证实了 R2 与 R3 的邻居状态最终为 full 状态，正如调试消息中提到的那样。（注意，为了便于阅读，一些调试消息已被删除。）

**示例 23-8** *从 R2 观察其与 R3 的邻居状态变化*

```
R2# debug ipv6 ospf adj
R2#

Jan 15 14:50:58.098: %OSPFv3-2-IPv6_ADJ: Gi0/0: Added 3.3.3.3 to nbr list
Jan 15 14:50:58.098: %OSPFv3-2-IPv6_ADJ: Gi0/0: 2 Way Communication to 3.3.3.3, state 2WAY
Jan 15 14:50:58.098: %OSPFv3-2-IPv6_ADJ: Gi0/0: DR: 3.3.3.3 (Id)  BDR: 2.2.2.2 (Id)
Jan 15 14:50:58.098: %OSPFv3-2-IPv6_ADJ: Gi0/0: Nbr 3.3.3.3: Prepare dbase exchange
Jan 15 14:50:58.098: %OSPFv3-2-IPv6_ADJ: Gi0/0: Send DBD to 3.3.3.3 seq 0x2AC5B307 opt 0x0013 flag 0x7 len 28
Jan 15 14:50:58.102: %OSPFv3-2-IPv6_ADJ: Gi0/0: Rcv DBD from 3.3.3.3 seq 0xBD091ED opt 0x0013 flag 0x7 len 28 mtu 1500 state EXSTART
Jan 15 14:50:58.102: %OSPFv3-2-IPv6_ADJ: Gi0/0: NBR Negotiation Done. We are the SLAVE
Jan 15 14:50:58.102: %OSPFv3-2-IPv6_ADJ: Gi0/0: Nbr 3.3.3.3: Summary list built, size 14
Jan 15 14:50:58.106: %OSPFv3-2-IPv6_ADJ: Gi0/0: Send DBD to 3.3.3.3 seq 0xBD091ED opt 0x0013 flag 0x7 len 308 mtu 1500 state EXCHANGE
Jan 15 14:50:58.106: %OSPFv3-2-IPv6_ADJ: Gi0/0: Rcv DBD from 3.3.3.3 seq 0xBD091EE opt 0x0013 flag 0x7 len 308 mtu 1500 state EXCHANGE
Jan 15 14:50:58.106: %OSPFv3-2-IPv6_ADJ: Gi0/0: Exchange Done with 3.3.3.3
Jan 15 14:50:58.106: %OSPFv3-5-ADJCHG: Process 2, Nbr 3.3.3.3 on GigabitEthernet0/0 from LOADING to FULL, Loading Done

R2# show ipv6 ospf neighbor

Neighbor ID     Pri   State      Dead Time   Interface ID   Interface
1.1.1.1         0     FULL/-     00:00:38    6               Serial0/1/0
3.3.3.3         1     FULL/DR    00:00:37    3               GigabitEthernet0/0
```

与 OSPFv2 一样，正常工作的 OSPFv3 邻居最终会稳定在 full 状态或 2-way 状态。大多数邻居会达到 full 状态，这意味着它们直接相互完整地交换了 LSDB。然而，对于任何使用指定路由器（DR）的 OSPF 网络类型，只有与 DR 和备份 DR（BDR）的邻居关系才会达到 full 状态。既不是 DR 也不是 BDR 的路由器——即 DROther 路由器——之间的邻居关系将稳定在 2-way 状态。

### 排除 OSPFv3 邻居故障

每当看起来 OSPFv3 未能学习到它本应学习的路由时，请查看预期的 OSPFv3 邻居关系。然后，如果你发现某个关系不存在，或者存在但未达到预期状态（full 或 2-way），你可以关注邻居关系无法工作的各种原因。

> **注意** 与 OSPFv2 一样，处于 full 状态的邻居被称为*完全邻接*，而两个稳定在 2-way 状态的 DROther 邻居则仅被称为*邻接*。

排除 OSPF 邻居关系故障需要你记住许多可能导致两个路由器根本无法成为邻居的细节。幸运的是，OSPFv3 使用与 OSPFv2 相同的列表，但有一个显著的区别：OSPFv3 不要求邻居位于同一子网。表 23-2 列出了排除 OSPF 邻居关系故障时需要考虑的项目。



图13-21在一个工作示例中展示了所有具体的MLPPP命令。该示例基于图13-19和图13-20中的设计。请注意，出于节省空间的考虑，图13-21仅展示了两个串行接口中一个接口的配置，但在用于MLPPP时，所有串行接口都应具有相同的子命令。

首先，请关注图13-21中用白色高亮框标出并用箭头指向的六条配置命令。每台路由器上的 **interface multilink 1** 命令会在该路由器上创建多链路接口。网络工程师选择接口编号，但两台路由器上的编号必须相同，否则链路将无法工作。此外，多链路接口和物理串行接口都必须具有 **ppp multilink group 1** 命令，并且它们都必须再次引用同一个编号（本例中为1）。可以使用范围内的任意编号，但该编号必须与图中高亮的命令相匹配。

![](img/79473ea15699e01619d2aa789f5bd43b_405_0.png)

**图 13-21** *MLPPP 配置*

现在来看 **ip address** 命令。请注意，配置中显示在多链路接口上配置了IPv4地址，而串行接口上完全没有配置IPv4地址。简而言之，多链路接口具有第3层配置，而串行接口没有。因此，路由和路由协议逻辑将基于多链路接口工作。

最后，请注意多链路接口和串行接口都有两条附加命令：**encapsulation ppp**（用于启用PPP）和 **ppp multilink**（用于添加多链路支持）。

> **注意** 图13-21仅展示了一个串行接口，但多链路组中的每个串行接口都需要相同的配置。

该命令列出启用了EIGRP的接口，列出Mu1（Multilink 1），而不列出MLPPP捆绑中的两个串行接口中的任何一个。最后，请注意 **show ip interface brief** 命令确实列出了两个串行接口和多链路接口，但输出确认串行接口上未配置IP地址，正如IP-Address列下的“unassigned”文本所示。

每个多链路接口都像任何其他接口一样具有线路和协议状态；如果该状态为up/up，则IOS认为该多链路接口正在工作。默认情况下，该工作状态意味着MLPPP组中的至少一条物理链路也在工作——也就是说，部分物理链路可以发生故障，而多链路仍保持up。你始终可以使用本章前面讨论过的相同命令（**show controllers**、**show interfaces**）直接验证多链路组中的串行接口。此外，示例13-9中的两条命令可帮助深入了解MLPPP操作的具体细节。

### 示例 13-9 验证 MLPPP 组的运行细节

```text
R1# show interfaces multilink 1
Multilink1 is up, line protocol is up
  Hardware is multilink group interface
  Internet address is 192.168.5.1/24
  MTU 1500 bytes, BW 3088 Kbit/sec, DLY 20000 usec,
    reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation PPP, LCP Open, multilink Open
  Open: IPCP, CDPCP, loopback not set
  Keepalive set (10 sec)
! lines omitted for brevity

R1# show ppp multilink

Multilink1
  Bundle name: R2
  Remote Username: R2
  Remote Endpoint Discriminator: [1] R2
  Local Username: R1
  Local Endpoint Discriminator: [1] R1
  Bundle up for 16:50:33, total bandwidth 3088, load 1/255
  Receive buffer limit 24000 bytes, frag timeout 1000 ms
    0/0 fragments/bytes in reassembly list
    0 lost fragments, 96 reordered
    0/0 discarded fragments/bytes, 0 lost received
    0x654D7 received sequence, 0x654D5 sent sequence
  Member links: 2 active, 0 inactive (max 255, min not set)
    Se0/1/1, since 16:50:33
    Se0/0/0, since 16:23:16
No inactive multilink interfaces
```

首先，请注意 show interfaces multilink 1 命令列出了许多熟悉的细节，以及一些关于多链路的内容。特别地，输出显示了传统的线路和协议状态，两者均处于up状态，表示接口正在工作。在第六行，输出在关于PPP控制协议的部分提到了多链路工作状态为“Open”，确认MLPPP正在生效。

最后，`show ppp multilink` 命令的输出标识了每个多链路捆绑中配置的链路，以及哪些链路处于活动状态。在本例中，在R1上，接口S0/0/0和S0/1/1处于活动状态，如示例底部高亮所示。旁边的计时器显示这两个接口已活动了16小时多一点。在列表中看到这两个接口，不仅确认物理接口正在工作，还确认MLPPP配置将这两条链路都包含在多链路组1中。

## 串行链路故障排除

本最后一大节讨论如何隔离并找出与本章前面所涵盖主题相关问题的根本原因。此外，本节不会重复本书第II部分中的IP故障排除内容，但会指出当串行链路两端发生第3层子网不匹配时，串行链路上可能出现的一些症状；这种不匹配会阻止路由器通过该串行链路路由数据包。

简单的 `ping` 命令可以确定串行链路能否转发IP数据包。对其他路由器串行IP地址执行ping——例如，在图13-11中R1上成功执行 `ping 192.168.2.2` 命令，该图用于HDLC和PPP配置示例——可以证明该链路是否工作。

如果ping不通，问题可能与第1、2或3层的功能有关。隔离最可能原因所在层的最佳方法是检查表13-5中描述的接口状态代码。

表 13-5 ping不通时的接口状态代码及典型含义

| 线路状态 | 协议状态 | 可能的一般原因/层 |
| --- | --- | --- |
| Administratively down | Down | 接口关闭 |
| Down | Down | 第1层 |
| Up | Down | 第2层 |
| Up | Up | 第3层 |

串行链路验证和故障排除过程应从简单的三步流程开始：

- **步骤1.** 从一台路由器ping另一台路由器的串行IP地址。
- **步骤2.** 如果ping失败，请检查两台路由器上的接口状态，并调查与表13-5中列出的可能问题区域相关的问题。
- **步骤3.** 如果ping成功，还要验证任何路由协议是否正在通过该链路交换路由，如第11章“排查IPv4路由协议故障”所述。

> **注意** 可以使用 `show interfaces`、`show ip interface brief` 和 `show interfaces description` 命令找到接口状态代码。

本节其余部分将根据表13-5中列出的接口状态代码组合，探讨ping失败时需要检查的具体项目。

### 排查第1层问题

接口状态代码（即接口状态）在隔离串行链路问题根本原因方面起着关键作用。事实上，链路两端的状态可能不同，因此检查链路两端的状态以帮助确定问题非常重要。

例如，当两台路由器中只有一台使用 **shutdown** 接口子命令管理性地禁用其串行接口时，串行链路就会失败。当一台路由器关闭其串行接口时，另一台路由器会处于down/down状态（线路状态为down，线路协议状态为down），前提是第二台路由器的接口也没有被关闭。解决方案就是在该接口上配置 **no shutdown** 接口配置命令。

串行链路两端线路状态均为 *down* 的串行接口——也就是说，两端都处于down/down状态——通常指向某种第1层问题。图13-22总结了此状态最常见的原因。在图中，R2的串行接口完全没有问题；图的中间和左侧显示了常见的根本原因，这些原因随后导致R2的串行接口处于down/down状态。

![](img/79473ea15699e01619d2aa789f5bd43b_409_0.png)

*图 13-22* 导致路由器R2处于Down/Down状态的问题

### 排查第2层问题

串行链路上的数据链路层问题通常会导致至少一台路由器的串行接口状态为up/down。换句话说，线路状态（第一个状态代码）为up，而第二个状态（线路协议状态）为down。表13-6列出了其中一些类型的问题。

**表 13-6** 串行链路上数据链路问题的可能原因

| 线路状态 | 协议状态 | 可能原因 |
|---|---|---|
| Up | 两端均为Down¹ | 封装命令不匹配 |
| Up | 一端为Down，另一端为Up | 使用HDLC时，处于Up状态的一端禁用了Keepalive |
| Up | 两端均为Down | PAP/CHAP认证失败 |

¹ 在这种情况下，状态可能会在up/up、up/down、up/up等之间反复变化，同时路由器会不断尝试使封装正常工作。

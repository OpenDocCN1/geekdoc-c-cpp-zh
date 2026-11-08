
```
D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
E1 - OSPF external type 1, E2 - OSPF external type 2
i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
ia - IS-IS inter area, * - candidate default, U - per-user static route
o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
+ - replicated route, % - next hop override

Gateway of last resort is not set

R1#
! Lines omitted for brevity
```

请注意，就本书讨论的深度而言，使用默认的OSPF网络类型完全合理。然而，更复杂的拓扑可能要求使用不同的OSPF网络类型，甚至同一子网中的某些路由器需要采用不同设置。CCNP和CCIE R&S考试包含更多关于如何使用OSPF网络类型的细节。请注意，ICND2 200-105认证指南的附录I“实现帧中继”讨论了OSPF网络类型与帧中继结合使用的一种场景。

> **注意**
> “(OSPFv3)链路状态通告”标题下的内容最近一次发布是在2013年针对200-101考试，收录于《Cisco CCNA Routing and Switching ICND2 200-101 Official Cert Guide》第17章。

## (OSPFv3)链路状态通告

下一节将考察OSPFv3定义的、用于通告IPv6路由的OSPFv3 LSA。

### OSPFv3 LSDB与LSA

一旦OSPFv3路由器成为邻居，它们就会在该子网上交换LSDB。在大多数情况下，两台路由器直接交换各自的LSDB，完成后，每台路由器都会将其邻居列为已达到full状态。一旦进入full状态，两台路由器对于该区域应当具有相同的链路状态通告（LSA）。

本节简要介绍一个区域中的LSDB和LSA，它们看起来再次与OSPFv2所用的LSDB和LSA相似。然后本节将讨论一个罕见的配置问题：它会让两台路由器短暂地成为OSPFv3邻居，同时导致拓扑交换过程失败。

### 验证OSPFv3 LSA

OSPFv3使用类似的概念，但对于相当于OSPFv2的Type 1、2和3 LSA，命名略有不同。正如上一节“OSPFv2链路状态通告”所解释的，OSPFv2使用Type 1路由器LSA和Type 2网络LSA来定义区域内的拓扑。然后，Type 3汇总LSA为一个区域描述存在于其他区域的子网——也可以说是区域间子网。

对于本书中展示的OSPFv2配置选项，OSPFv2 LSDB中只需要这三种类型的LSA。

OSPFv3保留了同样的三个LSA概念，但重命名了汇总LSA。下面的列表总结了这三种关键的OSPFv3 LSA类型，以及OSPFv3路由器创建每种LSA的原因：

- 为区域中的每台路由器创建一个路由器LSA（Type 1 LSA）（包括连接到该区域的ABR）
- 为每个拥有DR且至少有一个DR邻居的网络创建一个网络LSA（Type 2 LSA）
- 为存在于不同区域的每个IPv6前缀（子网）创建一个区域间前缀LSA（Type 3 LSA）

例如，在本附录使用的示例网络中，区域4存在两台路由器：内部路由器R4和ABR R1。因此，区域4的LSDB将包含每台路由器对应的一个路由器LSA。该区域中存在一个将使用DR的网络（R1与R4之间的以太网WAN）。R1和R4也会成为邻居，因此将为该网络创建一个网络LSA。最后，ABR R1会知道区域4之外存在五个不同的IPv6前缀，因此ABR R1应当创建五个区域间前缀LSA并泛洪到区域4中。图K-12显示了区域4中这些LSA的概念模型。

![](img/79473ea15699e01619d2aa789f5bd43b_1169_0.png)

**图K-12** *区域4中应存在的Type 1、2和3 LSA*

除了这种基本LSA结构之外，与OSPFv2相比，OSPFv3确实对LSA做了若干更改。这些LSA内部的细节发生了变化，并且OSPFv3增加了若干OSPFv2中没有的新LSA类型。不过，这些细节超出了本书范围。

要在实际路由器中查看图K-12中的LSA，示例K-8列出了路由器R4中区域4 LSDB的开头部分。该示例突出显示了区域间前缀LSA的标题和IPv6前缀。请注意，输出确实显示了两条路由器LSA、一行表示单个网络LSA，以及五行包含区域间前缀的条目。

**示例K-8** *从R4查看区域4中的LSDB内容*

```
R4# show ipv6 ospf database

              OSPFv3 Router with ID (4.4.4.4) (Process ID 4)

                         Router Link States (Area 4)

ADV Router       Age        Seq#          Fragment ID  Link count  Bits
  1.1.1.1        258        0x80000072    0            1           B
  4.4.4.4        257        0x80000030    0            1           None

                         Net Link States (Area 4)

ADV Router       Age        Seq#          Link ID       Rtr count
  4.4.4.4        257        0x80000001    4             2

                    Inter Area Prefix Link States (Area 4)

ADV Router       Age        Seq#          Prefix
  1.1.1.1        878        0x80000069    2001:DB8:1:1::/64
  1.1.1.1        878        0x80000068    2001:DB8:1:2::/64
  1.1.1.1        364        0x8000000B    2001:DB8:1:13::/64
  1.1.1.1        364        0x8000000A    2001:DB8:1:23::/64
  1.1.1.1        364        0x8000000A    2001:DB8:1:12::/64
! Lines omitted for brevity
```

> **注意**
> “本书讨论的IPv6路由协议”标题下的内容此前未在本书中发布，但曾为《Cisco CCNA Routing and Switching ICND2 200-105 Official Cert Guide》的早期草稿撰写。

## 本书讨论的IPv6路由协议

本书只讨论OSPF的传统方法；也就是说，除了这个简短介绍之外，本书忽略OSPFv3地址族。在本书前面的章节中，你看到的所有针对IPv4的OSPF示例都是OSPFv2示例。本节展示OSPFv3示例，仅针对IPv6路由，并且具体是不使用地址族功能的OSPFv3。

EIGRP（在第24章讨论）在其IPv6支持历史中也经历了与OSPF类似的转变。Cisco将传统EIGRP风格称为EIGRP*经典*模式或EIGRP*自治系统*模式。EIGRP支持一种更新的模式，称为EIGRP*命名*模式；这种模式与OSPFv3的地址族模式一样，在配置中使用地址族。第24章讨论用于IPv6经典模式的EIGRP。

最后，路由信息协议（RIP）也支持IPv6，但其历史并没有那么紧密地对应。RIP有两个支持IPv4的版本，名称符合预期：RIP版本1（RIPv1）和RIP版本2（RIPv2）。为了支持IPv6，一个工作组创建了RIP的新版本，称为*RIP下一代*（RIPng），其名称参考了*星际迷航*电视剧。（没错。）（Cisco今天常将这一协议称为用于IPv6的RIP。）迄今为止，IOS中的RIPng支持尚未经历类似的转变以包含地址族。

表K-4总结了这些协议的名称，以便复习和学习。本书讨论更经典的配置选项，不详细讨论地址族配置。

**表K-4** 内部路由协议的版本术语汇总

|  | RIP | OSPF | EIGRP |
|---|---|---|---|
| 用于通告IPv6路由的协议名称 | RIP下一代（RIPng） | OSPF版本3（OSPFv3） | 用于IPv6的EIGRP |
| 传统配置风格的名称 | N/A | N/A | EIGRP经典模式 |
| 使用地址族的新配置风格名称 | N/A | OSPFv3地址族 | EIGRP命名模式 |

## 考试主题交叉参考

本附录列出了与ICND2 200-105考试和CCNA 200-125考试相关的考试主题。Cisco在Cisco.com上列出了考试主题。尽管考试主题很少变更，你仍应始终查看这些考试主题以了解任何更新；请访问http://www.cisco.com/go/certifications，并导航到正确的考试页面。

Cisco按领域组织每个考试主题列表，领域是主要主题领域。Cisco说明了每个领域在考试中应占的百分比，因此你可以了解各领域的重要性。传统上，参加考试后收到的成绩报告会显示你在每个领域的百分比得分。

本附录包含三种不同类型的考试主题交叉参考：

- **按数字顺序排列的ICND2 200-105考试主题：** 本节按Cisco网站上列出的相同顺序列出ICND2 200-105考试主题，并指出每个考试主题所对应的本书章节。本质上，本节为每个考试主题提供交叉参考，指向至少包含该考试主题部分材料的章节。
- **本书章节与ICND2 200-105考试主题的映射：** 本节列出相同的ICND2 200-105考试主题，但按章节而非考试主题索引。本节作为本书各章与各章所涵盖考试主题之间的交叉参考。本节基本上将每章第一页出现的考试主题列表以精简形式集中在一处，便于参考和跟踪。
- **CCNA 200-125考试主题顺序：** 本附录的最后一节列出CCNA 200-125考试领域和主题。它通过突出显示与ICND2 200-105考试主题重叠的CCNA 200-125考试主题，起到交叉参考的作用。

### 按数字顺序排列的ICND2 200-105考试主题

ICND2 200-105考试包含五个主要主题领域（域），每个领域都列出了百分比。表L-1列出了这些领域及其百分比。

**表L-1** ICND2 200-105考试主题领域

| 领域 | 百分比 |
|---|---:|
| 领域1：LAN交换技术 | 26% |
| 领域2：路由技术 | 29% |
| 领域3：WAN技术 | 16% |
| 领域4：基础设施服务 | 14% |
| 领域5：基础设施维护 | 15% |

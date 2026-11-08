
命令中的第一个参数会与本地路由器上的每个接口 IP 地址进行匹配，试图找到匹配项。然而，路由器不是将 network 命令中的整个数字与接口上的整个 IPv4 地址进行比较，而是可以根据通配符掩码比较八位组的一个子集，如下所示：

### 关键主题

- **通配符 0.0.0.0：** 比较全部 4 个八位组。换句话说，数字必须完全匹配。
- **通配符 0.0.0.255：** 仅比较前 3 个八位组。比较数字时忽略最后一个八位组。
- **通配符 0.0.255.255：** 仅比较前 2 个八位组。比较数字时忽略最后 2 个八位组。
- **通配符 0.255.255.255：** 仅比较第一个八位组。比较数字时忽略最后 3 个八位组。
- **通配符 255.255.255.255：** 不比较任何内容——此通配符掩码表示所有地址都将与 network 命令匹配。

基本上，八位组中通配符掩码值为 0 会告诉 IOS 进行比较以查看数字是否匹配，而值为 255 则告诉 IOS 在比较数字时忽略该八位组。

由于通配符掩码，network 命令提供了许多灵活的选项。例如，在路由器 R3 中，可以使用许多 network 命令，其中一些匹配所有接口，另一些匹配接口子集。表 8-2 展示了一些选项示例及说明。

### 表 8-2 — R3 上 OSPF network 命令示例及预期结果

| 命令 | 命令中的逻辑 | 匹配的接口 |
|---|---|---|
| network 10.1.0.0 0.0.255.255 | 匹配以 10.1 开头的接口 IP 地址 | G0/0.341<br>G0/0.342<br>S0/0/0 |
| network 10.0.0.0 0.255.255.255 | 匹配以 10 开头的接口 IP 地址 | G0/0.341<br>G0/0.342<br>S0/0/0 |
| network 0.0.0.0 255.255.255.255 | 匹配所有接口 IP 地址 | G0/0.341<br>G0/0.342<br>S0/0/0 |
| network 10.1.13.0 0.0.0.255 | 匹配以 10.1.13 开头的接口 IP 地址 | S0/0/0 |
| network 10.1.3.1 0.0.0.0 | 匹配一个 IP 地址：10.1.3.1 | G0/0.341 |

通配符掩码为本地路由器提供了匹配其自身接口的规则。例如，示例 8-2 显示 R3 使用 network 10.0.0.0 0.255.255.255 area 0 命令。然而，通配符掩码允许许多不同的有效 OSPF 配置。例如，在同一个互联网络中，路由器 R1 和 R2 可以使用示例 8-3 所示的配置，并使用另外两个通配符掩码。在两台路由器上，OSPF 都在图 8-2 所示的所有接口上启用。

```text
10.1.1.1      0    FULL/ -    00:00:33   10.1.1.13    Serial0/0/0
10.1.24.4     1    FULL/DR    00:00:35   10.1.3.130   GigabitEthernet0/0.342
10.1.24.4     1    FULL/DR    00:00:36   10.1.3.4     GigabitEthernet0/0.341
```

输出中的详细信息提到了几个重要事实；对大多数人来说，在这种情况下从右向左阅读效果最好。例如，查看各标题：

- **接口：** 这是本地路由器连接到邻居的接口。例如，列表中的第一个邻居可通过 R3 的 S0/0/0 接口到达。
- **地址：** 这是该链路上邻居的 IP 地址。同样，对于第一个邻居，即 R1，该邻居使用的 IP 地址为 10.1.13.1。
- **状态：** 虽然存在许多可能的状态，但就本章讨论的细节而言，在这种情况下 FULL 是正确且完全正常工作的状态。
- **邻居 ID：** 这是邻居的路由器 ID。

接下来，示例 8-5 显示了路由器 R3 上 LSDB 的内容。有趣的是，当 OSPF 在采用单区域设计的互联网络中正常工作时，所有路由器将具有相同的 LSDB 内容。因此，无论在四台路由器中的哪一台上发出示例 8-5 中的 **show ip ospf database** 命令，都应列出完全相同的信息。

### 示例 8-5 图 8-2 中路由器 R3 上的 OSPF 数据库

```text
R3# show ip ospf database

            OSPF Router with ID (10.1.13.3) (Process ID 1)

                Router Link States (Area 0)

Link ID         ADV Router      Age        Seq#            Checksum Link count
10.1.1.1        1.1.1.1         498        0x80000006      0x002294 6
2.2.2.2         2.2.2.2         497        0x80000004      0x00EBC6 5
10.1.13.3       10.1.13.3       450        0x80000003      0x001043 4
10.1.24.4       10.1.24.4       451        0x80000003      0x09D7E 4

                Net Link States (Area 0)

Link ID         ADV Router      Age        Seq#            Checksum
10.1.3.4        10.1.24.4       451        0x80000001      0x0045FB
10.1.3.130      10.1.24.4       451        0x80000001      0x00546B
```

就本书而言，不必关注此命令输出中的具体细节。不过，为便于理解，请注意 LSDB 应为同一区域中的每台路由器列出一条“Router Link State”（Type 1 Router LSA）。在此设计中，四台路由器都在同一区域中，因此列出了四条突出显示的 Type 1 LSA。

接下来，示例 8-6 使用 **show ip route** 命令显示 R3 的 IPv4 路由表。请注意，它列出了直连路由以及 OSPF 路由。花点时间回顾图 8-2，找出未本地连接到 R3 的子网。然后在示例 8-6 的输出中查找这些路由。

**show ip ospf interface** 命令会列出一行，指出该接口为被动接口。

示例 8-11 显示了路由器 R1 上的这两个命令，其配置如示例 8-10 顶部所示。请注意，子接口 G0/0.11 和 G0/0.12 都出现在 **show ip ospf interface brief** 的输出中。

### 示例 8-11 显示被动接口

```text
R1# show ip ospf interface brief
Interface   PID   Area            IP Address/Mask    Cost  State Nbrs F/C
Gi0/0/12    1     0               10.1.1.129/25      1     DR    0/0
Gi0/0/11    1     0               10.1.1.1/25        1     DR    0/0
Se0/0/0     1     0               10.1.1.121/25      64    P2P   0/0
Se0/0/1     1     0               10.1.1.121/25      64    P2P   0/0

R1# show ip ospf interface g0/0.11
GigabitEthernet0/0.11 is up, line protocol is up
  Internet Address 10.1.1.1/25, Area 0, Attached via Network Statement
  Process ID 1, Router ID 10.1.1.129, Network Type BROADCAST, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1       no          no            Base
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router (ID) 10.1.1.129, Interface address 10.1.1.1
  No backup designated router on this network
  Timer intervals configured, Hello 10, Dead 40, Wait 40, Retransmit 5
    oob-resync timeout 40
    No Hello (Passive interface)
  ! Lines omitted for brevity
```

## 实现多区域 OSPFv2

在多区域设计中配置路由器几乎与为单区域配置 OSPFv2 一样。唯一的区别是，配置会将每台 ABR 上的一些接口放置在不同区域中。差异体现在 OSPFv2 的验证和运行中。

本章的第二个主要部分提供第二组配置，以对比多区域配置与单区域配置。这个新场景展示了基于图 8-3 和图 8-4 的多区域 OSPF 设计中各路由器的配置。图 8-3 显示了互联网络拓扑和子网 ID，图 8-4 显示了区域设计。请注意，图 8-3 在每个接口附近列出了每台路由器 IPv4 地址的最后一个八位组，而不是完整的 IPv4 地址，以减少杂乱。

花点时间思考图 8-4 所示的区域设计，并找出 ABR。只有 R1 才连接到骨干区域。其他三台路由器都是单个区域中的内部路由器。因此，事实证明，四台路由器中有三台采用单区域配置，所有接口都在同一区域中。

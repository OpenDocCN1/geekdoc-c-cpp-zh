

### HSRP 故障转移

每台路由器上的 HSRP 都需要完成一些工作，才能使网络按图 20-5 所示的方式运行。两台路由器都需要进行 HSRP 配置，其中包括虚拟 IP 地址。两台路由器会互相发送 HSRP 消息，以协商并决定当前哪台路由器应处于活动状态、哪台应处于备用状态。然后，两台路由器会继续互相发送消息，以便备用路由器知道活动路由器何时发生故障，从而能够接管成为新的活动路由器。

图 20-6 显示了图 20-5 中的 HSRP 活动路由器 R1 发生故障时的结果。R1 停止使用虚拟 IP 和 MAC 地址，而新的活动路由器 R2 开始使用这些地址。主机完全不需要更改其默认路由器设置，流量现在会流向 R2，而不是 R1。

![](img/79473ea15699e01619d2aa789f5bd43b_607_0.png)

| IP | MAC |
|---|---|
| 10.1.1.1 | VMAC1 |

**图 20-6** *R2（新的活动路由器）接管发生故障的 R1 后发送的数据包*

当故障转移发生时，确实会发生一些变化，但这些变化都不会发生在主机上。主机会保留相同的默认路由器设置，即设置为虚拟 IP 地址（本例中为 10.1.1.1）。主机的 ARP 表也不必更改，因为 HSRP 虚拟 MAC 会被列为虚拟路由器的 MAC 地址。

当故障转移发生时，路由器和 LAN 交换机上都会发生变化。显然，新的活动路由器必须准备好使用虚拟 IP 和 MAC 地址接收数据包（封装在帧内）。然而，前几幅图中未显示的 LAN 交换机此前会将发往 VMAC1 的帧发送给路由器 R1。现在，交换机必须知道要将这些帧发送给新的活动路由器 R2。

为了让交换机更改 VMAC1 的 MAC 地址表条目，R2 会发送一个以太网帧，并将 VMAC1 作为源 MAC 地址。交换机会像平常一样学习源 MAC 地址（VMAC1），但会将其关联到指向 R2 的新端口。该帧同时也是 LAN 广播，因此所有交换机都会学习到一条指向 R2 的 VMAC1 MAC 表条目。（顺便说明，这个以太网帧承载的是一条 ARP 应答消息，称为免费 ARP，因为路由器是在没有先收到 ARP 请求的情况下发送它的。）

### HSRP 负载均衡

HSRP 的活动/备用模型意味着，在一个子网中，所有主机都只通过一台路由器发送其发往子网外的数据包。换句话说，路由器不会分担工作负载，而是一台路由器处理所有数据包。例如，回到图 20-5，R1 是活动路由器，因此该子网中的所有主机都通过 R1 发送数据包，而该子网中没有任何主机通过 R2 发送数据包。

HSRP 确实支持负载均衡，方式是让不同子网优先选择不同的路由器作为活动路由器。大多数需要第二台路由器提供冗余的站点，其规模也足够大，可以在站点中使用多个 VLAN 和子网。两台路由器很可能会连接到所有 VLAN，并在每个 VLAN 中充当默认路由器。然后，可以将 HSRP 配置为在一个 VLAN 中优先选择一台路由器作为活动路由器，而在另一个 VLAN 中优先选择另一台路由器作为活动路由器，从而平衡流量。或者，你也可以在同一子网中配置多个 HSRP 实例（称为多个 HSRP 组），优先让一台路由器在一个组中作为活动路由器，而让另一台路由器在另一个组中优先作为活动路由器。

例如，图 20-7 显示了一个重新设计的 LAN，现在 VLAN 1 中有两台主机，VLAN 2 中有两台主机。R1 和 R2 都连接到该 LAN，并且都使用 VLAN 中继和单臂路由（ROAS）配置。两台路由器都在两个子网中使用 HSRP，互相支持。不过，R1 被有意配置为在 VLAN 1 中赢得协商并成为 HSRP 活动路由器，而 R2 被配置为在 VLAN 2 中获胜。

![](img/79473ea15699e01619d2aa789f5bd43b_608_0.png)

**图 20-7** *通过在每个子网中使用不同的活动路由器实现 HSRP 负载均衡*

请注意，通过让每台路由器在某些子网中充当 HSRP 活动路由器，该设计同时利用了这两台路由器和两条 WAN 链路。

任何充当默认路由器的设备都需要 FHRP，这当然包括传统路由器和三层交换机。HSRP 可以在配置了 IP 地址的接口上，在路由器和三层交换机上进行配置。不过，在大多数情况下，HSRP 用于连接到那些拥有需要默认路由器的主机的子网的接口。这些接口包括路由器物理接口、路由器中继子接口和三层交换虚拟接口（SVI）。

> **注意** 本章在提到使用 HSRP 的路由器时，展示的是物理接口上的示例，只是为了不必反复同时提及路由器和三层交换机以及各种接口。本章中关于 FHRP 和 HSRP 的所有概念，具体都适用于路由器物理接口、中继子接口和 SVI。

## 实施 HSRP

本章的第二个主要部分将展示 HSRP 基本功能的配置，并配合相应的 show 命令。本部分的目标是展示每个工具的足够操作细节，以强化第一部分讨论的概念。

### 配置和验证基本 HSRP

HSRP 配置只需要在希望使用 HSRP 分担默认路由器职责的两台（或更多）路由器上执行一条命令：**standby group ip virtual-ip** 接口子命令。第一个值定义 HSRP 组号，该组号在两台路由器上必须匹配。组号使一台路由器能够同时在同一接口上支持多个 HSRP 组，并使路由器能够基于组来识别彼此。该命令还会配置同一组中路由器共享的虚拟 IP 地址；虚拟 IP 地址是 VLAN 中的主机用作默认网关的地址。

示例 20-1 展示了一个配置示例，与图 20-5 和图 20-6 相关的 HSRP 示例相匹配。两台路由器都使用组 1，虚拟 IP 地址为 10.1.1.1，并配置 **standby 1 ip 10.1.1.1** 接口子命令。

**示例 20-1** *R1 和 R2 上共享 IP 地址 10.1.1.1 的 HSRP 配置*

```
R1# show running-config
! Lines omitted for brevity

interface GigabitEthernet0/0
 ip address 10.1.1.9 255.255.255.0
 standby version 2
 standby 1 ip 10.1.1.1
 standby 1 priority 110
 standby 1 name HSRP-group-for-book

! The following configuration on R2 is identical except for the HSRP priority and
! the interface IP address
R2# show running-config
! Lines omitted for brevity

interface GigabitEthernet0/0
 ip address 10.1.1.129 255.255.255.0
 standby version 2
 standby 1 ip 10.1.1.1
 standby 1 name HSRP-group-for-book
```

该配置还展示了其他可选参数。例如，R1 在该组中的优先级为 110，而 R2 默认为 100。在 HSRP 中，如果两台路由器同时启动，优先级更高的路由器会赢得选举并成为活动路由器。配置还展示了可以分配给该组的名称（在使用 **show** 命令时显示），以及选择使用 HSRP 版本 2 的设置。（本章将在后续内容中更详细地介绍这些设置。）

配置完成后，两台路由器会协商 HSRP 设置，并选择当前哪台路由器将成为活动路由器、哪台将成为备用路由器。按照所示的配置，R1 将因其更高（更好）的优先级而赢得选举并成为活动路由器。两台路由器会得出相同结论，示例 20-2 中 R1 和 R2 上 **show standby brief** 命令的输出证实了这一点。

**示例 20-2** *使用 show standby brief 查看 R1 和 R2 上的 HSRP 状态*

```
First, the group status as seen from R1
R1# show standby brief

                         P indicates configured to preempt.
                         |
Interface   Grp  Pri P  State    Active        Standby       Virtual IP
Gi0/0         1  110 P  Active   local         10.1.1.129     10.1.1.1

The output here on R2 shows that R2 agrees with R1.
R2# show standby brief

                         P indicates configured to preempt.
                         |
Interface   Grp  Pri P  State    Active        Standby       Virtual IP
Gi0/0         1  100 P  Standby  10.1.1.9      local          10.1.1.1
```

show standby brief 命令的输出中包含大量细节，因此请花些时间仔细查看突出显示的字段。首先，查看每条命令的 Grp 列。该列列出 HSRP 组号，因此在查看多台路由器的输出时，需要查看具有相同组号的行，以确保数据与那个 HSRP 组相关。在本例中，两台路由器都只有一个组号（1），因此很容易找到相关信息。

输出的每一行都列出了本地路由器对该组 HSRP 状态的看法。具体来说，根据各列标题，show standby brief 命令会标识以下内容：

![](img/79473ea15699e01619d2aa789f5bd43b_610_0.png)

- **Interface：** 本地路由器上配置该 HSRP 组的接口
- **Grp：** HSRP 组号
- **Pri：** 本地路由器的 HSRP 优先级
- **State：** 本地路由器当前的 HSRP 状态
- **Active：** 当前活动 HSRP 路由器的接口 IP 地址（如果本地路由器是 HSRP 活动路由器，则显示为“local”）
- **Standby：** 当前备用 HSRP 路由器的接口 IP 地址（如果本地路由器是 HSRP 备用路由器，则显示为“local”）
- **Virtual IP：** 该路由器为此组定义的虚拟 IP 地址

例如，按照示例 20-2 中突出显示的文本，R2 认为其自身当前状态为备用，接口地址为 10.1.1.9 的路由器处于活动状态（这种情况


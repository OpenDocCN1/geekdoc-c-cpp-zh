
本章将局域网路由选项分为四类：

- 使用路由器，为每个 VLAN 分别用一个路由器 LAN 接口和线缆连接到交换机（通常不使用）
- 使用路由器，通过 VLAN 中继连接到局域网交换机（称为单臂路由，或 ROAS）
- 使用带交换虚拟接口（SVI）的三层交换机
- 使用带路由接口的三层交换机（这些接口可能是也可能不是三层以太通道）

在所列选项中，第一种方案可行，但要实际使用则需要太多接口。这里提到它只是为了使列表完整。

至于另外三种选项，本章将依次讨论每一种，并分别作为本章三个主要部分之一的核心内容。如今每个特性都在真实网络中使用，选择使用哪一种取决于网络特定部分的设计和需求。图 19-1 展示了这些选项可能被使用的情形。

![](img/79473ea15699e01619d2aa789f5bd43b_578_0.png)

**图 19-1** *中心站点的三层交换*

图 19-1 展示了一个经典情形：右侧分支机构使用带 VLAN 中继的路由器，左侧中心站点使用三层交换机两种选项中的任一种。图中左侧显示一个中心站点园区 LAN，包含 12 个 VLAN。在中心站点，其中两台交换机充当三层交换机，结合了路由器和交换机的功能，在所有 12 个子网/VLAN 之间进行路由。这些三层交换机可以使用 SVI、路由接口或两者兼用来配置路由。此外，拥有 WAN 路由器和交换机的站点（如图右侧的远程分支站点）可能会使用 ROAS，以利用路由器通过 802.1Q 中继进行路由的能力。

注意，图 19-1 仅展示一个示例。工程师可以在每个站点使用三层交换，或在每个站点使用带 VLAN 中继的路由器。

“我是否已经掌握？”测验的答案：
1 A，2 B，3 C，4 C，5 D，6 A，7 B、C。

![](img/79473ea15699e01619d2aa789f5bd43b_581_0.png)

用于支持该子网的一些配置。为本征 VLAN 定义路由器接口的两种选项是

- 在物理接口上配置 **ip address** 命令，但不配置 **encapsulation** 命令；路由器会认为该物理接口使用本征 VLAN。
- 在子接口上配置 **ip address** 命令，并使用 **encapsulation dot1q vlan-id native** 子命令，告诉路由器 VLAN ID 以及它是本征 VLAN 这一事实。

例 19-2 展示了两种本征 VLAN 配置选项，它们是在例 19-1 的相同配置基础上做了一处小改动。在此情况下，VLAN 10 成为本征 VLAN。示例的上半部分展示了将路由器物理接口配置为使用本征 VLAN 10 的选项。示例的下半部分展示了如何在子接口上配置同一个本征 VLAN。在两种情况下，交换机配置也需要更改，使 VLAN 10 成为本征 VLAN。

**例 19-2** *在路由器 B1 上使用本征 VLAN 10 的路由器配置*

```text
! First option: put the native VLAN IP address on the physical interface
interface gigabitethernet 0/0
 ip address 10.1.10.1 255.255.255.0
!
interface gigabitethernet 0/0.20
 encapsulation dot1q 20
 ip address 10.1.20.1 255.255.255.0

! Second option: like Example 19-1, but add the native keyword
interface gigabitethernet 0/0.10
 encapsulation dot1q 10 native
 ip address 10.1.10.1 255.255.255.0
!
interface gigabitethernet 0/0.20
 encapsulation dot1q 20
 ip address 10.1.20.1 255.255.255.0
```

## 验证 ROAS

除了使用 **show running-config** 命令外，路由器上的 ROAS 配置最好通过两个命令来验证：**show ip route [connected]** 和 **show vlans**。与任何路由器接口一样，只要接口处于 up/up 状态并配置了 IPv4 地址，IOS 就会在 IPv4 路由表中放入一条直连（和本地）路由。因此，第一个明显的检查就是查看所有预期的直连路由是否存在。例 19-3 列出了根据例 19-1 所示配置得到的直连路由。

**例 19-3** *基于例 19-1 配置的直连路由*

```text
B1# show ip route connected
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
! Legend omitted for brevity

      10.0.0.0/8 is variably subnetted, 4 subnets, 2 masks
C    10.1.10.0/24 is directly connected, GigabitEthernet0/0.10
L    10.1.10.1/32 is directly connected, GigabitEthernet0/0.10
C    10.1.20.0/24 is directly connected, GigabitEthernet0/0.20
L    10.1.20.1/32 is directly connected, GigabitEthernet0/0.20
```

至于接口和子接口状态，请注意 ROAS 子接口状态在一定程度上取决于物理接口状态。具体来说，子接口状态不能优于对应物理接口的状态。例如，在目前示例中的路由器 B1 上，物理接口 G0/0 处于 up/up 状态，子接口也处于 up/up 状态。但如果你从该端口拔掉线缆，物理端口会变为 down/down 状态，子接口也会变为 down/down 状态。例 19-4 展示了另一个例子：物理接口被关闭，子接口因此自动变为管理性关闭（administratively down）状态。

**例 19-4** *子接口状态与物理接口状态关联*

```text
R1# configure terminal
Enter configuration commands, one per line. End with CNTL/Z.

R1(config)# interface g0/0
R1(config-if)# shutdown
R1(config-if)# ^z
R1# show ip interface brief | include 0/0
GigabitEthernet0/0       unassigned      YES manual administratively down down
GigabitEthernet0/0.10    10.1.10.1       YES manual administratively down down
GigabitEthernet0/0.20    10.1.20.1       YES manual administratively down down
```

此外，还可以在子接口配置模式下使用 **no shutdown** 和 **shutdown** 命令，独立于物理接口启用和禁用子接口状态。

另一个有用的 ROAS 验证命令 `show vlans` 会说明哪些路由器中继接口使用哪些 VLAN、哪个 VLAN 是本征 VLAN，以及一些数据包统计信息。数据包计数器在增长这一事实在验证流量是否发生时很有用。例 19-5 展示了一个示例，基于例 19-2（下半部分）中的路由器 B1 配置，其中本征 VLAN 10 配置在子接口 G0/0.10 上。注意，输出中标识了与物理接口关联的 VLAN 1、与 G0/0.10 关联的作为本征 VLAN 的 VLAN 10，以及与 G0/0.20 关联的 VLAN 20。它还列出了分配给每个接口/子接口的 IP 地址。

**例 19-5** *与示例路由器中继配置匹配的 show vlans 命令示例*

```text
R1# show vlans

Virtual LAN ID: 1 (IEEE 802.1Q Encapsulation)

VLAN Trunk Interface:  GigabitEthernet0/0

Protocols Configured:   Address:          Received:       Transmitted:
        Other                                  0               83
69 packets, 20914 bytes input
147 packets, 11841 bytes output

Virtual LAN ID: 10 (IEEE 802.1Q Encapsulation)

   VLAN Trunk Interface:    GigabitEthernet0/0.10

This is configured as native VLAN for the following interface(s) :
GigabitEthernet0/0        Native-vlan Tx-type: Untagged

   Protocols Configured:   Address:              Received:       Transmitted:
            IP             10.1.10.1                    2               3
         Other                                          0               1

   3 packets, 722 bytes input
   4 packets, 264 bytes output

Virtual LAN ID: 20 (IEEE 802.1Q Encapsulation)

   VLAN Trunk Interface:    GigabitEthernet0/0.20

   Protocols Configured:   Address:              Received:       Transmitted:
            IP             10.1.20.1                    0             134
         Other                                          0               1

   0 packets, 0 bytes input
 135 packets, 10498 bytes output
```

## ROAS 故障排除

排除 ROAS 故障时最大的挑战在于：如果你只错误配置了路由器，或只错误配置了交换机，中继上的另一台设备无法知道对端配置错误。也就是说，如果你在路由器上检查 `show ip route` 和 `show vlans` 命令，输出看起来符合预期配置，且正确子接口的直连路由也出现了，路由仍可能因所连接交换机上的问题而失败。因此，ROAS 故障排除通常从检查路由器和交换机两端的配置开始，因为任一设备都没有状态输出能告诉你问题可能出在哪里。

首先，要在路由器上检查 ROAS，你需要从预期配置入手，并针对配置提出以下问题：

![](img/79473ea15699e01619d2aa789f5bd43b_583_0.png)

- 1. 路由器上是否在子接口上使用封装 `dot1q vlan-id` 命令配置了每个非本征 VLAN？
- 2. 这些相同的 VLAN 是否存在于相邻交换机的中继上（`show interfaces trunk`），并且位于允许列表中、未被 VTP 修剪、未被 STP 阻塞？


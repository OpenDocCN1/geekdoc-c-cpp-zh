

- **平衡混合（balanced hybrid）** 多年来一直用于指代 EIGRP 路由协议背后的逻辑的术语。如今更常将此逻辑称为高级距离矢量逻辑。
- **带宽（bandwidth）** 比特在链路上发送和接收的速度。
- **带宽配置文件（bandwidth profile）** 在城域以太网中，对客户可以发送到服务中以及从服务中接收的流量量的合同定义。包括一个称为承诺信息速率（CIR）的概念，它定义了服务提供商将随服务交付的最小带宽（比特/秒）。
- **最佳路径选择（best path selection）** BGP 通过按顺序比较不同 BGP 路径属性列表来选择最佳路由的过程。
- **BGP 邻居（BGP neighbor）** BGP 对等体的另一种说法。指路由器与之建立 BGP 邻居或对等关系的另一台路由器。
- **BGP 对等体（BGP peer）** BGP 邻居的另一种说法。指路由器与之建立 BGP 邻居或对等关系的另一台路由器。
- **BGP 表（BGP table）** 每台路由器中由 BGP 进程维护的表，其中保存 BGP 已知的前缀和路径属性。
- **BGP 更新（BGP update）** 列出 BGP 路径属性和前缀的 BGP 消息。
- **BGP 更新源（BGP update source）** 在路由器上运行 BGP 时，用于与另一台路由器建立 BGP 对等关系的 TCP 连接所使用的接口 IP 地址。
- **阻塞状态（blocking state）** 在 802.1D STP 中，一种端口状态，在此状态下不处理任何接收到的帧，交换机也不从该接口转发任何帧，但 STP 消息除外。
- **启动字段（boot field）** Cisco 路由器配置寄存器中的低 4 位。启动字段中的值部分地告诉路由器到哪里查找要加载的 Cisco IOS 映像。
- **边界网关协议（Border Gateway Protocol, BGP）** 一种外部路由协议，如今用作互联网中交换路由的主要路由协议。
- **BPDU** 桥接协议数据单元。生成树协议消息的通用名称。
- **BPDU 保护（BPDU Guard）** 一种 Cisco 交换机特性，用于侦听传入的 STP BPDU 消息，如果收到任何此类消息则禁用接口。其目标是在交换机连接到预期仅连接主机的端口时防止环路。
- **桥 ID（bridge ID, BID）** 用于 STP 和 RSTP 的桥和交换机的 8 字节标识符。它由一个 2 字节优先级字段和一个通常填充 MAC 地址的 6 字节系统 ID 字段组成。
- **桥接协议数据单元（bridge protocol data unit）** 参见 BPDU。
- **广播地址（broadcast address）** 通常指代表所有设备的任何地址，可用于向所有设备发送一条消息。在以太网中，MAC 地址为全 1，即十六进制的 FFFF.FFFF.FFFF。对于 IPv4，参见子网广播地址。
- **广播域（broadcast domain）** 接收该集合中任何设备发出的广播帧的所有设备的集合。同一 VLAN 中的设备处于同一广播域中。
- **广播子网（broadcast subnet）** 在对 A 类、B 类或 C 类网络进行子网划分时，每个有类网络中所有子网位均为二进制 1 的那个子网。该子网的子网广播地址在数值上与有类网络的网络范围广播地址相同。

## C

- **有线电视互联网（cable internet）** 一种互联网接入技术，使用通常用于视频的有线电视（CATV）电缆来发送和接收数据。
- **运营商以太网（carrier Ethernet）** 根据 MEF 文档，这是以前称为城域以太网的术语，通常指任何使用以太网链路作为客户与服务提供商之间接入链路的 WAN 服务。
- **中心局（central office, CO）** 电信公司使用的术语，指容纳交换设备的建筑，电信公司的电缆设施接入该建筑，以便电信公司能够从每个家庭和企业铺设电缆到该建筑中。
- **集中式控制平面（centralized control plane）** 一种架构网络协议和产品的方法，将控制平面功能集中到一个集中式功能中，而不是将功能分布到网络设备上。
- **通道组（Channel-group）** Cisco 交换机用来指代一组链路的术语，这些链路在某些方面被视为单一链路。其他类似术语包括 EtherChannel 和 PortChannel。
- **CHAP** 质询握手认证协议。PPP 定义的一种安全特性，允许链路上的任一端点或两个端点将另一端设备认证为特定的授权设备。
- **机箱聚合（chassis aggregation）** 一种 Cisco 技术，用于将两台分布层或核心层交换机组合成一台交换机，在两台交换机上共享数据平面功能（称为*主动/主动*），并将控制平面功能集中在一台交换机上（称为*主动/备用*）。
- **CIDR** 无类域间路由。用于全球 IP 地址范围分配的 RFC 标准工具。CIDR 减小了互联网路由器 IP 路由表的大小，有助于应对互联网的快速增长。术语*无类*指的是汇总的地址组表示一组不符合 IPv4 有类（A 类、B 类和 C 类）分组规则的地址。
- **CIDR 记法（CIDR notation）** 参见前缀记法。
- **电路交换（circuit switching）** 一种交换系统，在“呼叫”期间，发送方和接收方之间必须存在专用的物理电路路径。在电话公司网络中被大量使用。
- **Cisco 访问控制服务器（Cisco Access Control Server, ACS）** 充当 AAA 服务器的 Cisco 产品。
- **Cisco AnyConnect 安全移动客户端（Cisco AnyConnect Secure Mobility Client）** Cisco 软件产品，用作创建设备 VPN 的用户设备上的客户端软件。通常称为 Cisco VPN 客户端。
- **Cisco 快速转发（Cisco Express Forwarding, CEF）** 一个长期的 Cisco IOS 内部特性，通过创建搜索效率更高的转发信息库（FIB）来优化转发过程，该 FIB 替代 IP 路由表使用，同时使用一张邻接表来缓存用于到达下一跳地址的新数据链路层头部。
- **Cisco Intercloud Fabric** Cisco 软件，提供多种功能，帮助公司连接到不同的云服务，并协助管理不同的公共云服务及在它们之间进行迁移。
- **Cisco Open SDN 控制器（Cisco Open SDN Controller, OSC）** Cisco 基于 OpenDaylight 控制器的商业 SDN 控制器。
- **Cisco Prime** 利用 SNMP 的图形用户界面（GUI）软件，可用于管理 Cisco 网络设备。术语 *Cisco Prime* 是一个“伞形”术语，涵盖许多不同的单独软件产品。
- **Cisco VPN 客户端（Cisco VPN client）** 参见 Cisco AnyConnect 安全移动客户端。
- **服务类别（Class of Service, CoS）** 802.1Q 头部中 3 位字段的非正式术语，用于标记和分类以太网帧以便应用 QoS 操作。优先级代码点（PCP）的另一种说法。
- **类别选择器（Class Selector, CS）** 八个 DSCP 值的名称，这些值均以二进制 000 结尾，目的是获得八个可识别的 DSCP 值，其前 3 位与旧 IP 优先级字段使用的八个值匹配。最初用于与 IP 优先级向后兼容，但如今这些值通常仅用作更多可用于报文标记的值。
- **有类寻址（classful addressing）** IPv4 寻址中的一个概念，将子网划分的 IP 地址定义为三部分：网络、子网和主机。
- **有类网络（classful network）** IPv4 A 类、B 类或 C 类网络。之所以称为有类网络，是因为这些网络由 IPv4 寻址的类别规则定义。
- **有类路由协议（classful routing protocol）** 路由协议的固有特性。具体而言，该路由协议不在其路由更新中发送子网掩码。这要求协议对有类网络做出假设，并使其无法支持 VLSM 和手工路由汇总。
- **分类（classification）** 检查网络消息中各个字段以识别哪些消息属于某些预定组（类别）的过程。
- **无类寻址（classless addressing）** IPv4 寻址中的一个概念，将子网划分的 IP 地址定义为两部分：前缀（或子网）和主机。
- **无类域间路由（classless interdomain routing, CIDR）** 参见 CIDR。
- **无类路由（classless routing）** IPv4 转发（路由）过程的一种变体，定义了默认路由使用方式的细节。默认路由始终用于目的 IP 地址不匹配任何其他路由的报文。
- **无类路由协议（classless routing protocol）** 路由协议的固有特性。具体而言，该路由协议在其路由更新中发送子网掩码，从而无需对特定子网或网络中的地址做出任何假设。这允许协议支持 VLSM 和手工路由汇总。
- **客户端 VPN（client VPN）** 一种 VPN，其中一个端点是用户设备，如电话、平板电脑或 PC。
- **时钟速率（clock rate）** 串行链路在传输介质上编码比特的速度。


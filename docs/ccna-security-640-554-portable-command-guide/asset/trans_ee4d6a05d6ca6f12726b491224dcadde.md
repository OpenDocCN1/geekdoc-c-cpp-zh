

| 命令 | 描述 |
|---|---|
| `S3(config-if)#switchport port-security violation shutdown` | 如果发生违规，则将端口置于错误禁用状态并生成消息。 |
| `S3(config-if)#switchport port-security mac-address aaaa.aaaa.aaaa` | 手动配置 IP 电话的 MAC 地址。 |
| `S3(config-if)#switchport port-security mac-address bbbb.bbbb.bbbb` | 手动配置主机的 MAC 地址。 |
| `S3(config)#errdisable recovery cause psecure-violation` | 启用错误禁用端口的动态错误恢复功能。 |
| `S3(config)#errdisable recovery interval 900` | 将默认等待时间从 300 秒更改为 900 秒。 |

> **注意：** 使用全局配置命令 `mac address-table notification` 配置 MAC 地址通知，以生成 MAC 地址学习和老化消息。

> **注意：** 虽然本示例中只使用了单个端口，但端口安全通常应在所有面向用户的端口上启用。

## 生成树协议攻击

冗余的第 2 层拓扑消除了单点故障，但更容易受到广播风暴、拓扑抖动和 MAC 地址表不稳定性问题的影响。

生成树协议（STP）是一种第 2 层协议，通过将某些端口置于阻塞状态来提供无环路的冗余网络拓扑。黑客可能通过更改网络拓扑来操纵 STP 进行攻击（例如，连接一个 rogue 交换机，试图接管成为根桥，并使即时交换域的所有流量都通过该交换机传输）。

> **注意：** 配置 STP 增强功能 PortFast、BPDU 防护和根防护，以缓解 STP 操纵攻击。

## STP 增强功能

| 功能 | 描述 |
|---|---|
| **PortFast** | ▪ 该功能最大限度地减少了接入端口等待生成树收敛的时间。<br>▪ 第 2 层接入端口立即从阻塞状态转换到转发状态，绕过监听和学习状态。<br>▪ 应在面向用户的接入端口上启用。 |
| **BPDU 防护** | ▪ 该功能保护交换网络免受在面向用户的端口上接收网桥协议数据单元（BPDU）所导致的潜在问题。<br>▪ 如果收到 BPDU，端口将转换为错误禁用模式并阻止所有流量。<br>▪ 端口必须手动重置，因此对无效配置提供了安全的响应。<br>▪ 应在面向用户的接入端口上启用，以防止 rogue 交换机的安装。 |
| **根防护** | ▪ 该功能强制根桥的放置位置，并限制可协商出根桥的交换机端口。<br>▪ 如果收到的 BPDU 通告的网桥 ID 低于当前网桥，端口将转换为根不一致状态（阻塞）。<br>▪ 一旦有问题的 BPDU 停止，端口将恢复。<br>▪ 应配置在面向用户的端口以及连接到交换机（但不应该是根桥）的交换机端口上。 |

> **注意：** 另一个 STP 增强功能是 BPDU 过滤功能，它会停止在端口上发送和接收 BPDU。但是，如果已启用 BPDU 防护，则不应配置此功能。

> **注意：** BPDU 防护和根防护类似，但其影响不同。BPDU 防护会禁用端口，并且必须手动启用。根防护会禁用端口，但一旦有问题的设备停止发送更优的 BPDU，端口就会恢复。

## 配置 STP 增强功能

您可以在全局或单个接入端口上启用 PortFast：

| 命令 | 描述 |
|---|---|
| `Switch(config)#spanning-tree portfast default` | 在所有端口上全局启用 PortFast 功能。<br><br>**注意：** 您必须在连接到交换机的交换端口上显式禁用 PortFast，因为它们可能会造成第 2 层环路。 |
| `Switch(config-if)#spanning-tree portfast` | 在指定端口上启用 PortFast。 |

> **注意：** 使用 `show running-config [interface interface-id]` 命令验证 PortFast 是否已启用。

您可以在全局或单个接入端口上启用 BPDU 防护：

| 命令 | 描述 |
|---|---|
| `Switch(config)#spanning-tree portfast bpduguard default` | 在所有启用 PortFast 的端口上全局启用 BPDU 防护。 |
| `Switch(config-if)#spanning-tree bpduguard enable` | 在指定端口上启用 BPDU 防护。 |

> **注意：** 使用 `show spanning-tree summary` 和 `show spanning-tree summary totals` 命令显示 STP 状态信息。

您可以在接入端口或连接到另一台交换机（但绝不应成为根桥）的交换机端口上启用根防护。

| 命令 | 描述 |
|---|---|
| `Switch(config-if)#spanning-tree guard root` | 在指定端口上启用根防护。 |

> **注意：** 要验证，请使用 `show spanning-tree inconsistentports` 命令。

您还可以配置交换机在指定时间后自动恢复 BPDU 防护错误禁用的端口：

| 命令 | 描述 |
|---|---|
| `Switch(config)#errdisable recovery cause bpduguard` | 启用计时器以从 BPDU 防护错误禁用状态中恢复。 |

> **注意：** 使用 `show errdisable recovery` 命令显示错误禁用恢复计时器信息。

## 配置 STP 增强功能示例

图 8-2 显示了配置 STP 增强功能示例的拓扑。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_130_0.png)

图 8-2 — 配置 STP 增强功能示例的网络拓扑

```
switch(config)#storm-control
{[broadcast | multicast | unicast]
[level {level | level-low} | bps bps
[bps-low] | pps pps [pps-low]] |
[action {shutdown | trap}]}
```

在第 2 层端口和 EtherChannel 上启用风暴控制，以监控接收流量的速率。可以监控广播、组播和单播流量。

`level {level | level-low}` 指定上升和下降抑制级别，以端口总带宽的百分比（保留两位小数）表示。

`level bps {bps [bps-low]}` 以每秒位数指定上升和下降级别。

`level pps {pps [pps-low]}` 以每秒数据包数指定上升和下降级别。

可以采取的操作包括

- **shutdown：** 在风暴期间禁用端口
- **trap：** 在风暴期间发送 SNMP 陷阱

> **注意：** 默认情况下，交换机接口上的单播、广播和组播风暴控制处于禁用状态；也就是说，抑制级别为 100%。

## 配置风暴控制示例

此示例演示如何在端口上将广播地址风暴控制级别设置为 25%。当广播流量超过总可用带宽的 25% 时，交换机会丢弃所有广播流量，直到流量风暴控制间隔结束：

```
S1(config-if)#storm-control broadcast level 25
```

在第 2 层接口上启用风暴控制，以监控接收流量的速率。

## VLAN 跳转攻击

### 欺骗 DTP 消息

攻击者发送欺骗的动态中继协议（DTP）消息，试图与交换机建立中继链路。如果成功，攻击者可以发送带有目标 VLAN 标记的流量，并让交换机将数据包传送到目的地。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_134_0.png)

- 在所有中继链路上：
  - 启用中继。
  - 禁用 DTP。
  - 使用唯一的本征 VLAN。
- 在所有未使用的端口上：
  - 禁用中继。
  - 将所有未使用的端口分配到专用 VLAN。
  - 禁用该端口。
- 在接入端口上：
  - 禁用中继。

图 8-3 缓解 VLAN 攻击示例的网络拓扑

| 命令 | 描述 |
| :--- | :--- |
| `S3(config)#interface range Fa0/1 - 2` | 配置两个中继端口 Fa0/1 和 Fa0/2。 |
| `S3(config-if-range)#switchport mode trunk` | 显式启用中继。 |
| `S3(config-if-range)#switchport nonegotiate` | 禁用 DTP。 |
| `S3(config-if-range)#switchport trunk native vlan 88` | 将本征 VLAN 分配给 VLAN 88。VLAN 88 不用于任何其他流量。 |
| `S3(config-if-range)#interface Fa0/3` | 切换到接口 Fa0/3。 |
| `S3(config-if)#switchport mode access` | 禁用中继。 |
| `S3(config)#interface range Fa0/4 - 24` | 配置所有其他未使用的端口。 |
| `S3(config-if-range)#switchport mode access` | 禁用所有未使用端口上的中继。 |
| `S3(config-if-range)#shutdown` | 禁用所有未使用的端口。 |

## 高级第 2 层安全功能

其他交换机安全功能包括：

- 访问控制列表（ACL）和私有 VLAN
- Cisco 集成安全功能
- 安全管理平面安全功能

> **注意：** 这些功能的配置超出了本书的范围。


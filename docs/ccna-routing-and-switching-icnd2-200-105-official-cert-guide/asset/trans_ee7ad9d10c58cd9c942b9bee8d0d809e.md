

![](img/79473ea15699e01619d2aa789f5bd43b_1156_0.png)

| 角色 | 路由器 | 地址 |
|---|---|---|
| AVG | R1 | 10.1.1.1 |
| 转发器 | R1 | VMAC1 |
| 转发器 | R2 | VMAC2 |

**图 K-3** *GLBP 通过发送带有 R1 的 VMAC1 的 ARP 应答来引导主机 A*

该图从上到下显示三条消息，具体操作如下：

- 1. 主机 A 的 ARP 表中没有其默认路由器 10.1.1.1 的表项，因此主机 A 发送 ARP 请求来获取 10.1.1.1 的 MAC 地址。
- 2. 本例中的 GLBP AVG（即 R1）会返回 ARP 应答。AVG 选择在 ARP 应答中包含自己的虚拟 MAC 地址 VMAC1。
- 3. 主机 A 后续发送的 IP 数据包会被封装在以太网帧中，目的地址为 VMAC1，因此这些数据包会到达 R1。

从现在起，由于主机 A 的 ARP 表中存有默认网关（10.1.1.1）的表项，主机 A 将子网外的数据包发送给 R1。主机 A 的 ARP 表中 10.1.1.1 的表项现在指向 R1 上的 MAC 地址（VMAC1），因此主机 A 发送到子网外的数据包都会经由 R1 转发。

为了平衡负载，AVG 会使用交替路由器的 MAC 地址来应答每个新的 ARP 请求。图 K-4 继续展示这种负载均衡效果，此时来自主机 B 的 ARP 请求的目标是 10.1.1.1。充当 AVG 的路由器（R1）仍然发送 ARP 应答，但这次使用的是 R2 的虚拟 MAC（VMAC2）。

![](img/79473ea15699e01619d2aa789f5bd43b_1156_1.png)

| 角色 | 路由器 | 地址 |
|---|---|---|
| AVG | R1 | 10.1.1.1 |
| 转发器 | R1 | VMAC1 |
| 转发器 | R2 | VMAC2 |

**图 K-4** *GLBP 通过发送带有 R2 的 VMAC2 的 ARP 应答来引导主机 B*

- 1. 主机 B 发送 ARP 请求以获取 10.1.1.1 的 MAC 地址。
- 2. GLBP AVG（R1）返回 ARP 应答，其中列出 R2 的虚拟 MAC 地址 VMAC2。
- 3. 对于后续发送到子网外的数据包，主机 B 会将数据包封装在以太网帧中，目的地址为 VMAC2，因此这些数据包会到达 R2。

图 K-3 和图 K-4 所示的过程按主机平衡流量，但各路由器还必须做好在另一台路由器发生故障时接管其工作的准备。GLBP 将每台路由器称为一个*转发器*。一切正常时，每台路由器都充当自己的转发器，负责处理自己的虚拟 MAC 地址，同时监听 GLBP 消息以确保其他转发器仍在工作。如果某个转发器发生故障，仍在正常工作的转发器将接管故障转发器的虚拟 MAC 地址角色，并继续转发流量。

### 配置和验证 GLBP

GLBP 的配置在很大程度上与 HSRP 配置类似。

示例 K-1 展示了一个 GLBP 配置，两台路由器均使用 GLBP 组 1，虚拟 IP 地址为 10.1.1.1，使用 **glbp 1 ip 10.1.1.1** 接口子命令。

**示例 K-1** *R1 和 R2 上共享 IP 地址 10.1.1.1 的 GLBP 配置*

```text
! First, the configuration on R1
R1# show running-config
! Lines omitted for brevity
interface GigabitEthernet0/0
 ip address 10.1.1.9 255.255.255.0
 glbp 1 ip 10.1.1.1
 glbp 1 priority 110
 glbp 1 name GLBP-group-for-book

! The following configuration, on R2, is identical except for
! the interface IP address, and the GLBP priority
R2# show running-config
! Lines omitted for brevity
interface GigabitEthernet0/0
 ip address 10.1.1.129 255.255.255.0
 glbp 1 ip 10.1.1.1
 glbp 1 name GLBP-group-for-book
```

配置完成后，两台路由器会协商决定哪一台担任 AVG。与 HSRP 一样，如果两台路由器同时启动，R1 将获胜，因为 **glbp 1 priority 110** 命令将其优先级设置为 110，而 R2 的默认优先级为 100。但是，如果其中一台路由器先于另一台启动，则该路由器会直接承担 AVG 角色。

仔细查看 GLBP 的 show 命令输出比 HSRP 要费事一些，尤其是因为 GLBP 的工作方式包含更多细节。首先，请看路由器 R1 上的 **show glbp brief** 命令，如示例 K-2 所示。（请注意，许多 **show glbp** 命令与对应的 HSRP **show standby** 命令有相同的选项。）

**示例 K-2** *使用 show glbp brief 查看 R1 上的 GLBP 状态*

| 接口 | 组 | 转发器 | 优先级 | 状态 | 地址 | 活动路由器 | 备用路由器 |
|---|---:|---:|---:|---|---|---|---|
| Gi0/0 | 1 | - | 110 | Active | 10.1.1.1 | local | 10.1.1.129 |
| Gi0/0 | 1 | 1 | - | Listen | 0007.b400.0101 | 10.1.1.129 | - |
| Gi0/0 | 1 | 2 | - | Active | 0007.b400.0102 | local | - |

在查看输出的右侧之前，先稍微考虑一下上下文。此示例列出标题行和三行数据。这些数据行以 Grp 和 Fwd 标题标识，分别是 Group 和 Forwarder 的缩写。由于只配置了一个 GLBP 组，R1 只列出组 1 的行。更重要的是，每一行都定义了 GLBP 不同工作部件的详细信息，如下所示：

- **Fwd 为 -：** 该行不指任何转发器，而是描述 AVG。
- **Fwd 为 1：** 该行描述 GLBP 转发器（路由器）1。
- **Fwd 为 2：** 该行描述 GLBP 转发器（路由器）2。

输出通常先列出关于 AVG 的行，这一点由转发器列中的破折号表示。现在来看示例 K-2 右侧突出显示的部分。这一行列出了虚拟 IP 地址，并标识了活动 AVG 和备用 AVG。这条来自路由器 R1 的特定命令将 R1 本身（“local”）列为活动路由器。因此，R1 就是当前的 AVG。

接下来的两行分别列出其中一个转发器角色的状态信息；也就是说，路由器使用一个虚拟 MAC 地址，接收发送到该地址的帧，并对这些帧中封装的数据包进行路由。为此，地址列列出 MAC 地址，具体来说是 GLBP 使用的虚拟 MAC 地址，而不是接口 MAC 地址。

每个转发器行还在“活动路由器”列中标识当前使用所列虚拟 MAC 的路由器。在示例 K-2 中，0007.b400.0101 由接口 IP 地址为 10.1.1.129（恰为 R2）的路由器使用。0007.b400.0102 由本地路由器（即执行 show 命令的路由器）支持，即 R1。

**show glbp brief** 命令的简略输出列出了许多细节，但需要花些功夫才能学会如何筛选。为了更全面地了解输出，示例 K-3 列出了同样的 show glbp brief 命令，这次是在 R2 上。请注意，Fwd 列再次将输出的第一行标识为关于 AVG 的行，接下来的两行是关于两个转发器的行。

**示例 K-3** *使用 show glbp brief 查看 R2 上的 GLBP 状态*

| 接口 | 组 | 转发器 | 优先级 | 状态 | 地址 | 活动路由器 | 备用路由器 |
|---|---:|---:|---:|---|---|---|---|
| Gi0/0 | 1 | - | 100 | Standby | 10.1.1.1 | 10.1.1.9 | local |
| Gi0/0 | 1 | 1 | - | Active | 0007.b400.0101 | local | - |
| Gi0/0 | 1 | 2 | - | Listen | 0007.b400.0102 | 10.1.1.9 | - |

```text
State is Listen
    2 state changes, last state change 00:20:34
MAC address is 0007.b400.0101 (learnt)
Owner ID is 0200.0202.0202
Redirection enabled, 598.272 sec remaining (maximum 600 sec)
Time to live: 14398.272 sec (maximum 14400 sec)
Preemption enabled, min delay 30 sec
Active is 10.1.1.129 (primary), weighting 100 (expires in 8.352 sec)
Client selection count: 1
Forwarder 2
    State is Active
    1 state change, last state change 00:24:25
MAC address is 0007.b400.0102 (default)
Owner ID is 0200.0101.0101
Redirection enabled
Preemption enabled, min delay 30 sec
Active is local, weighting 100
Client selection count: 1
```

> **注意** 标题“HSRP 跟踪”下的内容最近一次发布于 2013 年的 200-101 考试中，出自《*Cisco CCNA Routing and Switching ICND2 200-101 Official Cert Guide*》的附录 B。

## HSRP 跟踪

第 20 章展示了如何配置 HSRP 优先级，以便在 HSRP 组中优先选择某台路由器作为活动路由器。例如，第 20 章中的示例 20-1 展示了同一 HSRP 组中的两台路由器，R1 使用略好（数值较高）的优先级 110，R2 使用默认优先级 100，因此当两台路由器都启动并正常工作时，R1 成为活动路由器。图 K-5 展示了一个类似的设计，其中路由器 R1 为活动（优先级 110），R2 为备用（优先级 100），使用 HSRP 虚拟 IP 地址 10.1.1.1。

![](img/79473ea15699e01619d2aa789f5bd43b_1160_0.png)

**图 K-5** *受益于 HSRP 跟踪的设计*


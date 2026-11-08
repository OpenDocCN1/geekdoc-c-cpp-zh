
![](img/0d9540c65a85f4cb1c32cee46038d8ab_262_0.png)

**图17-15** VPN故障排除窗口

**提示：** 单击“详细信息”可查看详细结果。

当提示启用调试时，单击“是”。

这将打开另一个VPN故障排除窗口，如图17-16所示。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_263_0.png)

**图17-16** VPN故障排除窗口

在目标网络上输入IP地址，然后单击**继续**。

最终，CCP会报告VPN状态。如果成功，将出现一条消息，指示VPN隧道已建立。否则，将出现错误消息。请按需要进行故障排除。

**提示：** 如果生成错误，请比较每个对等体的运行配置。

## 使用CCP监控已建立的IPsec VPN连接

通过使用图17-17中所示的VPN状态选项，CCP监控得以简化。

选择**监控 > 安全 > VPN状态**。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_264_0.png)

**图17-17** VPN状态屏幕

此窗口显示路由器上可能存在的VPN连接树，包括所有类型的VPN（远程访问、站点到站点等）。

**注意：** 站点到站点隧道显示为IPsec隧道。

该组显示路由器上配置的每个IPsec VPN的统计信息。表格中的每一行代表一个IPsec VPN。此窗口展示“监控隧道”和“测试隧道”选项，这些选项对故障排除过程至关重要。

**提示：** 您必须单击“更新”以刷新IPsec隧道表并显示路由器中的最新数据。

| 型号 | 描述 |
|---|---|
| ASA 5550 | 园区、企业边缘和数据中心解决方案，最大提供1-Gbps吞吐量 |
| ASA 5585 | 大型企业和数据中心解决方案，最大提供40-Gbps吞吐量 |

**注意：** 对于Cisco ASA 5505，默认DRAM内存为256 MB（可升级至512 MB），默认内部闪存为128 MB。

**注意：** 本节重点介绍ASA 5505。

## 路由和透明防火墙模式

ASA设备支持两种防火墙运行模式：

| 模式 | 描述 |
|---|---|
| **路由模式** | • 部署防火墙的传统模式。<br>• 两个或多个接口，用于分隔第3层网络。<br>• ASA是网络中的路由器跃点，可以在相连网络之间执行网络地址转换（NAT）。<br>• 路由模式支持多个接口，每个接口位于不同子网，并且需要该子网上的IP地址。 |
| **透明模式** | • ASA的功能类似于第2层设备。<br>• 也称为*在线设备*或*隐身防火墙*。<br>• ASA只需要在全局配置模式下配置一个管理IP地址。<br>• 透明模式不支持动态路由协议、VPN、服务质量（QoS）或动态主机配置协议（DHCP）中继。 |

**注意：** 本节重点介绍路由模式。

## ASA许可证

ASA 5505安全设备预装了Base许可证或Security Plus许可证，后者支持更高的连接容量、完整的非军事区（DMZ）功能、VLAN中继和高可用性特性。

您可以使用`show activation-key`或`show version`命令验证许可证信息：

```
ciscoasa# show version

<Output omitted>

Licensed features for this platform:

Maximum Physical Interfaces       : 8          perpetual
VLANs                             : 3          DMZ Restricted
Dual ISPs                         : 3          Disabled      perpetual
VLAN Trunk Ports                  : 0          perpetual
Inside Hosts                      : 10         perpetual
Failover                          : Disabled   perpetual
VPN-DES                           : Enabled    perpetual
VPN-3DES-AES                     : Enabled    perpetual
AnyConnect Premium Peers          : 2          perpetual
AnyConnect Essentials             : Disabled   perpetual
Other VPN Peers                   : 2          perpetual
Total VPN Peers                   : 25         perpetual
Shared License                    : Disabled   perpetual
AnyConnect for Mobile             : Disabled   perpetual
AnyConnect for Cisco VPN Phone    : Disabled   perpetual
Advanced Endpoint Assessment      : Disabled   perpetual
UC Phone Proxy Sessions           : 2          perpetual
Total UC Proxy Sessions           : 2          perpetual
Botnet Traffic Filter             : Disabled   perpetual
Intercompany Media Engine         : Disabled   perpetual

This platform has a Base license.

Serial Number: TMX15364077
Running Permanent Activation Key: 0x970bc671 0x305cf569 0x70d21158
0x6ec2c9 0x8a003afb
Configuration register is 0x41 (will be 0x1 at next reload)
Configuration last modified by enable_15 at 10:03:12.749 UTC Fri Sep 23
2011
ciscoasa#
```

**注意：** 可以购买其他可选许可证（例如AnyConnect Premium许可证）或基于时间的许可证（例如Botnet Traffic Filter许可证）。

**注意：** 预装许可证与附加许可证组合构成永久许可证，需要使用activation-key命令进行激活。产品激活密钥可从Cisco客户代表处购买。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_271_0.png)

**图18-2** ASA 5505后面板

图18-2中ASA 5505后面板的功能编号如下：

| 编号 | 功能 | 描述 |
|---|---|---|
| 1 | **电源连接器** | 需要48 VDC适配器。 |
| 2 | **SSC插槽** | 可以使用Cisco高级检测与防御安全服务卡（AIP-SSC）添加IPS功能。 |
| 3 | **控制台端口** | 用于设备的初始配置。 |
| 4 | **防盗锁槽** | 用于物理固定设备。 |
| 5 | **重置按钮** | 重置按钮默认禁用。 |
| 6 | **USB端口** | 共三个USB端口可用于启用附加服务与功能（背面两个，正面一个）。 |
| 7–8 | **八端口快速以太网交换机** | 每个端口可分组创建最多三个独立VLAN（或区域），以支持网络分段和安全。端口6和7是以太网供电（PoE）端口。 |

## ASA 5510前面板和后面板

ASA 5510支持300-Mbps吞吐量和每秒9,000个防火墙连接容量，非常适合大多数办公需求。Cisco ASA 5510、5520、5540和5550均为一机架单元（1RU）。每个设备都有一个用于安全服务模块（SSM）的扩展插槽。ASA 5510前面板具有电源、状态、活动、VPN和闪存LED指示灯。图18-3中突出显示了ASA 5510的前面板和后面板。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_272_0.png)

**图18-3** ASA 5510前面板和后面板

图18-3中ASA 5510后面板的功能编号如下：

| 编号 | 功能 | 描述 |
|---|---|---|
| 1 | **SSM** | SSM可用于添加以下模块：<br>• 4端口千兆以太网安全服务模块（4GE SSM）<br>• 高级检测与防御安全服务模块（AIP-SSM）<br>• 系列内容安全与控制安全服务模块（CSC-SSM） |
| 2 | **USB端口** | 两个USB端口可用于启用附加服务与功能。 |
| 3 | **OOB管理接口** | 专用的快速以太网带外（OOB）管理接口。 |
| 4 | **四个快速以太网接口** | 默认情况下，Fa0/0至Fa0/2接口已启用，但Fa0/3已禁用。<br><br>OOB接口也可用作第五个快速以太网端口（必须受ASA软件支持）。 |
| 5 | **闪存卡插槽** | 为系统映像和配置文件提供存储空间。 |
| 6 | **LED指示灯** | 电源、状态、活动、VPN和闪存LED指示灯。 |
| 7 | **管理端口** | 用于初始配置的控制台端口。<br><br>辅助端口可用于OOB管理。 |

## ASA安全级别

ASA安全的基础是将接口分配给安全级别，以区分内部（可信）网络和外部（不可信）网络：

- 安全级别定义了接口的可信程度。
- 级别越高，接口越受信任。


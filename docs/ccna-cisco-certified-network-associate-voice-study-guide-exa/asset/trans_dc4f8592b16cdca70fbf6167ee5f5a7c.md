
**图 10-1**

Cisco 3550 交换机（由 Cisco Systems, Inc. 提供。未经授权不得使用。）

![](img/ee67e6cd30f16bc39d653f87870eabb5_303_0.png)

为在 VoIP 网络中使用而配置交换机所需的常见任务包括：

- 为语音和数据配置 VLAN
- 为语音接入配置交换机端口
- 在适当的交换机端口上启用 CDP 协议
- 配置 QoS 设置

**图 10-2**

Cisco 2950 交换机（由 Cisco Systems, Inc. 提供。未经授权不得使用。）

![](img/ee67e6cd30f16bc39d653f87870eabb5_303_1.png)

以下命令表示 Cisco 2950 交换机上的典型操作：

```text
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#interface fastethernet 0/4
Switch(config-if)#switchport mode access
Switch(config-if)#

             cdp                 Global CDP configuration subcommands
             channel-group       EtherChannel/port bundling configuration
             channel-protocol    Select the channel protocol (LACP, PAgP)
             description         Interface specific description
             duplex              Configure duplex operation.
             exit                Exit from interface configuration mode
             mac-address         Manually set interface MAC address
             mls                 Mls interface command
             no                  Negate a command or set its defaults
             shutdown            Shutdown the selected interface
             spanning-tree       Spanning Tree Subsystem
             speed               Configure speed operation.
             storm-control      Storm configuration
             switchport          Set switching mode characteristics
             tx-ring-limit       Configure PA level transmit ring limit
Switch(config-if)#cdp enable
Switch(config-if)#mls ?
 qos  qos command keyword
Switch(config-if)#mls qos trust ?
 cos       cos keyword
 device    trusted device class
 dscp      dscp keyword
 <cr>
Switch(config-if)#mls qos trust device cisco-phone
Switch(config-if)#exit
```

## 路由器

用于 VoIP 服务的 Cisco 路由器也称为集成服务路由器（ISR）。多年来，Cisco 推出了多个路由器系列。较旧的 Cisco 设备，包括 1700 系列、2600 系列和 3600 系列路由器，仍可用于实施和测试 VoIP 实验。较新的 800、1800、2800 和 3800 系列路由器也可用于语音服务。800 系列实际上仅适用于在网络中路由语音数据包，因为无法在路由器本身上管理语音服务。1800 到 3800 系列路由器可执行 VoIP 操作。图 10-3 展示了 Cisco 2851 路由器，配有 IP 电话和用于 Cisco Unity Express 部署的 AIM-CUE 卡。

![](img/ee67e6cd30f16bc39d653f87870eabb5_305_0.png)

### 工作现场

> 我最喜欢的 Cisco 路由器之一是 2801 ISR。这款路由器几乎可用于现代 Cisco 考试所需的任何学习。通过这款入门级 2800 系列设备，您可以实施安全功能、语音功能、Security Device Manager、Call Manager Express 以及更多功能。它具有四个扩展槽、对板载 PVDM 模块的支持、基于 CompactFlash 的存储器（用于 IOS 存储）以及两个内置快速以太网端口。

Cisco 路由器在 VoIP 网络中执行的常见任务包括：

- 充当 VoIP 网关
- 充当 H.323 网守
- 执行 IP 路由
- 实施模拟和数字端口

Cisco 路由器上的常见配置任务包括：

- 安装 Call Manager Express（CME）软件
- 通过 CLI 或 Web 界面配置 CME
- 配置外部交换站（FXS）和外部交换局（FXO）端口
- 配置 T1 和 E1 端口
- 配置基本 IP 接口

## Cisco IP 电话

路由器和交换机就位后，您就可以开始连接 Cisco IP 电话。Cisco IP 电话有两种基本版本：硬件版和软件版。基于硬件的 IP 电话看起来就像我们组织中已使用数十年的传统 PBX 电话。基于软件的 IP 电话在 PC 上运行，并模拟基于硬件的 IP 电话的功能。

Cisco 提供的基于软件的电话现在称为 Cisco IP Communicator，以表明它不仅仅是一部电话。图 10-4 展示了在 Windows 机器上运行的 Cisco IP Communicator 软件的界面。您可以看到，它看起来很像传统电话。

![](img/ee67e6cd30f16bc39d653f87870eabb5_306_0.png)

根据 Cisco IP Communicator 2.1 版的 Cisco 数据表，提供以下设计功能：

- **八个线路键**——这些键提供电话线路和对电话功能的直接访问。
- **五个软键**——这些键动态为您提供呼叫功能选项。
- **消息**——此键提供对语音邮件消息的直接访问。
- **目录**——Cisco IP Communicator 识别传入消息并在屏幕上对其进行分类，使您能够使用直接回拨功能快速有效地回电。公司目录与轻量级目录访问协议第 3 版（LDAP3）标准目录集成。
- **设置**——此键允许您从大量铃声和背景图像中进行选择。
- **服务**——Cisco IP Communicator 允许您快速访问各种信息，例如天气、股票、每日名言或任何其他基于 Web 的信息。该电话使用 XML 提供通向不断增长的功能和信息世界的门户。
- **帮助**——联机帮助功能为您提供有关电话按键、按钮和功能的信息。

除设计功能外，还支持以下呼叫功能：

- 多条线路或目录号码
- 可配置快速拨号
- 主叫姓名和号码显示
- 呼叫等待
- 呼叫前转
- 呼叫转移
- 三方通话（会议）
- 呼叫驻留
- 呼叫代接
- 重拨
- 呼叫保持
- 强插
- 回叫
- 分机移动性

由于 Cisco IP Communicator 在 Windows PC 上运行，考虑硬件要求很重要。对于 Windows 2000 和 Windows XP，Cisco 指定以下要求：

- Microsoft Windows 2000 Professional（Service Pack 4）或 Windows XP Professional（Service Pack 2）
- Pentium P4 1.0 GHz 或同等处理器（建议 Pentium P4 1.5 GHz 或更高）
- 1 GB RAM
- 100 MB 可用磁盘空间
- 非 ISA 全双工声卡（集成或基于 PCI）或 USB 声音设备
- 800×600×16 位屏幕分辨率（建议 1024×768×16 位或更好）
- 128 kbps 网络连接

对于 Windows Vista 或 Windows 7，必须满足以下要求：

- 性能分数为 3 或更高
- 200 MB 可用磁盘空间
- 1 GB RAM
- 非 ISA 全双工声卡（集成或基于 PCI）或 USB 声音设备
- 10/100 Mbps 以太网网络接口卡
- SVGA 视频卡
- 800×600×16 位屏幕分辨率（建议 1024×768×16 位或更好）

**图 10-5**

Cisco 基于硬件的 IP 电话

（由 Cisco Systems, Inc. 提供。未经授权不得使用。）

![](img/ee67e6cd30f16bc39d653f87870eabb5_309_0.png)

基于硬件的 IP 电话相比基于 PC 的 IP 电话具有多项优势。首先，它们不在 PC 上运行，因此不会占用其他计算操作的资源。其次，基于硬件的 IP 电话具有传统听筒，可以像家庭 PSTN 电话一样使用。第三，基于硬件的 IP 电话的界面对用户来说非常熟悉，因为从拨号、接听和基本操作的角度来看，它的工作方式与他们习惯的传统电话完全相同。图 10-5 展示了几部 Cisco 基于硬件的 IP 电话。另请注意 UC500 系列一体化路由器/交换机/语音网关，以及显示在所示显示器上运行的 Cisco Configuration Assistant（CCA）应用程序。

## 认证目标 10.01

### 640-460：使用 Cisco Configuration Assistant 实施 UC500

UC500 系列设备面向 SOHO 市场。它们附带实施有线网络、无线网络和 VoIP 网络所需的大多数端口、软件和其他组件。在本节中，您将了解 UC500 系列的功能和型号，然后探索可用的配置选项。

### UC500 简介

统一通信（UC）500 系列是智能商业通信系统（SBCS）解决方案的一部分。UC500 系列面向小型企业、分支机构和家庭办公室，并提供多种不同版本。有关 SBCS 解决方案的详细信息，请访问 http://www.cisco.com/go/sbcs。


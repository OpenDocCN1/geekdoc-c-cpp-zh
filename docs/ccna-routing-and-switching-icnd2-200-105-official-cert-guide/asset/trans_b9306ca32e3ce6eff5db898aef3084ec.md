

## 第 28 章

- **1.** A. *数据平面*包括所有网络设备与接收、处理和转发每条消息相关的操作，如问题中描述的情况。*表平面*一词不用于网络领域。*管理平面*和*控制平面*不涉及针对每条消息的转发操作。
- **2.** C. *控制平面*包括所有网络设备创建在消息处理时数据平面所使用的信息的操作。控制平面包括诸如 IP 路由协议和生成树协议（STP）等功能。
    
    *表平面*一词不用于网络领域。*管理平面*和*数据平面*不涉及收集数据平面随后使用的信息。
- **3.** C. 尽管 SDN 架构存在多种变体，但它们通常使用集中式控制器。该控制器可以将部分甚至全部控制平面功能集中到控制器中。然而，接收消息、基于报文头字段进行匹配、采取行动（如做出转发决策）以及转发消息等数据平面功能仍然发生在网络设备（交换机）上，而不是在控制器上。
    
    对于不正确的选项，控制平面功能可以全部发生在控制器上，或者部分发生在控制器上，部分在交换机上。北向接口和南向接口是控制器上的 API 接口，而不是交换机上的。
- **4.** A. Cisco Open SDN Controller 使用开放 SDN 模型，其南向接口采用开放网络基金会（ONF）定义的 OpenFlow。ONF SDN 模型集中了大部分控制平面功能。面向数据中心的 APIC 模型部分集中了控制平面功能。APIC-EM 控制器（截至发布时）不对路由器和交换机的控制平面做任何更改，使其以完全分布式控制平面运行。
- **5.** D. APIC-EM 实现了答案中描述的所有功能。APIC-EM 内置了发现网络拓扑的功能，使用 SSH、CDP 和 LLDP 等多种协议。一旦发现拓扑，APIC-EM 的路径追踪（Path Trace）功能会根据用户输入的源地址和目的地址分析每台设备上的转发表。随后 Path Trace 确定数据包通过网络所经过的路径，包括第 2 层和第 3 层路径。
    
    名为路径追踪 ACL 分析（Path Trace ACL Analysis，或 Path Trace ACL Trace，或类似名称）的功能，是指 APIC-EM 进一步执行的分析，即将该模拟数据包与网络中现有的 ACL 进行比较。该工具会显示这些 ACL，并指出哪些 ACL 会根据其当前配置拒绝（即丢弃）该数据包。

### 从 ACL 逆向推导地址范围

对于这第二组问题，查看表 D-2 中现有的 access-list 命令。在每种情况下，记录该命令所匹配的确切 IP 地址或 IP 地址范围。

**表 D-2** 查找现有 ACL 所匹配的 IP 地址/范围

| 问题 | 需预测源地址范围的命令 |
|---|---|
| 1 | access-list 1 permit 192.168.4.5 |
| 2 | access-list 2 permit 192.168.4.128 0.0.0.3 |
| 3 | access-list 3 permit 192.168.4.128 0.0.0.127 |
| 4 | access-list 4 permit 172.25.96.0 0.0.0.255 |
| 5 | access-list 5 permit 192.168.4.128 0.0.0.31 |
| 6 | access-list 6 permit 192.168.4.128 0.0.0.7 |
| 7 | access-list 7 permit 172.25.96.0 0.0.7.255 |
| 8 | access-list 8 permit 172.25.96.0 0.0.0.63 |
| 9 | access-list 9 permit 10.10.16.0 0.0.7.255 |
| 10 | access-list 10 permit 10.10.16.0 0.0.0.127 |
| 11 | access-list 11 permit 192.168.171.112 0.0.0.7 |
| 12 | access-list 12 permit 192.168.171.112 0.0.0.15 |
| 13 | access-list 13 permit 172.19.200.0 0.0.0.63 |
| 14 | access-list 14 permit 172.19.200.0 0.0.1.255 |
| 15 | access-list 15 permit 10.1.0.0 0.0.255.255 |

> **注意** 只有当你确定 access-list 命令来自路由器，并且确实不是有人简单地写在纸上时，你才能依赖将这些数字相加的方法（如第 16 章“基本的 IPv4 访问控制列表”所示）。在这种情况下，你可以假定表 D-2 中的语句来自路由器。

### 早期练习题的答案

本节包含两组练习题的答案。

### 答案：构建 access-list 命令练习

表 D-3 列出了表 D-1 中问题的答案。

**表 D-3** 构建单行标准 ACL：答案

| 问题 | 答案 |
|---|---|
| 1 | access-list 1 permit 10.1.1.1 |
| 2 | access-list 2 permit 10.1.0.0 0.0.0.255 |
| 3 | access-list 3 permit 10.1.0.0 0.255.255.255 |
| 4 | access-list 4 permit any |
| 5 | access-list 5 permit 192.168.3.128 0.0.0.7 |
| 6 | access-list 6 permit 192.168.3.192 0.0.0.15 |
| 7 | access-list 7 permit 192.168.3.64 0.0.0.31 |
| 8 | access-list 8 permit 172.20.1.192 0.0.0.63 |
| 9 | access-list 9 permit 172.20.200.0 0.0.3.255 |
| 10 | access-list 10 permit 172.20.203.0 0.0.0.127 |
| 11 | access-list 11 permit 192.168.9.99 0.0.0.3 |
| 12 | access-list 12 permit 192.168.99.0 0.0.0.15 |
| 13 | access-list 13 permit 172.28.28.0 0.0.1.255 |
| 14 | access-list 14 permit 172.28.28.0 0.0.3.255 |
| 15 | access-list 15 permit 172.28.28.0 0.0.0.255 |

### 答案：从 ACL 逆向推导地址范围

表 D-4 列出了表 D-2 中问题的答案。

**表 D-4** — 表 D-2 中问题的地址范围：答案

| 问题 | 地址范围 |
|---|---|
| 1 | 一个地址；192.168.4.5 |
| 2 | 192.168.4.128 – 192.168.4.131 |
| 3 | 192.168.4.128 – 192.168.4.255 |
| 4 | 172.25.96.0 – 172.25.96.255 |
| 5 | 192.168.4.128 – 192.168.4.159 |
| 6 | 192.168.4.128 – 192.168.4.135 |
| 7 | 172.25.96.0 – 172.25.103.255 |
| 8 | 172.25.96.0 – 172.25.96.63 |
| 9 | 10.10.16.0 – 10.10.23.255 |
| 10 | 10.10.16.0 – 10.10.16.127 |
| 11 | 192.168.171.112 – 192.168.171.119 |
| 12 | 192.168.171.112 – 192.168.171.127 |
| 13 | 172.19.200.0 – 172.19.200.63 |
| 14 | 172.19.200.0 – 172.19.201.255 |
| 15 | 10.1.0.0 – 10.1.255.255 |

## 附录 E

### 思维导图解答

本附录提供了“部分复习”（Part Review）章节中思维导图练习的解答。你也可以在 DVD 上找到这些解答的 PDF 和 XMIND 格式文件。（下载页面上的示例思维导图使用 XMIND 应用程序 [www.xmind.net]，该应用程序在发布时支持 Windows、OS X 和 Linux 上的免费版本。）

### 第一部分复习 STP 概念思维导图解答

![](img/79473ea15699e01619d2aa789f5bd43b_1017_0.png)

### 第一部分复习关键术语思维导图解答

![](img/79473ea15699e01619d2aa789f5bd43b_1018_0.png)

### 第一部分复习命令思维导图解答

- switchport access vlan vlan-id
- vlan vlan-id
- name vlan-name
- { no } shutdown
- { no } vlan vlan-id
- vtp mode { server | client | transparent }
- vtp { server | client }

- show vlan brief
- show vlan id vlan-id
- show vlan name vlan-name
- show vlan status
- switchport trunk { dynamic { auto | desirable } | trunk }
- switchport trunk allowed vlan { add | all | except | remove } vlan-list
- switchport trunk encapsulation { dot1q | isl | negotiate }
- switchport nonegotiate
- switchport mode trunk
- switchport trunk native vlan vlan-id

- show interfaces interface-id switchport
- show interfaces interface-id trunk

- vtp domain domain-name
- vtp password password
- vtp mode { server | client | transparent }
- vtp version { 1 | 2 }
- { no } vtp pruning

- show vtp status
- show vtp password

- show vlan brief
- show vtp status

- spanning-tree mode { rapid-pvst | mst }
- spanning-tree { vlan vlan-number } root primary
- spanning-tree { vlan vlan-number } root secondary
- spanning-tree { vlan vlan-number } priority priority
- spanning-tree { vlan vlan-number } cost cost
- spanning-tree { vlan vlan-number } port-priority port-priority
- channel-group channel-group-number mode { auto | desirable | on | active | passive }
- spanning-tree portfast
- spanning-tree portfast default
- spanning-tree bpduguard enable
- spanning-tree bpdufilter enable
- { no } spanning-tree portfast bpduguard default
- { no } spanning-tree portfast default

- show spanning-tree
- show spanning-tree interface interface-id
- show spanning-tree { vlan vlan-id }
- show spanning-tree { vlan vlan-id } root
- show spanning-tree { vlan vlan-id } bridge
- show spanning-tree summary
- show spanning-tree interface-type interface-number portfast
- show etherchannel { channel-group-number } summary
- { clear | default } port channel-group-number

第 1 部分
命令


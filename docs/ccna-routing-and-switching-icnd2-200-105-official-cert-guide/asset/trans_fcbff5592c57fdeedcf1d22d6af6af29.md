
- 1. 在命令 router ospf 1 之后，以下哪条 network 命令会告诉此路由器在 IP 地址为 10.1.1.1、10.1.100.1 和 10.1.120.1 的接口上开始使用 OSPF？
    - a. network 10.0.0.0 255.0.0.0 area 0
    - b. network 10.0.0.0 0.255.255.255 area 0
    - c. network 10.0.0.1 0.0.0.255 area 0
    - d. network 10.0.0.1 0.0.255.255 area 0

- 2. 在命令 router ospf 1 之后，以下哪条 network 命令会告诉此路由器在 IP 地址为 10.1.1.1、10.1.100.1 和 10.1.120.1 的接口上开始使用 OSPF？
    - a. network 10.1.0.0 0.0.255.255 area 0
    - b. network 10.0.0.0 0.255.255.0 area 0
    - c. network 10.1.1.0 0.0.0.255 area 0
    - d. network 10.1.1.0 255.0.0.0 area 0
    - e. network 10.0.0.0 255.0.0.0 area 0

- 3. 以下哪些命令列出接口 serial 0/0 上的 OSPF 邻居？（选择两个答案。）
    - a. show ip ospf neighbor
    - b. show ip ospf interface brief
    - c. show ip neighbor
    - d. show ip interface
    - e. show ip ospf neighbor serial 0/0

- 4. 路由器 R1、R2 和 R3 分别是区域 1、2 和 3 的内部路由器。路由器 R4 是一台 ABR，连接到骨干区域（0）以及区域 1、2 和 3。以下哪个答案描述了路由器 R4 上使其成为 ABR 的配置，该配置与其他三台路由器不同？
    - a. abr enable 路由器子命令。
    - b. network 路由器子命令引用单个非骨干区域。
    - c. network 路由器子命令引用多个区域，包括骨干区域。
    - d. 该路由器在区域 0 中有一个接口，而某个 OSPF 邻居的接口位于不同区域。

- 5. 工程师连接到路由器 R1 并发出 show ip ospf neighbor 命令。邻居 2.2.2.2 的状态显示为 FULL/BDR。BDR 是什么意思？
    - a. R1 是区域边界路由器。
    - b. R1 是备份指定路由器。
    - c. 路由器 2.2.2.2 是区域边界路由器。
    - d. 路由器 2.2.2.2 是备份指定路由器。

- 6. 工程师从在 OSPF 配置模式中使用 network 命令的较传统 OSPFv2 配置迁移到改用 OSPFv2 接口配置。在新配置中，以下哪条命令配置分配给接口的区域号？
    - a. 接口配置模式下的 area 命令
    - b. 接口配置模式下的 ip ospf 命令
    - c. 接口配置模式下的 router ospf 命令
    - d. 接口配置模式下的 network 命令

- 7. 使用 OSPFv2 时，路由器上的以下哪个配置设置不会影响路由器选择添加到其 IPv4 路由表中的 IPv4 路由？
    - a. auto-cost reference-bandwidth
    - b. delay
    - c. bandwidth
    - d. ip ospf cost

## 基础主题

### 实现单区域 OSPFv2

OSPF 配置只包含少量必需步骤，但有许多可选步骤。在选定 OSPF 设计之后——在较大的 IP 互联网络中，这项任务可能很复杂——配置可以简单到在每台路由器接口上启用 OSPF，并将该接口放入正确的 OSPF 区域。

本节展示几个配置示例，全部采用单区域 OSPF 互联网络。在这些示例之后，正文将继续介绍若干额外的可选配置设置。作为参考，以下列表概述了本章第一个主要部分涵盖的配置步骤，并简要提及所需命令：

![](img/79473ea15699e01619d2aa789f5bd43b_251_0.png)

- 步骤 1. 使用 router ospf process-id 全局命令进入特定 OSPF 进程的 OSPF 配置模式。
- 步骤 2.（可选）通过以下方式配置 OSPF 路由器 ID：
    - A. 使用 router-id id-value 路由器子命令定义路由器 ID
    - B. 使用 interface loopback number 全局命令以及 ip address address mask 命令，在环回接口上配置 IP 地址（选择所有工作环回接口中最高的 IP 地址）
    - C. 依赖接口 IP 地址（选择所有工作非环回接口中最高的 IP 地址）
- 步骤 3. 使用一条或多条 network ip-address wildcard-mask area area-id 路由器子命令，在由配置的地址和掩码匹配的任何接口上启用 OSPFv2，从而为所列区域在该接口上启用 OSPF。
- 步骤 4.（可选）使用 passive-interface type number 路由器子命令，将任何 OSPF 接口配置为被动接口，前提是该接口上不能或不应发现邻居。

为了更直观地了解 OSPFv2 配置，图 8-1 显示了关键 OSPF 配置命令之间的关系。请注意，配置在一部分中创建路由进程，然后在每个接口上间接启用 OSPF。配置并未指定在哪些接口上启用 OSPF，而是要求 IOS 通过将 OSPF network 命令与接口 ip address 命令进行比较来应用某种逻辑。接下来的示例将进一步讨论这一逻辑。

### 配置

![](img/79473ea15699e01619d2aa789f5bd43b_252_0.png)

### OSPF 单区域配置

图 8-2 显示了一个示例网络，将用于单区域 OSPF 配置示例。所有链路都位于区域 0。该设计有四台路由器，每台连接到一个或两个 LAN。但是，请注意，图中顶部的路由器 R3 和 R4 连接到相同的两个 VLAN/子网，因此它们也会在每条 VLAN 上彼此形成邻居关系。（该设计顶部的两台交换机作为二层交换机使用。）

**示例 8-1** *R3 上的 IPv4 地址配置（包括 VLAN 中继）*

```
interface GigabitEthernet 0/0.341
 encapsulation dot1q 341
 ip address 10.1.3.1 255.255.255.128
!
interface GigabitEthernet 0/0.342
 encapsulation dot1q 342
 ip address 10.1.3.129 255.255.255.128
!
interface serial 0/0/0
 ip address 10.1.3.13 255.255.255.128
```

![](img/79473ea15699e01619d2aa789f5bd43b_253_0.png)

**图 8-2 OSPF 单区域配置的示例网络**

R3 上初始的单区域配置如示例 8-2 所示，它在图 8-2 所示的所有接口上启用 OSPF。首先，router ospf 1 全局命令将用户置于 OSPF 配置模式，并设置 OSPF process-id。该编号只需在本地路由器上唯一，从而允许路由器通过使用不同的进程 ID 在单台路由器中支持多个 OSPF 进程。（router 命令使用 process-id 来区分这些进程。）process-id 不必在每台路由器上匹配，并且可以是 1 到 65,535 之间的任意整数。

**示例 8-2** 在 R3 上使用一条 network 命令的 OSPF 单区域配置

```
router ospf 1
network 10.0.0.0 0.255.255.255 area 0
```

概括地说，而不是针对此示例，OSPF network 命令告诉路由器查找其本地接口中与 network 命令前两个参数匹配的接口。然后，对于每个匹配的接口，路由器在这些接口上启用 OSPF，发现邻居，创建邻居关系，并将该接口分配到 network 命令中列出的区域。（请注意，区域可以配置为整数或点分十进制数，但本书习惯将区域号配置为整数。整数区域号的范围为 0 到 4,294,967,295。）

对于示例 8-2 中的具体命令，任何匹配的接口都被分配到区域 0。但是，前两个参数——ip_address 和 wildcard_mask 参数值 10.0.0.0 和 0.255.255.255——需要一些解释。在本例中，该命令匹配路由器 R3 所示的所有三个接口；下一主题将解释原因。

### 使用 OSPF network 命令进行匹配

理解本第一个示例中所示传统 OSPFv2 配置的关键，是理解 OSPF network 命令。OSPF network 命令会比较

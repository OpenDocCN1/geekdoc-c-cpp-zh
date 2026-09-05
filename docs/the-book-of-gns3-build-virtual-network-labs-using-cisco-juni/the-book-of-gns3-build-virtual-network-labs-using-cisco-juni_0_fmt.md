
# GNS3 指南：使用 Cisco、Juniper 等工具构建虚拟网络实验室

# GNS3 之书：使用 Cisco、Juniper 及更多技术构建虚拟网络实验室

### Jason C. Neumann 著

由 No Starch Press 出版

# 前言

网络无处不在。它们连接着各种业务，从本地书店到巨型企业，再到大学，跨越了多个城市和大陆。网络在概念上易于理解，但它们正变得越来越复杂，软件定义网络（SDN）、物联网（IoT）以及其他领域的创新已触手可及。

要理解、设计和管理当今复杂的网络，网络专业人员不仅必须精通理论，还必须在不断变化的环境中实践并验证概念。这正是 GNS3 发挥用场的地方：它为用户提供了巨大的灵活性来构建自己的网络实验室，允许他们尝试新的网络功能、捕获数据包以分析协议，并验证配置以便稍后部署到真实设备上。这一切都不需要投资昂贵的硬件。GNS3 是一个强大且适应性强的工具，不断演进以集成多个供应商，并满足网络专业人士日益增长的需求。但你如何掌握 GNS3 本身，又要从哪里开始呢？

在《GNS3 之书》中，Jason 涵盖了网络工程师、管理员以及准备认证的人所需的所有入门内容，从引导你安装和配置 GNS3，到创建和管理你的项目。Jason 在深入研究的同时展示了该软件真正的广度，涵盖了如何捕获网络包、如何连接到真实网络和现场交换机，以及如何在实验室中加入 Juniper 的 vSRX Firefly 和 Cisco 的 IOS-XRv 等高级系统。他花费了大量时间解释概念并提供技巧，这些将让你迅速成为专家用户。

Jason 的书是利用 GNS3 并充分发挥网络实验室价值的理想之选。无论你是网络领域的新手还是资深人士，我都能保证你会有新的收获。

Jeremy Grossmann

GNS3 联合创始人 2015 年 5 月

# 致谢

俗话说“养育一个孩子需要全村的力量”，而 GNS3 是大家的心血。我想感谢所有帮助创建和推广 GNS3 并使其成为如今如此出色的软件工具的人们。你们都太棒了！

特别感谢：

- 我的妻子 Sharon，感谢她的耐心，以及允许我成为一个 GNS3 的“超度极客”（`übergeek`）。
- Jeremy Grossmann，我们仁慈的 GNS3 独裁者。
- Christophe Follot，Dynamips 的创建者，开启一切的人。
- Julien Duponchelle，沉默的编程大师。
- Stephen Guppy，他一天内回复的邮件比我一年的还多。
- Mark Blackwell，卓越的 GNS3 传教士。
- Flávio J. Saraiva，Dynamips 大师。
- Chris Welch，GNS3 Workbench 的创建者，以及 Jungle 人群控制的维护者。
- Radovan Brezula，他能让任何网络操作系统在 GNS3 中运行。
- Daniel Lintott——我们可以转换那个项目，但让我们用 Debian 吧！
- gns3vault.com 的 Rene Molenaar，u bent groot. Dank u veel!（非常感谢！）
- Bryant Advantage 的 Chris Bryant，斗牛们集合！
- Jeremy Cioara，卓越的 Cisco 之神（握力排名第一）。
- Keith Barker，卓越的 Cisco 之神（握力排名第二）。
- Andrew Coleman，GNS3 超级管理员，去睡会儿吧！
- GNS3 众筹者——你们知道自己是谁！

我还特别感谢 No Starch Press 的每一个人，感谢他们在创建《GNS3 之书》过程中提供的所有帮助。特别，我想感谢：

- Jennifer Griffith-Delgado——你是最棒！
- Serena Yang——你对我非常有耐心，你太棒了！
- Bill Pollock，NSP 霸主。

因为由于我是个笨蛋，我确定自己漏掉了很多重要人物，但请放心，我也感激你们！现在，让我对你们那里所有未点名的灵魂说：谢谢你们！

# 引言

我在 GNS3 开发早期就开始使用它，并且如鱼得水。从一开始，我就预见到它将成为一个无价的网络工具。我曾用它来获取 Cisco `IOS`、`Junos OS` 和 `Arista` 等操作系统的实践经验，并通过了许多网络认证考试。直到今天，我仍经常使用它在将真实设备部署到现场之前测试路由器配置。《GNS3 之书》是我将这一优秀资源分享给像你这样的其他网络专业人士的方式。

# 适合对象

本书适用于任何涉及路由器、交换机或防火墙的人。无论你使用 Cisco、Juniper、Arista、`Vyatta` 还是其他网络操作系统，GNS3 都是构建物理实验室的极佳替代方案。与使用物理设备的实验室不同，GNS3 虚拟实验室让你能够创建和保存无限的网络配置，而无需拆卸现有的实验室。本书涵盖了让你的项目快速运行起来的所有细节。

# 本书内容

《GNS3 之书》将引导你如何在 Windows、OS X 和 Linux 上安装、配置和运行 GNS3，并在过程中向你展示一些极客且有趣的技巧。无论你是刚开始，还是已经用过 GNS3，我想你将发现，当你拥有正确的工具时，会对这种可能性产生新的认识。我没有涵盖 TCP/IP 基础知识，但我确实提供了许多如何配置 GNS3 的示例。

## 我的方法

最有效的学习方法是实操。这就是为什么我采用基于教程的方法来使用 GNS3 创建功能完整的实验室。教程解释了如何使用章节中介绍的虚拟设备来构建和配置实验室。我提供了配置 `IOS`、`Junos OS` 和 Juniper `vSRX` 的示例。你不需要成为网络操作系统的专家，因为我将一步步引导你完成配置。你可能会在网络上花费几天甚至几周的时间来研究如何配置某些功能，例如连接到现场交换机、创建虚拟访问服务器或将你的虚拟实验室连接到互联网。但在读了《GNS3 之书》之后，没必要那样做了。

## 概述

《GNS3 之书》引导你完成 GNS3 的安装和使用，每一章都引入了基于之前的新概念。你将学习如何创建和管理简单到复杂的项目，无论是使用单台计算机还是在多台计算机之间分配负载。

- **第一章**涵盖了什么是 GNS3 以及它是如何工作的，提供了 GNS3 的概述，并讨论了虚拟网络的优势。
- **第二章**讨论了在 Windows、OS X 和 Linux 上安装 GNS3，并解释了使用虚拟设备运行 GNS3 作为直接在 PC 上安装的替代方案。
- **第三章**查看了如何安装 Cisco `IOS` 镜像并使用 `Dynamips` 设置你的第一个虚拟路由器。你还将学习为 `Dynamips` 路由器设置 `Idle-PC` 值的重要性。
- **第四章**教你如何配置虚拟路由器。之后，你将查看所有的工具栏选项并创建一个双路由器网络。
- **第 5 章**将向你展示如何安装 VPCS 并使用它为你的项目添加类似 PC 的简单主机。你将学习如何使用 VirtualBox 添加完整的虚拟机，并使用虚拟的 Cisco IOS 路由器和 VirtualBox Linux PC 创建一个实验室。然后，你将学习如何使用 Wireshark 捕获数据包。
- **第 6 章**将解释如何安装 QEMU 并使用它创建你自己的虚拟 Juniper 路由器。你将使用 Juniper 和 Cisco 创建一个网络，学习如何安装 Juniper vSRX Firefly，并配置基础 vSRX 防火墙。
- **第 7 章**将演示 GNS3 内置的设备节点，并解释如何使用它们来节省你 PC 上的资源。你还将学习如何将你的 GNS3 项目连接到实时交换机和互联网。
- **第 8 章**将带你从设置 GNS3 设备到配置设备的过程。你将创建一个 Cisco ASA 防火墙和一个 IDS/IPS，并使用 Cisco IOS-XRv 创建一个网络实验室。
- **第 9 章**将继续设备创建的主题。你将学习如何在 Unix 上安装 Cisco IOS，并使用 NX-OSv 创建虚拟的 NX OS 交换机。
- **第 10 章**将介绍一些你利用新学的 GNS3 知识可以做的趣味趣事，例如创建一个模拟的接入服务器来管理你的设备，并将 GNS3 虚拟设备配置部署到真实的 Cisco 路由器上。
- **附录 A**讨论了你可能在 GNS3 中遇到的一些常见问题并提供了解决方案来纠正它们。
- **附录 B**列出了与 GNS3 的 Cisco 路由器以及哪些 Cisco IOS 镜像文件最好。
- **附录 C**提供了关于 GNS3 中使用的 Unix 版 IOS 以及 NM-16ESW Cisco 交换机的信息。

现在，准备好进入 GNS3 世界吧。在开始这段旅程之前，请向你的家人告别，因为一旦开始，你将无法停下！

# 第 1 章 介绍 GNS3

GNS3 是一款跨平台的图形化网络模拟器，运行在 Windows、OS X 和 Linux 上。它是某些极具天赋的、工业级极客合作的结晶——例如 Christophe Fillot、Jeremy Grossmann 和 Julien Duponchelle 等。Fillot 是 MIPS 处理器仿真程序 `Dynamips` 的创建者，该程序允许你运行 Cisco 的路由器操作系统，而 Grossmann 是 GNS3 的创建者。他将 `Dynamips` 及其与其他开源软件集成到一个易于使用的图形化用户界面中。Duponchelle 协助 GNS3 的代码编写，他的贡献帮助了该软件的发展。

GNS3 允许你在 PC 上设计和测试虚拟网络，包括但不限于 Cisco IOS、Juniper、MikroTik、Arista 和 Vyatta 网络。它常用于在准备 Cisco 认证网络专员（CCNA）和 Cisco 认证网络专业人员（CCNP）考试期间需要 Cisco IOS 路由和交换实践经验的学生。但这仅仅是 GNS3 功能冰山一角。在本章中，我将讨论 GNS3 是什么以及该软件的优缺点。

## 为什么要使用 GNS3？

在虚拟化出现之前，网络工程师、管理员和学生必须使用物理硬件构建实验室或租机架时间。这两种方案都既昂贵又不方便，并且限制了你可以使用的网络设计。如 `RouterSim` 和 `Boson NetSim` 等软件模拟程序也存在很久了，但这些应用程序仅仅模拟了 Cisco IOS 的命令。Cisco 教育确实提供了基于 Unix 版 Cisco IOS（`IOU`）的更廉价的虚拟机架租赁，但它只允许你在特定的预配置网络配置上进行练习。它还要求你拥有活跃的互联网连接才能访问实验室。Cisco 还提供了一个名为虚拟网络路由实验室（`VIRL`）的产品，它与 GNS3 类似，但需要支付年费，限制了你在实验室中使用对象数量，并且仅使用模拟的 Cisco 系统。

相反，GNS3 允许你自定义网络实验室以精确满足你的需求，使用 Cisco 和非 Cisco 技术创建无限项目，向项目中添加无限对象，并且无论互联网连接情况如何，都可以随时访问这些项目。GNS3 通过结合运行真实网络操作系统（如 Cisco IOS）的仿真硬件设备、模拟操作系统（如 `NX-OSv`）以及跨多台计算机资源的能力，为你的设计提供了最大的灵活性。

## 仿真硬件

GNS3 的图形界面允许你创建包含各种路由器、交换机和 PC 的虚拟化网络实验室，但它在与 Cisco IOS 配合使用时最为出彩。与类似的应用程序不同，GNS3 不仅仅是模仿 Cisco IOS 命令或功能。相反，它使用后端虚拟机程序来仿真硬件。由于只有硬件是被仿真的，你在 PC 上运行的是真实的 IOS 镜像。所有的配置命令都来自真实的 IOS，理论上，任何 IOS 版本支持的协议或功能都可以用于你的设计。这一功能将 GNS3 与 `RouterSim`、`Boson NetSim` 或模拟环境的 `VIRL` 等程序区分开来。

## 模拟操作系统

除了仿真硬件外，GNS3 还集成了模拟操作系统，并且它们可以与其他 GNS3 设备完全联网。一个例子就是 IOU，我将在第 9 章中介绍。IOU 由一组模拟 IOS 功能的 Linux 二进制文件组成，并被 GNS3 完全支持。

除了 Cisco IOS，GNS3 还可以集成虚拟机（`QEMU`）和运行 Linux、BSD 或 Windows 等系统的 VirtualBox 虚拟机。例如，为了练习在 Linux 上安装和配置 Apache 服务器，只需将运行 Linux 和 Apache 的 VirtualBox 虚拟机（`VM`）添加到 GNS3，并通过另一个 VirtualBox 主机访问它来对其测试。这一切都在 GNS3 用户环境中完成。如果你想在 Apache 服务器之前加一个防火墙，可以使用 Cisco 路由器、自适应安全设备（`ASA`）防火墙，甚至是基于 Linux 的防火墙（如 Vyatta）。

## GNS3 服务器的可扩展性

GNS3 利用了客户端-服务器技术；就像浏览器连接到 Web 服务器以访问并显示网页一样，GNS3 图形界面（`GUI`）程序访问 GNS3 服务器，从而启动、停止并控制 GNS3 设备。这使得你的项目可以扩展，因为它们不再局限于运行在单台计算机上。如果你处理大型或复杂的拓扑结构，你可以在 GNS3 GUI 程序所在的 PC 上运行 GNS3 服务器程序。如果你拥有一台具有大量内存和处理能力的高端服务器，你可以在服务器硬件上安装 GNS3 服务器程序，但在运行在普通 PC 上的 GNS3 GUI 程序上控制所有设备。

GNS3 的真正之处在于它能够将你的虚拟设备连接起来，通常使用互联网协议版本 4（`IPv4`）和互联网协议版本 6（`IPv6`）等协议，从而创建一个仅在单台计算机上运行的实验室。一些简单的设计可能只包含几个组件，如图 1-1 所示的项目。

![集成 Fedora Linux、Cisco 和 Juniper 路由器的 GNS3 拓扑](img/httpatomoreillycomsourcenostarchimages2208871.png.jpg)

图 1-1. 集成 Fedora Linux、Cisco 和 Juniper 路由器的 GNS3 拓扑

图 1-1 中的项目允许 Fedora Linux 主机通过交换机、一台 Juniper 路由器、一台 Cisco 路由器并通过一个 GNS3 云节点访问实时互联网。这是一个简单的网络，但你也可以创建由十个或更多路由器、交换机和 PC 组成的复杂网络，如图 1-2 所示的设计。

![复杂的多协议 GNS3 拓扑](img/httpatomoreillycomsourcenostarchimages2208873.png.jpg)

图 1-2. 复杂的多协议 GNS3 拓扑

图 1-2 中的项目配置了超过 25 个设备，包括冗余交换机组、EtherChannel、二层热备备路由协议（`HSRP`）、帧中继（`Frame Relay`）、增强型内部网关路由协议（`EIGRP`）、开放最短路径优先（`OSPF`）和边界网关协议（`BGP`），但该项目可以在配置适中的 PC 上运行。为了让你的设备清晰可见，你还可以使用彩色的可缩放文本对你的设计进行注释，就像我在示例中做的那样。如果你有一台笔记本电脑，你甚至可以带着项目在路上向客户演示、解决设计问题或为认证考试复习。CCNA 或 CCNP 候选人还可以创建所有必要的训练实验室，以学习 Cisco 的考试材料，在真实的操作系统上进行练习并随时随地学习。

GNS3 具有将实验室设备中的虚拟接口桥接到你 PC 中的一个或多个物理以太网接口的能力。这允许你将虚拟网络连接到路由器、交换机和其他 PC 等真实硬件。例如，你可以使用多台 PC 运行两个或多个 GNS3 网络，并使用以太网交叉线或物理交换机将 PC 连接起来。这样做让你具备了跨所有 PC 连接所有 GNS3 设备的能力。（我亲切地称之为 GNS3 `ubernet`！）

# 开源集成

GNS3 通过利用开源技术（包括 Dynamips、QEMU 和 VirtualBox）来实现它的魔法。它可以像运行 Cisco IOS 一样轻松运行 Juniper、Arista 以及许多其他网络操作系统。

## Dynamips 虚拟机管理器

为了仿真 Cisco 硬件，GNS3 自带了 Dynamips，这是一个由法国人 Christophe Fillot 在 2005 年创建的优秀应用程序，并由 Flávio J. Saraiva 等人的贡献保持着最新状态。Dynamips 虚拟机管理器程序可以仿真 Cisco 1700、2600、3600、3700 和 7200 系列路由器硬件。得益于 Dynamips，你可以快速方便地在 GNS3 中使用各种模拟的 Cisco 网络插槽和 WAN 接口卡（`WICs`）来配置这些路由器型号。虚拟输入/输出（`I/O`）卡允许你向设备中添加多个以太网接口、交换机模块和串口。你甚至可以根据项目需求和 Cisco IOS 版本按每个设备为单位添加或移除内存。

## QEMU 和 VirtualBox

你可以将 QEMU 和 VirtualBox 虚拟机添加到 GNS3 并在项目中使用它们。这些设备可以与其他 GNS3 设备连接，以形成完整的端到端网络。例如，你可以将 VirtualBox 主机连接到一系列交换机和路由器，并允许它访问网络上另一个 VirtualBox 主机上的资源。在这种情况下，你可以配置和测试各种路由协议以及如网络地址转换（`NAT`）、访问控制列表（`ACLs`）和虚拟专用网络（`VPNs`）等功能。自然地，你物理计算机的硬件对你的资源存在限制，但现代计算机有许多未使用的资源等待 GNS3 的开发。

## 一些局限性

GNS3 并非没有局限性。Dynamips 的局限性在于你无法在生产环境中使用它，使其仅适用于教育。此外，交换功能局限于适宜的命令集，除非你在 GNS3 项目中集成一个或多个物理 Catalyst 交换机。幸运的是，IOU 有助于弥补部分差距。

## 需要组装

任何伟物都有代价，GNS3 例外。最值得注意的是，GNS3 需要一个或多个 Cisco IOS 镜像在你的虚拟 Dynamips 路由器上运行，而 GNS3 并不提供这些镜像。

## 有限的仿真



Dynamips 无法仿真 Cisco 交换机的应用专用电路（`ASIC`）硬件。对于需要交换机高级特性的未来 CCIE 人来说，这是一个小的挫折。然而，GNS3 的灵活性允许你将 GNS3 与实际 Catalyst 交换机集成。当你不需要这些高级特性时，可以将虚拟交换机模块（如 `NM-16ESW`）添加到你的一个路由器中，创建一个简单的三层交换机。该设备应该能够满足基本的交换需求，包括虚拟局域网（`VLANs`）、802.1Q 链路、生成树、EtherChannel 以及使用 EIGRP、OSPF、BGP 的多协议路由。最后，可以使用 Cisco IOU 镜像仿真交换机，它们提供的命令比 Dynamips 交换机模块多。

由于 Dynamips 是不提供硬件加速的仿真器，吞吐量限制为每秒 1.5Mb 到 800Mb，取决于你使用的 IOS。这似乎是一个限制，但实际上是好事，因为它防止了用户将 Cisco 硬件虚拟化并投入生产环境。想象一下仿真设备以全速运行：从这里到廷布图的每个网络极客都会在便宜 PC 上安装虚拟路由器并用于生产网络。如果发生这种情况，Cisco 会严厉惩罚 Dynamips 开发者，GNS3 现在就不会存在了。在使用 GNS3 进行教育和测试时，这种局限性几乎没有影响。

## 结语

现在我已经介绍了 GNS3 的亮点，我希望你像我一样兴奋能在自己的计算机上使用它。与其他类似的应用程序或工具不同，GNS3 给了你完全的控制权，让你自由发挥想象力创建、学习和开发满足你需求的复杂网络。此外，你无需投入资金购买路由器和交换机，却换来一满屋吵且耗电的硬件。

在下一章中，我将向你如何安装 GNS3。让我们开始吧！

向硬件世界告别，欢迎来到 GNS3 的世界！这是一种学习网络的全新方式。在本章中，我将指导你如何在 Microsoft Windows、Mac OS X 和 Ubuntu Linux 上安装基础版 GNS3 系统。

基础安装包含 GNS3 应用程序和几个辅助应用程序。在 Windows 和 OS X 上，所有先决条件应用程序都包含在 GNS3 安装包中，该安装包可以从 GNS3 网站（[`www.gns3.com/`](http://www.gns3.com/)）获取。

在 Linux 上安装时，你可以通过特定平台的包管理器下载并安装 GNS3，或者直接从源码安装。从源代码安装的原理适用于任何基于 Unix 的系统，而且这是确保你拥有最新软件的绝佳方法。

# 通用硬件要求

运行 GNS3 的要求在很大程度上取决于你安装的操作系统、你希望在项目中使用的路由器型号和数量，以及你是否在设计中集成了如 `QEMU` 或 `VirtualBox` 等外部程序。过去几年购买的大多数计算机都能够无障碍地运行此基础安装。

尽管如此，如果你决定不再仅仅使用 Cisco 路由器创建项目，而是在你的 GNS3 设计中引入其他虚拟环境（如 Linux、`BSD`、`ASA`、`IDS` 或 Juniper），你将希望尽可能获得强大的性能。内存和处理能力越高，一切运行得越良好，因为像 `QEMU` 和 `VirtualBox` 等程序需要 RAM 来运行其客户操作系统，并且它们与你的原生操作系统竞争 CPU 时间。你还需要额外的磁盘空间来存储客户操作系统。

你可以访问 GNS3 网站来验证你操作系统的要求，但对于简单的基础安装，一个很好的经验法则如下：

- 1.5 GHz 处理器
- 4GB RAM
- 250MB 空闲磁盘空间

这些是最低规格，拥有这些配置的系统应该能够运行使用少量 Cisco 路由器的简单 GNS3 拓扑。当然，随着你的项目变得越来越庞复杂，GNS3 将极大受益于更强大的系统。

### 注意

如果现在的安装说明看起来让人无从从，不要担心！直接跳转到 GNS3 设备学习如何下载预构建的 GNS3 设备，并直接开始吧。

# 在 Microsoft Windows 上安装

与其他操作系统相比，在 Windows 上安装 GNS3 是一件不用考虑的事。Windows 安装包包含了 GNS3 需要的几乎所有应用程序，外几个在其他平台上未找到的额外程序，而且所有内容只需少量用户干预即可完成安装。

Windows 安装程序包含了几个额外的实用程序，包括用于 `Juniper` 和 `ASA` 的 `QEMU`；流行的网络监控程序 `Wireshark`；`PuTTY`（一个 Windows 终端仿真程序）；以及 `VPCS`（一个简单的类 DOS 命令行模拟器，用于使用 `ping` 和 `traceroute` 命令测试连接性）。安装程序包含 GNS3 的 32 位和 64 位版本，它应该会自动安装正确的版本。

按照以下步骤在 Windows 上安装 GNS3：

1. 从 GNS3 网站下载 GNS3 全合一安装程序（[`www.gns3.com/`](http://www.gns3.com/)）并启动它开始安装。
2. 在设置向导界面上点击 **Next**（下一步），在许可协议界面上点击 **I Agree**（我同意）。
3. 选择你希望安装程序在开始菜单中放置应用程序快捷方式的文件夹，然后点击 **Next**。（默认文件夹为 `GNS3`。）
4. 随后你可以选择要包含在安装中的组件，如图 2-1 所示。默认选项安装所有组件以创建一个功能完整的 GNS3 系统，包括 `Wireshark`、`VPCS` 和 `QEMU`。为了节省磁盘空间，或者如果你不需要这些附加功能，请取消勾选这些选项。`NIO` 以太网云连接需要 `WinPCAP`，使用 Cisco 路由器和交换机创建项目需要 `Dynamips`。做出你的选择然后点击 **Next**。

   ![选择要安装的 GNS3 组件](img/httpatomoreillycomsourcenostarchimages2208875.png.jpg)

   图 2-1. 选择要安装的 GNS3 组件
5. 你应该看到选择安装位置界面，如图 2-2 所示。要将 GNS3 安装到其他位置，请在“目标文件夹”字段中输入新位置并点击 **Install**（安装）。
6. 继续遵循所有提示完成安装。我建议你接受所有默认设置。

![选择目标文件夹位置](img/httpatomoreillycomsourcenostarchimages2208877.png.jpg)

图 2-2. 选择目标文件夹位置

安装完成后，GNS3 应该会在你的桌面上创建一个图标。

## 在 OS X 上安装

GNS3 仅支持运行 OS X 的 Intel 芯片 Mac。你可能应该确保你拥有最新版本的 OS X。

要在 OS X 上安装 GNS3，你应该从 GNS3 网站下载相应的安装程序（[`www.gns3.com/`](http://www.gns3.com/)），然后双击它，会出现一个映像文件。双击映像文件打开 `GNS3` 文件夹，并将 GNS3 图标拖入你的 `Applications` 文件夹，如图 2-3 所示。

![将 GNS3 程序拖入应用程序](img/httpatomoreillycomsourcenostarchimages2208879.png.jpg)

图 2-3. 将 GNS3 程序拖入应用程序

要在当前的 OS X 上运行 GNS3，第一次运行时可能需要右键点击应用程序图标并选择 **Open**。你会看到一个对话框警告你该软件包来自未识别的开发者，并询问你是否确定打开它。点击 **Open** 按钮绕过此 OS 功能。从此 GNS3 将正常运行，不再有警告。

# 在 Ubuntu Linux 上安装

GNS3 在许多 Linux 发行版上运行良好，但大多数版本都缺乏文档。在本节中，我将揭开谜底，向你展示在基于 Unix 的平台上运行 GNS3 是有多简单。我选择 Ubuntu 是因为它是最常用的发行版之一。

在 Linux 上安装 GNS3 有两种方法。你可以通过包管理器安装捆绑包，也可以从源码安装。使用包安装既快捷又简单，但缺点是你受限于移植到特定平台的 GNS3 版本，这可能不是最新版本。这就是源码安装大显身手的地方。从源码安装只需要几个额外的步骤，并为你提供最新版本的 GNS3。尽管我强烈建议从源码安装，但我们在这里介绍这两种方法。

## 从包安装 GNS3

使用高级软件包工具安装 GNS3，打开终端程序并输入以下命令：

```bash
$ sudo apt-get install gns3
```

提示时输入你的密码。此命令的输出显示了将安装的包列表，并显示安装将占用多少磁盘空间。安装程序会在执行前提示确认。确认后，软件包将完成安装，GNS3 准备就绪。

你可以通过在终端程序输入 `gns3` 或从显示器应用程序菜单中启动 GNS3 来启动该程序。你现在已经准备好配置 GNS3 了。

# 从源码安装 GNS3

从源码安装可以确保你获得最新版本的 GNS3，在我看来，这是在类 Unix 系统上安装 GNS3 的最佳方法。无论你使用哪个版本的 Linux，都应该能够将这些指令作为指南，让你的系统中运行起 GNS3。在接下来的示例中，我将使用 Ubuntu Linux 作为框架，但请记住，这些指令适用于几乎任何基于 Unix 的发行版。发行版之间的主要区别在于所需的依赖项以及它们的安装方式。请务必检查 GNS3 网站以获取最新的依赖要求。

我在 Solaris、FreeBSD、OpenBSD、Ubuntu、Mint、OpenSUSE、Fedora、Fuduntu、Debian、Arch、Gentoo、Kali、Netrunner 和 PCLinuxOS 上安装过 GNS3，所以我确定你也可以在你的系统上运行它！

从 GNS3 网站下载并解压安装文件（[`www.gns3.com/`](http://www.gns3.com/)）。

## 提取源码

当你下载 Linux 版本的 GNS3 时，你会得到一个包含 Linux 源码的 ZIP 文件。解压文件后，你会看到 GNS3 使用的每个程序的独立 ZIP 文件。使用以下命令解压 GNS3 源码文件，将 `x` 替换为文件版本：

```bash
$ cd ~/Download
$ unzip GNS3-x-source.zip

dynamips-x.zip
gns3-gui-x.zip
gns3-server-x.zip
vpcs-x.zip
iouyap-x.zip
```

接下来，你需要更新 Ubuntu 包管理器。

### 更新包管理器

更新包管理器的索引文件可以确保你安装的是最新版本的依赖项。在 Ubuntu 上，打开终端程序并输入：

```bash
$ sudo apt-get update
```

### 安装依赖项

GNS3 的依赖和包名取决于特定的 Linux 发行版，因此你需要下载适用于你操作系统的部分。你可能还想先检查 GNS3 网站，因为依赖项会随时间变化。在 Ubuntu 上，输入以下命令：

```bash
$ sudo apt-get install python3-dev
$ sudo apt-get install python3-setuptools
$ sudo apt-get install python3-pyqt4
$ sudo apt-get install python3-ws4py
$ sudo apt-get install python3-netifaces
```

安装完所有 Python 包后，继续处理 Dynamips。

### 安装 Dynamips

在编译 Dynamips 之前，你需要在 Ubuntu 系统上额外安装几个包：

```bash
$ sudo apt-get install libpcap-dev
$ sudo apt-get install libelf-dev
$ sudo apt-get install uuid-dev
$ sudo apt-get install cmake
```

接下来，使用以下命令解压源码文件、编译并安装 Dynamips。将 `x` 替换为软件版本。

```bash
$ unzip dynamips-x.zip
$ cd dynamips-x
$ mkdir build
$ cd build
$ cmake ..
$ make
$ sudo make install
```

完成后，你应该在 `/usr/local/bin/` 目录下看到一个名为 `dynamips` 的文件。将程序的所有者更改为 root，并将文件权限更改为可执行。这允许 Dynamips 设备通过你 PC 的以太网适配器连接到互联网或 Cisco 交换机等硬件。

```bash
$ sudo chown root /usr/local/bin/dynamips
$ sudo chmod 4755 /usr/local/bin/dynamips
```

对于关注安全的人，还有另一种方法。你可以在不为 Dynamips 提供 root 级权限的情况下实现这一功能。以下方法适用于 Ubuntu，并适用于大多数运行 Linux 内核 2.2 或更高版本的系统。此方法不适用于基于 BSD 的系统。

```bash
$ sudo apt-get install libcap2
$ sudo setcap cap_net_raw,cap_net_admin+eip /usr/local/bin/dynamips
```

接下来，将安装 GNS3 服务器和 GUI 源码。

### 安装 GNS3 服务器和 GUI

GNS3 由两个主要应用程序组成：服务器程序和 GUI 应用程序。服务器程序在 PC 后台运行，普通用户看不到。它运行并管理所有的辅助程序，例如 Dynamips、QEMU 和 VirtualBox。GUI 应用程序提供前端用户体验，你与 GNS3 的交互就在这里。

```bash
$ unzip gns3-server-x.zip
$ unzip gns3-gui-x.zip
```

要完成安装，为每个应用程序运行 GNS3 设置脚本。此步骤需要特权 root 权限，请准备好你的 root 密码。从 GNS3 服务器开始。

```bash
$ cd gns3-server-x
$ sudo python3 setup.py install
```

接下来，安装 GNS3 GUI 应用程序。

```bash
$ cd gns3-gui-x
$ sudo python3 setup.py install
```

安装完成后，应用程序将安装在 `/usr/local/bin/` 下。

接下来，通过解压 `vpcs` ZIP 文件并运行 `mk.sh` 脚本安装虚拟 PC 模拟器（`VPCS`）。这模拟了一个简单的 PC 并用于路由器。

```bash
$ unzip vpcs.zip
$ cd vpcs/src
$ mk.sh
$ sudo cp vpcs /usr/local/bin
```

最后一步适用于 Ubuntu 以及其他发行版。如果没有此命令，程序可以正常运行，但 GNS3 中不会显示图标。

```bash
$ conftool-2 --type Boolean --set /desktop/gnome
```

启动程序，输入以下终端命令：

```bash
$ gns3
```

就这些！你现在准备好配置 GNS3 并创建项目了。

# GNS3 镜像

在 PC 上安装 GNS3 的替代方案是使用预配置的 `GNS3 镜像`。GNS3 镜像简单来说就是一个安装了 GNS3 的虚拟机。GNS3 镜像通过类似 `VirtualBox` 的应用程序运行，非常灵活。

## 优缺点

在虚拟环境中运行 GNS3 有几个优点。主要的是易用性和便携性。大部分设置工作已经为你完成，你将拥有一个便携 GNS3 安装，可以在 PC 之间迁移。如果你购买了新电脑，可以将镜像拷贝到新 PC，一切将如以前一样运行，无论新电脑运行的是什么硬件或操作系统。

另一方面，如果你希望客户操作系统和 GNS3 运行良好，你的主机需要快速的处理器和大量的内存，特别是当你创建大型或复杂的项目时。由于你正在模拟客户操作系统的硬件，取决于底层硬件，你的项目性能可能会轻微下降。

## GNS3 Workbench

有多个 GNS3 镜像供选择，但我推荐 GNS3 Workbench（[`rednectar.net/gns3-workbench/`](http://rednectar.net/gns3-workbench/)），如图 2-4 所示。开发者在界面简洁方面做得很好，配置也相当直观。由于基于 Linux 构建，GNS3 Workbench 预装了 GNS3、Wireshark 和 VPCS。它还包含许多练习和预配置的实验，以帮助你准备 Cisco 的 CCNA 认证考试。许多实验包含需要故障排除的问题，且目标明确。

图 2-4. GNS3 Workbench

GNS3 Workbench 假设用户具有少量的 Linux 经验，但某些 Linux 经验会有帮助。包含的 Linux 脚本可以帮助你安装 IOS，并且实验设计为仅需几个镜像即可运行。作为奖励，开发者包含了许多来自 GNS3 Vault 的练习。GNS3 网站（[`www.gns3.com/`](http://www.gns3.com/)）专注于 GNS3 相关内容，并为准备 CCNA 或 CCNP 认证的人员提供了练习。

## 安装 GNS3 Workbench

GNS3 Workbench 是免费的，仅以虚拟机的形式提供。不过，你可以导入镜像并使用 VirtualBox 运行设备。如果你想原生使用 VMware 运行设备，请访问其网站（[`www.vmware.com/`](http://www.vmware.com/)）并验证你的平台是否支持。否则，我建议使用 VirtualBox（[`virtualbox.org/`](http://virtualbox.org/)），因为它支持更多平台——特别是 Windows、Linux、FreeBSD 和 OS X——而且对所有人免费。

在开始之前，确保你的工作站有 10GB 的空闲磁盘空间，并且已经安装了 VirtualBox。要在 VirtualBox 下安装 GNS3 Workbench，请从 GNS3 网站（[`www.gns3.com/`](http://www.gns3.com/)）下载 GNS3 Workbench 设备并按照以下步骤操作：



1. 在 VirtualBox 启动屏幕中，点击**新建（New）**来创建一个虚拟机。向导打开后，点击**继续（Continue）**开始。

2. 为你的虚拟机命名，选择 `Linux` 作为操作系统，选择 `Ubuntu` 作为版本（如图 2-5 [#ch02.html_creating_a_new_ubuntu_linux_virtual] 所示），然后点击**继续（Continue）**。

![为 GNS3 创建新的 Ubuntu Linux 虚拟机](img/gatomoreillycomsourostarchimages2208883.jpg)

图 2-5. 创建一个新的 Ubuntu Linux 虚拟机

3. 根据需要调整内存设置并点击**继续（Continue）**进入虚拟磁盘对话框。然后，勾选**使用现有硬盘（Use existing disk）**单选按钮，点击黄色文件夹图标，浏览到你保存 GNS3 Workbench 文件的位置。选择名为 `GNS3 Workbench.vmdk` 的文件，确保**启动磁盘（Start-up Disk）**旁边有一个勾选，并点击**继续（Continue）**，如图 2-6 [#ch02.html_selecting_the_vmware_disk_image_to_use_w] 所示。这相当于从一台 PC 拆下硬盘并安装到另一台 PC 中。

![使用 VirtualBox 选择 VMware 镜像](img/gatomoreillycomsourostarchimages2208885.jpg)

图 2-6. 使用 VirtualBox 选择 VMware 镜像

4. 点击**下一步（Next）**和**完成（Complete）**结束安装。

5. 最后，启动 GNS3 Workbench 并安装增强功能（guest additions）。增强功能软件为你的新虚拟机提供硬件驱动程序。点击**设备（Devices）** ▸ **安装增强功能（Install Guest Additions）**并按照屏幕说明操作。在 FreeBSD 上，增强功能通过 `virtualbox-ose-additions` 软件包安装。

### 注意事项

如果你的主机 PC 有额外的 RAM，你可能想给 GNS3 Workbench 分配 2GB 的 RAM（或更多），而不是默认的 1GB。1GB RAM 对于 GNS3 来说是最低配置。增加可用内存将提高性能。

安装完成后，点击**启动（Start）**启动 Ubuntu。关于如何配置和使用 GNS3 Workbench 的指令将会出现。

## 结语

在本章中，你学习了 GNS3 可以安装在几乎任何操作系统上，而且你不需要计算机科学博士学位就能完成它。这并不意味着它在每个系统上的安装过程都同样容易。例如，某些 Linux 发行版可能根本没有 GNS3 软件包（或者可用软件包可能过旧，无法满足你的需求），但这就是开源软件的魅力所在：你可以直接从源码安装。

# 第 3 章 配置

安装 GNS3 只是第一步，下一步是配置。在本章中，你将学习如何配置 GNS3 以构建网络实验。

## 获取 IOS 镜像

安装 GNS3 是通往配置道路的第一步；在本章中，我们将介绍如何配置 GNS3 以运行 Dynamips。在启动路由器之前，你需要至少一个 IOS 镜像。IOS 是 Cisco 系统的知识产权，不向公众。此外，由于法律原因，GNS3 开发者无法为你提供 IOS 镜像。

获取 IOS 镜像最简单的方法是从你拥有的 Cisco 路由器复制镜像。这种方法的优点是你不是在偷窃镜像；缺点是 GNS3 只支持数百种型号中的几种，你的路由器可能不是其中。

### 使用 FTP

要将 IOS 镜像从路由器复制到工作站，登录路由器并使用 Cisco `copy` 命令将文件从路由器的闪存复制到 FTP 服务器。如果你不知道 IOS 镜像名称，可以在路由器上使用 `show flash` 命令。在以下示例中，IOS 镜像名为 `c7200-ios-version.bin`；我的 FTP 服务器位于 IP 地址为 `192.168.1.25` 的 PC 上，我的 FTP 用户名和密码分别为 `jason` 和 `mypass`。

```
## copy flash:c7200-ios-version.bin ftp://jason:mypass@192.168.1.25
```

当从路由器执行该命令时，镜像文件将从路由器的闪存复制到运行在 `192.168.1.25` 上的 FTP 服务器。

如果你想用 TFTP，请从 Jounin 网站下载免费的 TFTP 服务器（[`tftpd32.jounin.net/`](http://tftpd32.jounin.net/)）。当服务器安装并运行时，使用以下 `tftp` 命令将文件从你的路由器复制到你的 TFTP 服务器：

```
## copy flash:c7200-ios-version.bin tftp
远程主机的地址或名称 []? 192.168.1.25
目标文件名 [c7200-ios-version.bin]? <enter>
```

在`目标文件名 [c7200-ios-version.bin]`后按回车键完成复制。

另一方面，如果你没有拥有 Cisco 路由器，还有其他不那么正当的方法来寻找 IOS 镜像文件，你通过简单的互联网搜索一定能找到它们。虽然像 Cisco 和 Juniper 这样的公司过去对这类行为视而不见（只要软件仅用于教育目的），但你可能不想使用盗版的 Cisco IOS。这些镜像可能可能运行得很好，但始终存在它们可能包含恶意软件或以意料之外的方式被篡改的风险。

最后，如果你在一家恰好是 Cisco 合作伙伴的大型公司工作，你应该能够使用你的合作伙伴凭据登录 Cisco 网站并获取你需要的任何 IOS 镜像。请注意，这种活动可能会导致你被送上公司的绞刑架，因此在使用公司账户之前请获得许可。

无论你通过何种方式获得 IOS 镜像，你只能使用为 GNS3 支持的路由器型号设计的镜像文件，而且对于特定型号，某些 IOS 版本可能比其他版本更好。如果你发现 Dynamips 路由器运行得很奇怪，尝试将 IOS 更为不同的版本，因为这通常可以解决问题。

### 注意

通常情况下，请远离 `c26xx` 镜像，因为它们看起来是最稳定的！

选择正确的路由器和 IOS 镜像对于创建稳定的项目至关重要。推荐的 IOS 版本是 `c36xx`、`c37xx` 和 `c7200`（但不是 `c7200p`），因为这些是 Dynamips 和 GNS3 最稳定的版本。也要考虑 IOS 版本号。虽然新的 IOS 版本提供了最新的功能，但旧版本倾向于使用更少的 PC 资源，例如处理器和内存。如果你正在为 CCNA 学习创建简单的项目，你可能想使用 `12.2` 或 `12.3` 系列的旧版 IOS 以节省资源，但如果你正在准备 CCIE 考试，你可能需要安装最新的 IOS。

## 设置你的第一台 IOS 路由器

一旦有了 IOS 镜像，在开始使用虚拟路由器之前你需要完成几件事。首先，验证 Dynamips 的路径（这适用于 Linux）。接下来，将你的 IOS 镜像拷贝到文件夹中，然后将镜像添加到 GNS3。最后，为你添加到 GNS3 的每个 IOS 镜像设置 Idle-PC 值。现在我将引导你完成这些步骤。

## 配置 Dynamips

在 Windows 和 OS X 上，设置应该已经为你配置好了，但在 Linux 上，你应该验证 Dynamips 应用程序的路径是否正确。转到 `Edit（编辑）` ▸ `Preferences（首选项）`，选择 `Dynamips`，并点击 `General settings（常规设置）`选项卡，如图图 3-1 所示。

验证 `Path to Dynamips` 字段指向 `/usr/local/bin/dynamips`。如果你将程序安装在其他目录下，请将路径设置为该目录。

![Dynamips preferences, General settings tab](img/httpatomoreillycomsourcenostarchimages2208887.png.jpg)

图 3-1. Dynamips preferences, General settings tab

接下来，点击 `Advanced settings（高级设置）`选项卡以显示图 3-2 所示设置。

![Dynamips preferences, Advanced settings tab](img/httpatomoreillycomsourcenostarchimages2208889.png.jpg)

图 3-2. Dynamips preferences, Advanced settings tab

Dynamips 高级设置选项大多与 Dynamips 的稳定内存使用有关。原则上，你不应该更改它们，但我将讨论这些选项以便你自行决定。

内存使用优化设置完全关乎节省 PC 内存。Dynamips 每个路由器使用的内存越少，你就可以在项目中添加更多的路由器。`Enable ghost IOS support（启用 ghost IOS 支持）`选项通过分配一个多个路由器可以使用的共享内存区域来减少 PC 中的内存消耗，只要它们运行相同的 IOS 镜像。这是在项目中多次使用相同路由器模型的良好理由；使用具有不同 IOS 版本的多个模型将消耗更多的 PC 内存。`Enable mmap support（启用 mmap 支持）`选项允许路由器内存的内容写入硬盘上的文件，类似于缓存或交换文件。`Enable sparse memory support（启用稀疏内存支持）`选项减少路由器使用的虚拟内存量，以便每个 Dynamips 进程可以运行更多的路由器实例。

## 向 GNS3 添加 IOS 镜像

在使用 IOS 路由器创建项目之前，先向 GNS3 添加至少一个 IOS 镜像。要添加 IOS 镜像，在 Windows 和 Linux 上选择 `Edit（编辑）` ▸ `Preferences（首选项）`，在 OS X 上选择 `GNS3` ▸ `Preferences（首选项）`。从左侧面板展开 `Dynamips` 并点击 `IOS routers（IOS 路由器）`，如如图图 3-3 所示。

![IOS routers preferences](img/httpatomoreillycomsourcenostarchimages2208891.png.jpg)

图 3-3. IOS routers preferences

点击 `New（新建）`启动向导，然后点击 `Browse（浏览）`按钮找到你的镜像文件。选择镜像文件后，系统会询问你是否想要解压 IOS 镜像，如图图 3-4 所示。

![Deciding to decompress the image](img/httpatomoreillycomsourcenostarchimages2208893.png.jpg)

图 3-4. Deciding to decompress the image

建议让 GNS3 解压镜像；否则路由器每次加载时都必须解压。解压镜像后，点击 `Next（下一步）`，GNS3 将尝试识别 IOS 所属的平台，如图图 3-5 所示。

![Name and platform screen](img/httpatomoreillycomsourcenostarchimages2208895.png.jpg)

图 3-5. Name and platform screen

GNS3 已确定我的镜像文件属于 `c3745` 路由器平台并自动命名为 `c3745`。如果你认为这不正确，可以使用下拉菜单选择其他平台，但根据我的经验，GNS3 处理得很好。你可以通过在 `Name` 字段中输入名称为你的路由器命名。

通常，从这里你可以直接点击所有的配置设置来配置基础路由器模型，但向导在此过程中提供了让你自定义路由器内存和其他功能的机会。现在，点击 `Next（下一步）`继续。你将看到如图 3-6 所示的 Memory 屏幕。

![IOS Memory screen](img/httpatomoreillycomsourcenostarchimages2208897.png.jpg)

图 3-6. IOS Memory screen

你的路由器使用默认内存设置应该运行良好。但如果不确定，点击 `Check for minimum RAM（检查最小内存）`，GNS3 将启动网络浏览器并带你进入 [`www.cisco.com/`](http://www.cisco.com/) 上的 Cisco Feature Navigator 网页。在这里，你可以搜索你的 IOS 镜像特定的内存需求。将该值输入 `Default RAM` 字段。完成后，点击 `Next（下一步）`，你将看到如图 3-7 所示的网络适配器屏幕。

![Network adapters screen](img/httpatomoreillycomsourcenostarchimages2208899.png.jpg)

图 3-7. Network adapters screen

默认设置将您的路由器配置为与真实的 Cisco 路由器型号相同的标准选项。如果您想添加更多接口，请使用可用插槽旁的下拉菜单并选择所需的网络模块。插槽选项将限于真实版 Cisco 路由器可提供的实际选项。完成后，点击 `Next` 并选择您想要安装的任何 WIC 模块。然后再次点击 `Next` 显示 Idle-PC 屏幕，如图图 3-8 所示。

![Idle-PC screen](img/httpatomoreillycomsourcenostarchimages2208901.png.jpg)

图 3-8. Idle-PC 屏幕

如果您在 GNS3 中启动路由器时没有设置 Idle-PC，您电脑的 CPU 使用率将迅速飙升至 100% 并保持在该。这是因为 Dynamips 尚不知道虚拟路由器是否正在执行需要系统资源的操作，因此它会通过提供所有能提供的资源来过度补偿。在纠正这一点之前，GNS3 运行将会变得缓慢，如果 CPU 使用率长时间保持在 100%，您的电脑处理器可能会过热。

您可以轻松地修复此，让 GNS3 在 IOS 程序代码中寻找是否存在空闲循环（空闲循环会导致 CPU 飙升）；此计算结果被称为 `Idle-PC value`。当应用了正确的 Idle-PC 值时，Dynamips 应该在执行这些空闲循环时定期让路由器`睡眠`，这极大地降低了 CPU 使用率。如果您不在乎所有细节，只需记住 Idle-PC 值是防止 Dynamips “吃掉”您的处理器的关键。

要让 GNS3 自动查找值，点击 `Idle-PC finder` 按钮，GNS3 将尝试搜索一个值。如果 GNS3 找到了合适的值，您就完成了；点击 `Finish`。如果未成功，请留空该字段并点击 `Next` 以保存没有 Idle-PC 配置的路由器。

## 设置手动 Idle-PC 值

如果 GNS3 无法自动找到 Idle-PC 值，您将需要手动查找。您只需要为每个 IOS 镜像计算一次 Idle-PC 值。GNS3 会将此设置应用到`所有`使用该镜像文件的虚拟路由器。关闭首选项（Preferences）窗口，从设备工具栏将路由器拖到 GNS3 工作空间，如图图 3-9 所示。

![Adding a router to a blank workspace](img/httpatomoreillycomsourcenostarchimages2208903.png.jpg)

图 3-9. 向空白工作区添加路由器

接下来，通过右键点击路由器图标并选择 `Start` 来启动路由器；然后立即右键点击路由器并选择 `Console` 以验证 IOS 是否正确加载。一个 Cisco 控制台窗口将打开并显示路由器的启动信息。如果路由器启动正常，您就可以开始 Idle-PC 计算了；如果没有，请确保分配给路由器的型号和默认 RAM 设置正确，或者尝试不同的 IOS 镜像。

如果您正在运行 Linux 并在选择 `Console` 后没有出现 Cisco 控制台，请检查您的 GNS3 控制台设置。进入 `Edit` ▸ `Preferences`，点击 `General` 并选择 `Console applications` 选项卡，如图图 3-10 所示。

使用预配置（Preconfigured）命令下拉菜单，选择您的 Linux 终端类型，然后点击 `Set`、`Apply` 和 `OK`。

当路由器启动时，您电脑的 CPU 使用率将迅速激增至 100%。监控您的 CPU 使用率，以便在设置 Idle-PC 值后验证 CPU 使用率是否已经稳定。在 Windows 上，按下 CTRL-ALT-DEL 并点击 `Task Manager` 显示 CPU 使用率。在 OS X 上，从 `Applications/Utilities` 文件夹打开活动监视并点击`CPU`。在 Linux 系统上，使用系统监器（System Monitor）或在终端输入 `top`。

![Choosing a Console application using Ubuntu Linux](img/httpatomoreillycomsourcenostarchimages2208905.png.jpg)

图 3-10. 使用 Ubuntu Linux 选择控制台程序

要开始计算值，右键点击路由器并在菜单中选择 `Idle-PC`，如图图 3-11 所示。

GNS3 现在应该计算 Idle-PC 值并提供一个或多个值供选择。这可能需要一分钟，所以给它一点时间在 Idle-PC values 窗口中显示结果，如图图 3-12 所示。

如果给定值旁边有一个星号（`*`），则 GNS3 认为该值是最好的，您应该选择它。点击 `Apply` 进行选择。

![Manually calculating Idle-PC values](img/httpatomoreillycomsourcenostarchimages2208903.png.jpg)

图 3-11. 手动计算 Idle-PC 值



![Idle-PC values](img/httpatomoreillycomsourcenostarchimages2208909.png.jpg)

图 3-12. Idle-PC 值

你不仅可以保存多个项目，还可以保存整个项目配置的多个快照。`snapshot`（快照）保留了你项目的网络布局以及在特定时刻所有路由器配置的状态。你可以随时需要恢复快照，将整个项目回滚到拍摄快照时的状态。

### 注意

快照非常适用于练习 CCNA 或 CCNP 配置演练。你可以创建一个实验室，应用演练所需的节点路由器配置（如网络地址、路由协议等），然后拍摄快照。一旦你拥有了基础设置的快照，就可以练习将场景目标应用到网络中了。如果你以后想再次练习相同的任务，可以恢复到基础快照，你的路由器将无需额外配置即可准备就绪。

GNS3 还赋予了你管理虚拟硬件的能力。就像使用真实路由器一样，你可以使用 Cisco 扩展模块来升级你的虚拟路由器。你可以添加广泛的功能，例如额外的随机访问存储器（RAM）、以太网接口、串口端口、异步传输模式（ATM）和基于 SONET 的分组传输（POS）端口。

## 术语

在开始之前，让我们先探索一些重要的术语。你需要了解拓扑结构（topology）和项目（project）之间的区别。`topology` 文件是一个以 `.gns3` 结尾的文本文件，主要指的是设备及其之间的链路。`project` 是用户定义的项目文件夹（例如 `MyLab`），存储在 `GNS3/projects` 文件夹内。用户项目文件夹包含一个名为 `<project_name>.gns3` 的拓扑文件、路由器配置、非易失性随机访问存储（NVRAM）的内容以及其他保存的信息。换句话说，它代表了整个网络，包括拓扑和所有设备配置。

另一个你应该熟悉的术语是 `node`（节点）。在计算机网络中，节点是连接到网络的任何设备。在 GNS3 中，节点是设备工具栏上的任何设备。

为了有效地管理设备和项目，你需要的不仅仅是词；还需要熟悉 GNS3 的屏幕布局。

## 屏幕布局

让我们看看标准的 GNS3 布局（如图 4-1），并定义程序使用的几个概念。

![GNS3 工作区中显示两个路由器和一个交换机的屏幕布局](img/httpatomoreillycomsourcenostarchimages2208911.png.jpg)

图 4-1. GNS3 工作区中显示两个路由器和一个交换机的屏幕布局

- **➊ GNS3 工具栏**：一组用于方便执行常用任务的图标。
- **➋ 设备工具栏**：用于添加路由器、交换机、终端设备和安全设备，以及创建设备之间的链路。要创建拓扑结构，从工具栏中选择设备类型，并将设备从设备窗口拖到你的工作区。设备有两种类型：模拟（simulated）和仿真（emulated）。`simulated` 设备模拟真实设备的所有特征（如以太网交换机节点），并且不运行操作系统。`emulated` 设备仿真真实设备的硬件，需要操作系统才能运行（如运行 Cisco IOS 的虚拟 Dynamips 路由器）。
- **➌ 控制台（Console）**：命令行界面，你可以在其中管理设备的各个方面。
- **➍ 拓扑摘要**：显示你项目中设备的状态。设备旁边的绿色圆圈表示设备已启动，红色圆圈表示设备已停止，黄色圆圈表示设备已挂起。模拟设备（如以太网交换机节点）始终是绿色的。要查看特定设备上使用的链路，点击设备名称旁三角形。
- **➎ 工作区（Workspace）**：你设计网络的区域。从设备工具栏将设备拖到工作区并将它们连接起来。

现在你已经了解 GNS3 主屏幕的样式了，让我们仔细看看你在那里能找到的选项。

# 使用 GNS3 工具栏

GNS3 工具栏包含几组图标，大致按功能组织，并提供了完成任务的简单方法。第一组处理项目，第二组处理链路，第三组处理设备和快照，第四组则提供视觉化组织项目的其他方法。

## 第一组工具栏

第一组工具栏图标所示于图 4-2，涉及影响整个项目的操作。

![第一组工具栏](img/httpatomoreillycomsourcenostarchimages2208913.png.jpg)

图 4-2. 第一组工具栏

从左到右，这些图标如下：

- **新建空白项目（New blank project）**：创建一个新的项目文件夹并允许选择选择名称。
- **打开项目（Open project）**：打开之前保存的项目。
- **保存项目（Save project）**：将你的路由器配置和项目保存到 `GNS3/projects` 文件夹。

## 第二组工具栏

第二组工具栏图标所示于图 4-3，允许你创建快照、显示或隐藏接口标签以及连接到设备。

![第二组工具栏](img/httpatomoreillycomsourcenostarchimages2208915.png.jpg)

图 4-3. 第二组工具栏

从左到右，这些图标如下：

- **快照（Snapshot）**：对你的设备、链路和配置拍摄快照，以记录当时工作区的状态。你可以保存多个快照并在任何时间恢复。选项有：创建、删除、恢复和关闭。
- **显示接口标签（Show interface labels）**：显示或隐藏链路使用的接口名称。这些标签以缩写形式显示在设备旁（例如 `f0/0`）。
- **控制台（Console）**：打开工作区中所有路由器的控制台连接。

### 注意

当你打开所有设备的连接时，除非你的终端支持标签页，否则屏幕可能会变得混乱。在处理大型拓扑结构时，通过右键点击设备并选择控制台按需要打开和关闭单个会话可能会更容易。

## 第三组工具栏

第三组工具栏图标所示于图 4-4，主要用于控制设备。

![第三组工具栏](img/httpatomoreillycomsourcenostarchimages2208917.png.jpg)

图 4-4. 第三组工具栏

从左到右，这些图标如下：

- **启动/恢复所有设备（Start/Resume all devices）**：启动工作区中所有停止的设备或恢复所有挂起的设备。
- **挂起所有设备（Suspend all devices）**：将所有支持挂起的设备处于挂起状态。
- **停止所有设备（Stop all devices）**：停止所有设备。
- **重新加载所有设备（Reload all devices）**：重新加载所有设备。重新加载之前务必保存你的路由器配置和项目，否则可能会丢失配置！

## 第四组工具栏

最后一组工具栏图标所示于图 4-5，提供了更清晰展示网络布局的工具。你可以在项目中添加矩形和椭圆等对象，甚至可以生成工作区的截图。

![第四组工具栏](img/httpatomoreillycomsourcenostarchimages2208919.png.jpg)

图 4-5. 第四组工具栏

从左到右，最后一个工具栏组中的图标如下：

- `Add a note`：在您的工作区中创建文本注释。双击文本可以修改，右键点击文本对象可以更改 `Style` 属性（如字体大小和颜色）。您还可以将文本对象旋转 0 到 360 度。
- `Insert a picture`：向您的项目添加图像和徽标。GNS3 支持 PNG、JPG、BMP、XPM、PPM 和 TIFF 文件格式。
- `Draw a rectangle`：绘制动态调整大小的矩形。您可以右键点击矩形对象来更改边框和边框颜色的 `Style` 属性。矩形对象可以进行 0 到 360 度的旋转。
- `Draw an ellipse`：绘制动态调整大小的椭圆。您可以右键点击椭圆对象来更改边框样式和颜色。
- `Zoom in`：放大工作区以查看细节。
- `Zoom out`：缩小工作区以获得更广阔的视角。
- `Screenshot`：生成工作区的截图。该图像可以保存为 PNG、JPG、BMP、XPM、PPM 或 TIFF 文件，默认保存位于您的 `GNS3/projects` 文件夹中。

### 窗口样式与停靠

GNS3 提供了多种窗口样式供选择。要更改默认样式，在 Linux 和 Windows 上选择 `Edit` ▸ `Preferences`，在 OS X 上选择 `GNS3` ▸ `Preferences`。选择 `General` 类别，选择 `General` 选项卡，使用 Style 下方的下拉菜单选择您的新默认样式。点击 `Apply` 和 `Okay` 激活您的更改。GNS3 会在程序重启后记住您的选择。

另一方面，窗口停靠是环绕 GNS3 工作区域的窗口。GNS3 默认显示 `Console` 和 `Topology Summary` 停靠。

要查看或隐藏窗口停靠，选择 `View` ▸ `Window Docks` 并选择您想要显示的停靠；任何名称旁带有复选标记的停靠都应显示在屏幕上。要调整停靠的大小，点击停靠窗口与工作区连接的边界，并拖动边界直到达到所需尺寸。

您添加到工作区的对象（注释、图片和形状）可以分层分组。要提高或降低对象，右键点击该对象并选择 `Raise one layer` 或 `Lower one layer`。此功能允许您在不影响其他层的情况下操作某层中的对象。可以通过菜单菜单选择 `View` ▸ `Show Layers` 显示对象的层位置，这在高级层操作期间非常有用。

通过此工具栏添加形状和颜色，您可以将网络组件划分为逻辑组。通过文本，您可以添加关于项目配置的注释和提醒。图 4-6 显示了您如何使用形状、颜色和注释文本消息更清晰地展示信息。

![Sample project with annotations](img/httpatomoreillycomsourcenostarchimages2208921.png.jpg)

图 4-6. 带有注释的示例项目

一旦您创建了几个项目，很容易忘记是如何配置它们的或您的目标是什么。添加注释（如图 4-6 中非常有用的注释）是快速提醒自己这些信息的简单方法，特别是在几周或几个月之后。注释太棒了——用起来吧！

# 使用设备工具栏

设备工具栏（如图 4-7 所示）按功能组织设备。点击设备工具栏上的图标查看该设备组中的所有设备。

![Devices toolbar](img/httpatomoreillycomsourcenostarchimages2208923.png.jpg)

图 4-7. 设备工具栏

要向您的项目添加设备节点，点击设备工具栏上的图标显示已配置设备列表，然后将设备拖入工作区。您可以按 `SHIFT` 键添加多个相同的设备。从左到右，工具栏中的设备类型如下：

- `Routers`：显示所有已配置有效 IOS 镜像文件的可用 Dynamips 路由器节点，以及 IOU L3 路由器。
- `Switches`：显示所有可用交换机节点，包括以太网交换机、以太网集线器、ATM 交换机、帧中继交换机、EtherSwitch 路由器和 IOU L2 交换机。
- `End Devices`：显示所有可用终端设备，包括 QEMU 访客、VirtualBox 访客、主机和云。
- `Security Devices`：显示所有可用安全设备，包括 ASA 防墙、IDS/IPS 以及您创建的任何自定义节点。
- `Add a Link`：选择此项时，鼠标指针将变为十字准，表示您可以使用虚拟接口连接两个设备。要连接设备，点击第一个设备并选择一个接口；对第二个设备重复操作以完成连接。

现在点击 `All Devices` 图标，您应该看到一个包含 GNS3 中所有配置设备的窗口。您可以将任何设备拖入工作区并使用它们。

# 创建第一个项目

现在您已经熟悉了 GNS3 界面，让我们深入研究一些项目管理。我将介绍最简单的方法，但请记住 GNS3 通常提供多种处理问题的方法。

当启动 GNS3 时，会出现一个新项目窗口，如图 4-8 所示。在这里，您可以打开现有项目或创建一个新项目。

![New project window](img/httpatomoreillycomsourcenostarchimages2208925.png.jpg)

图 4-8. 新项目窗口

要创建新项目，将 `untitled` 替换为您的项目名称并点击 `OK`。如果您已经在 GNS3 中，选择 `File` ▸ `New` 创建新项目。

## 使用路由器

通过从设备工具栏将路由器拖到 GNS3 工作区开始项目。如果您在添加设备时按下 `SHIFT`，您应该看到一个允许添加多个相同设备的对话框。尝试用这样添加第一对路由器。如果在设备工具栏上没有看到任何路由器，请参考设置第一个 IOS 路由器学习如何将设备添加到 GNS3。

将路由器添加到工作区后，它们应被自动命名为 R1 和 R2。路由器名称来自 GNS3 文件 `ios_base_startup-config.txt` 中的 `hostname %h` 命令。该文件包含应用于您所有路由器的默认 IOS 设置，并在使用 IOS 镜像文件配置时将其分配给设备。要定位 Dynamips 配置文件，转到 **Preferences**，从左侧面板选择 `Dynamips`，然后选择 `IOS Routers`。选择已配置的路由器并点击 `Edit` 显示 Dynamips IOS 路由器配置选项，如图 4-9 所示。

从这里开始，你可以验证设备启动配置（startup-config）和私有配置（private-config）文件的路径。当路由器被放置在你的工作区时，`startup-config` 文件 `ios_base_startup-config.txt` 的内容将应用于路由器启动配置，并在路由器启动时加载到路由器的运行配置中。如果你想创建全局应用于路由器的自定义参数（例如，自动启动接口或使用预留的用户名和密码），可以使用文本编辑器修改并保存 `ios_base_startup-config.txt` 文件。只要你的 IOS 支持，你就可以对该文件应用任何合法的 Cisco IOS 命令。你可能不需要修改 `ios_base_private-config.txt` 文件。该文件由 GNS3 安装，以便你在路由器重启之间使用安全外壳（SSH），而无需在路由器上重新生成加密密钥。

![Dynamips IOS 路由器配置对话框](img/httpatomoreillycomsourcenostarchimages2208927.png.jpg)

图 4-9. Dynamips IOS 路由器配置对话框

需要注意的是，你所所的更改仅应用于你添加到新项目的路由器，而无法追溯地应用于之前保存项目中的路由器。

## 警告

在修改 `ios_base_startup-config.txt` 文件之前，你可能想保存一个备份副本。如果你输入了无效命令，你的路由器可能会产生错误并异常运行。

## 在路由器之间创建链接

在工作区中放置设备后，你需要在它们之间添加链接，以创建一个功能完整的网络。这等同于为真实网络布线，不同之处是你使用的是虚拟电缆而不是物理电缆。要为你的设备添加链接，请点击设备工具栏中的“添加链接（Add a link）”图标。你的光标应该变为十字准星，表示你可以选择设备。要创建链接，点击一个设备。你将看到一个可用接口的下拉菜单，如图 4-10 所示。

![具有两个 FastEthernet 接口的路由器](img/httpatomoreillycomsourcenostarchimages2208929.png.jpg)

图 4-10. 具有两个 FastEthernet 接口的路由器

接口旁边的红色圆圈表示该接口可用；绿色圆圈表示该接口已被现有链接占用。选择任何可用接口以建立链接，然后在另一个设备上选择一个接口以完成连接。你可以在两个兼容的接口类型之间创建连接。换句话说，就像物理硬件一样，你不能将串行线插到以太网接口中。

在某个时刻，你可能想要断开两个设备之间的链接以模拟故障、重新配置网络或其他原因。要断开两个设备之间的链接，右键点击该链接并选择“删除（Delete）”，如图 4-11 所示。

![删除设备间的链接](img/httpatomoreillycomsourcenostarchimages2208929.png.jpg)

图 4-11. 删除设备间的链接

要重新链接，再次点击“添加链接（Add a link）”图标并选择相同的设备。

## 配置虚拟硬件

当你向工作区中放置虚拟路由器时，它们具有与配置设备 IOS 镜像时所相同的配置选项。但这并不意味着你的路由器受限于此配置。就像 PC 一样，Cisco 路由器具有扩展端口以提供额外功能，GNS3 Dynamips 路由器提供了与其物理对应物相同的扩展选项。要修改路由器的硬件配置，右键点击路由器并选择“配置（Configure）”，然后点击节点名称（例如 `R1`），如图 4-12 所示。

![Cisco IOS 路由器节点配置器对话框](img/httpatomoreillycomsourcenostarchimages2208927.png.jpg)

图 4-12. Cisco IOS 路由器节点配置器对话框

在节点配置器对话框中，你应该看到该型号路由器的可用配置选项。基础模型仅允许添加简单选项，例如 Cisco `SLOT`、`WIC` 或 `RAM` 卡，而高级模型允许你定义功能，例如机箱类型或网络处理引擎（NPE）类型（这些可以在 Cisco 7200 系列路由器中找到）。

你可以对第 3 章 中涵盖内存和插槽配置并应用相同的设备选项，但你在此处的更改仅应用于你在项目中选择的设备或设备组。所有其他设备将不受影响。

## 启动、停止和暂停路由器

我已经向你展示了如何通过右键点击路由器并选择“启动（Start）”或“停止（Stop）”来启动停止路由器，但你也可以通过右键点击路由器并选择“暂停（Suspend）”。当你想要模拟故障而无需经历保存配置、停止路由器并重启的过程时，暂停路由器非常方便。事实上，反复停止和重启 GNS3 路由器可能会导致某些 IOS 版本崩溃，因此我建议使用暂停。

暂停功能在网络测试中确实非常出色。你可以快速模拟故障和恢复，以测试如 `RIP`、`EIGRP` 和 `OSPF` 等协议，以及 `HSRP`、`VRRP` 和 `GLBP` 等冗余协议。要模拟故障，点击“暂停（Suspend）”并监控其他路由器以验证切换是否发生。



要模拟恢复，通过右键点击设备并选择“启动（Start）”来恢复路由器。由于 `Dynamips` 的吞吐量限制，收敛可能比你使用真实硬件时慢一些。不要担心——这完全正常。

当然，即使你可以启动和停止路由器，在登录控制台之前，你无法对它们做什么。

## 登录路由器

你使用模拟的控制台端口登录路由器。如果这听起来很熟悉，这也是你登录实际设备的方法。在物理硬件上，控制台是你插入 Cisco 蓝色控制线的地方。在打开控制台连接之前，确保路由器已启动；否则你将无法控制台屏幕。

### 配置终端设置

无论你运行 Windows、OS X 还是 Linux，都有多种供 GNS3 使用的终端类型。但为什么你会倾向于其中一个而不是另一个呢？原因可能是它位于你的系统中。例如，在 Linux 上，你可能在使用 Gnome 桌面，它默认安装了 `gnome terminal`。在这种情况下，你可能想修改 GNS3 终端设置为使用 `gnome terminal`。另一个原因是某些终端程序提供的功能更多。你可能想选择一个支持标签页窗口的终端类型，这样你就可以同时打开多个控制台而不会让大量窗口弄乱屏幕。

要修改终端设置，转到“首选项（Preferences）”，点击“常规（General）”，然后点击“控制台应用程序（Console applications）”选项卡以显示如图 4-13 所示的窗口。

![终端设置](img/httpatomoreillycomsourcenostarchimages2208935.png.jpg)

图 4-13. 终端设置

从这里开始，你可以选择预定义的终端类型，并在控制台（Console）应用下自定义命令设置。（请检查您的终端应用程序文档以了解您的系统上可用哪些选项。）完成后，点击 `Set`，然后点击 `Apply` 和 `OK`。

要一次性登录所有路由器，请点击第二个工具栏组中的 `Console connect to all devices` 图标（参见图 4-3）。若要登录单个路由器，请在工作区中右键点击路由器节点，并从菜单中选择 `Console` 或 `Auxiliary console`（参见图 4-14）。

要更改路由器控制台或 AUX 端口监听的传输控制协议 (TCP) 端口号，请在工作区中右键点击设备，点击 `Configure` 并选择 `General` 标签页。您选择的端口号对于 GNS3 中的每个设备以及您的 PC 必须是唯一的。按照原则，除非必要，否则我尽量不去动端口号。GNS3 在管理这些端口方面做得很好，乱动它们可能会带来很多麻烦。但如果您的 PC 上运行的其他 TCP/IP 恰好与 GNS3 冲突，您可能在登录路由器之前需要进行一些更改。

![选择 Console 或 Auxiliary console 连接到路由器](img/httpatomoreillycomsourcenostarchimages2208937.png.jpg)

图 4-14. 选择 Console 或 Auxiliary console 连接到路由器

### 注意事项

*在您的 PC 上使用 `netstat` 命令来验证哪些 TCP/IP 端口已被占用。*

一旦建立了与路由器的控制台连接，您应该会看到熟悉的 Cisco 控制台窗口。

```
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
Connected to Dynamips VM "R1" (ID 1, type c3725) - Console port
Press ENTER to get the prompt.
ROMMON emulation microcode.

Cisco 1720 (MPC860) processor (revision 0x202) with 55206K/9830K bytes of memory.
Processor board ID FTX0945WOMY (4279256517), with hardware revision 000
M860 processor: part number 0, mask 0
Bridging software.
X.25 software, Version 3.0.0.
1 FastEthernet/IEEE 802.3 interface(s)
32K bytes of non-volatile configuration memory.
4096K bytes of processor board System flash (Read/Write)

SETUP: new interface FastEthernet0 placed in "shutdown" state

Press RETURN to get started!
00:00:02: %LINK-5-CHANGED: Interface FastEthernet0, changed state to administratively down
00:00:03: %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0, changed state to down
R1#
```

此时，您可以开始使用标准的 IOS 命令来配置路由器。一个看起来可能很奇怪的命令是 `show flash` 命令。通常，此命令显示保存在闪存中的文件，例如路由器的 IOS 镜像文件以及来自 Cisco 的其他默认文件。但在 GNS3 中，您会发现默认这里没有保存任何文件。此外，闪存驱动可能是未格式化的；如果是是的话，您需要在执行 `erase flash:` 命令之前才能将文件保存到闪存中。否则，您可能会收到类似下面的错误：

```
%Error opening slot0:router-confg (Bad device info block)
```

### 注意事项

*如果您使用 NM-16ESW 交换机模块，您可能在创建 VLAN 之前必须清除路由器的闪存；否则，VLAN 数据库 (`vlan.dat`) 将无法保存。*到目前为止本节一直是 Dynamips 路由器，但您也可以在 GNS3 项目中使用交换机，我将在接下来介绍。

# 以太网交换机节点

以太网交换机节点是一个仿真虚拟交换机，允许您创建 VLAN 访问端口和中继端口（trunk ports）。以太网交换机节点支持访问端口、行业标准 802.1Q 中继端口以及 QinQ 标记。然而，它不支持 Cisco 专有的交换机链路 (ISL) 中继协议。

要使用以太网交换机节点，请将节点拖到工作区。您永远不需要启动以太网交换机节点；它们始终准备可用。

要配置交换机，请右键点击 `Ethernet switch node` 图标并选择 `Configure`。使用图 4-15 所示的节点配置窗口，点击交换机名称（例如 SW1）来修改默认交换机端口或添加新端口。

默认情况下，有八个访问端口分配给 VLAN 1。要更改端口，点击端口号并根据需要修改设置。

![以太网交换机节点配置窗口](img/httpatomoreillycomsourcenostarchimages2208939.png.jpg)

图 4-15. 以太网交换机节点配置窗口

# 修改符号和组织设备

您可以更改用于表示工作区中设备的符号，并选择它们在“设备”工具栏中的位置。假设您想更改 IOS 路由器的符号。要更改设备符号，在 Linux 和 Windows 上选择 `Edit` ▸ `Preferences`，或在 OS X 上选择 `GNS3` ▸ `Preferences`。接下来，找到您想要更改的设备，右键点击设备并选择 `Change symbol`，如图 4-16 所示。

![修改符号](img/httpatomoreillycomsourcenostarchimages2208941.png.jpg)

图 4-16. 修改符号

可以使用相同的方法更改 IOU 设备、VirtualBox 虚拟机和 QEMU 虚拟机的符号。点击 `Change symbol` 后，将出现图 4-17 所示的符号选择窗口。

![符号选择和设备类别](img/httpatomoreillycomsourcenostarchimages2208943.png.jpg)

图 4-17. 符号选择和设备类别

要更改设备符号，在符号选择窗口中向下滚动并选择要使用的符号。接下来，使用下拉菜单选择一个类别。这是设备在“设备”工具栏中放置的类别。类别包括交换机、路由器、终端设备和安全设备。完成后，点击 `OK` 完成更改。

## 结语

在本章中，您学习了设置 GNS3 网络的的基础知识，因此现在是创建几个实验并练习您所学内容的好时机。如果您正在准备 Cisco 认证，尽可能多在 Cisco 设备上进行实际手操作是获得通过考试所需经验的唯一途径（它们很难的！）

首先在图 4-1 中创建网络。创建拓扑结构后，登录路由器，配置它们的接口，并尝试在它们之间进行 ping。使用 `suspend`（挂起）和 `resume`（恢复）功能，或者通过启动和停止设备来模拟故障和恢复。在探索了一些 `IOS` 命令和 GNS3 功能后，尝试创建一个包含三个或更多路由器的简单 CCNA 实验；网上有大量的 CCNA 和 CCNP 示例实验可用。

最后一点警告：如果你创建了使用多协议路由的大型拓扑结构，你可能会发现必须增加路由器的协议计时器，以防止接口反复出现启动和关闭状态。（这种情况很少见，但有时会发生。）该问题是由 `Dynamips` 内部固有的延迟引起的。串口连接是另一个常见问题区域；某些路由器镜像在模拟串口上运行时可能会不稳定。如果你发现路由器的串口端口出现异常（导致路由器崩溃或连接闪变），请尝试其他路由器模型或不同的 `IOS` 镜像。通常，`c36xx`、`c37xx` 和 `7200` `IOS` 镜像在 `Dynamips` 中最为稳定，应尽可能使用。

在第 5 章，你将探索使用 `Wireshark` 捕获网络包的基础，并通过使用 `VPCS`、`VirtualBox` 和 `Linux` 添加主机来扩展你的网络。

# 第 5 章集成主机和使用 Wireshark

到为止，你已经学习了如何使用 Cisco 设备创建网络，但 GNS3 的功能远不止此！它使用了一套强大的网络工具，允许你将外部应用程序集成到 GNS3 项目中。在本章中，你通过学习如何使用 `Virtual PC Simulator`（虚拟机 PC）和 `VirtualBox` 将 PC 主机集成到项目中来探索这些工具。本章还将涵盖使用 `Wireshark` 进行基础数据包嗅探。

## Virtual PC Simulator

向项目添加主机的方法之一是使用 `VPCS`，这是一个可以模拟多达九台类 DOS PC 的小型应用程序。`VPCS` 主机的命令有限，但非常适合测试跨 GNS3 网络的端到端连通性。`VPCS` 使用的 PC 资源极少，允许你向项目中添加大量主机而不会拖慢你的 PC。

### 安装 VPCS

如果你运行的是 Windows 或 OS X，在安装 GNS3 时应该已经包含了 `VPCS`。如果你使用的是 `Linux` 系统，`VPCS` 源代码应该包含在你的 GNS3 for Linux 下载包中，但在使用它之前需要对其进行编译。使用以下命令进行编译和安装，将 `x` 替换为你的 `VPCS` 源文件的版本号：

```
$ unzip vpcs-x.zip
$ cd vpcs-x/src
$ sh mk.sh
$ sudo cp vpcs /usr/local/bin/
```

要使用 `VPCS`，从设备工具栏的 `End Devices`（终端设备）拖入一个 `VPCS` 主机节点到你的工作区。在启动 `VPCS` 主机之前，它必须连接到项目中的另一个设备。启动 `VPCS` 主机并打开控制台后，你将看到一个类似于图 5-1 的窗口。

![VPCS 控制台](img/httpatomoreillycomsourcenostarchimages2208945.png.jpg)

图 5-1. VPCS 控制台

如果你没有看到 `VPCS` 控制台，或者你的应用程序显示错误，请验证程序是否存在于 `/usr/local/bin/`（在 `Linux` 上），以及 GNS3 偏好中是否正确设置了路径。开发者提供的支持或文档非常少，因此如果你继续遇到问题，你可能想要访问 GNS3 论坛 (`http://community.gns3.com/`) 获取可能的解决方案。

## VPCS 命令

`VPCS` 中的命令大部分是自显易懂的，但我在这里介绍其中几个以帮助你开始。要查看支持的命令的完整列表，你可以输入问号 `?`。要显示主机的配置，可以输入 `show` 命令。要显示特定命令的参数，输入命令名称后跟一个问号。例如，输入 `ping ?` 将显示 `ping` 命令的所有选项。

### 注意

与 Cisco `IOS` 一样，`VPCS` 支持缩写命令语法。例如，`ping` 命令可以输入 `p`。你可以缩写任何 `VPCS` 命令，但你必须输入足够的字母，使其与其他以相同字母开头的命令区分开。

## VPCS IP 地址分配

启动 `VPCS` 后，你需要配置主机以供 GNS3 使用。通常，这只需要设置 IP 地址、子网掩码和网关地址。

`VPCS` 支持 `IPv4` 和 `IPv6` 寻。你可以手动配置 IP 地址，或者如果 GNS3 项目中运行了动态主机配置协议 (`DHCP`) 服务器，则可以自动获取。要手动配置 `IPv4` 地址，你需要输入 `ip-address mask gateway`。以下示例将 `IPv4` 地址设置为 `192.168.1.50`：`ip-address 192.168.1.50 255.255.255.0 192.168.1.1`。你可以使用无类域路由 (CIDR) 表示法来代替子网掩码：`ip 192.168.1.50/24`。

要手动配置 `IPv6` 地址，输入 `ip` 后跟有效的 `IPv6` 地址和掩码。以下示例设置了 `2014:1a::50` 使用 `64` 位掩码：`ip 2014:1a::50/64`。

要使用 `DHCP` 自动配置主机，为需要地址的主机输入 `dhcp` 命令，如下所示：`dhcp`。

使用 `save` 命令在 GNS3 中保存你的 `VPCS` 设置。设置将保存在 `GNS3/projects/<project_name>/project-files/vpcs/<uuid>`。当你加载 GNS3 项目时，配置设置将应用于主机。要测试 `VPCS`，创建一个 `VPCS` 主机节点并连接到其他设备（如路由器）。为 `VPCS` 主机和其他设备分配 IP 地址，然后使用 `ping` 或 `trace` 测试连通性。如果一切顺利，你应该收到如例所示的回复：

```
PC1> ping 192.168.1.1
192.168.1.1 icmp_seq=1 ttl=255 time=35.821 ms
```

成功 ping 设备后，可以使用 `arp` 命令查看 ARP 缓存（MAC 地址到 IP 表），如下：

```
PC1> arp
cc:00:05:a9:00:00 192.168.1.1 expires in 114 seconds
```

如果 ping 失败，`VPCS` 会显示“主机不可达”的消息：

```
PC1> ping 192.168.1.1
host (192.168.1.1) not reachable
```

通过验证 GNS3 中的路由器接口是否启动以及检查所有 IP 地址和子网掩码是否正确分配来排除此问题。

另一个可能是 PC 的防火墙设置，特别是当你使用 Windows PC 时。通常，在使用 GNS3 时完全禁用防火墙是一个好主意，可能会解决此及其他问题。

## VirtualBox

VPCS 是向 GNS3 添加简单主机和测试连通性的极佳工具，但有时你需要一个运行真实操作系统而非模拟操作系统的主机。这就是 `VirtualBox` 大显用武之地。`VirtualBox` 可以运行大多数基于 PC 的操作系统，包括 Windows、`Linux`、`FreeBSD` 等。它也有用于运行网络操作系统，如 Arista `vEOS`、Juniper `Firefly` 和 `NX-OSv`。

使用 VirtualBox 的优势是它可以为你提供运行实际操作系统的主机；缺点是这些操作系统可能会消耗你 PC 大的大量资源。如果你只需要测试连通性，那么请继续使用 VPCS；但如果你需要一个提供强大网络工具集的主机（例如为了测试你的 GNS3 网络安全性），或者需要运行其他路由器或交换机操作系统，那么你可能想要使用 VirtualBox。

## 在 Windows 上安装

要在 Windows 上安装 VirtualBox，请从 VirtualBox 网站 `[`www.virtualbox.org/`](http://www.virtualbox.org/)` 下载相应的安装程序。启动安装程序，在看到欢迎界面时点击 `Next` 弹出自定义窗口。在此处进行任何所需的自定义，并按照屏幕上的指示完成安装。我建议接受默认值，以确保 VirtualBox 能够与 GNS3 正常运行。

安装完成后，你可以通过 Windows 开始菜单或点击 VirtualBox 图标来启动应用程序。

## 在 OS X 上安装

要在 OS X 上安装 VirtualBox，请从 VirtualBox 网站 `[`www.virtualbox.org/`](http://www.virtualbox.org/)` 下载相应的安装程序并启动它。当 VirtualBox 安装界面出现时，双击 `VirtualBox.pkg` 图标并按照屏幕上的指示操作。安装需要管理员权限，因此请准备好你的管理员密码。软件包安装完成后，你可以从 `Applications` 文件夹中双击 VirtualBox 图标来启动它。

# 在 Linux 上安装



VirtualBox 支持大多数 Linux 发行版，但请检查你的 Linux 软件包管理器以验证它是否支持你的特定平台。在 Ubuntu 和大多数其他基于 Debian 的 Linux 系统上，请使用 `apt-get` 工具更新你的软件包管理器并安装最新版本的 VirtualBox。请确保你已连接网络，并在终端窗口中输入以下内容：

```
$ sudo apt-get update
$ sudo apt-get install virtualbox
```

一旦安装了该工具，你可以通过打开终端窗口并输入 `virtualbox`，或者通过你的 Linux 窗口管理器启动它。

## 导入设备

VirtualBox `appliance` 指的是一个预配置的虚拟机，通常运行自定义的 Linux 发行版，你可以在 GNS3 项目中使用它。使用真实的操作系统比使用 VPCS 这样的模拟器能给你更多的命令和更大的灵活性。你可以从 GNS3 网站的 Download 部分下载预配置的 VirtualBox 设备。

在使用这些设备之前，需要将它们导入 VirtualBox。设备包名以 `.ova` 结尾，代表 `Open Virtual Appliance`，通常被称为 `OVA` 文件。要导入设备，启动 VirtualBox，你将看到 VirtualBox Manager 窗口。通过 VirtualBox Manager，你可以导入或创建新的虚拟机客户端，并管理你所有已安装的操作系统。导入设备是添加客户端的一种快速且简单的方法，因为操作系统的配置和安装已经为你完成了。

在 GNS3 网站上找到设备通常经过优化，比标准安装的相同操作系统消耗少的 PC 资源。遗憾的是，这意味着你的设备可能没有你所需的所有命令或工具，但你应该可以通过其软件包管理器更新或安装额外的软件。

在 图 5-2 中，你可以看到 VirtualBox 已经配置了一个客户端（Linux Microcore）。

![VirtualBox Manager showing an imported Linux guest OS](img/httpatomoreillycomsourcenostarchimages2208947.png.jpg)

图 5-2. VirtualBox Manager 显示导入的 Linux 虚拟机操作系统

选择操作系统将显示客户端配置的基本信息，例如基础内存和分配给虚拟机的磁盘空间。要修改虚拟机的设置，请高亮客户端并点击工具栏中的 `Settings`。就像真实的 PC 一样，虚拟客户端在获得更多资源（如内存或额外的 CPU 核心）时通常运行得更好。

要导入 VirtualBox 客户端设备，请下载镜像文件并复制到用户目录下的文件夹中。启动 VirtualBox 并选择 `File` ▸ `Import Appliance`；然后点击 `Open Appliance` 并浏览到你保存文件的位置。选择镜像文件并点击 `Continue` 然后点击 `Import` 完成该过程。要测试你的 VirtualBox 客户端，点击 `Start`，你的操作系统应该像普通 PC 一样启动并运行。

测试完新导入的操作系统后，就可以配置 GNS3 VirtualBox 偏好了。

## VirtualBox 偏好

为了管理 VirtualBox 客户端，GNS3 使用 `VBoxManage` 应用程序。该程序在安装 VirtualBox 时会自动安装。在将 VirtualBox 客户端添加到 GNS3 之前，请验证 `VBoxManage` 的路径。启动 GNS3，在 OS X 上选择 `GNS3` ▸ `Preferences`，在 Windows 和 Linux 上选择 `Edit` ▸ `Preferences`，然后点击 `VirtualBox` 进入图 5-3 所示的窗口。

![VirtualBox General Settings tab](img/httpatomoreillycomsourcenostarchimages2208949.png.jpg)

图 5-3. VirtualBox General Settings tab

在 Ubuntu Linux 上，General 选项卡上的路径应设置为 `/usr/bin/vboxmanage`。根据需要调整路径，然后点击 `Apply` 和 `OK`。在 Windows 和 OS X 上，不需要更改 `VBoxManage` 路径。

取消勾选 `Use the local server` 将允许你选择本地或远程 GNS3 服务器。勾选此框确保 VirtualBox 客户端运行在你的 PC 本地。

如果你在启动 VirtualBox 主机或打开主机的控制台连接时遇到问题，可能是一个或多个默认控制台端口号已被 PC 上运行的应用程序占用。要解决此问题，请尝试关闭冲突的程序或禁用 PC 防火墙。另一种可能是你正在使用的 VirtualBox 客户端未配置为接受控制台连接。

## VirtualBox 虚拟机设置

在 GNS3 中配置（或至少检查）VirtualBox 偏好后，你需要设置一个或多个 VirtualBox 主机供项目使用。首先，从左窗格中选择 `VirtualBox VM`。点击 `New` 从 VM 列表下拉菜单中选择你的 VirtualBox 虚拟机，如图 5-4 所示。

![New VirtualBox VM screen](img/httpatomoreillycomsourcenostarchimages2208951.png.jpg)

图 5-4. New VirtualBox VM screen

点击 `Finish` 完成安装。你应该看到虚拟机当前分配的设置，如图 5-5 所示。

![VirtualBox VMs preferences](img/httpatomoreillycomsourcenostarchimages2208953.png.jpg)

图 5-5. VirtualBox VMs preferences

默认情况下，你的虚拟机设备可以在设备工具栏的 End Devices 下找到。通过在偏好窗口中右键点击虚拟机图标（本例中 Linux Microcore），你可以为虚拟机分配不同的图标，并选择它在设备工具栏中的位置。这可以让你更好地组织你所有的 GNS3 设备。

要修改虚拟机的设置，请选择虚拟机并点击 `Edit`。大多数情况下，您会希望进入 General（常规）设置选项卡，并勾选 `Enable remote console`（启用远程控制台）和 `Start VM in headless mode`（以无头模式启动虚拟机），如图 5-6 所示。第一个选项允许您从 GNS3 分配的终端应用程序访问运行中虚拟机的控制台；第二个选项则防止在 GNS3 中启动虚拟机时从 VirtualBox 弹出控制台窗口。

![VirtualBox 虚拟机配置的常规设置卡](img/httpatomoreillycomsourcenostarchimages2208955.png.jpg)

图 5-6. VirtualBox 虚拟机配置的常规设置卡

要修改网络设置，点击 `Network`（网络）选项卡。你可以更改虚拟机中安装的适配器数量、启动适配器编号（通常为 0 或 1）以及在虚拟机中安装的适配器类型。完成后，点击 `Apply`（应用）和 `OK`（确定）以保存修改。

在配置好虚拟机客户操作系统后，你就可以在 GNS3 项目中使用它。

## 在项目中使用 VirtualBox 主机

要向项目添加 VirtualBox 主机，请从 End Devices（终端设备）窗口将 VirtualBox 主机节点图标拖入 GNS3 工作区。

每个 GNS3 项目只能使用一次 VirtualBox 主机。如果你想多次使用某个特定的 VirtualBox 主机，请启动 VirtualBox 并使用 Clone（克隆）功能创建虚拟机的克隆副本。

然后启动 GNS3 并按照之前列出的步骤在 VirtualBox Preferences（VirtualBox 偏好）下配置克隆主机。下次当你向工作区添加 VirtualBox 主机节点时，克隆的操作系统即可用。

向工作区添加 VirtualBox 主机节点后，你就可以将其连接到其他 GNS3 设备了。

## 将 VirtualBox 主机节点连接到其他设备

要在 VirtualBox 主机节点与其他设备之间建立链接，请点击 `Add a Link`（添加链接）工具栏图标；然后点击你的 VirtualBox 主机节点并选择用于链接的接口。选择另一个设备并选择一个接口以完成连接。

要启动主机，右键点击 VirtualBox 主机节点图标并选择 `Start`（启动）。通过在你的 VirtualBox 主机和与其连接的设备上配置 IP 地址来测试连接；然后使用 `ping` 命令验证连通性。

在大多数 Linux 系统（如 Microcore）上，你可以使用 `ifconfig` 和 `route` 命令手动配置 IP 地址和默认网关。要查看 Linux 中可用的网卡（NIC）列表，请在不带任何配置选项的情况下运行 `ifconfig` 命令。

```
$ ifconfig

eth0      Link encap:Ethernet HWaddr 08:00:27:7F:91:0A
          UP BROADCAST MULTICAST MTU:1500 Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B) TX bytes:0 (0.0 B)
          Interrupt:10 Base address:0xd020

eth1      Link encap:Ethernet HWaddr 08:00:27:C5:FC:66
          UP BROADCAST MULTICAST MTU:1500 Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B) TX bytes:0 (0.0 B)
          Interrupt:9 Base address:0xd060
```

### 注意

并不是所有的 Linux 系统都使用 `ifconfig` 或 `route` 命令来配置 TCP/IP，但大多数系统都是。如果你的发行版中没有这些命令，请检查你的 Linux 文档查看如何配置接口。

如果你使用的是 Windows PC 虚拟机，可以通过打开 Network and Sharing Center（网络和共享中心）并点击 `Change Adapter Settings`（更改适配器设置）来手动配置 IP 地址。右键点击你想配置的适配器并选择 `Properties`（属性）来修改 TCP/IP 设置，如图 5-7 所示。

![Windows TCP/IP 接口属性](img/httpatomoreillycomsourcenostarchimages2208957.png.jpg)

图 5-7. Windows TCP/IP 接口属性

输入你的 IP 地址信息并点击 `OK`。如果你在 GNS3 项目中配置了 DHCP 服务器，可以留空字段并选择 `Obtain an IP address automatically`（自动获取 IP 地址）。

## 使用 Linux 机的简单 VirtualBox 项目

现在你已经向 GNS3 添加了 Linux VirtualBox 虚拟机，让我们来创建一个简单的项目，将主机连接到 Cisco IOS 路由器。首先，在图 5-8 中创建项目。

![VirtualBox 主机和 Cisco IOS 路由器项目](img/httpatomoreillycomsourcenostarchimages2208959.png.jpg)

一旦你已经向 GNS3 添加了 Linux VirtualBox 虚拟机，让我们来创建一个将主机连接到 Cisco IOS 路由器的简单项目。

当你首次启动 Wireshark 时，OS X 会询问 X Window 程序的路径。在 `File` 窗口中，点击 `Browse`，导航到 `Applications/Utilities` 文件夹，然后选择 `XQuartz`。

### 注意

首次启动 Wireshark 时，`XQuartz` 会打开一个 `Xterm` 窗口而不是 Wireshark。这个奇怪的现象可以通过关闭 `XQuartz` 并重新启动 Wireshark 来轻松解决。打开过程可能需要一点时间，但这是正常的。当应用程序启动时，你应该能看到 Wireshark 的欢迎界面。

现在 Wireshark 已经安装好了，让我们看看如何从项目中的设备中捕获数据包。

# 在 Linux 上安装

要在 Ubuntu Linux 上使用高级软件包工具（Advanced Package Tools）安装最新版本的 Wireshark，请打开终端程序并输入以下命令：

```bash
$ sudo apt-get update
$ sudo apt-get install wireshark
```

在出现提示时确认安装，软件包将完成安装。进程完成后，Wireshark 就可以使用了。

# 在 GNS3 中捕获数据包

要开始捕获数据包，右键点击两个设备之间的链路，并选择 `Start Capture`，如图 5-9 所示。（如需停止捕获，右键点击同一条链路并选择 `Stop Capture`。）

![Start capturing packets.](img/httpatomoreillycomsourcenostarchimages2208961.png.jpg)

图 5-9. 开始捕获数据包。

GNS3 会提示你选择源设备、接口名称以及用于捕获数据的封装类型。你可以在以太网接口和串口接口上捕获数据。在以太网连接上，你只能选择以太网封装：`DLT_EN10MB`；但在串口连接上，你可以选择 Cisco HDLC 封装：`DLT_C_HDLC`、Cisco PPP 封装：`DLT_PPP_SERIAL` 或帧中继封装：`DLT_FRELAY`。

要捕获标准的 Cisco 串口数据（高级数据链路控制），请选择 `HDLC`；要捕获串口点对点协议数据，选择 `PPP`；要捕获帧中继数据，选择 `FRELAY`。使用下拉菜单进行选择，如图 5-10 所示。

![Source selection for capturing serial packets](img/httpatomoreillycomsourcenostarchimages2208963.png.jpg)

图 5-10. 捕获串口数据包的源选择

选择并点击 `OK` 后，GNS3 将打开 Wireshark 并开始捕获数据包，如图 5-11 所示。注意，Wireshark 窗口被分为三个不同的面板。

*   **➊ 数据包列表面板 (Packet List)**：窗口顶部的面板用于显示正在捕获的单个数据包。数据包字段显示在顶部，包括包序列号 (`No.`)、时间戳 (`Time`)、源 IP 地址 (`Source`)、目的 IP 地址 (`Destination`)、协议名称 (`Protocol`)、帧长度 (`Length`) 和信息字段 (`Info`)。包含不同协议类型的数据包以不同的颜色显示，以便于识别。

*   **➋ 数据包详情面板 (Packet Details)**：从数据包列表中选择一个数据包后，中间面板将显示有关该数据包协议和协议字段的详情。你可以展开和折叠字段以显示或隐藏其详情。显示的字段名称特定于捕获的数据包类型，并会随数据包类型的不同而变化。

*   **➌ 数据包字节面板 (Packet Bytes)**：主窗口下部的面板以十六进制格式显示原始数据，右侧显示 ASCII 字符。这是数据在跨网络传输时的原始形态。Wireshark 允许你以十六进制或二进制格式查看此信息。

![Simple Wireshark capture from GNS3](img/httpatomoreillycomsourcenostarchimages2208965.png.jpg)

图 5-11. 来自 GNS3 的简单 Wireshark 捕获

如果你在数据包列表中没有看到任何显示的数据包，请关闭 Wireshark 并停止捕获。确保你的路由器接口已启用并已分配 IP 地址，然后重启捕获并再次启动 Wireshark。

### 注意

为了学习更多关于使用 Wireshark 的知识，我强烈推荐阅读 Chris Sanders 写的《Practical Packet Analysis, 2nd Edition》（No Starch Press, 2011）。你甚至可以成为认证网络分析师 (WCNA)。

要更改 GNS3 中 Wireshark 的默认行为，请进入 `Preferences` 并选择 `Packet Capture`。要防止 GNS3 在你捕获数据包时自动启动 Wireshark，请取消勾选 `Automatically start the packet capture application`，如图 5-12 所示。

你可以选择保存数据包并在以后进行分析。从下拉菜单（预配置数据包捕获读取器命令下）选择 `Wireshark Traditional Capture`，然后点击 `Set, Apply` 和 `OK`。现在当 GNS3 捕获数据时，它会自动保存捕获的文件。

![Wireshark capture preferences](img/httpatomoreillycomsourcenostarchimages2208967.png.jpg)

图 5-12. Wireshark 捕获设置

## 结语



GNS3 的一个关键特性是其模块化设计以及使用其他软件扩展项目的能力。通过 VPCS，你可以添加许多简单的 PC 主机，而通过 VirtualBox，你就可以运行完整的操作系统。

Wireshark 是最被低估的工具之一，但它也是最强大的工具之一。通过 Wireshark，你可以深入了解网络上正在发生的情况。无论你是网络新手还是已经通过了认证，打开 Wireshark 并分析数据包都是磨练技能和增加对协议理解的极佳方法。

在第 6 章中，你将查看 Quick Emulator（另一种开源 PC 模拟器），并使用它创建一个特殊的 Juniper Junos OS 版本，即 Juniper Olive。Juniper Olive 允许向你的 GNS3 项目添加功能完整的 Juniper 路由器。

# 第 6 章 Juniper Olive 和 VSRX Firefly

你可以通过多种方式在 GNS3 中安装和运行 Juniper 路由器。在本章中，我向你介绍如何使用 VirtualBox 和 Quick Emulator (QEMU) 创建适用于 GNS3 的 Juniper 设备，然后安装 Juniper vSRX Firefly 防火墙。

QEMU 是一种与 VirtualBox 类似的开源 PC 模拟器。它没有那么完善，但具有许多强大功能并完全集成到 GNS3 中。使用 QEMU，你可以运行许多网络操作系统，包括 Cisco ASA、IDS、IOS-XR、NX-OSv 以及特殊的 Juniper Olive 版本 Junos OS。在本章中，我只关注 Juniper。

# 在 Windows 和 OS X 上安装 QEMU

如果你在 Windows 或 OS X 上安装了 `GNS3`，那么系统应该已经为你安装了 `QEMU`。`GNS3` 安装程序可能安装了两个版本的 `QEMU`：是在安装 `GNS3` 过程中自动配置的稳定版本，另一个是包含额外未经测试功能的新版本。如果你需要项目保持完全稳定，我建议只使用预配置的版本。

如果你是使用第 2 章中列出的默认设置安装的 `GNS3`，那么你应该在 32 位和 64 位的 Windows 系统上都能在 `C:\Program Files\GNS3\qemu-0.13.0` 下找到 QEMU 应用程序，但请记住，随着 `QEMU` 新版本的引入并加入 `GNS3`，该目录会发生变化。在 OS X 上，你应该在 `/Applications/GNS3.app/Contents/Resources/qemu/bin/` 找到 `QEMU`。

# 在 Linux 上安装 QEMU

Ubuntu 上的 `QEMU` 可以通过软件包安装，也可以从源代码编译。若要通过软件包安装，请更新你的包管理器并在命令行安装 `QEMU`。

```
$ sudo apt-get update
$ sudo apt-get install qemu
```

或者，你可以安装 `qemu-system-x86` 软件包。这是一个小得多的安装版本，能够运行你想要在 `GNS3` 中使用的任何操作系统。要安装仅限 x86 架构版本的 `QEMU`，请使用以下命令：

```
$ sudo apt-get install qemu-system-x86
$ sudo apt-get install qemu-utils
```

取决于你的系统可用的 `QEMU` 版本，你可能想要从源代码编译 `QEMU`。虽然许多 Linux 发行版都存在预编译的 `QEMU` 软件包，但它们可能不是最新版本，并且可能不包含 `QEMU` 图形用户界面的 GTK 工具。在这种情况下，你可以通过安装 VNC 查看器程序（如 `GNC Viewer`）来访问 `QEMU` 界面。

从源代码安装时，你还必须在编译源码之前安装 `QEMU` 需要的其他软件包。现在更新你的包管理器并安装这些软件包：

```
$ sudo apt-get update
$ sudo apt-get install flex
$ sudo apt-get install bison
$ sudo apt-get install zlib1g-dev
$ sudo apt-get install libglib2.0-dev
$ sudo apt-get install libgtk2.0-dev
$ sudo apt-get install libncurses5-dev
$ sudo apt-get install libpcap-dev
$ sudo apt-get install dh-autoreconf
```

接下来，从 QEMU 网站（[`www.qemu-project.org/`](http://www.qemu-project.org/)）下载 `QEMU` 源码并解压文件，如下：

```
$ wget http://www.qemu-project.org/download/qemu-2.1.2.tar.bz2
$ bunzip2 qemu-2.1.2.tar.bz2
$ tar xvf qemu-2.1.2.tar
```

解压文件后，移动到 `QEMU` 安装目录并执行 `configure` 和 `make` 命令来编译源码。

```
$ cd qemu-2.1.2
$ ./configure
$ make
```

最后，通过将编译后的文件安装到系统中来完成该过程。这必须使用 root 权限完成。

```
$ sudo make install
```

安装完成后，你应该会在 `/usr/local/bin/` 下找到 `QEMU` 二进制文件，`QEMU` 支持文件应该在 `/usr/local/share/qemu/` 目录下。

安装好 `QEMU` 后，你就可以在 GNS3 中开始创建和使用 `QEMU` 设备了。

# 介绍 Juniper

大多数人都听过思科（Cisco），但很少有人听过瞻远网络（Juniper Networks）。和思科一样，瞻远生产各种网络硬件，互联网服务提供商使用其极吞吐量的设备为客户高效路由数以十计的数据包。

所有的 Juniper 设备都围绕共同的 FreeBSD 代码库，尽管并不是每个 Juniper 设备都运行 FreeBSD 操作系统。相反，它们仅将该内核作为另一个名为 `Junos OS` 的操作系统的框架。然而，由于 `Junos OS` 是围绕 FreeBSD 设计的，……

# 安装 Juniper

俗话说：“授人以鱼，不如解其腹以一日；授人以渔，能受用终身。”在创建 Juniper Olive 时，这句格言依然适用。

配合 `GNS3` 使用时，Juniper Olive 软件通常使用 `VirtualBox` 或 `QEMU` 安装。

让我们看看如何创建一个 Olive 以及哪里获取软件。

## 流程概述

Juniper Olive 安装软件非常像一种常见的寄生虫，以 FreeBSD 为其不防备的主机。要创建一个 Olive，你将使用 `QEMU` 或 `VirtualBox` 安装 FreeBSD。接下来，你会将 Juniper Olive 软件的 gzipped 压缩包拷贝到你的 FreeBSD 虚拟机。在那里，你将解压缩包并进行微小的修改，然后将文件压缩回 FreeBSD 可安装包。最后，你将安装该包并重启 FreeBSD 系统。

这就是有趣的地方。当你第一次启动系统时，Juniper Olive 软件会入侵其 FreeBSD 主机。它将重新分区 FreeBSD 硬盘，将新文件复制到系统，并保留它需要的 FreeBSD 文件。完成后，你应该拥有一个功能完整的 Juniper 路由器。

## 获取 FreeBSD

使用 `QEMU` 安装 FreeBSD 需要一个 FreeBSD CD 镜像。有多个版本适用于创建 Juniper Olive，但我推荐使用小型镜像（mini ISO）。它包含了所有必要的文件，下载最快。从 FreeBSD 归档下载 `4.11-RELEASE-i386-miniinst.iso` 文件（ftp://ftp-archive.freebsd.org/）。我推荐这个 FreeBSD 版本而不是更晚的版本，因为它似乎与任何 Olive 版本都配合得很好。

### 注意

*你可以在 GNS3 网站（[`www.gns3.com/`](http://www.gns3.com/)）的下载部分的 QEMU 设备列表下找到预先安装了 FreeBSD 的 QEMU（以及 VirtualBox）镜像。*

接下来，你需要获取 Juniper Olive 软件。该软件以 FreeBSD 可安装包的形式提供，名称类似于 `jinstall-12.1R1.9-domestic-olive.tgz`。由于 Juniper 不支持 Juniper Olive，你无法直接从 Juniper 获取该软件的副本。

## 创建 Juniper Olive CD 镜像文件

获取 Juniper Olive 软件后，你需要一种方法将包拷贝到你的 FreeBSD 虚拟机中进行安装。这种方法有多种，但最简单的方法是在 FreeBSD 虚拟机上挂载 ISO 镜像文件，就像使用普通 CD 一样。在此之前，你必须为 Olive 软件创建自己的 ISO 镜像。

## 在 Windows 中创建 ISO

使用 Windows 创建 ISO 镜像文件，首先需要安装 ISO 镜像制作软件。我推荐 ISO Recorder（[`isorecorder.alexfeinman.com/isorecorder.htm`](http://isorecorder.alexfeinman.com/isorecorder.htm)）。它免费、易安装且运行良好。下载软件并启动安装程序，然后点击 `Next` 并按照提示完成安装。

安装 ISO Recorder 后，你应该能够创建 Juniper Olive 软件的 ISO 镜像了。创建一个文件夹，并将你的 gzipped Olive 文件拷贝到该文件夹（例如命名为 `juniper-olive`）。然后，右键点击文件夹并选择 `Create ISO image file`。

出现 ISO Recorder 创建向导，如图图 6-1 所示。

![ISO Recorder 创建向导](img/httpatomoreillycomsourcenostarchimages2208969.png.jpg)

图 6-1. ISO Recorder 创建向导

在 Create image（创建映像）下，选择 `Directory` 单选按钮，将 Image 格式更改为 `CD`，点击 `Next` 并按照提示创建你的 ISO 镜像。获取 Juniper ISO 后，你就可以在 Windows 上安装 Juniper Olive 了。

## 在 OS X 中创建 ISO

在运行 OS X 的计算机上，将你的 Juniper 镜像文件拷贝到一个文件夹中，并使用 `hdiutil` 创建该文件夹内容的 ISO 镜像。在下面的列表中，我使用名为 `JUNOS` 的文件夹创建了一个名为 `juniper-olive.iso` 的 ISO 镜像文件：

```
$ mkdir JUNOS
$ cp jinstall-12.1R1.9-domestic.tgz JUNOS
$ hdiutil makehybrid -iso -joliet -o juniper-olive.iso JUNOS
```

现在你已经有了适用于 Olive 软件的 ISO，就可以在 OS X 上安装 Juniper Olive 了。

## 在 Linux 中创建 ISO

在 Ubuntu Linux 上创建 ISO 镜像与在 OS X 上几乎相同，仅你使用的是 `mkisofs` 应用。将你的 Juniper 镜像文件拷贝到一个文件夹（例如 `JUNOS`），并输入以下命令来创建 ISO：

```
$ mkdir JUNOS
$ cp jinstall-12.1R1.9-domestic.tgz JUNOS
$ mkisofs -o juniper-olive.iso JUNOS
```

现在你已经有了 ISO，在创建 Juniper Olive 之前只剩下几件事要做了。

# 使用 QEMU 安装和配置 FreeBSD

创建 Juniper Olive 的第一步创建一个 FreeBSD 的 QEMU 虚拟机。QEMU 没有图形用户界面，因此你将通过命令行完成所有操作。你将使用 `qemu-img` 程序创建虚拟磁盘镜像文件，并使用 `qemu` 程序来安装和测试你的虚拟机。

### 注意

并不是所有的 QEMU 安装都相同。在某些安装中，QEMU 文件可能命名为 `qemu-system-i386` 或 `qemu-system-x86_64`，或者你可能两个都安装了。如果不确定，请检查 QEMU 安装目录。

## 准备构建目录

首先创建一个构建目录，然后将 FreeBSD 安装 ISO 和 Juniper Olive ISO 文件拷贝到该目录，如下例所示：

```
$ mkdir Juniper
$ cp 4.11-RELEASE-i386-miniinst.iso Juniper
$ cp juniper-olive.iso Juniper
```

如果你使用的是 Windows，请打开命令提示符窗口并输入以下命令：

```cmd
c: mkdir Juniper
c: copy 4.11-RELEASE-i386-miniinst.iso Juniper
c: copy juniper-olive.iso Juniper
```

现在构建目录中的一切都已就绪，你可以开始安装系统了。

## 安装兼容 Junos 的 FreeBSD 系统

在本节中，你将使用 `qemu-img` 创建虚拟硬盘并在虚拟磁盘上安装 FreeBSD。我将只涵盖为 Olive 准备 FreeBSD 的基础知识，不会详细介绍 FreeBSD 本身。

### Windows 和 OS X 的初步检查

如果你是 Windows 用户，在开始之前请从“程序和功能”控制面板安装 Telnet 客户端应用程序。

如果你是 OS X 用户，你可能将 QEMU 文件目录添加到 OS X 的搜索路径中。验证 QEMU 文件的安装路径。如果你是手动安装的 QEMU，应该在 `/opt/local/bin` 或 `/usr/local/bin/` 寻找 `qemu-img` 文件。如果你使用的是通过 GNS3 安装的 QEMU，你应该能找到。

## 开始

通过创建一个名为 `juniper.img` 的 8GB 虚拟磁盘文件开始安装。

```bash
$ mkdir Juniper
$ qemu-img create juniper.img 8G
```

接下来，使用以下命令从 FreeBSD ISO 启动 QEMU：

```bash
$ qemu-system-i386 -m 512 -hda juniper.img -cdrom 4.11-RELEASE-i386-miniinst.iso
```

Windows 用户应该打开命令提示符并使用以下命令：

```cmd
c: mkdir Juniper
c: qemu-img create juniper.img 8G
c: qemu-system-i386 -m 512 -hda juniper.img -cdrom 4.11-RELEASE-i386-miniinst.iso
```

当 FreeBSD 启动时，会出现内核配置菜单，如图图 6-2 所示。

![FreeBSD 内核配置菜单](img/httpatomoreillycomsourcenostarchimages2208971.png.jpg)

图 6-2. FreeBSD 内核配置菜单

按 Enter 跳过内核配置并继续安装。

接下来，会出现 sysinstall 主菜单，如图图 6-3 所示。

![sysinstall 主菜单](img/httpatomoreillycomsourcenostarchimages2208973.png.jpg)

图 6-3. sysinstall 主菜单

使用方向键向下移动，选择 **Standard**（标准）开始标准安装，然后按 Enter 继续。

### 分区文件系统

下一个屏幕如图图 6-4 所示，显示了关于使用 FDISK 分区编辑器的基本信息。

![FDISK 分区消息屏幕](img/httpatomoreillycomsourcenostarchimages2208975.png.jpg)

图 6-4. FDISK 分区消息屏幕

阅读说明并按 Enter 进入 FDISK 分区编辑器菜单。

`FDISK` 分区编辑器允许你选择想要分配给 FreeBSD 的磁盘空间。选择 `A` 使用整个磁盘，然后选择 `Q` 完成。

接下来将出现 `Install Boot Manager` 菜单，如图 6-6 所示。

![安装启动管理器菜单](img/httpatomoreillycomsourcenostarchimages2208979.png.jpg)

图 6-6. 安装启动管理器菜单

使用方向键向移动移动，选择 `Standard` 以安装标准主引导记录 (MBR)，并按 `ENTER` 继续。

随后，BSD 会显示一条关于在新创建的 `FDISK` 分区内创建 BSD 分区的消息，如图 6-7 所示。

![BSD 分区消息](img/httpatomoreillycomsourcenostarchimages2208981.png.jpg)

图 6-7. BSD 分区消息

阅读该消息后，按 `ENTER` 继续进入 FreeBSD 磁盘标签编辑器。

### 创建兼容 Juniper 的分区

下一步是创建`兼容 Juniper 的分区`。密切你如何对虚拟硬盘进行分区非常重要，因为 Juniper Olive 软件包必须看到正确的 FreeBSD 分区，否则安装将失败。你还必须按照特定顺序创建分区。

要创建第一个分区，选择 `C` 并在提供的字段中输入分区大小，如图 6-8 所示。

![指定分区大小。](img/httpatomoreillycomsourcenostarchimages2208983.png.jpg)

图 6-8. 指定分区大小。



我输入了`1024M`来创建一个 1GB 的分区。按`ENTER`接受此值，你将看到分区类型选项屏幕，如图 6-9 所示。

![选择分区类型。](img/httpatomoreillycomsourcenostarchimages2208985.png.jpg)

图 6-9. 选择分区类型。

按`ENTER`创建文件系统 (FS) 分区类型，你将获得选择该分区挂载点的选项，如图 6-10 所示。

![为分区选择挂载点。](img/httpatomoreillycomsourcenostarchimages2208987.png.jpg)

图 6-10. 为分区选择挂载点。

为根分区创建挂载点，输入正斜杠`/`并按`ENTER`完成第一个分区的配置。

参考表 6-1，按照相同的步骤创建完整的文件系统布局。顺序非常重要！在创建根分区`/`后，按列表向下操作，以`/var`分区结束。当你轮交换分区时，确保分区类型选择`swap`而不是`FS`。`/var`分区是最后一个，因此在创建它时，接受默认分区块大小。此值使用了分区上剩余的可用空间。记住，如果分区不是按顺序创建，分区名称将与挂载点不匹配，Juniper Olive 将无法安装。

表 6-1. 用于 Juniper Olive 的 FreeBSD 分区

| 分区 | 挂载 | 大小 |
| --- | --- | --- |
| ad0s1a | `/` | 1024 MB |
| ad0s1b | `swap` | 1024 MB |
| ad0s1e | `/config` | 1024 MB |
| ad0s1f | `/var` | 剩余空间 |

为安装 Olive 准备 FreeBSD 分区有很多方法，但我发现这种方法在不同版本的 Juniper Olive 中是最可靠的。完成后，文件系统看起来应该和图 6-11 完全所示。

![适用于 Juniper Olive 的完全配置分区布局](img/httpatomoreillycomsourcenostarchimages2208989.png.jpg)

图 6-11. 适用于 Juniper Olive 的完全配置分区布局

配置好所有分区后，选择`Q`完成分区过程，然后选择你的发行集，如图 6-12 所示。

![FreeBSD 发行版选择](img/httpatomoreillycomsourcenostarchimages2208991.png.jpg)

图 6-12. FreeBSD 发行版选择

使用方向键向下移动，选择`Standard`以安装标准主引导记录 (MBR)，并按`ENTER`继续。

### 完成安装

任何显示的其他屏幕指令都可以被忽略，因为它们适用于真实的 Juniper 路由器，而不是 PC 上的 Olive 安装。然而，在继续之前，您需要使用`halt`命令关闭 FreeBSD 系统并退出 QEMU。

```
# halt
```

安装 Olive 的最后一步是重启系统，并给软件包留时间完成对 FreeBSD 的接管。此时，您必须为安装程序提供额外的内存，否则安装将失败。尽管 Junos OS 在 512MB RAM 的情况下可以运行良好，但安装程序需要 1024MB RAM 来创建在安装期间使用的 RAM 磁盘。

在 Linux 和 OS X 中，按照如下命令使用 1024MB RAM 启动 Juniper Olive 以完成安装：

```bash
$ sudo qemu-system-i386 -m 1024 -hda juniper.img -serial telnet:127.0.0.1:1001,
server,nowait,nodelay -localtime
```

Windows 用户应该输入以下命令：

```bash
c: qemu-system-i386w -m 1024 -hda juniper.img -serial telnet:127.0.0.1:1001,
server,nowait,nodelay -localtime
```

启动系统后，您可以使用 telnet 连接到本地的 1001 端口来观察 Olive 软件的安装。（在 Windows 上，您可能需要先从“程序和功能”控制面板安装 Telnet 客户端程序。）打开第二个 Windows 命令提示符或终端窗口，输入以下命令查看控制控制上显示的安装输出：

```bash
telnet localhost 1001
```

我强烈建议监控您的安装过程。这是排查是否出现问题的极佳方法。否则，您将不知道安装失败的原因。一个常见问题是为虚拟机分配的内存不足；另一个是分区大小太小或创建不正确。

Juniper Olive 的安装可能需要 15 分钟或更长时间，取决于您的硬件，因为安装程序执行了许多任务，例如对 FreeBSD 硬盘进行重新分区以及提取各种软件包。当一切完成后，系统应该会自动重启、加载 Junos OS，并向您显示看起来像 FreeBSD 登录提示的界面，如图 6-15 所示。

![Successful Junos OS boot messages and login](img/httpatomoreillycomsourcenostarchimages2208997.png.jpg)

图 6-15. Junos OS 启动消息和登录

此提示是您登录 Junos OS 的地方。如果您看到了之前的消息和登录提示，那么您的 Juniper 路由器就可以使用了。

## 备份 Juniper Olive

在创建好可用的 Olive 后，请制作镜像的备份副本以备保存。毕竟，谁想重做一遍所有工作呢？我不想！

首先，正确关闭 Junos OS 以防触发脏文件系统（dirty filesystem）。当文件没有被正确关闭时就会发生脏文件系统问题。这种情况会导致文件损坏，甚至破坏 Junos 操作系统。如果文件系统被标记为脏，下次启动 Junos OS 时将触发文件系统检查，启动时间可能比通常更长，直到系统被检查并标记为洁（这意味着没有发现错误，或所有错误都已修复）。

要关闭 Junos OS，请以`root`身份登录（无需密码）并输入以下命令：

```bash
Login: root
root@% cli
root> request system halt
Halt the system ? [yes,no] (no) yes
```

在看到指示操作系统已停止的消息后（如下所示），退出 QEMU 是安全的：

```
The operating system has halted.
Please press any key to reboot.
```

要为您的 Juniper 镜像制作备份，请在镜像文件所在的目录下输入以下命令：

```bash
$ cp juniper.img backup-juniper.img
```

Windows 用户可以使用此命令：

```bash
c: copy juniper.img backup-juniper.img
```

现在您有了一个 Juniper 路由器，需要配置 GNS3 使其可以在您的项目中使用。

# 在 GNS3 中配置 Juniper 路由器

在 GNS3 中配置 Juniper 路由器，在 Windows 和 Linux 上选择 **Edit** ▸ **Preferences**，或在 OS X 上选择 **GNS3** ▸ **Preferences**。从侧边栏双击`QEMU`并选择 **QEMU VMs** 以打开 QEMU VMs 首选项窗口，如图 6-16 所示。

![QEMU VMs preferences window](img/httpatomoreillycomsourcenostarchimages2208999.png.jpg)

图 6-16. QEMU VMs 首选项窗口

从这里您可以创建、编辑和删除 QEMU 虚拟机，允许将 Juniper 虚拟机引入 GNS3。

## 将 Juniper 虚拟机添加到 GNS3

要将 Juniper 虚拟机添加到 GNS3，点击 **New** 启动新 QEMU VM 向向。为您的虚拟机输入一个名称。选择 **QEMU VMs** 打开 QEMU VMs 首选项窗口，如图 6-16 所示。

```
R1> enable
R1# configure-terminal
R1(config)# interface f0/0
R1(config-if)# ip address 10.10.10.1 255.255.255.0
R1(config-if)# no shutdown
```

现在打开你的 Juniper 器的控制台，登录并使用与 Cisco 路由器相同的子网配置 IP 地址。

```
Login: root
root@% cli
root> edit
➊ root# set system root-authentication plain-text password
New password: olive1
Retype new password: olive1
root# set interfaces em0 unit 0 family inet address 10.10.10.2/24
root# commit
commit complete
```

为了安全起见，Junos OS 要求你在向路由器提交任何其他配置更改之前必须 ➊ 分配 root 密码，请现在执行此操作。我将密码设置为`olive1`，但你可以输入任何你想要的密码。

### 注意

在本示例中，你可以看到 Juniper 的语法与 Cisco 的语法完全不同。如果你不熟悉 Juniper 语法，请访问 Juniper 网站 ([`www.juniper.net/`](http://www.juniper.net/)) 获取有关配置 Juniper 路由器的详细信息。

配置好两个设备后，ping 你的 Cisco 路由器以测试连接性。

```
root# exit
root> ping 10.10.10.1
```

如果 ping 测试失败，可能是你的 IP 地址或 QEMU 安装存在问题。如果你是从源码编译 QEMU 的，请验证你安装的是已知与 Juniper Olive 兼容的版本。如有必要，请重新编译并安装 QEMU。如果问题仍然存在，尝试安装或编译另一个版本的 QEMU。

你也可以使用 VirtualBox 创建 Olive。该过程基本上与 QEMU 相同，但你将使用 VirtualBox 的 GUI 工具而不是命令行。在创建 VirtualBox 虚拟机时，将 Type（类型）设置为 BSD，并将 Version（版本）设置为 FreeBSD (32-bit)。

# 运行 Juniper vSRX Firefly

除了 Junos OS 外，你还可以运行 Juniper SRX 防火墙的虚拟版本，称为`vSRX Firefly`。如果你在 Juniper 注册，可以从网站免费下载 Firefly 的评估版（[`www.juniper.net/`](http://www.juniper.net/)））。你需要下载 Firefly VMware Appliance - FOR EVALUATION! 软件包。正如名称所示，它是为运行在 VMware 上而设计的，但你可以对其进行调整以运行在 VirtualBox 或 QEMU 上。我在这里介绍 VirtualBox，因此在开始之前，请确保你的系统上已安装了 VirtualBox 程序。

下载 Firefly 软件后，请注意它是一个 Open Virtual Appliance (OVA) 文件，文件名类似于`junos-vsrx-ver.x-domestic.ova`。OVA 文件是一个特殊的压缩包文件，可以使用`tar`命令解压。要在 Linux 或 OS X 上从该文件中提取内容，请使用以下命令：

```
$ tar xvf junos-vsrx-ver.x-domestic.ova
```

### 注意

如果你运行的是 Windows，可以使用 7-zip 应用 ([`www.7-zip.org/`](http://www.7-zip.org/)) 来提取文件。

在提取完所有文件后，你需要将 VMware 虚拟机磁盘文件（扩展名为`.vmdk`的文件）转换为 VirtualBox 可以使用的虚拟磁盘镜像 (VDI) 文件。要转换该文件，请使用 VirtualBox 自带的`vboxmanage`实用程序。

```
$ vboxmanage clonehd -format VDI junos-vsrx-ver.x.domestic-disk1.vmdk
junos-vsrx-ver.x.domestic-disk1.vdi
```

转换磁盘镜像后，你可以删除所有新的 VDI 文件（在本示例中为`junos-vsrx-ver.x-domestic-disk1.vdi`）。这就是你将导入到 VirtualBox 中的硬盘镜像文件。

## 使用 VirtualBox 创建 Firefly 虚拟机

你需要在 VirtualBox 中创建一个新虚拟机并导入 Firefly 硬盘镜像文件。启动 VirtualBox 并点击 **New**（新建）打开创建虚拟机对话框，如图 6-20 所示。

![Create Virtual Machine dialog](img/atomatomoreillycomsourcenostarchimages2209007.png.jpg)

图 6-20. 创建虚拟机对话框

为虚拟机命名（在本示例中为`Firefly`），将 Type 设置为`BSD`，并将 Version 设置为 **FreeBSD (32-bit)**。完成后，点击 **Next**（下一步）分配内存大小，如图 6-21 所示。

![Adjust the memory size.](img/atomatomoreillycomsourcenostarchimages2209009.png.jpg)

图 6-21. 调整内存大小。

按照 Juniper 的说明设置内存大小。在本示例中，我选择了 2048 MB，因为这是 Juniper 建议的。完成后，点击 **Next**，并勾选 **Use existing hard drive**（使用现有硬盘），如图 6-22 所示。使用浏览图标找到你创建的 VDI 文件。

![Choose Junos-vsrx firefly VDI file](img/atomatomoreillycomsourcenostarchimages2209011.png.jpg)

图 6-22. 选择 Junos-vsrx firefly VDI 文件

完成后，点击 **OK**。配置好虚拟机后，在 VirtualBox 中右键点击你的虚拟机并选择 **Clone**（克隆），创建一个副本以便在 GNS3 中运行。原始虚拟机将保持闲状态，你将始终有一个干净的、未配置的主副本。

## 为你的虚拟机提供更多处理器

创建虚拟机后，你必须增加处理器的数量，因为 SRX 需要两个。如果你的虚拟机只配置了一个处理器，Firefly 将启动并运行，但你将无法配置任何接口。在 VirtualBox 中选择你的虚拟机名称，进入 **Settings**（设置） ▸ **System**（系统），并点击 **Processor**（处理器）选项卡。

![Processor tab](img/atomatomoreillycomsourcenostarchimages2209013.png.jpg)

图 6-23. 处理器选项卡

使用滑动条选择两个处理器，并点击 **OK**。

## 将 vSRX Firefly 添加到 GNS3

启动 GNS3，在 Windows 和 Linux 上选择 **Edit**（编辑） ▸ **Preferences**（首选项），在 OS X 上选择 **GNS3** ▸ **Preferences**。在左侧窗格中双击 **VirtualBox**，选择 **VirtualBox VMs** 打开 VirtualBox 虚拟机首好设置。要将你的 Firefly VirtualBox 虚拟机添加到 GNS3，点击 **New**（新建）启动新虚拟机向导。从下拉菜单中选择你的 Firefly 虚拟机并点击 **Finish**（完成）。

![VirtualBox VMs preferences](img/atomatomoreillycomsourcenostarchimages2209015.png.jpg)

图 6-24. VirtualBox 虚拟机设置

在 General（常规）设置选项卡上，勾选 **Enable remote console**（启用远程控制台）和 **Start VM in headless mode**（无界面模式启动虚拟机）。这将允许你使用控制台登录 Firefly。最后，点击 **Network**（网络）选项卡，将接口数量更改为 6，并将网络类型设置为 **Paravirtualized Network (virtio net)**。

## 创建基于区域的防火墙项目

在本节中，你将使用 Firefly 作为网络防火墙创建一个简单的项目。Firefly 的功能类似于 Cisco 的 ASA 防火墙，但配置方式有所不同。我不会进行过多细节，但这个项目应该可以帮你入门。如果你想了解更多关于 Juniper SRX 的信息，可以在 Juniper 网站找到大量详细文档。

让我们从创建图 6-25 所示的 GNS3 项目开始。从终端设备（End Devices）工具栏将一个 Firefly 设备拖到你的工作区。接下来，将两个 Cisco 路由器拖到工作区并将设备连接起来。将`R1`的接口`f0/0`连接到`vSRX Firefly`的接口`e1`。将`R2`的接口`f0/0`连接到`vSRX Firefly`的接口`e0`。

![vSRX Firefly project](img/httpatomoreillycomsourcenostarchimages2209017.png.jpg)

图 6-25. vSRX Firefly 项目

## 项目概述



路由器`R1`将配置为使用 Firefly Trust 区域（trust zone）。`R1`代表你局域网上的一个信任主机。路由器`R2`将配置为使用 Firefly 不信区域（untrust zone）。不信区域代表不可信的网络，例如互联网。你配置 Firefly，使得你的信任主机（`R1`）能够通过 NAT 使用 vSRX Firefly 防火墙 ping 你的不可信主机（`R2`）。

## 配置路由器 R1

首先为路由器`R1`配置 IP 地址和默认网关。

```
R1(config)# interface f0/0
R1(config-if)# ip address 192.168.1.100 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# ip route 0.0.0.0 0.0.0.0 192.168.1.1
```

## 配置路由器 R2

接下来，在不可信路由器`R2`上配置 IP 地址。这里不需要配置网关。

```
R2(config)# interface f0/0
R2(config-if)# ip address 100.1.1.1 255.255.255.0
R2(config-if)# no shutdown
```

## 配置 vSRX Firefly

配置好路由器 IP 地址后，你可以关注 Firefly 了。使用 root 账户登录以配置 vSRX Firefly 防火墙。由于是新安装，你不会被要求输入密码。登录后，输入以下命令创建你的防火墙；你将从创建密码和配置网络设置开始：

```
root@%cli
  root>edit
➊ root#set system root-authentication plain-text-password
  New password:firefly1
  Retype new password:firefly1
➋ root#set interface ge-0/0/0.0 family inet address 100.1.1.2/24
➌ root#set interface ge-0/0/1.0 family inet address 192.168.1.1/24
➍ root#set routing-options static route 0.0.0.0/0 next-hop 100.1.1.1
```

和 Juniper 路由器一样，在为 root 账户分配密码之前，你无法在 SRX 设备上保存任何配置更改，因此首先进入 edit 模式并创建一个 root 密码 ➊。我输入了`firefly1`，但你可以选择任何喜欢的密码。

接下来，在 ➋ 处，你在 WAN 接口（`ge-0/0/0.0`）上设置 IP 地址，在 ➌ 处，设置 LAN 接口（`ge-0/0/1.0`）。最后，在 ➍ 处，使用不可信路由器的 IP 地址（`100.1.1.1`）设置默认网关地址。

## 安全区域与策略

通过定义安全区域和安全信任策略完成配置。

```
➊ root#set security zones security-zone trust interfaces ge-0/0/1.0
➋ root#set security nat source rule-set interface-nat from zone trust
➌ root#set security nat source rule-set interface-nat to zone untrust
➍ root#set security nat source rule-set interface-nat rule rule1 match
   source-address 0.0.0.0/0 destination-address 0.0.0.0/0
➎ root#set security nat source rule-set interface-nat rule rule1 then source-nat
   interface
➏ root#set security policies from-zone trust to-zone untrust policy permit-all
   match source-address any destination-address any application any
➐ root#set security policies from-zone trust to-zone untrust policy permit-all
   then permit
➑ root#commit
```

将你的 LAN 接口分配到`trust`区域 ➊。将 interface-nat 源区域设置为`trust` ➋，将 interface-nat 目的区域设置为`untrust` ➌，并创建一条匹配任何源 IP 地址和目的 IP 地址（`0.0.0.0/0`）的规则 ➍。在生产环境中，你会收紧这些限制，但对于你的 GNS3 练习实验，这是没问题的。现在在 WAN 接口上配置 NAT 过载（overloading） ➎。

### 注意

> vSRX Firefly 的`interface-nat`命令用于实现等于 Cisco NAT/PAT overloading 的。

要完成配置，定义允许区域之间传输的流量类型 ➏。在这种情况下，你允许从`trust`区域到`untrust`区域的所有协议和应用程序。最后，创建安全策略 ➐ 并提交更改 ➑，你就完成了。

```
➊ root#set security zones security-zone trust interfaces ge-0/0/1.0
➋ root#set security nat source rule-set interface-nat from zone trust
➌ root#set security nat source rule-set interface-nat to zone untrust
➍ root#set security nat source rule-set interface-nat rule rule1 match
   source-address 0.0.0.0/0 destination-address 0.0.0.0/0
➎ root#set security nat source rule-set interface-nat rule rule1 then source-nat
   interface
➏ root#set security policies from-zone trust to-zone untrust policy permit-all
   match source-address any destination-address any application any
➐ root#set security policies from-zone trust to-zone untrust policy permit-all
   then permit
➑ root#commit
```

## 结语

在本章中，你学习了 Juniper 和 Olive，我为你展示了如何使用 QEMU 和 VirtualBox 创建 Juniper。我还向你介绍了 vSRX Firefly，并提供了有关如何使用 SRX 设备配置基础区域防火墙的见解。

在大多数情况下，Juniper 在企业界不如 Cisco 流行，但在较大的环境中（如园区站点和 ISP 路由交换市场），它是一个大角色。如果你将网络职业生涯转向这些领域，Juniper 认证可以让你从其他申请者中脱颖而出而 GNS3 是学习 Juniper 路由器和 SRX 的极佳方法。你应该从 JNCIA 认证开始，这是 Juniper 的入门级认证（等同于 Cisco CCNA），它是高级认证的先决条件。Juniper 的培训网站提供了所需的所有信息。

内置设备节点模拟了特定设备类型（如交换机）的功能。它们很容易配置，如果你需要节省时间和 PC 资源，或者只是想在了解底层技术所有细节的情况下完成任务，它们会非常有用。

如果你创建了一个使用 VLAN 的拓扑，可以将 GNS3 以太网交换机节点拖到工作区，并使用简单的菜单快速创建 VLAN 或 VLAN 中继链路。当然，如果你正在准备涉及交换的 Cisco 考试，你需要知道如何配置真实的 Cisco IOS 交换机。

# 节点配置器

到目前，你已经知道节点配置器可以用于配置单个设备节点的功能，也可以用于同时修改多个设备。随着项目的增长和你使用的设备越来越多，此功能可以为你节省大量时间。

要同时打开多个设备，请使用鼠标在工作区选择这些设备，然后右键点击任何设备并选择`Configure`。选中的设备将显示在节点配置器中，如图图 7-1 所示。

![使用节点配置器修改多个设备](img/httpatomoreillycomsourcenostarchimages2209019.png.jpg)

图 7-1. 使用节点配置器修改多个设备

要配置单个设备，从左侧列中选择该设备。配置每个设备并点击`Apply`。完成所有设备的配置后，点击`OK`完成过程。

要修改多个设备，使用`SHIFT`键从左侧列一次性选择几个设备，然后像配置单个设备一样对它们进行配置。假设你有 10 台 7200 系列路由器，并想在所有 10 台路由器的 0 槽中添加相同的网络模块。使用`SHIFT`键选择所有路由器，将模块添加到 0 槽，然后点击`Apply`和`OK`即可对所有 10 台设备应用更改。

你也可以通过点击它们的组名称来选择整个路由器组。在之前的图中，你可以通过选择组名`Router c3725 group` ➊ 来同时配置 R1、R2 和 R3。

# 以太网集线器

GNS3 提供了一个以太网集线器（参见图 7-2），作为网络教师可以使用该工具来教授学生以太网环路、过度广播和多端口中的危险。

![以太网集线器节点配置器](img/httpatomoreillycomsourcenostarchimages2209021.png.jpg)

图 7-2. 以太网集线器节点配置器

作为一个一般原则，你应该坚持使用 GNS3 交换机并避免在项目中包含集线器。但如果你确实需要使用以太网集线器，可以通过打开节点配置器并从左列表中选择你的集线器来更改可用以太网端口的数量。默认值为八端口，如果你需要不同的数量，请在右侧的`Settings`字段中输入该数字。

# EtherSwitch 路由器

GNS3 提供两种 Dynamips 交换机：以太网交换机节点和 EtherSwitch 路由器。我在第 4 章中讨论过以太网交换机节点，因此在这里我只介绍 EtherSwitch 路由器。

`EtherSwitch router`不是像以太网集线器或以太网交换机节点那样的模拟设备。相反，它是一个运行 Cisco IOS 并配置了 16 端口交换模块 (`NM-16ESW`) 的 Dynamips 路由器。这是安装在真实的 Cisco 路由器上的相同交换模块，具有相同的功能和限制（详情请参见附录 C）。尽管交换模块的功能有限，但它非常适用于 CCNA 和许多 CCNP 研究。对于更高级的交换功能，你需要将真实的交换机集成到你的 GNS3 项目中或使用 Cisco IOU 交换机。

### 注意

`EtherSwitch router`需要你进行配置。要配置 EtherSwitch 路由器，从左侧列选择设备并点击`Configure`，如图图 7-3 所示。

`EtherSwitch router`不是像以太网集线器或以太网交换机节点那样的模拟设备。相反，它是一个运行 Cisco IOS 并配置了 16 端口交换模块 (`NM-16ESW`) 的 Dynamips 路由器。这是安装在真实的 Cisco 路由器上的相同交换模块，具有相同的功能和限制。

```
EtherSwitch router
```

![EtherSwitch 节点配置器](img/httpatomoreillycomsourcenostarchimages2209023.png.jpg)

图 7-3. EtherSwitch 路由器

# 帧继交换机

GNS3 提供了一个简单的`Frame Relay switch`，能够模拟帧继的基础功能。帧继交换机的好处是它需要非常少的配置。缺点是它有时可能不稳定。

## 警告

`Frame Relay switch`仅支持`ansi` LMI 类型。在帧继中，`数据链路标识符 (DLCI)`用于通过串口端口将帧分配给永久虚拟电路 (PVC)`。要将 DLCI 配置到串口端口，右键点击帧继交换机并打开节点配置器。使用`Source`和`Destination`字段创建映射。完成后，点击`Apply`和`OK`。

图 7-4 中的示例将在之后用于创建一个简单的帧继网络。

![帧继配置器](img/httpatomoreillycomsourcenostarchimages2209025.png.jpg)

图 7-4. 帧继配置器

# 简单的帧继轮型与星型型配置

配置帧继网络有多种方法，理解 DLCI 到串口的映射对于理解和配置任何一种方法都至关重要。为了更好地理解映射关系，让我们使用之前讨论的 DLCI 到串口映射来配置一个简单的网络。我不会涉及过多的理论，但会解释足够的内容让你开始。

这个简单的网络是 Frame Relay（帧中继）星型拓扑（hub and spoke topology）的一个示例，它可以让你很好了解 Frame Relay 网络中`DLCI`映射是如何工作的。路由器`R2`将位于`10.10.10.0`子网，路由器`R3`将位于`10.10.10.32`子网。路由器`R1`是我们星型拓扑中的中心节点。它将连接到两个子网，并通过 Frame Relay 交换机在它们之间转发数据包。此配置允许路由器`R2` ping 路由器`R3`，反之亦然。

要创建此项目，请向工作区添加一个 Frame Relay 交换机节点，并按照我们在图 7-4 中的方法进行设置。添加三个路由器，并为每个配置一个串口卡（如`WIC`或`NM-4T`）。如图所示将路由器连接到`FR1`交换机。确保`R1`连接到`FR1`的`Port 1`，`R2`连接到`Port 2`，`R3`连接到`Port 3`。在连接设备并并在`FR1`交换机上配置`Port:DLCI`映射后，按照如下代码配置中心节点路由器`R1`。

```
 R1(config)# interface Serial0/0
➊ R1(config-if)# encapsulation frame-relay
➋ R1(config-if)# frame-relay lmi-type ansi
➌ R1(config-if)# clock rate 64000
  R1(config-if)# no shutdown
  R1(config-if)# no ip address
```

在串口接口上，启用 Frame Relay 封装 ➊，并将`LMI`类型设置为`ANSI` ➋。虽然 GNS3 并不强制要求，但我设置设置了时钟速率 ➌，因为取决于你的`IOS`版本，在实际的 Frame Relay 交换机上可能需要该命令。

接下来，配置点对点接口和`DLCIs`。

```
➊ R1(config-if)# interface Serial0/0.100 point-to-point
➋ R1(config-subif)# frame-relay interface-dlci 100
➌ R1(config-subif)# ip address 10.10.10.1 255.255.255.224
➍ R1(config-subif)# interface Serial0/0.200 point-to-point
➎ R1(config-subif)# frame-relay interface-dlci 200
➏ R1(config-subif)# ip address 10.10.10.33 255.255.255.224
```

在串口接口`Serial0/0.100`上使用`DLCI` 100 ➋ 配置一个点对点子接口 ➊，并为该接口分配一个来自第一个子网的 IP 地址 ➌ (`10.10.10.0/27`)。以相同的方法添加第二个点对点接口 ➍ 以完成配置，但使用`DLCI` 200 ➎，并为接口分配来自第二个子网的 IP ➏ (`10.10.10.32/27`)。在这个示例中，我将使用子网中的第一个地址，即`10.10.10.33`。

### 注意

使用`DLCI`数字作为子接口编号被认为是 Cisco 的最佳实践。`Serial0/0.100`是`DLCI` 100 的子接口示例。以下列表包含了配置`R2`所需的所有命令。

```
 R2(config)# interface Serial0/0
➊ R2(config-if)# encapsulation frame-relay
➋ R2(config-if)# frame-relay lmi-type ansi
➌ R2(config-if)# clock rate 64000
  R2(config-if)# no shutdown
  R2(config-if)# no ip address
➍ R2(config-if)# interface Serial0/0.101 point-to-point
➎ R2(config-subif)# frame-relay interface-dlci 101
➏ R2(config-subif)# ip address 10.10.10.2 255.255.255.224
  R2(config-subif)# exit
➐ R2(config)# ip route 0.0.0.0 0.0.0.0 10.10.10.1
```



要配置`R2`，进入串口接口模式并启用 Frame Relay 封装 ➊，然后将`LMI`类型设置为`ANSI` ➋，设置时钟速率 ➌ 并启用接口。使用`DLCI` 101 ➎ 配置一个点对点子接口 ➍，并为子接口分配来自第一个子网的 IP 地址 ➏ (`10.10.10.0/27`)。最后，使用路由器`R1`接口`DLCI` 100 下配置的 IP 地址 ➐ 设置路由器的默认网关（`10.10.10.1`）。由于`R1`是我们的 Frame Relay 中心拓扑结构，它作为`R2`和`R3`之间路由的网关。

最后，为`R3`添加配置以完成项目。

```
R3(config)# interface Serial0/0
R3(config-if)# encapsulation frame-relay
R3(config-if)# frame-relay lmi-type ansi
R3(config-if)# clock rate 64000
R3(config-if)# no shutdown
R3(config-if)# no ip address
➊ R3(config-if)# interface Serial0/0.201 point-to-point
➋ R3(config-subif)# frame-relay interface-dlci 201
➌ R3(config-subif)# ip address 10.10.10.34 255.255.255.224
R3(config-subif)# exit
R3(config)# ip route 0.0.0.0 0.0.0.0 10.10.10.33
```

路由器`R3`的配置与`R2`几乎相同，但使用了`DLCI` 200 ➊ 以及来自第二个子网的 IP 地址 ➋ (`10.10.10.33`)。这就！所有路由器现在应该能够相互 ping。要验证 Frame Relay 电路是否激活，请在每个路由器上输入`show frame-relay`命令。

```
R1# show frame-relay

PVC for interface Serial0/0 (Frame Relay DTE)

             Active      Inactive       Deleted
Local         1             0            0
Switched        0             0            0
Unused          0             0            0
```

如果你设置正确，`PVCs`应该显示为`Active` ➊。

## 使用 IOS 创建 Frame Relay 交换机

尽管 Frame Relay 交换机很方便，但有时你可能创建自己的 Frame Relay 交换机。你可能想使用不同的`LMI`类型（如`q3a`），或者你的学习需要实际 Frame Relay 交换机的细节。在任何情况下，设置 IOS 交换机都非常简单。以下列表创建了与之前配置 Frame Relay 交换机具有`DLCI`映射相同的 IOS 交换机。它初看起来很复杂，但其实不然；你只需要理解如何使用`connect`命令来配置端口的`DLCI`。

```
➊ FRSW(config)# frame-relay switching
FRSW(config)# interface Serial0/0
FRSW(config-if)# description Serial connection to R1 (Hub)
FRSW(config-if)# no shutdown
FRSW(config-if)# no ip address
➋ FRSW(config-if)# encapsulation frame-relay
➌ FRSW(config-if)# clock rate 64000
➍ FRSW(config-if)# frame-relay lmi-type ansi
➎ FRSW(config-if)# frame-relay intf-type dce
FRSW(config-if)# interface Serial0/1
FRSW(config-if)# description Serial connection to R2 (Spoke)
FRSW(config-if)# no shutdown
FRSW(config-if)# no ip address
FRSW(config-if)# encapsulation frame-relay
FRSW(config-if)# clock rate 64000
FRSW(config-if)# frame-relay lmi-type ansi
FRSW(config-if)# frame-relay intf-type dce
FRSW(config-if)# interface Serial0/2
FRSW(config-if)# description Serial connection to R3 (Spoke)
FRSW(config-if)# no shutdown
FRSW(config-if)# no ip address
FRSW(config-if)# encapsulation frame-relay
FRSW(config-if)# clock rate 64000
FRSW(config-if)# frame-relay lmi-type ansi
FRSW(config-if)# frame-relay intf-type dce
FRSW(config-if)# exit
➏ FRSW(config)# connect PVC1 Serial0/0 100 Serial0/1 101
➐ FRSW(config)# connect PVC2 Serial0/0 200 Serial0/2 201
```

配置 Frame Relay 交换机时，你必须首先使用`frame-relay switching`命令 ➊ 启用 Frame Relay 交换。你还需要使用`encapsulation frame-relay`命令 ➋ 在每个串口接口上配置 Frame Relay 封装。然后，使用`clock rate`命令 ➌ 设置时钟速率，使用`frame-relay lmi-type`命令 ➍ 选择一种 LMI 类型，并使用`frame-relay intf-type dce`命令 ➎ 将接口类型设置为 DCE。启动接口后，你就可以定义你的 PVC 了。

### 注意

*在某些 IOS 版本上，`clock rate`命令可能需要输入为`clockrate`（无空格）。*

DLCI 到端口映射通过`connect connection-name interface dlci interface dlci`命令配置。此配置中的最后两个命令定义了两个 Frame Relay PVC 之间的连接映射。命令`connect PVC1 Serial0/0 100 Serial0/1 101` ➏ 定义了路由器`R1`和`R2`之间的 PVC，并用于创建我们的第一个子网。源接口为`Serial0/0`，源 DLCI 为`100`。PVC 通过接口`Serial0/1`和在路由器`R2`上配置的 DLCI `101`完成。

命令`connect PVC2 Serial0/0 200 Serial0/2 201` ➐ 使用相同的语法在路由器`R1`和`R3`之间创建第二个 PVC（用于第二个子网）。

创建你自己的 Frame Relay 交换机的操作就这些了。在使用 Cisco IOS 配置 Frame Relay 交换机时，LMI 类型可以设置为`cisco`、`ansi`或`q933a`，但你必须在所有参与 Frame Relay 路由上保持一致。

# ATM 交换机

GNS3 提供了一种简单配置 *异步传输模式 (ATM)* 交换机的方法。ATM 与 Frame Relay 相似之处在于它是一个二层协议，将物理端口映射到逻辑电路。

要配置 VPI/VCI 到端口映射，右键点击 ATM 交换机图标并选择 **Configure**（配置），如图 7-6 所示。在这里，我使用`ATM1`交换机节点上的两个端口配置了一个简单的虚拟电路。

![Node configurator](img/httpatomoreillycomsourcenostarchimages2209029.png.jpg)

图 7-6 节点配置器

使用 Source（源）和 Destination（目的）字段创建你的端口映射，然后点击 **Add**（添加）。当完成所有端口映射后，点击 **Apply**（应用）和 **OK**（确定）完成配置。

现在让我们快速运行一个使用 ATM 交换机创建简单点对 WAN 连接的示例。首先，按照图 7-7 所示创建拓扑。

![Sample ATM network](img/httpatomoreillycomsourcenostarchimages2209031.png.jpg)

图 7-7. 示例 ATM 网络

向你的工作区添加一个 ATM 交换机，并根据图 7-6 中的信息进行配置。接下来，添加两个路由器并在每个路由器与交换机之间建立链路。你需要使用*7200 系列路由器*，每个路由器都在槽位 1 中配置了*ATM 端口适配器* (`PA-A1`)。从每个路由器的`a1/0`建立一条连接到 ATM 交换机的链路，如图 7-7 所示，然后输入以下命令在路由器`R1`上配置 ATM。

```
R1(config)# interface ATM1/0
R1(config)# no shutdown
R1(config)# interface ATM1/0.100 point-to-point
R1(config-subif)# ip address 10.10.10.1 255.255.255.252
R1(config-subif)# pvc 25/100
R1(config-if-atm-vc)# protocol ip 10.10.10.2 broadcast
R1(config-if-atm-vc)# encapsulation aal5snap
```

接下来，对路由器`R2`应用类似的配置。

```
R2(config)# interface ATM1/0
R2(config)# no shutdown
R2(config)# interface ATM1/0.200 point-to-point
R2(config-subif)# ip address 10.10.10.2 255.255.255.252
R2(config-subif)# pvc 25/200
R2(config-if-atm-vc)# protocol ip 10.10.10.1 broadcast
R2(config-if-atm-vc)# encapsulation aal5snap
```

要验证你的 ATM 电路是否已建立，输入`show atm pvc`命令。

```
R1# show atm pvc
```

如果 PVC 状态显示`UP`，则两个路由器都已建立。

# 云节点 (Cloud Nodes)

云节点是一个高度可配置的设备，它并不模拟硬件。相反，它将 GNS3 设备连接到物理接口或其他网络。要配置连接，右键点击云图标并选择 **Configure**，如图 7-6 所示。

云节点提供了多种连接选项：

- **Ethernet**: 到物理或逻辑接口的连接。
- **UDP**: 到其他程序的套接连接。
- **TAP**: 到虚拟接口的连接。
- **UNIX**: 到其他应用程序的 UNIX 连接。
- **VDE**: 到虚拟分布式以太网设备的连接。
- **NULL**: 用于测试的虚拟链路。
- **Misc.**：允许重命名云节点。

要配置连接，选择连接类型、选择所需的选项，然后点击 **Add**。你可以为云节点配置多个连接，就像在路由器上使用多个接口一样。

在 Linux 系统上，你可能希望使用通用连接，这可能比 Linux 特定连接更可靠。原因之一是 Linux 特定连接可能会剥离传入的 VLAN 标签。如果你在 Linux 上配置连接遇到困难，请尝试两种方法看看哪种有效。

# 将 GNS3 设备连接到物理硬件

将项目连接到物理硬件的能力是将 GNS3 从一块顽石变为非洲之星的关键。通过云节点，你可以与真实的 Cisco 交换机建立链路，甚至从 GNS3 设备访问互联网。这为 GNS3 提供了无限的网络可能性。将 GNS3 连接到真实设备在某些系统上比其他系统更容易，但在所有主流操作系统上都应该是行的。

## Dynamips 权限

在将 GNS3 设备连接到物理以太网适配器之前，你可能需要在 PC 上进行一些更改。如果你的云节点在 Windows 系统上使用 NIO Ethernet 配置，你应该通过右键点击 GNS3 图标并选择以管理员身份运行。要使此选项永久化，右键点击 GNS3 图标并选择“属性”。选择兼容性选项卡并勾选“以管理员身份运行此程序”。

在基于 Unix 的系统上，在使用 NIO Ethernet 或 NIO TAP 连接之前，你需要提升 Dynamips 的权限。如果你跳过这一步，将不得不使用 root 账户运行 GNS3。否则，NIO 连接将失败，GNS3 会在 GNS3 控制台窗口中显示错误消息。

要在 OS X 上设置正确的 Dynamips 权限，请使用以下命令：

```
$ sudo chown root /Applications/GNS3.app/Contents/Resources/dynamips*
$ sudo chmod 4755 /Applications/GNS3.app/Contents/Resources/dynamips*
```

在大多数 Linux 发行版中设置权限的方法相同；只需如下列代码所示，将文件路径替换为你的`dynamips`文件的正确位置。如果你运行的是类似 Ubuntu 等基于 Debian 的 Linux 系统，请使用`setcap`命令，因为它更安全。

```
$ sudo apt-get install libcap2
$ sudo setcap cap_net_raw,cap_net_admin+eip /usr/local/bin/dynamips*
```

在更改 Dynamips 权限后，你可以以普通用户身份运行 GNS3，但 Dynamips 将被视为由 root 账户运行的。

## 为你的 PC 准备桥接（Bridge）

某些操作系统不允许 GNS3 直接与你电脑的以太网硬件通信，Wi-Fi 适配器通常也无法工作。在这些系统上使用以太网适配器运行 GNS3 之前，你可能需要安装额外的软件使其能够工作。

常见的解决方案是安装虚拟接口驱动程序，并使用桥接将其与电脑的物理以太网适配器关联。GNS3 然后将网络数据传递给虚拟接口，然后由虚拟接口通过桥接交给物理以太网接口。在基于 Unix 的系统中，虚拟接口通常使用 TUN/TAP 驱动提供。在 Windows 上，你将使用一个与物理以太网适配器桥接的环回适配器（loopback adapter）。

即使你电脑的以太网硬件可以直接与 GNS3 配合，仍推荐使用以下方法作为连接 GNS3 到外部世界的可靠预测方式。

## 在 Windows 上使用环回适配器

在 Windows 中，`loopback adapter driver`提供了一个虚拟网络接口，该接口可以桥接到你电脑上的物理以太网适配器。若要在 Windows 中添加环回适配器，请前往`控制面板` ▸ `设备管理器`。在列表中右键点击你的计算机名称，并选择`添加旧设备硬件`。点击“下一步”，选择“从列表手动选择要安装的硬件（高级）”，然后再次点击“下一步”。从列表中选择“网络适配器”并点击“下一步”。在“添加硬件”向导中（参考图 7-9），在厂商下选择`Microsoft`，然后向下滚动并选择名为`Microsoft Loopback Adapter`的网络适配器。点击“下一步”和“完成”完成安装。安装 Microsoft Loopback 适配器后，你必须重启 Windows。

也可以通过从 GNS3 安装目录运行`loopback-manager.cmd`命令来安装 Microsoft loopback 适配器。

要在环回适配器和以太网适配器之间创建桥接，请前往`控制面板` ▸ `网络和共享中心`并选择`更改适配器设置`。选择这两个适配器并右键点击以显示如图 7-10 所示的菜单。选择`桥接连接`在两个适配器之间创建桥接口。完成后，重启 Windows 使更改生效。

![选择 Microsoft Loopback 适配器](img/httpatomoreillycomsourcenostarchimages2209035.png.jpg)

图 7-9. 选择 Microsoft Loopback 适配器

![使用 Microsoft Loopback 适配器和以太网适配器创建桥接](img/httpatomoreillycomsourcenostarchimages2209037.png.jpg)

图 7-10. 使用 Microsoft Loopback 适配器和以太网适配器创建桥接

为了让 GNS3 在 Windows 系统上使用物理以太网适配器，你需要配置一个带有环回适配器的 Cloud 节点（参见将 GNS3 设备连接到物理硬件）。重命名你的环回适配器是一个好主意，这样它在 GNS3 中就可以被清晰识别。在示例中，我建议将`Local Area Connection 2`改为`Loopback`。

## OS X 上的 TUN/TAP 驱动



如果你使用 OS X，在 GNS3 访问物理以太网接口之前，你需要安装虚拟接口驱动程序。若要在 OS X 上安装 TUN/TAP 驱动，请从 SourceForge（`tuntaposx.sourceforge.net/`）下载适用于你 OS X 版本的驱动程序，运行安装程序并按照说明操作。

驱动程序应安装在 `/Library/Extensions` 下并在重启系统时自动加载。要手动加载驱动，切换到 `/Library/Extensions` 目录并输入以下内容：

```
$ sudo kextload tap.kext
```

在启动 GNS3 之前，输入以下命令为你的 TAP 接口设置权限。每次重启 Mac 时都必须输入该命令。

```
$ sudo chown $(id -un):$(id -gn) /dev/tap*
```

要激活 TAP 接口并将其桥接到电脑上的物理以太网端口，你必须在添加 Cloud 节点并将路由器连接到使用 `/dev/tap0` 配置的 `nio_tap` 接口*之后*输入以下命令。如果你提前输入命令，它们将失败且你的桥接将无法工作。

```
$ sudo ifconfig bridge0 create
$ sudo ifconfig bridge0 addm en0
$ sudo ifconfig bridge0 addm tap0 up
```

输入命令后，你应该使用 `ifconfig` 验证 Mac 以太网接口的名称，然后将 `en0` 替换为该名称。

### 注意

如果你更改接口的最大单元（MTU）大小，在创建桥接时可能会遇到错误 `ifconfig: BRDGADD tap0: Invalid argument`。在这种情况下，你需要确保物理接口的 MTU 大小与 TAP 接口的 MTU 大小匹配。

建议在项目中添加包含这些命令的注释，作为打开项目时的提醒。打开项目后，你可以复制注释并粘贴到终端。

## Ubuntu Linux TUN/TAP 驱动

在 Linux 上，你可以通过 Cloud 配置器下的 NIO 选项卡将 Cloud 节点直接连接到接口，但如果你发现 Ubuntu 需要 TUN/TAP 驱动，请更新包管理器并输入以下命令安装该包。

```
$ sudo apt-get install uml-utilities
```

如果你运行的是其他版本的 Linux，可能需要安装不同的包，但此包适用于大多数 Debian 发行版。

# 连接到实时交换机

GNS3 是一款很棒的软件，但它也有一些局限性。例如，`NM-16ESW` 交换模块并不包含实际第 2 层或第 3 层交换机的所有高级功能。如果你想处理高级交换功能，必须使用额外的软件（如 Cisco IOU）或使用物理 Cisco 交换机。如果你正在创建 CCNA 实验，一台实时交换机可能足够了，但如果你在创建 CCNP 或 CCIE 实验，你可能需要多个实时交换机。通常目标是让 GNS3 路由器连接到每个外部交换机。这很复杂，因为大多数电脑只有一个以太网适配器。幸运的是，GNS3 和 IOS 解决了这个问题。你的选择是通过电脑上的单个以太网适配器将 VLAN 汇干到交换机，或者在电脑中安装多个以太网适配器。

在本节中，我将介绍两种将 GNS3 设备连接到实时 Cisco 交换机方法。

* **标准 802.1Q Trunk**。这种方法使用标准的 802.1Q trunk 允许 GNS3 设备通过你 PC 上的以太网适配器与真实的 Cisco 交换机通信。

* **分叉交换机 (Breakout Switch)**。这种方法使用一个称为分叉交换机的特殊以太网交换机，允许 GNS3 设备通过 PC 中的单个以太网适配器连接到多个真实的交换机。要创建分叉交换机，你必须准备第二个物理以太网交换机作为分叉交换机。

你的选择取决于你拥有多少交换机、PC 操作系统以及 PC 中已安装哪些以太网适配器。让我们先看看 802.1Q trunk 是如何工作到达 Cisco 交换机的。

## 配置标准 802.1Q Trunk

在我看来，802.1Q trunk 是将真实交换机连接到你的 GNS3 项目的最佳方式。标准 802.1Q trunk 的优点是易于设置，且工作方式与将交换机连接到物理网络相同。缺点是你的 PC 操作系统或 PC 的以太网驱动程序可能不支持它。它们通常会剥离从交换机发往 PC 的数据包中的 802.1Q 标签。如果没有正确的标签，GNS3 无法知道数据包属于哪个 VLAN，反之也不知道将数据包转发到哪里，这破坏了你的网络。

如果你在网上搜寻，你会发现人们想出了许多规避此问题的创意解决方案，但这些方案通常针对特定平台，且因机器而异。

### 注意

防止 OS X 和 Linux 上剥离标签的一种方法是使用支持 802.1Q 标记和巨型帧的 USB 以太网适配器。其中一个好用的适配器是 StartTech USB31000SW，但任何使用 ASIX AX88772A 芯片的适配器都应该可以使用。

在这个示例中，你将在工作区放置一个 EtherSwitch 路由器或以太网交换机节点，并配置其配置 802.1Q trunk 协议。接下来，你向工作区添加一个 Cloud 节点并使用 NIO 接口对其进行配置，然后将其连接到 GNS3 交换机。Cloud 节点可以直接连接到 PC 的以太网适配器，也可以通过桥接连接（取决于你的操作系统）。然后你用以太网线从 PC 的以太网适配器连接到真实 Cisco 交换机的端口。你选择的交换机端口也需要配置 802.1Q trunk。在 GNS3 交换机和物理交换机都配置完成后，你应该能够通过 trunk 将 GNS3 生成的 VLAN 数据包路由到真实交换机。

在本节中，我们将创建一个简单的项目，使用两个 VLAN（10 和 20）将我们的 GNS3 网络连接到真实的 `c3550` 交换机。首先创建如图 7-11 所示的拓扑。在配置 Cloud 节点时，选择你的 PC 适配器名称（在 NIO Ethernet 选项卡下找到）。

![使用标准 dot1q trunk 连接真实交换机的示例拓扑](img/httpatomoreillycomsourcenostarchimages2209039.png.jpg)

图 7-11. 使用标准 dot1q trunk 连接真实交换机的示例拓扑。

要使用 EtherSwitch 路由器配置 VLAN 和 802.1Q trunk，在 `ESW1` 上打开控制台并输入以下命令：

```
ESW1# vlan database
➊ ESW1(vlan)# vlan 10
➋ ESW1(vlan)# vlan 20
  ESW1(vlan)# apply
  ESW1(vlan)# exit
  ESW1# configure terminal
  ESW1(config)# int f1/15
➌ ESW1(config-if)# switchport mode trunk
➍ ESW1(config-if)# switchport trunk encapsulation dot1q
  ESW1(config-if)# int f1/0
  ESW1(config-if)# switchport mode access
➎ ESW1(config-if)# switchport access vlan 10
  ESW1(config-if)# int f1/1
  ESW1(config-if)# switchport mode access
➏ ESW1(config-if)# switchport access vlan 20
```

之前的命令在交换机上创建了 VLAN 10 ➊ 和 20 ➋，使用 dot1q 协议 ➍ 配置了端口 ➌，并将接入端口分配给 VLAN 10 ➎（用于路由器 R2）和 VLAN 20 ➏（用于路由器 R3）。

如果你选择使用以太网交换机节点，将一个端口配置为 802.1Q trunk，并将其他端口配置为 VLAN 接入端口，如图 7-12 所示。

![配置了 dot1q trunk 端口的以太网交换机节点](img/httpatomoreillycomsourcenostarchimages2209041.png.jpg)

图 7-12. 配置了 dot1q trunk 端口的以太网交换机节点。

端口 1 和 2 是 802.1Q 接入端口，端口 3 是 802.1Q trunk 端口。要完成项目，连接到真实交换机并配置。以下是配置 `c3550` 交换机的示例：

```
c3550# configure terminal
c3550(config)# ip routing
c3550(config)# vlan 10
c3550(config-vlan)# ip address 10.0.0.1 255.255.255
c3550(config-vlan)# exit
c3550(config)# vlan 20
c3550(config-vlan)# ip address 20.0.0.1 255.255.255
c3550(config-vlan)# exit
c3550(config)# interface f0/1
c3550(config-if)# switchport encapsulation dot1q
c3550(config-if)# switchport mode trunk
c3550(config-if)# switchport trunk vlan 10,20
c3550(config-if)# exit
c3550(config)# interface f0/2
c3550(config-if)# switchport encapsulation dot1q
c3550(config-if)# switchport mode trunk
c3550(config-if)# switchport trunk vlan 10,20
c3550(config-if)# exit
c3550(config)# interface f0/3
c3550(config-if)# switchport mode access
c3550(config-if)# switchport access vlan 10
c3550(config-if)# exit
c3550(config)# interface f0/4
c3550(config-if)# switchport mode access
c3550(config-if)# switchport access vlan 20
c3550(config-if)# exit
```

这种交换方法至少需要两台真实的 Cisco 交换机；一台作为突破交换机（breakout switch），另一是你 GNS3 项目中一台或多个真实的 Cisco 交换机。突破交换机用于欺骗真实的 Cisco 交换机，使其认为你的每个 GNS3 路由器都通过以太网线`直接连接`到真实的交换机。实际上，你的 PC 仅使用一个以太网适配器将你所有的 GNS3 路由器连接到真实的交换机，而该适配器连接到突破交换机。然后，配置突破交换机将`所有 VLAN 分解`到各个接口，你使用以太网线将这些接口插入其他真实的 Cisco 交换机（每个 VLAN 一根）。我将这些称为`突破线`（breakout cables）。图 7-13 显示了你的 PC 和交换机的物理布局。

![使用突破交换机和真实 Cisco 交换机的物理布局](img/httpatomoreillycomsourcenostarchimages2209043.png)

图 7-13. 使用突破交换机和真实 Cisco 交换机的物理布局

以下是工作原理的概述。在你的 Linux 以太网适配器上使用 `vlan` 软件包配置突破 VLAN，并在突破交换机上配置 802.1Q 中继链路。在 GNS3 中，你将添加一个或多个 Cloud 节点，并使用 NIO 以太网接口配置 Linux 突破 VLAN。在你的 GNS3 项目中，每个路由器连接到 Cloud 节点的每个 VLAN 接口（每个接口一个路由器）。离开路由器的数据包进入 Cloud 节点，Linux 为它们打上 VLAN ID 标记并通过你 PC 的以太网适配器将其传递给突破交换机。突破交换机在标准的 802.1Q 中继端口上接收数据包。从那里，突破交换机利用 VLAN ID 识别并透明地将数据包传递给（或多个）真实的 Cisco 交换机。这种方法的巧妙之处在于，尽管你的 PC 只有一个以太网适配器，但每个 GNS3 路由器都有一根独立的以太网线连接到真实 Cisco 交换机的端口。

在 Linux 上设置突破交换机非常简单。首先更新你的包管理器并在你的 Ubuntu 系统上安装 VLAN 支持。

```
$ sudo apt-get install vlan
```

现在，使用 `modprobe` 命令启用 `8021q` Linux 模块。

```bash
$ sudo modprobe 8021q
```

接下来，增加以太网接口上的 MTU 帧大小，并使用 `vconfig` 命令创建你的突破 VLAN。确保将 `eth0` 替换为你的接口名称。

```
➊ $ sudo ifconfig eth0 mtu 1546
➋ $ sudo vconfig add eth0 10
➌ $ sudo vconfig add eth0 20
```

## 配置说明

### 备注

*你的以太网适配器必须支持高于标准最大 1500 字节的帧大小。*

增加帧大小 ➊ 为额外的 VLAN 标记留出了空间。为你的项目中的每个路由器创建一个突破 VLAN。在之前的列表项，我在我的 Linux PC 的 `eth0` 接口上创建了两个突破 VLAN（10 ➋ 和 20 ➌）。

### 备注

*不要将突破 VLAN 与你在 GNS3 项目中创建的 VLAN 混淆。重要的是，突破 VLAN 仅供 Linux 和突破交换机使用——它们不用于你的 GNS3 项目或真实的 Cisco 交换机。*

通过增加系统级 MTU 大小开始配置突破交换机。输入命令后，必须重启交换机才能生效。

```
Breakout(config)# system mtu 1546
```

交换机重启后，登录并按如下方式配置 802.1Q 中继链路：

```
 Breakout# configure terminal
  Breakout(config)# interface FastEthernet 0/1
➊ Breakout(config-if)# switchport trunk encapsulation dot1q
➋ Breakout(config-if)# switchport mode trunk
➌ Breakout(config-if)# switchport trunk allowed vlan all
```

你配置为中继的接口随后通过以太网线连接到 PC 的物理以太网适配器。如下所示，在中继端口 ➋ 上配置了 dot1q 封装 ➊，所有 VLAN ➌ 都允许通过中继。

接下来，进入你计划连接到真实交换机的每个接口，并为每个 VLAN 配置突破 VLAN 和 dot1q 隧道，如下列表所示：

```
 Breakout(config)# vlan 10
  Breakout(config-vlan)# vlan 20
  Breakout(config-vlan)# exit
  Breakout(config)# interface FastEthernet 0/2
  Breakout(config-if)# description GNS3 R1 Physical Uplink to Live Switch SW1
➊ Breakout(config-if)# switchport access vlan 10
➋ Breakout(config-if)# switchport mode dot1q-tunnel
➌ Breakout(config-if)# l2protocol-tunnel cdp
  Breakout(config-if)# interface FastEthernet 0/3
  Breakout(config-if)# description GNS3 R2 Physical Uplink to Live Switch SW2
➍ Breakout(config-if)# switchport access vlan 20
  Breakout(config-if)# switchport mode dot1q-tunnel
  Breakout(config-if)# l2protocol-tunnel cdp
```

当你完成向 Cloud 节点添加 breakout VLAN 后，请向你的工作区添加几个路由器，并为每个路由器创建一条到 Cloud 节点上 breakout VLAN 的链路。如在图 7-15 所示，路由器 R1 (F0/0) 使用 `nio_gen_eth:eth0.10` 连接到 Cloud 中的 VLAN 10，而 R2 (F0/0) 使用 `nio_gen_eth:eth0.20` 连接到 VLAN 20。

![使用 Cloud 节点连接到 Linux VLAN 的虚拟路由器](img/httpatomoreillycomsourcenostarchimages2209047.png.jpg)

图 7-15. 使用 Cloud 节点连接到 Linux VLAN 的虚拟路由器

由于 breakout 交换机仅用于将 VLAN 拆分到多个物理端口，因此不需要进一步的配置。在本例中，路由器 R1 现在已连接到插入 breakout 交换机端口 `f0/2` 的任何活动交换机，而 R2 应该连接到插入端口 `f0/3` 的任何活动交换机。

### Note

*如果你使用许多 VLAN 创建大型项目，可能可能只想为每个 Cloud 节点分配一个 Linux VLAN 接口，以帮助明确工作区的布局。*

你的 GNS3 路由器现在应该能够与一个或多个真实的 Cisco 交换机通信。

## 可选的 breakout 交换机配置



如果你正在运行 Windows 或 OS X，你可能可以使用 `GNS3 Switch` 节点将项目连接到 breakout 交换机，如图 7-16 所示。在此设置中，breakout 交换机的配置与之前相同，但你需要对 PC 进行一些调整。以太网交换机节点使用 `NIO` 接口连接到 `Cloud` 节点，在 Windows 上配置回环适配器（loop-back adapter），在 OS X 上配置 `TAP` 接口。该虚拟适配器桥接到你 PC 的物理以太网适配器上。这允许 `Cloud 1` 通过你 PC 的以太网适配器连接到 breakout 交换机。

![使用以太网交换机节点配置 breakout 交换机](img/httpatomoreillycomsourcenostarchimages2209049.png.jpg)

图 7-16. 使用以太网交换机节点配置 breakout 交换机

为了让 breakout 交换机工作，你应该增大 PC 物理以太网适配器的 `MTU` 大小，但并非所有的适配器都支持此功能。

如果你是 OS X 用户，必须在物理适配器和虚拟适配器上都增大 `MTU` 大小。要从命令行增大 `MTU` 大小，请使用示例：

```
$ sudo ifconfig en0 mtu 1546
$ sudo ifconfig tap0 mtu 1546
```

### Note

*在 OS X 上，使用相同的 `MTU` 大小配置虚拟和物理适配器，否则桥接创建将失败。*

你可能需要检查以太网适配器文档以在 Windows 上配置你的适配器。然而，在许多适配器上，`MTU` 设置可以在适配器的“高级”（Advanced）属性下找到，如图 7-17 所示。在本例中，`Intel PRO/1000 MT` 卡上的 `Jumbo Packet` 值设置为 9014 字节。

![在 Windows 上设置巨型帧包大小](img/httpatomoreillycomsourcenostarchimages2209051.png.jpg)

图 7-17. 在 Windows 上设置巨型帧包大小

接下来，打开以太网交换机节点的配置器来定义 `VLAN` 和 `dot1q` 继端口，如图 7-18 所示。

![配置用于 breakout 交换机的以太网交换机节点](img/httpatomoreillycomsourcenostarchimages2209053.png.jpg)

图 7-18. 配置用于 breakout 交换机的以太网交换机节点

在本例中，`R1` 连接到接入端口 1（VLAN 10），`R2` 连接到接入端口 2（VLAN 20），而端口 3 是到 breakout 交换机的 `dot1q` 继链路。在 GNS3 中完成所有配置后，你可以登录并按照之前描述的方法用 `VLAN` 和 `dot1q` 隧道配置 breakout 交换机。

## 在 PC 中使用多个适配器

与其使用 `802.1Q` 躯干或 breakout 交换机，你也可以为 GNS3 中的每个路由器使用一个物理以太网接口。如果你有一台笔记本，可以使用 USB 集线器并将多个 USB 以太网适配器连接到你的 PC；如果是台式机，你可以使用 USB 集线器方法或购买多口以太网卡。图 7-19 显示了该设计的物理布局。

![PC 中使用多个适配器的物理布局](img/httpatomoreillycomsourcenostarchimages2209055.png.jpg)

图 7-19. PC 中使用多个适配器的物理布局

# 创建一个简单的网络

通过在工作区中添加路由器和一个 `Cloud` 节点来创建一个项目，并添加一条从路由器到 `Cloud` 的链接。在图 7-20 中，`Cloud` 是使用 Windows 环回适配器配置的，命名为 `Local Area Connection 2`。

![使用 Windows 环回适配器连接到云](img/httpatomoreillycomsourcenostarchimages2209057.png.jpg)

图 7-20. 使用 Windows 环回适配器连接到云

要测试 Internet 连接性，请用以太网线从你的 PC 连接到互联网设备（如电缆调制解调器），并在你的 GNS3 路由器上配置 IP 地址。如果你像我这里一样使用 `DHCP` 分配 IP 地址，你可能需要等待片刻让路由器接收 IP 地址后才能测试连通性。

```
R1(config)# ip domain-lookup
R1(config)# ip name-server 8.8.8.8
R1(config)# interface f0/0
R1(config)# no shutdown
R1(config-if)# ip address dhcp

Mar 1 00:01:08.875: %DHCP-6-ADDRESS_ASSIGN: Interface FastEthernet0/0 assigned
DHCP address 192.168.1.101, mask 255.255.255.0, hostname R1
```

在路由器获取 IP 地址后，你应该能够 ping 通互联网上的主机。尝试 ping 一下[www.gns3.net](http://www.gns3.net)！你并不局限于使用路由器连接互联网；你还可以使用 `ASA` 设备、Juniper 路由器或任何支持 `TCP/IP` 的其他设备。

### 注意

如果你在路由器 `R1` 后面还有其他设备，你需要在 `R1` 上配置 `NAT`，它们才能路由到互联网。如需更多信息，请访问 Cisco 网站（[`www.cisco.com/en/US/tech/tk648/tk361/technologies_tech_note09186a0080094e77.shtml#topic6`](http://www.cisco.com/en/US/tech/tk648/tk361/technologies_tech_note09186a0080094e77.shtml#topic6)）。

### 总结

在本章中，我们查看了如何配置 GNS3 设备节点并使用 `Cisco IOS` 将它们集成到你的项目中。它们设置简单，非常适合大型项目，因为它们大大减少了 PC 的负载。与 `Dynamips` 设备相比，GNS3 设备节点几乎不消耗 PC 资源。

将 GNS3 设备连接到真实的 Cisco 交换机是复杂的。如果你选择创建一个标准的 `802.1Q` trunk 来连接到真实的交换机，可以使用 `EtherSwitch` 路由器或 `Ethernet` 交换机节点，但你的 PC 操作系统和以太网适配器驱动程序必须都支持 `802.1Q` 标记。如果没有正确的标记，trunk 将无法工作。

如果你有一个额外的 `IOS` 交换机，你可以创建一个分出交换机（breakout switch），这是将多个 Cisco 交换机集成到 GNS3 项目的一种非常可靠的方法。分出交换机在 Linux 上运行最可靠，也可以使用 Windows 和 OS X 进行配置。在下一章中，我们将查看一些高级功能，包括 `ASA`、`IDS/IPS`。

# 第 8 章 Cisco ASA、IDS/IPS 和 IOS-XR

你已经看到了 GNS3 与其他软件和操作系统交互的一些方式。在本章中，我们将深入研究 GNS3 的功能，并探索如何通过与额外的 `QEMU` 设备和软件交互来扩展你的项目。

了解如 Cisco 的 `ASAs`、入侵检测/防御系统（`IDS/IPS`）以及 `IOS-XR` 等技术可以拓宽你对 Cisco 和 GNS3 的视野，并在选择网络路径时非常有用。此外，玩玩这些大多数人无法访问的虚拟化 Cisco 产品也是很有趣。学习如何使用 Cisco 的一些基于 GUI 的工具也很重要。

我将首先向你演示如何安装 Cisco Configuration Professional（`CCP`）软件，这是一种通过命令行界面配置路由器的 Web 替代方案。接下来，你将学习如何配置和运行 `ASA`。我将讨论使用 Cisco 的适应安全管理器（`ASDM`）软件，它与之前提到的软件类似，但用于配置 `ASAs`。到本章结束，你将学会设置 `IDS/IPS` 时耐心不仅是一种美德，更是前提。最后，我将向你演示如何在 GNS3 中配置和使用 `IOS-XR` 设备。

# Cisco Configuration Professional

大多数工程师使用 `IOS` 命令来配置路由器和交换机，但还有其他方法。`CCP` 是一种基于 Web 的替代方案，使用“智能向导”来简化路由器配置，并提供工具帮助你监控和排除网络故障。简而言之，`CCP` 让经验少的用户也能让设备运行起来。

## 项目配置

要在 GNS3 中使用 `CCP`，你将使用一个路由器和一个运行 Windows 的 `VirtualBox` 虚拟机创建一个简单的项目，如图 8-1 所示。

![路由器和 Windows 的拓扑结构](img/httpatomoreillycomsourcenostarchimages220905.png.jpg)

图 8-1. 路由器和 Windows 的拓扑结构

禁用 Windows 防火墙以确保 `CCP` 能与路由器无限制通信（在本例中，10.10.10）。接下来，在路由器上进行配置。

```
➊ R1(config)# ip http server
R1(config)# ip secure-server
R1(config)# ip http authentication
➋ R1(config)# username 15 secret cisco
R1(config)# interface f0/0
➌ R1(config-if)# ip address 10.10.10.1 255.255.255.0
R1(config-if)# no shutdown
```

你需要启用路由器的 Web 服务器 ➊，创建一个具有完全执行权限的用户 ➋，并为接口分配 IP 地址 ➌。在本例中，路由器的 IP 地址为 `10.10.10.1`。

### 注意

创建一个具有完全执行权限的 Cisco 账户，以便以后可以使用 `CCP` 配置路由器。

配置路由器后，使用 `ping` 命令测试 Windows 客机与路由器之间的连通性。

```
C:> ping 10.10.10
```

如果成功 ping 通路由器，就可以继续。如果无法 ping 通路由器，请检查你的 IP 地址和接口。

## CCP 安装

`CCP` 是一个基于 Java 的应用程序，与 Web 浏览器交互，因此在开始之前，如果你还没有 `Java`，请下载并安装（[`www.java.com`](http://www.java.com)）。确保你还有最新版本的 Adobe Flash Player（[`www.adobe.com`](http://www.adobe.com)）。你可以从 Cisco 网站下载 Cisco Configuration Professional（[`www.cisco.com`](http://www.cisco.com)）。

要安装 `CCP`，登录你的 Windows 虚拟机并启动设置程序；你应该能看到 `CCP` 安装向导。点击“下一步”并按照指示完成设置。

## 运行 CCP

右键点击程序图标并选择“以管理员身份运行”启动 Cisco Configuration Professional。程序打开时，将要求输入要管理的路由器的 IP 地址。你应该看到 `CCP` 设备管理器，如图 8-2 所示。

![CCP 设备管理器](img/httpatomoreillycomsourcenostarchimages2209061.png.jpg)

输入你分配给路由器的 IP 地址（`10.10.10.1`），输入你之前分配的管理员用户名和密码（`admin` 和 `cisco`），然后点击 `OK`。登录后，你应该能看到 `CCP` 管理界面，如图 8-3 所示。

![Cisco CCP management screen](img/httpatomoreillycomsourcenostarchimages2209063.png.jpg)

图 8-3. Cisco CCP 管理界面。

在管理路由器之前，你必须首先点击路由器主机名 `R1` ➊，然后点击 `Discover` ➋，以便 `CCP` 能够发现它的功能和能力。被发现后，你可以点击工具栏中的 `Configure` ➌ 来设置路由器。使用 `CCP` 的优势在于，它可以引导你完成分配 IP 地址、`NAT`、VPN 以及其他 Cisco 特性的过程，而你不需要了解任何 `IOS` 命令。请注意，Cisco 认证考试主要关注 `IOS` 命令，而不是通过 `CCP` 来配置设备。

# Cisco ASA 防火墙

Cisco ASA 是旧版 PIX 防火墙的改进版本。GNS3 模拟了 Cisco ASA `5520`。虽然它不是路由器，但你可能会惊讶地发现 ASA 支持多种路由协议，包括 `RIP`、`EIGRP` 和 `OSPF`，允许你轻松地与其他 GNS3 路由设备建立网络连接。

## 获取镜像

在可以使用 GNS3 的 ASA 虚拟机之前，你需要一个 ASA 操作系统的镜像文件。获取 ASA 操作系统镜像最快的方法是从你已拥有的 ASA 中复制（即从 ASA 安装光盘或直接从 ASA 设备复制）。从 Cisco ASA 复制文件的方法与从 Cisco 路由器复制文件的方法相同：你可以使用 `FTP` 或 `TFTP`。在本例中，你将使用 `TFTP` 服务器。有很多免费的 `TFTP` 服务器可以选择，找一个你喜欢的并将其安装在 PC 上即可。

在你的网络上运行 `TFTP` 服务器后，登录你的物理 ASA 并将 ASA 镜像文件复制到 PC 上。在接下来的列表中，我的 ASA 镜像文件名为 `asa824-k8.bin`，我的 `TFTP` 服务器运行在 IP 地址为 `192.168.1.100` 的 PC 上：

```
ciscoasa# copy flash:asa824-k8.bin tftp
Address or name of remote host []? 192.168.1.100
```

获取 ASA 镜像文件后，你需要在使用 GNS3 之前对该文件进行一些修改。

## 为 GNS3 准备 ASA 镜像

Cisco ASA 实际上是一台小型 Linux PC，像 `asa824-k8.bin` 这样的 ASA 镜像文件包含了设计在 ASA 硬件上的精简 Linux 操作系统。

镜像文件包含 Linux 内核以及该设备的辅助软件。要使用 GNS3 运行 ASA 软件，你必须解压 `.bin` 文件，进行一些修改，并以适合 `QEMU` 的方式重新打包。幸运的是，Linux 和 Cisco 社区中有许多聪明的人，他们编写了镜像解包软件来为你完成这些工作。你可以从 GNS3 网站下载 Windows 版的 Cisco Image Unpacker，或者使用像 `repack.v4.sh` 这样的 Linux Shell 脚本。无论你选择哪种解包器，都需要找到一个适用于你的 ASA 软件版本的工具。运行脚本后，你应该会得到两个文件：`asa-vmlinuz`（Linux 内核）和 `asa-initrd.gz`（内存磁盘文件）。这些是 `QEMU` 和 GNS3 使用的文件。

如果你不想修改自己的 ASA 镜像文件，在互联网上快速搜索就能找到许多现成的 ASA 文件。这些镜像通常以 `.zip` 文件格式提供，其中包含两个文件（`asa-vmlinux` 和 `asa-initrd.gz`）。

## 为 ASA 配置 GNS3

在 GNS3 中配置 ASA 之前，请检查 PC 上是否安装并测试了 `QEMU`。（请参见第 6 章中针对你特定操作系统的 `QEMU` 安装信息）。接下来，启动 GNS3，在 Linux 和 Windows 上选择 `Edit` ▸ `Preferences`，或在 OS X 上选择 `GNS3` ▸ `Preferences`，并从左面板选择 `QEMU VMs`，如图 8-4 所示。

![QEMU VMs preferences](img/httpatomoreillycomsourcenostarchimages2209065.png.jpg)

图 8-4. QEMU VMs 偏好。

要在 GNS3 中创建新的 ASA，点击 `New` 启动新 QEMU VM 向导。在 `Type` 下拉菜单中选择 `ASA 8.4(2)`，如图 8-5 所示。

![Creating a new QEMU virtual machine and setting Type to ASA 8.4](img/httpatomoreillycomsourcenostarchimages2209067.png.jpg)

图 8-5. 创建新的 QEMU 虚拟机并将 Type 设置为 ASA 8.4。

默认情况下设备命名为 `ASA`，但你可以根据喜好重命名。完成后，点击 `Next` 继续。

向导应该自动找到正确的 `QEMU` 二进制文件，如图 8-6 所示。

![Selecting the ASA and memory](img/httpatomoreillycomsourcenostarchimages2209069.png.jpg)

图 8-6. 选择 ASA。

如果未找到 `QEMU` 二进制文件，请验证 PC 上是否正确安装了 `QEMU` 并重试。默认内存值为 `1024MB`，这是运行 ASA 所需的最小量。你可以通过在该字段输入新值来增加它。完成后，点击 `Next` 继续。

最后一步是浏览并选择你的内存磁盘和内核镜像，如图 8-7 所示。

![Linux boot-specific settings for ASA](img/httpatomoreillycomsourcenostarchimages2209071.png.jpg)

图 8-7. ASA 的特定启动设置。



将初始磁盘（initrd）和内核镜像设置为对应电脑的文件；这些文件通常命名为`asa824-initrd.gz`和`asa824-vmlinuz`。

选择完两个镜像后，点击`Finish`完成安装。成功添加 ASA 后，ASA 设备应显示在 QEMU VM 偏好窗口中，如图 8-8 所示。

![QEMU VMs preferences for ASA virtual machine](img/httpatomoreillycomsourcenostarchimages2209073.png.jpg)

图 8-8. ASA 虚拟机的 QEMU VM 偏好。

ASA 的当前设置将显示在右面板中，你需要注意的是 CPU throttling（位于 Optimizations）。

与 Dynamips 设备不同，ASA 没有 Idle-PC 选项来控制 CPU 消耗。这意味着 ASA 可能会消耗你的整个 CPU，就像未设置 Idle-PC 值的 Dynamips 路由器一样。为了防止这种情况，GNS3 使用另一个开源应用程序（`cpulimit`）来调整 QEMU/ASA 实例可以消耗的最大 CPU 数量。默认值为 80%，在大多数情况下都适用。你可以编辑 ASA 设置并提高或降低该值，但要小心：过低的 CPU（通过降低百分比）会导致 ASA 性能下降和频繁崩溃，而将百分比设置得过高可能会导致 PC 整体性能变慢。

在“优化”（Optimizations）下的另一个需要注意的设置是`Process priority`（进程优先级）。GNS3 的默认值为`low`，但可以设置为`low`、`medium`或`high`。`Process priority`决定了`QEMU/ASA`实例何时获取 CPU 时间。高优先级进程比低优先级进程先访问 CPU。通常情况下，更改优先级对您的系统几乎或没有影响，但为了安全起见，请保持设置为`low`，以防止您的 ASA 可能覆盖重要的系统进程。

在 Windows 和 OS X 上，安装 GNS3 时应该已经包含了`cpulimit`程序。在 Ubuntu Linux 上，您需要使用以下命令安装`cpulimit`：

```
$ sudo apt-get install cpulimit
```

现在你的 ASA 虚拟机不会接管你的系统了，让我们登录 ASA 并进行基础配置。

## 在 GNS3 中测试 ASA

从设备（Devices）工具栏拖入一个 ASA 防火墙节点到工作区。你的 ASA 应该位于工具栏的安全设备（Security Devices）部分。启动 ASA 并打开 GNS3 控制台连接。在加载期间，你应该能看到标准的 ASA 启动消息，随后是 ASA 命令行提示符：

```
ciscoasa>
```

提示符之前出现几条错误信息是完全正常的，但如果你的 ASA 无法启动或看到大量错误，请检查你的设置或尝试不同的 ASA 镜像文件。

### 注意

GNS3 中的 ASA 在启动循环期间挂起或停顿并不罕见，特别是在较旧的硬件上。如果发生这种情况，请停止并重启 ASA。可能需要尝试几次才能成功启动。

要测试简单的网络连通性，从 ASA 到工作区中的另一个 GNS3 设备建立链路。接下来，打开 ASA 的控制台连接并配置带有 IP 地址的接口。

```
ciscoasa> enable
ciscoasa# configure terminal
ciscoasa(config)# interface GigabitEthernet0
ciscoasa(config-if)# ip address 10.10.10.1 255.255.255.0
ciscoasa(config-if)# nameif inside
ciscoasa(config-if)# no shutdown
```

配置接口后，使用`ping`命令测试从 ASA 到项目项目中其他设备的连通性。

## 警告

即使启用了 CPU 限制，ASA 设备也是处理器密集型的，因此你可能希望在项目中谨慎使用它们，特别是当你有一台低端 PC 时。

在验证你的 ASA 设备运行正常后，你就可以准备开始将它们添加到项目中了。这对于学习如何配置 ASA 或准备 Cisco 认证考试将非常有帮助。

# ASDM 安装

Cisco 的 ASDM 与在 Cisco Configuration Professional 中过的`CCP`软件类似，因此许多细节是相同的。与 CCP 类似，ASDM 提供基于 Java 的点击式 Web 界面。CCP 和 ASDM 的关键区别在于 ASDM 设计用于配置 Cisco ASA，而不是其他 Cisco 设备。

在安装 ASDM 软件之前，创建一个类似于图 8-9 的项目。你将使用 Windows 虚拟机安装并运行 ASDM，然后启动 ASDM 并使用它来查看 ASA。

![ASDM topology with an ASA firewall and Windows guest](img/httpatomoreillycomsourcenostarchimages2209075.png.jpg)

图 8-9. 带有 ASA 防火墙和 Windows 客户端的 ASDM 拓扑结构

获取 ASDM 软件有两种方法：从真实 ASA 的闪存内存中复制它，或者在网上查找。获取 ASDM 软件后，需要将其将其存储在虚拟 ASA 的闪存驱动器中；从那里，你将使用浏览器将其安装到你的 Windows 虚拟机 PC 上。我推荐使用 Mozilla Firefox，因为我发现它运行 ASDM 的效果比 Internet Explorer 更好。（只需务必禁用任何弹出窗口拦截器和防火墙，并安装最新版本的 Java。）你还需要 FTP 或 TFTP 服务器软件，以便将 ASDM 软件从 GNS3 Windows 虚拟机复制到 ASA。

在获得 ASDM 镜像后，需要在 ASA 设备上进行一些准备工作，以便复制 ASDM 镜像。在 ASA 上输入这些命令：

```
ciscoasa(config)# interface gigabitEthernet0
➊ ciscoasa(config-if)# ip address 10.10.10.1 255.255.255.0
  ciscoasa(config-if)# nameif inside
  ciscoasa(config-if)# no shutdown
  ciscoasa(config-if)# exit
➋ ciscoasa(config)# username admin password cisco privilege 15
➌ ciscoasa(config)# http server enable
  ciscoasa(config)# http 10.10.10.0 255.255.255.0 inside
```

就像设置 CCP 一样，首先为 inside 接口分配 IP 地址 ➊。然后，创建一个本地用户账户 ➋，并启用 HTTP 服务器 ➌。

在 ASA 配置完成且你已经在 FTP 或 TFTP 服务器上拥有 ASDM 软件后，将软件从 Windows 虚拟机复制到 ASA 的闪存内存中。

```
ciscoasa# copy tftp flash
Source filename [] asdm-bin
Address or name of remote host [] 10.10.10.0
Destination filename [] asdm-bin
```

IDS/IPS 软件使用`QEMU`运行，因此在开始之前，请确保你已经在 PC 上安装了它并使用`GNS3`进行过测试。然后，为你的 IDS/IPS 创建一个构建目录，并将 ISO 文件复制到该目录中。这将是你创建 IDS/IPS 虚拟机的地方。

要在`QEMU`虚拟机上安装 IDS/IPS 软件，你必须创建两个`QEMU`虚拟硬盘镜像文件。打开终端窗口并输入以下命令来创建镜像：

```
$ qemu-img create ipsdisk1.img 512M
$ qemu-img create ipsdisk2.img 4000M
```

### Note

在 Windows 和 OS X 上，你可能需要设置系统路径以包含`QEMU`安装的位置。详情请参阅在 Windows 和 OS X 上安装 QEMU。

现在你已经创建了虚拟磁盘，输入以下命令从 ISO 镜像文件启动你的虚拟机：

```
$ qemu-system-i386 -hda ipsdisk1.img -hdb ipsdisk2.img -m 1024 -cdrom IPS-K9
-cd-1.1-a-6.0-6-E3.iso -boot d
```

在 Windows 系统上，将此命令中的`qemu-system-i386`替换为`qemu-system-i386w`。系统启动后，你应该能看到类似于图 8-13 的屏幕。

![IDS/IPS installation screen](img/httpatomoreillycomsourcenostarchimages2209083.png.jpg)

图 8-13. IDS/IPS 安装界面

在`boot:`提示符处，输入`k`执行全系统恢复。在恢复过程中，你的`QEMU`虚拟机将从 ISO 镜像启动 Linux，安装`GRUB`引导程序，并安装 IDS/IPS 软件。当安装完成文件复制后，虚拟机将自动重启并以“FATAL”启动错误消息结束，如图 8-14 所示。

![FATAL: No bootable device](img/httpatomoreillycomsourcenostarchimages2209085.png.jpg)

图 8-14. FATAL: 无可启动设备

不要担心，这个错误是完全正常且符合预期的。退出`QEMU`并输入以下命令重新启动 IDS/IPS：

```
$ qemu-system-i386 -name IPS4215 -hda ipsdisk1.img -hdb ipsdisk2.img -m
1024 -smbios type=1,product=IDS-4215 -net nic,vlan=1,model=e1000 -net
nic,vlan=2,model=e1000
```

IDS/IPS 虚拟机将启动到 Linux`GRUB`引导菜单。在引导菜单中，输入`e`编辑一个项目。使用方向键向下移动以高亮`kernel`项，并再次输入`e`编辑此条目。

使用左箭头键定位并将`init=/loadrc`更改为`init=1`。按回车键接受更改，并按`b`从修改后的`GRUB`菜单启动。系统现在应该启动，跳过 IDS/IPS 启动，并带你进入 Linux 控制台。从控制台命令行，你将使用`vi`编辑器修改一些 IDS/IPS 配置文件。

### Note

你必须使用`vi`编辑器修改文件，因为没有安装其他编辑器。如果你不熟悉`vi`，在继续之前可能想要复习一下。只需在网络上搜索`man vi`或在命令行中输入`man vi`来查看帮助页即可。

在你熟悉了`vi`编辑命令后，就可以继续操作了。

# 劫持硬件

首先，你需要欺骗 IDS/IPS 软件，让它认为你的`QEMU`虚拟机是一个真实的 Cisco IDS-4215 设备传感器。为了欺骗软件，你必须修改两个文件：`ids_functions`和`interface.conf`。修改这些文件非常繁琐，即使微小的错误也会导致你无法创建一个运行的 IDS/IPS 设备。

从 shell 提示符开始输入以下命令：

```
-sh-2.05b# /loadrc
-sh-2.05b# cd /etc/init.d
-sh-2.05b# ./rc.init
```

这将挂载 IDS/IPS 使用的 Linux 文件系统并初始化系统。接下来，使用`vi`打开`ids_functions`文件。

```
-sh-2.05b# vi ids_functions
```

打开文件后，输入命令`/845`让`vi`定位到以下条目：

```
elif [[ `isCPU 845` -eq $TRUE && $NUM_OF_PROCS -eq 1 ]]; then
        MODEL=$IDS4215
        HTLBL=8
        MEM_PAGES=${MEM_PAGES}
        DEFAULT_MGT="eth0"
```

修改`elif`语句和`DEFAULT_MGT`语句，使其读取如下：

```
elif [[ `isCPU 845` -eq $TRUE && $NUM_OF_PROCS -eq 1 ]]; then
        MODEL=$IDS4215
        HTLBL=8
        MEM_PAGES=${MEM_PAGES}
        DEFAULT_MGT="eth0"
```

当你完成编辑并确定修改无误后，保存文件并退出`vi`。接下来，你需要编辑`interface.conf`文件。

```
-sh-2.05b# vi interface.conf
```

使用方向键移动到以`IDS4215`开头的部分，确保每个接口都如下所示：

```
interface GigabitEthernet0/0
    type FastEthernet
    address 192.168.1.1
    mask 255.255.255.0
    gateway 192.168.1.254
interface GigabitEthernet0/1
    type FastEthernet
    address 10.0.0.1
    mask 255.255.255.0
    gateway 10.0.0.254
```

在你完成接口编辑后，滚动查看并确认每个接口都已正确。保存文件并退出`vi`。使用`reboot`命令重启 IDS/IPS 虚拟机。

```
-sh-2.05b# reboot
```

系统应该启动、配置一些设置然后再次重启。在自动重启后，当你看到`GRUB`引导管理器时，立即退出`QEMU`，如图 8-15 所示。如果你没有使用正确的选项就重新启动`QEMU`，安装将失败，你必须从头开始。

此时，你可以继续使用 IDS/IPS 虚拟机，也可以从头开始。我建议你重新开始并创建一个新的 IDS/IPS，直到你能够无错误地登录。如果你继续操作，IDS/IPS 系统可能会产生更多错误且无法按预期方式工作。

![“UNSUPPORTED HARDWARE DETECTED”错误](img/httpatomoreillycomsourcenostarchimages2209091.png.jpg)

图 8-17. “UNSUPPORTED HARDWARE DETECTED”错误

当你能够无错误地登录时，就可以继续操作了。

## 测试 IDS/IPS（或者耐心是美德）

当你第一次登录到 IDS/IPS 虚拟机时，需要等待大约 20 分钟左右，让系统重新构建其正则表达式缓存表。即使对于真实的 IDS/IPS 硬件设备这也是正常现象，你不应该中断它。你可以使用`iplog-status`命令定期检查进度。

```
sensor# iplog-status
```

如果状态消息显示“Error: getIpLogList: Analysis Engine is busy rebuilding regex tables. This may take a while.”，说明系统仍在运行，不应中断。重建完成后，你应该看到“No IP logs available.”。

重建完成后，输入`reset`命令来关闭并重启虚拟机。遗憾的是，没有一种优雅的方法来关闭系统。为了避免文件损坏，当重启到达 GRUB 启动菜单时，你应该退出 QEMU。

## 为 IDS/IPS 配置 GNS3

在 GNS3 中添加 IDS/IPS 与添加 ASA 类似。要添加 IDS/IPS 设备，请启动 GNS3，在 Linux 和 Windows 上选择**Edit**（编辑）▸**Preferences**（首选项），在 OS X 上选择**GNS3**▸**Preferences**，并从侧边栏选择**QEMU VMs**，如图 8-18 所示。

![IDS 首选项](img/httpatomoreillycomsourcenostarchimages2209093.png.jpg)

图 8-18. IDS Preferences

要在 GNS3 中创建新的 IDS/IPS，点击**New**（新建）启动新建 QEMU VM 向导。在 Type（类型）下拉菜单中选择**IDS**，如图 8-19 所示。

![在新建 QEMU VM 向导中选择 IDS](img/httpatomoreillycomsourcenostarchimages2209095.png.jpg)

图 8-19. 在新建 QEMU VM 向导中选择 IDS

默认情况下，你的设备被自动命名为`IDS`。点击**Next**（下一步）继续。GNS3 应该自动定位并为你的 PC 选择正确的 QEMU 二进制文件，如图 8-20 所示。

![QEMU 二进制文件和内存屏幕](img/httpatomoreillycomsourcenostarchimages2209097.png.jpg)

图 8-20. QEMU binary and memory screen

将 RAM 字段设置为**1024 MB**或更大，点击**Next**（下一步）继续到磁盘镜像（hda）选择，如图 8-21 所示。

![选择磁盘镜像](img/httpatomoreillycomsourcenostarchimages2209099.png.jpg)

图 8-21. Chooseing a disk image



浏览并选择在构建 QEMU 就绪 IDS 系统时创建的 `ipsdisk1.img` 文件。点击 **Next**（下一步）继续到磁盘镜像（hdb）选择界面并选择 `ipsdisk2.img`。点击 **Finish**（完成）以完成安装。现在，你已经准备好测试你的 IDS 了。

## 在 GNS3 中验证 IDS/IPS

为了验证你的 IDS/IPS 是否工作，请将 IDS/IPS 节点拖到你的工作区并启动设备。在 IDS/IPS 设备完全启动之前，GNS3 无法为其打开控制台连接。这意味着在登录提示符出现之前，你不会看到任何 IDS/IPS 消息。登录提示符出现后，你应该能够登录并配置 IDS/IPS。为了防止文件损坏，每当关闭设备时，请使用 `reset` 命令。

在确定你的 IDS/IPS 运行良好后，你应该对 QEMU 磁盘镜像文件进行备份。如果你的工作 IDS/IPS 设备发生任何故障，文件的备份副本可以在以后为你节省数小时的工作。

# Cisco IOS-XRv

Cisco 提供了一种 32 位虚拟机形式的 IOS-XR 版本，称为 IOS-XRv。IOS-XRv 的酷之处在于它不是像 IOU 或 NX-OSv 那样的仿真器。相反，它是“阉割版”的 IOS-XR，仅包含单个路由处理器（RP）。网络吞吐量限制为 2Mbps，并且有一个名为 `cisco`、密码为 `cisco` 的硬编码 AAA 用户，这使其无法在生产环境中使用，除非你需要一个缓慢且不安全的网络。尽管有这些限制，操作系统仍然包含管理功能、路由和转发能力。

## 为 IOS-XRv 配置 GNS3

Cisco 提供了一种 32 位虚拟机形式的 IOS-XR 版本，名为 IOS-XRv。IOS-XRv 的酷之处在于它不是像 IOU 或 NX-OSv 那样的仿真器。相反，它是“阉割版”的 IOS-XR，仅包含单个路由处理器（RP）。网络吞吐量限制为 2Mbps，并且有一个名为 `cisco`、密码为 `cisco` 的硬编码 AAA 用户，这使其无法在生产环境中使用，除非你需要一个缓慢且不安全的网络。尽管有这些限制，操作系统仍然包含管理功能、路由和转发能力。

## IOS-XRv 配置 GNS3

Cisco IOS-XRv 以两种格式提供：一个是 OVA，另一个是磁盘（VMDK）。OVA 镜像（后缀为 `.ova`）适用于 ESXi；VMDK 文件（后缀为 `.vmdk`）适用于 QEMU。

在 GNS3 中添加 IOS-XRv 与添加 ASA 类似。启动 GNS3，在 Linux 和 Windows 上选择 **Edit**（编辑）▸ **Preferences**（首选项），在 OS X 上选择 **GNS3**▸ **Preferences**，并从侧边栏选择 **QEMU VMs**。点击 **New**（新建）启动新建 QEMU VM 向导，如图 8-22 所示。

![新建 QEMU VM](img/httpatomoreillycomsourcenostarchimages220910.png.jpg)

图 8-22. IDS Preferences

在 Type（类型）下拉菜单中选择 **Default**。点击 **Next**（下一步）继续到 QEMU 二进制文件和内存设置，如图 8-23 所示。

![配置-XRv](img/httpatomoreillycomsourcenostarchimages220911.png.jpg)

图 8-23. IDS Preferences

为设备输入名称 `IOS-XRv`。由于我运行的是 64 位操作系统，我选择了 64 位的 QEMU 二进制文件 `qemu-system-x86_64`（如图 8-23 所示），并将 RAM 设置为 **2048 MB**，这是推荐值。然而，如果你运行的是 32 位操作系统（例如 Windows），你必须将 RAM 设置为小于 2048MB。这是因为 32 位的 QEMU 程序无法分配这么多内存。在这种情况下，你应该输入 **1920 MB** 并使用下拉菜单选择 QEMU 二进制文件 `qemu-system-i386w.exe`，如图 8-24 所示。

![32 位设置](img/httpatomoreillycomsourcenostarchimages220912.png.jpg)

图 8-24. IDS Preferences

点击 **Next**（下一步）继续到磁盘镜像选择界面，如图 8-25 所示。

![选择磁盘镜像](img/httpatomoreillycomsourcenostarchimages220913.png.jpg)

图 8-25. Selecting a disk image

点击 **Browse**（浏览）按钮来定位并选择你的 IOS-XRv 镜像的 `.vmdk` 镜像文件。我选择了名为 `iosxrv-k9-demo-5.2.2.vmdk` 的磁盘镜像。

当你完成图像选择后，点击 `Finish` 关闭向导。接下来，选择你新创建的 `IOS-XRv` 设备并点击 `Edit`。选择 `Network` 选项卡并将适配器数量增加到 `4`。点击 `OK` 关闭窗口，然后点击 `Apply` 和 `OK` 提交更改。你可以将适配器数量设置为最适合你需求的任何值，但四个对于大多数 GNS3 项目来说已经足够。

## 创建简单的 IOS-XR 项目

Cisco IOS-XR 与 IOS 非常非常相似，但它并不是 IOS。在本节中，你将使用一个 Dynamips 路由器和一个 `IOS-XRv` 设备来配置一个简单的项目，如图 8-26 所示。

![一个简单的 IOS-XRv 项目](img/httpatomoreillycomsourcenostarchimages2209109.png)

图 8-26. 一个简单的 IOS-XRv 项目

你将使用 `EIGRP` 从路由器 `R1` 向 `IOS-XRv1` 设备发布三个网络。最后，你将使用一些 IOS-XR 命令验证路由。这仅仅是对 IOS-XR 的基础介绍。如果你真的想学习 IOS-XR，你必须深入研究 Cisco 的文档。

### 配置路由器

从配置路由器 `R1` 开始。在连接到 `IOS-XRv1` 的以太网接口上配置 IP 地址。

```
R1# configure terminal
R1(config)# interface f0/0
R1(config-if)# ip address 10.1.1.1 255.255.255.0
R1(config-if)# no shutdown
```

接下来，在路由器 `R1` 的回 back 接口上配置三个 IP 地址。

```
R1(config-if)# interface loopback1
R1(config-if)# ip address 172.16.1.1 255.255.255.0
R1(config-if)# interface loopback2
R1(config-if)# ip address 172.16.2.1 255.255.255.0
R1(config-if)# interface loopback3
R1(config-if)# ip address 172.16.3.1 255.255.255.0
R1(config-if)# exit
```

这些地址将通过 `EIGRP` 发布到你的 `IOS-XRv1` 设备。最后，配置 `EIGRP` 并发布所有网络。

```
R1(config)# router eigrp 10
R1(config-router)# no auto-summary
R1(config-router)# network 10.0.0.0
R1(config-router)# network 172.16.0.0
```

完成路由器 `R1` 的配置后，配置 IOS-XR 设备。

#### 配置 IOS-XR 设备

登录 `IOS-XRv1` 并创建一个与你在路由器 `R1` 上创建的类似的配置。你将配置 IP 地址并启用 `EIGRP`，允许 `IOS-XRv1` 和路由器 `R1` 交换路由信息。

```
➊ RP/0/0/CPU0:ios#
  RP/0/0/CPU0:ios# configure terminal
  RP/0/0/CPU0:ios(config)# interface GigabitEthernet 0/0/0/0
➋ RP/0/0/CPU0:ios(config-if)# ipv4 address 10.1.1.2/24
  RP/0/0/CPU0:ios(config-if)# no shutdown
  RP/0/0/CPU0:ios(config)# router eigrp 10
➌ RP/0/0/CPU0:ios(config-eigrp)# address-family ipv4
➍ RP/0/0/CPU0:ios(config-eigrp-af)# interface GigabitEthernet 0/0/0/0
➎ RP/0/0/CPU0:ios(config-eigrp-af)# commit
```

IOS 和 IOS-RX 之间的第一个显著区别是命令提示符。`IOS-XRv1` 命令提示符 ➊ 表示你的上下文是第一个路由处理器（`RP/0/0/CPU0`）。因为这是 IOS-XR 的演示版本，所以它仅限于这一个路由处理器。

接下来，当以太网接口上配置 IP 地址时，你必须指定所使用的 IP 地址族（`IPv4` 或 IPv6），并且子网掩码用 CIDR 表示法（`/24`）➋。同样，在配置 `EIGRP` 路由进程时，你必须指定 IPv4 或 IPv6 ➌。最后，你通过将配置了 IP 的接口放在 `EIGRP` 路由进程下 ➍ 来发布网络。完成后，确保提交你的更改 ➎。

一旦配置好所有内容，输入 `show eigrp neighbors` 命令，你应该能看到此输出：

```
RP/0/0/CPU0:ios# show eigrp neighbors
IPv4-EIGRP Neighbors for AS(10) VRF default

H   Address                 Interface      Hold Uptime   SRTT   RTO  Q   Seq
                                           (sec)         (ms)        Cnt
0   ➊10.1.1
```

当你完成图像选择后，点击 `Finish` 关闭向导。接下来，选择你新创建的 `IOS-XRv` 设备并点击 `Edit`。选择 `Network` 选项卡并将适配器数量增加到 `4`。点击 `OK` 关闭窗口，然后点击 `Apply` 和 `OK` 提交更改。你可以将适配器数量设置为最适合你需求的任何值，但四个对于大多数 GNS3 项目来说已经足够。

## 创建一个简单的 IOS-XR 项目

Cisco IOS-XR 与 IOS 非常相似，但它并不是 IOS。在本节中，你将使用一个 Dynamips 路由器和一个 `IOS-XRv` 设备来配置一个简单的项目，如图 8-26 所示。

![一个简单的 IOS-XRv 项目](img/httpatomoreillycomsourcenostarchimages2209109.png)

图 8-26. 一个简单的 IOS-XRv 项目

你将使用 `EIGRP` 从路由器 `R1` 向 `IOS-XRv1` 设备发布三个网络。最后，你将使用一些 IOS-XR 命令验证路由。这仅仅是对 IOS-XR 的基础介绍。如果你真的想学习 IOS-XR，你必须深入研究 Cisco 的文档。

### 配置路由器

从配置路由器 `R1` 开始。在连接到 `IOS-XRv1` 的以太网接口上配置 IP 地址。

```
R1# configure terminal
R1(config)# interface f0/0
R1(config-if)# ip address 10.1.1.1 255.255.255.0
R1(config-if)# no shutdown
```

接下来，在路由器 `R1` 的回 back 接口上配置三个 IP 地址。

```
R1(config-if)# interface loopback1
R1(config-if)# ip address 172.16.1.1 255.255.255.0
R1(config-if)# interface loopback2
R1(config-if)# ip address 172.16.2.1 255.255.255.0
R1(config-if)# interface loopback3
R1(config-if)# ip address 172.16.3.1 255.255.255.0
R1(config-if)# exit
```

这些地址将通过 `EIGRP` 发布到你的 `IOS-XRv1` 设备。最后，配置 `EIGRP` 并发布所有网络。

```
R1(config)# router eigrp 10
R1(config-router)# no auto-summary
R1(config-router)# network 10.0.0.0
R1(config-router)# network 172.16.0.0
```

完成路由器 `R1` 的配置后，配置 IOS-XR 设备。

#### 配置 IOS-XR 设备

登录 `IOS-XRv1` 并创建一个与你在路由器 `R1` 上创建的类似的配置。你将配置 IP 地址并启用 `EIGRP`，允许 `IOS-XRv1` 和路由器 `R1` 交换路由信息。

```
➊ RP/0/0/CPU0:ios#
  RP/0/0/CPU0:ios# configure terminal
  RP/0/0/CPU0:ios(config)# interface GigabitEthernet 0/0/0/0
➋ RP/0/0/CPU0:ios(config-if)# ipv4 address 10.1.1.2/24
  RP/0/0/CPU0:ios(config-if)# no shutdown
  RP/0/0/CPU0:ios(config)# router eigrp 10
➌ RP/0/0/CPU0:ios(config-eigrp)# address-family ipv4
➍ RP/0/0/CPU0:ios(config-eigrp-af)# interface GigabitEthernet 0/0/0/0
➎ RP/0/0/CPU0:ios(config-eigrp-af)# commit
```

IOS 和 IOS-RX 之间的第一个显著区别是命令提示符。`IOS-XRv1` 命令提示符 ➊ 表示你的上下文是第一个路由处理器（`RP/0/0/CPU0`）。因为这是 IOS-XR 的演示版本，所以它仅限于这一个路由处理器。

接下来，当以太网接口上配置 IP 地址时，你必须指定所使用的 IP 地址族（`IPv4` 或 IPv6），并且子网掩码用 CIDR 表示法（`/24`）➋。同样，在配置 `EIGRP` 路由进程时，你必须指定 IPv4 或 IPv6 ➌。最后，你通过将配置了 IP 的接口放在 `EIGRP` 路由进程下 ➍ 来发布网络。完成后，确保提交你的更改 ➎。

一旦配置好所有内容，输入 `show eigrp neighbors` 命令，你应该能看到此输出：

```
RP/0/0/CPU0:ios# show eigrp neighbors
IPv4-EIGRP Neighbors for AS(10) VRF default

H   Address                 Interface      Hold Uptime   SRTT   RTO  Q   Seq
                                           (sec)         (ms)        Cnt
0   ➊10.1.1
```

2010 年，Cisco 将 `IOU` 集成到 Cisco Learning Network 中，为 CCNA 和 CCNP 学生提供在线虚拟实验室。这些实验室价格低廉且设计良好。如果你对 Cisco Learning Labs 感兴趣，应该查看 Cisco Learning Center（[`learningnetwork.cisco.com/`](http://learningnetwork.cisco.com/)）。

正如其名称所示，Unix 上的 `IOS` 仅运行在基于 Unix 的系统上。它有时被称为 Linux 上的 `IOS`（`IOL`），是在 Solaris Unix 和 Linux 上开发的。

## 这里的 IOU 对 GNS3 意味着什么

在 Cisco 宣布其放弃行业标准硬件，转而使用专有的集成服务路由器（`ISR`）硬件之后，GNS3 社区疑惑 `Dynamips` 和 `GNS3` 的时代是否已经结束。由于无法获取新专有硬件的技术规范，无法创建运行最新 `IOS` 软件所需的新虚拟机管理器（hypervisor）。最终，旧的 `Dynamips` 设备将停止 `IOS` 更新并过时。

Cisco 实际上为 GNS3 使用的 7200 系列路由器维护着最新的 `IOS`，但所有其他 GNS3 路由器在 `IOS` 版本 12.4(15)T 处停止了更新，这限制了对 VoIP 等现代技术的学习。这就是为什么 `IOU` 令人兴奋的原因。它允许你将更新的 `IOS` 技术集成到你的 GNS3 项目中，为 `GNS3` 注入了新的活力——这非常酷！

## 交换、交换、更多的交换！

将 `IOU` 集成到 `GNS3` 的最佳理由之一是你可以使用 Cisco 的许多高级交换功能，而这些功能在 `Dynamips` 的 `NM-16ESW` 模块中是缺失（参考附录 C“附录 C. NM-16ESW 和 IOU L2 限制”）。这些功能允许 GNS3 提升水平，成为适用于 CCIE 等更高级认证的全方位培训工具。



有了 `IOU`，你不再需要购买物理交换机并创建分线交换机（breakout switch），或者使用像 `ISL` 桥接这样的奇技技巧来访问真实的交换机。使用 GNS3 `EtherSwitch` 路由器，现在可以从你的 Dynamips 交换机创建一个标准的 `802.1Q` 链路，连接到运行在你 PC 上的 `IOU` 交换机组。`IOU` 交换机稳定、运行快速，而且与物理交换机不同，它们是完全便携的，这意味着它们可以作为你 GNS3 项目的一部分随笔记本电脑携带。

## IOU 镜像

IOU 镜像围绕 `IOS` 功能设计，其文件名通常揭示了它们包含的功能，就像 `IOS` 镜像文件名一样。例如，让我们分解名为 `I86BI_LINUXL2-UPK9-M-15.0` 的 IOU 交换机的文件名。

- `I86BI`：表示这是一个 Intel 32 位的二进制镜像。
- `LINUX`：表示它运行在 Linux 上。
- `L2`：表示它是一个 L2/L3 交换机。
- `UPK9`：表示镜像包含高级加密功能，如 `3DES`/`AES`。
- `M`：表示它是主线（mainline）`IOS`。
- `15.0`：指定了镜像所基于的 `IOS` 版本。

利用这些信息，你应该能够通过查看几乎任何 IOU 文件名来快速确定它包含哪些功能。

## 安装 IOU 之前需要知道的事

默认情况下，标准的 GNS3 安装不允许你运行 `IOU` 设备。`IOU` 设备是 Linux 二进制文件，因此只能在 Linux 操作系统上运行。通常，镜像是 32 位二进制文件，但有了适当的库文件，你可以轻松地在 64 位 Linux 系统上运行它们。

如果你在 Windows 或 OS X 上运行 GNS3，你必须安装像 `VirtualBox` 这样的虚拟化程序，并使用 Linux 虚拟机运行 `IOU` 设备。幸运的是，GNS3 提供了一个可以从 GNS3 网站下载的 `IOU` 虚拟机。GNS3 IOU 虚拟机已准备好运行 IOU 镜像，为你提供了一种简易的上传镜像的方法，并且不需要你了解如何使用 Linux 命令。

在 Linux 中运行 GNS3 的优点是安装和配置 `IOU` 更加直接，且一切都应该无缝运行，无需额外配置。缺点是你必须了解一点 Linux，但在我看来，这是一个很小的代价。

当你在 Windows 或 OS X 上运行 GNS3 时，你必须配置它通过 `TCP/IP` 与 Linux 虚拟机通信，这管理起来非常麻烦。如果你的工作站或 IOU 虚拟机的 IP 地址发生变化（经常发生），你必须重新配置 GNS3 使用新的 IP 地址。此外，当你升级 GNS3 时，必须升级运行在 IOU 虚拟机上的 GNS3 服务器软件。版本号必须一致，否则 IOU 将无法运行。当你在 Linux 上同时运行 GNS3 和 IOU 时，这些步骤是不必要的。

# 在 Linux PC 上设置 IOU

在 Linux PC 上运行 GNS3 和 IOU 有一些明显的优势。最大的优点是你不需要使用 IOU 虚拟机，因为 IOU 镜像文件在 Linux 上是原生运行的。这意味着你不需要放弃 IOU 虚拟机将占用的宝贵资源（如 CPU 周期和内存）。

另一个优势是你可以使用 `Wireshark` 捕获和监控两个 IOU 设备之间的包，而使用 IOU 虚拟机时无法做到这一点。这是因为在启动 Wireshark 捕获时生成的 `.pcap` 捕获文件保存在 IOU 虚拟机而非本地，因此 `Wireshark` 无法访问该文件。

如果你在 Linux 上运行 GNS3，请按照本节中的指令使 IOU 运行。否则，请跳到“在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机”。

## 安装 IOU

运行 IOU 镜像时，镜像会寻找文件 `libcrypto.so.4`，没有它将无法运行。虽然系统中可能已经安装了 `libcrypto` 库文件，但你应该安装 `libssl1.0.0`，因为该版本被证明与 IOU 镜像配合稳定。

接下来，从 `libcrypto.so.1.0.0` 创建 `libcrypto.so.4` 的符号链接（sym-link）；符号链接是 Windows 快捷方式的 Linux 等价物。

```bash
ln -s libcrypto.so.1.0.0 libcrypto.so.4
```

在位 Ubuntu 系统上运行时，你需要使用以下命令安装 32 位的 `libssl` 包：

```bash
sudo apt-get install libssl1.0.0:386
sudo ln -s /lib/i386-linux-gnu/libcrypto.so.1.0.0 /lib/i386-linux-gnu/libcrypto.so.4
```

配置好 `libcrypto.so.4` 后，将一个或多个 IOU 镜像文件复制到你的 Ubuntu 系统。你必须在运行之前赋予 IOU 文件执行权限，方法如下：

```bash
sudo chmod 555 I86BI_LINUXL2-UPK9-M-15.0.bin
```

接下来，安装 GNS3 程序所需的依赖项。该程序负责设置 IOU 与其他 GNS3 设备（如 Dynamips 路由器）之间的通信。首先安装 `bison` 和 `flex`，这是编译 `iouyap` 需要的两个包。

```bash
sudo apt-get install bison
sudo apt-get install flex
```

现在，使用以下命令安装并编译 `iniparser` 程序：

```bash
sudo apt-get install git
git clone http://github.com/ndevilla/iniparser.git
cd iniparser
make
sudo cp libiniparser.* /usr/lib/
sudo cp src/iniparser.h /usr/local/include
sudo cp src/dictionary.h /usr/local/include
```

包含 `iouyap` 的 ZIP 压缩包应该包含在你的 GNS3 Linux 下载包中。解压 `iouyap-<x>.zip`（将 `<x>` 替换为你所拥有的版本），并使用以下命令编译程序：

```bash
cd iouyap-x
sudo make
sudo make install
```

如有必要，将编译后的应用程序拷贝到 `/usr/local/bin` 目录。

```bash
sudo cp iouyap /usr/local/bin
```

现在所有应用程序已安装完毕，你需要进行一些配置。

## 创建许可证文件

在运行 IOU 之前，你必须创建一个包含你的 PC 主机名（hostname）和有效许可证密钥的许可证文件。许可证密钥根据你的 Linux 主机名生成，因此请确保你对 PC 的主机名满意。如果你更改了主机名，将需要输入新的许可证密钥。

一旦获取了许可证密钥，请使用文本编辑器创建许可证文件。我通常将文件命名为 `.iourc`，但任何名称都可以。以下是一个名为 Ubuntu 的 PC 对应许可证密钥 `1234567812345678` 的许可证文件示例。主机名对大小写敏感，因此在许可证文件中输入时请务必小心。

```ini
[license]
Ubuntu = 1234567812345678
```

如果你不确定你的 Linux 主机名称，可以使用终端中的 `hostname` 命令来显示该名称。

## 配置 GNS3

接下来，在 IOS on UNIX 偏好中设置 `iouyap` 应用程序的路径以及你的 IOU 许可证文件。`iouyap` 应用程序用于将 Dynamips 以及其他 GNS3 设备与 IOU 设备桥接，以便你的所有设备能够无缝连接在一起。

选择 **Edit（编辑）** ▸ **Preferences（偏好选项）**，然后从左侧菜单选择 **IOS on UNIX**，如图 9-1 所示。

![IOS on UNIX preferences, General settings tab](img/httpatomoreillycomsourcenostarchimages2209111.png.jpg)

图 9-1. IOS on UNIX preferences, General settings tab

在 General（常规）设置选项卡中，在 Path to IOURC 中设置你的许可证文件的路径和名称。这指的是你之前创建的 IOU 许可证文件。同样，在 Path to iouyap 中设置你的 `iouyap` 文件的路径，通常为 `/usr/local/bin/iouyap`。接下来，转到 Server（服务器）设置选项卡，如图 9-2 所示。

勾选 **Always use the local server (Linux only)**（始终使用本地服务器（仅限 Linux））复选框，以便 IOU 使用本地 PC 进行 GNS3 和 IOU 的集成。然后，转到 Advanced（高级）设置选项卡，如图 9-3 所示。

每个 IOU 设备在定义的范围内都被分配了一个唯一的控制端口号。除非该范围与你 PC 上运行的其他基于 IP 的应用程序发生冲突，否则不要更改这些值；UDP 隧道端口范围也是如此。UDP 端口用于建立 IOU 与其他 GNS3 设备之间的网络通信。

![IOS on UNIX preferences, Server settings tab](img/httpatomoreillycomsourcenostarchimages2209113.png.jpg)

图 9-2. IOS on UNIX preferences, Server settings tab

![IOS on UNIX preferences, Advanced settings tab](img/httpatomoreillycomsourcenostarchimages2209115.png.jpg)

图 9-3. IOS on UNIX preferences, Advanced settings tab

最后，展开 Preferences 窗口左侧菜单中的 **IOS on UNIX**，以显示 IOU 设备部分，如图 9-4 所示。从这里，你可以向 GNS3 添加一个或多个 IOU 镜像文件。

![Adding IOU images to GNS3](img/httpatomoreillycomsourcenostarchimages2209117.png.jpg)

图 9-4. Adding IOU images to GNS3

要向 GNS3 添加 IOU 镜像文件，点击 **New（新建）** 按钮启动 New IOU 设备向导，如图 9-5 所示。

![New IOU device wizard](img/httpatomoreillycomsourcenostarchimages2209119.png.jpg)

图 9-5. New IOU device wizard

为你的新设备输入名称（在本例中为 `IOU_L2`）；然后点击 **Browse（浏览）** 按钮定位并选择你的 IOU 镜像文件。完成后，点击 **Finish（完成）** 结束向导。添加后，你的 IOU 镜像文件应被拷贝到 GNS3 用户目录下的 `GNS3/images/IOU` 中。

要配置 IOU 设备，请从 IOU devices 部分拖入 IOU 设备图标到你的工作区。右键点击设备以打开配置器，如图 9-6 所示。

![IOU configurator](img/httpatomoreillycomsourcenostarchimages2209121.png.jpg)

图 9-6. IOU configurator

General 选项卡上的选项允许你重命名设备并更改控制端口号和 RAM 值。默认为两个，但你可以根据需要调整数量。在 Network 选项卡中，设置以太网和串口适配器的数量。默认为两个，但你可以根据需要调整数量。适配器的总数不能超过 16，每个 IOU 设备共有 64 个接口。

要导出 IOU 配置，从 IOU 控制台输入 `copy running-config unix:initial -cfg`，然后右键点击设备并选择 Export。系统将提示输入文件名和保存位置。你也可以选择 Import 来导入。

如果你想在 Windows 或 macOS 上运行 IOU，请阅读下一节。否则，你可以跳到 NX-OSv。

# 在 Windows 和 macOS 上使用 GNS3 IOU 虚拟机

正如我在“安装 IOU 之前需要知道的事”中提到的，Windows 和 macOS 系统只能通过 Linux 虚拟机运行 IOU。如果你还没有，请下载并安装 VirtualBox（[`www.virtualbox.org/`](https://www.virtualbox.org/)）。接受默认安装设置应提供运行 IOU 虚拟机所需的所有内容。

安装 VirtualBox 后，访问 GNS3 网站（[`www.gns3.com/`](http://www.gns3.com/)）并下载名为 `GNS3 IOU VM.ova` 的 OVA 文件。这是一个预配置了运行 IOU 所需工具的 Linux 虚拟机，但它不包含任何 IOU 镜像文件。相反，它提供了一个 Web 工具，让你能够轻松上传镜像文件到设备，但在使用之前，你需要将设备导入 VirtualBox。

## 将 GNS3 IOU 虚拟机导入 VirtualBox

首先启动 VirtualBox 应用程序。程序加载后，选择 **File（文件）** ▸ **Import Appliance（导入设备）**。你将看到导入虚拟机设备的对话框，如图 9-7 所示。

![Select the virtual appliance.](img/httpatomoreillycomsourcenostarchimages2209123.png.jpg)

图 9-7. Select the virtual appliance.

使用浏览图标定位并选择 `GNS3 IOU VM.ova` 文件。在图 9-7 中，我的虚拟机位于我的 `Downloads` 目录，即 `C:\Users\jneumann\Downloads`。一旦选择了该文件，点击 **Next**（下一步）并验证设备设置。它们看起来应该与图 9-8 相似。

![Virtual Appliance settings](img/httpatomoreillycomsourcenostarchimages2209125.png.jpg)

图 9-8. 虚拟机设备设置

你应该接受建议的设备设置。请注意，默认 RAM 设置为 2048MB。我发现，如果你在项目中仅使用少数几个 IOU 设备，可以将 RAM 减少到 1024MB。这样做可以减少 PC 占用的内存总量，并且在资源紧张时可能帮助 GNS3 运行得更好。如果你不确定，只需接受默认设置并点击 **Import**（导入）完成导入。你以后可以修改设置。

导入虚拟机后，点击 **Settings**（设置），然后点击 **Network**（网络）访问网络面板，如图 9-9 所示。

![Bridge the network adapter to your PC.](img/httpatomoreillycomsourcenostarchimages2209127.png.jpg)

图 9-9. 将网络适配器桥接到你的 PC。

在 Adapter 1 卡中，选择 **Enable Network Adapter**（启用网络适配器）选项。然后，在 Attached（连接到）字段旁边选择 **Bridged Adapter**（桥接适配器）。完成后，点击 **OK**。这会将你的虚拟机的以太网适配器桥接到你的 PC，并允许其访问互联网，以便在需要时安装额外的包。

## 上传 IOU 镜像文件

现在你已经导入了 GNS3 IOU 虚拟机，你应该能够运行虚拟机并上传你的 IOU 镜像文件了。要启动虚拟机，选择 **GNS3 IOU VM**，如图 9-10 所示，并点击 **Start**（启动）。

![Select and start your GNS3 IOU virtual machine.](img/httpatomoreillycomsourcenostarchimages2209129.png.jpg)

图 9-10. 选择并启动你的 GNS3 IOU 虚拟机。

虚拟机启动一两分钟是正常的，因为它正在启动一个功能完整的 Linux 操作系统。虚拟机运行后，屏幕上应该会显示类似下面的控制消息：

```text
Welcome to GNS3 IOU appliance
Use 172.16.231.204 to configure a remote server in GNS3 Preferences
Use your browser with http://172.16.231.204:8000/upload to upload IOS images

gns3-iouvm login:
```

注意，屏幕指示你使用 PC 的网络浏览器将 IOU 镜像文件上传到设备。要使此生效，你的 PC 和 GNS3 IOU 虚拟机必须分别从你的本地网络分配 IP 地址。在示例中，我的虚拟机的 IP 地址是 `172.16.231.204`。

### 注意

有时 IOU 虚拟机可能不显示 IP 地址。在这种情况下，使用用户名 `root` 和密码 `cisco` 登录虚拟机。然后输入 `ifconfig eth0` 来显示虚拟机以太网接口的 IP 地址。

要上传 IOU 镜像文件，打开你的网络浏览器并按照指示使用端口 `8000` 访问 IP 地址。输入 URL（此示例中为 `http://172.16.231.204:8000/upload`）后，你应该会看到一个类似于图 9-11 所示的网页。

![Select and upload your IOU image files.](img/httpatomoreillycomsourcenostarchimages2209131.png.jpg)

图 9-11. 选择并上传你的 IOU 镜像文件。



使用`Browse...`（浏览...）按钮从 PC 选择 IOU 镜像文件。一旦选中，点击`upload`（上传）完成过程。对于你想在 GNS3 中使用的每个镜像和 IOU 许可证文件重复此步骤。镜像存储在 IOU 虚拟机的`/home/gns3/GNS3/images`下，路径显示在网页上以供稍后参考。在 GNS3 中配置 IOU 镜像时将需要这些信息。

## 为 IOU 配置 GNS3

现在 IOU 已经准备就绪，告诉 GNS3 在哪里寻找许可证。选择`IOS devices`并点击`New`（新建）启动向导。在 Server type 类型下，确保`Remote`（远程）旁边有勾选，并点击`Next`（下一步）。会出现一条关于选择镜像路径的消息；点击`OK`，你将看到新的 IOU 设备窗口，如图 9-15 所示。

为你的 IOU 设备输入名称（例如`IOU_L2`），然后输入 IOU 镜像路径。由于 IOU 镜像安装在 Linux 虚拟机上，你必须输入镜像文件的“Linux 路径”。该路径为`/home/gns3/GNS3/images/<image_name>`。在示例中，我输入了`/home/gns3/GNS3/images/i86bi-linux-l2-adventprisek9-15.1a.bin`。你可以在用于上传镜像的网页上找到这些信息（参考图 9-11）。注意正确输入路径和文件名；否则 IOU 将无法工作。我建议直接从 IOU 虚拟机网页复制并粘贴信息，以避免任何混淆。

![IOU devices preferences](img/httpatomoreillycomsourcenostarchimages2209137.png.jpg)

图 9-14. IOU 设备偏好设置

![New IOU device window](img/httpatomoreillycomsourcenostarchimages2209139.png.jpg)

图 9-15. 新的 IOU 设备窗口

完成后，点击`Finish`关闭向导，然后点击`Apply`和`OK`完成配置。一旦你添加了 IOU 镜像，就可以在你的项目中使用开始使用 IOU 设备了。

如果你将 GNS3 升级到新版本，还必须将 GNS3 IOU 虚拟机上的服务器升级到相同版本，否则它将无法工作。要升级服务器，请登录到 GNS3 IOU 虚拟机并输入以下命令，将`version`替换为你的 GNS3 版本：

```
Login: root
Password: cisco
# pip3 install gns3-server==version
```

## IOU 的实战

现在，让我们创建一个简单的项目，允许 IOU 交换机在两个 VLAN 之间路由 TCP/IP 流量。首先，按照[图 9-16]所示所示创建项目](#ch09.html_vlan_routing_using_an_iou_switch "Figure 9-16. VLAN routing using an IOU switch")

![VLAN routing using an IOU switch](img/httpatomoreillycomsourcenostarchimages2209141.png.jpg)

图 9-16. 使用 IOU 交换机进行 VLAN 路由

在这个项目中，你将配置一个具有两个 VLAN（VLAN 10 和 VLAN 20）的 IOU L2 交换机。然后你将路由器 R1 分配到 VLAN 10，将路由器 R2 分配到 VLAN 20。在此实验中，IOU 交换将在两个 VLAN 之间路由数据包，以便 R1 和 R2 能够相互 ping。首先如下配置 IOU1 交换机：

```
 IOU1# configure terminal
➊ IOU1(config)# ip routing
➋ IOU1(config)# vlan 10
  IOU1(config-vlan)# vlan 20
➌ IOU1(config-vlan)# interface vlan 10
➍ IOU1(config-if)# ip address 192.168.1.1 255.255.255.0
➎ IOU1(config-if)# no shutdown
  IOU1(config-if)# interface vlan 20
  IOU1(config-if)# ip address 192.168.2.1 255.255.255.0
  IOU1(config-if)# no shutdown
➏ IOU1(config)# interface Ethernet 0/0
➐ IOU1(config-if)# switchport mode access
➑ IOU1(config-if)# switchport access vlan 10
  IOU1(config-if)# no shutdown
  IOU1(config-if)# interface Ethernet 0/1
  IOU1(config-if)# switchport mode access
  IOU1(config-if)# switchport access vlan 20
  IOU1(config-if)# no shutdown
```

启用 IP 路由 ➊，然后使用`vlan`命令 ➋ 创建两个 VLAN（10 和 20）。接下来，为每个 VLAN 创建一个交换虚拟接口 (SVI) ➌ 并为每个 SVI 分配 IP 地址 ➍。使用`no shutdown`命令 ➎ 启用接口。现在进入连接到 R1 和 R2 的物理接口 ➏，将它们设置为接入端口 ➐，并分配到相应的 VLAN ➑。

接下来，在路由器 R1 上配置 IP 地址。

```
R1(config)# interface f0/0
R1(config-if)# ip address 192.168.1.100 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# ip route 0.0.0.0 0.0.0.0 192.168.1.1
```

为 R1 的 F0/0 分配 IP 地址后，将默认网关设置为 192.168.1.1，以便路由器使用 IOU1 作为网关。最后，以类似的方式配置 R2。

```
R2(config)# interface f0/0
R2(config-if)# ip address 192.168.2.100 255.255.255.0
R2(config-if)# no shutdown
R2(config-if)# ip route 0.0.0.0 0.0.0.0 192.168.2.1
```

配置项目后，你可以使用`ping`命令测试 VLAN 路由。路由器 1 应该通过 IOU1 交换机 ping 通路由器 2，如下：

```
R1# ping 192.168.2.100

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.2.100, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 16/24/32 ms
```

这就是使用 GNS3 运行 IOU 设备的所有操作。现在让我们来看看思科最新的操作系统 NX-OS。

# 思科 NX-OS 运行在名为 Nexus 的数据中心级交换机上。虽然与 IOS 相似，但 NX-OS 不是 IOS，它使用不同的配置命令。NX-OSv（有时被称为 Titanium）是一个使用 VirtualBox 等虚拟化软件运行 NX-OS 的 Linux 虚拟机。NX-OSv 不是一个完整的操作系统，缺少很多功能。它提供了足够的功能和命令让你熟悉 NX-OS 的工作原理，并可以连接到 GNS3 设备。获取 NX-OSv 镜像后，将其放在安全的地方，以防工作副本损坏。

在 GNS3 目录下为 NX-OSv 创建一个目录并将 NX-OSv 镜像文件复制那里。你应该有一个名为`N7K.vmdk`的文件。你的文件名可能会根据 NX-OSv 版本而不同。镜像文件到位后，是时候在 VirtualBox 中连接 NX-OSv 了。

## 将 NX-OSv 导入 VirtualBox

NX-OSv 通常以单个虚拟机磁盘文件（`.*vmdk`）的形式提供，你可以使用 VMware、VirtualBox 或 QEMU 运行它。VirtualBox 是免费的，即使在 Core 2 Duo 等旧款电脑上也能可靠地运行 NX-OSv，因此我在这里介绍 VirtualBox。配置包括将磁盘镜像文件导入自定义 Linux 虚拟机并调整一些设置。如果你的电脑上没有安装 VirtualBox，请现在下载并安装。

启动 VirtualBox 并点击`New`创建新虚拟机。你应该会看到如[图 9-17]所示的创建虚拟机向导](#ch09.html_create_virtual_machine_wizard_comma_name "Figure 9-17. Create Virtual Machine wizard, Name and operating system window")

![Create Virtual Machine wizard, Name and operating system window](img/httpatomoreillycomsourcenostarchimages2209143.png.jpg)

图 9-17. 创建虚拟机向导，名称和操作系统窗口

为设备输入名称，将类型设置为`Linux`，版本设置为`Other Linux (64-bit)`，点击`Next`继续。你应该会看到如[图 9-18]所示的内存大小窗口](#ch09.html_create_virtual_machine_wizard_comma_memor "Figure 9-18. Create Virtual Machine wizard, Memory size")

要调整内存大小，请使用滑块或在提供的字段中输入数值。NX-OSv 在 2048MB 内存下运行效果最好。完成后，点击`Next`配置硬盘设置，如[图 9-19]所示所示](#ch09.html_create_virtual_machine_wizard_comma_hard "Figure 9-19. Create Virtual Machine wizard, Hard drive window")

![Create Virtual Machine wizard, Memory size window](img/httpatomoreillycomsourcenostarchimages2209145.png.jpg)

图 9-18. 创建虚拟机向导，内存大小窗口

![Create Virtual Machine wizard, Hard drive window](img/httpatomoreillycomsourcenostarchimages2209147.png.jpg)

图 9-19. 创建虚拟机向导，硬盘窗口

要将 NX-OS 虚拟硬盘挂载到你的虚拟机，选择`Use an existing virtual hard drive file`并点击浏览图标定位你的 NX-OSv .*vmdk 文件。选择该文件并点击`Create`完成虚拟机的创建。

## 为 NX-OSv 配置 GNS3

启动 GNS3 并 NX-OSv 虚拟机添加到你的虚拟机库。选择`Edit` ▸ `Preferences`并展开`VirtualBox`以显示 VirtualBox 虚拟机，如[图 9-20]所示所示](#ch09.html_adding_the_nx-osv_virtualbox_virtual_mac "Figure 9-20. Adding the NX-OSv VirtualBox virtual machine to GNS3")。在这里你可以将 VirtualBox 虚拟机添加到 GNS3，这是使用 NX-OSv 之前的最后一步。

![Adding the NX-OSv VirtualBox virtual machine to GNS3](img/httpatomoreillycomsourcenostarchimages2209149.png.jpg)

点击`New`启动 VirtualBox 向导，从虚拟机名称下拉菜单中选择你的 NX-OSv 虚拟机，然后点击`Finish`。现在点击`Edit`并导航到 General（常规）设置标签页。勾选`Enable remote console`（启用远程控制）和`Start VM in headless mode`（无模式启动虚拟机）并点击`Apply`。在 Network（网络）标签页下，将接口数量从`1`改为`6`，并点击`Apply`关闭窗口。然后点击`Apply`和`OK`完成安装。要在项目中使用 NX-OSv 虚拟机，请从 End devices（终端设备）工具栏将你的 NX-OSv 虚拟机拖入工作区。

## 在实战中的 NX-OSv

现在你已经将 NX-OSv 设备添加到 GNS3 中，让我们在项目中使用它吧。创建一个包含一个 NX-OSv 设备和一个 IOS 路由器的拓扑结构，如图图 9-21 所示。该项目将使用 Cisco EIGRP 协议从`R1`向`NX-OSv`广播所有的`172.16.0.0`网络。

![使用 NX-OSv 的简单拓扑](img/httpatomoreillycomsourcenostarchimages2209151.png.jpg)

图 9-21. 使用 NX-OSv 的简单拓扑

创建项目后，启动所有设备并打开到 NX-OSv 的控制连接。在 PC 上运行的 NX-OS 启动需要长时间，并且经常会在`SCSI disk detected`处挂起一分钟，如图图 9-22 所示。这是正常现象，在启动期间请耐心等待。

![启动 NX-OSv](img/httpatomoreillycomsourcenostarchimages2209153.png.jpg)

图 9-22. 启动 NX-OSv

如果你没有看到启动信息，可能是某些配置有误。回去检查 VirtualBox 和 GNS3 中的所有设置。如果问题持续存在，可能是你的`N7K.vmdk`镜像文件有问题。

系统启动后，你应该会看到登录提示，如下所示：

```
User Access verification
vNX-OS-01 login:
```

默认登录名和密码应该是`admin`和`admin`。使用这些凭据登录 NX-OSv。现在是输入几条命令的好时机。我会从`show run`、`show version`和`show interface brief`开始，但你可以尝试任何你熟悉的 IOS 命令。有些在 NX-OS 上是相同的，有些则不是。你可以使用问号（`?`）显示完整列表。

现在你已经预览了 NX-OSv，可以配置你的项目了。首先，你将配置路由器`R1`。在路由器`R1`上打开控制台并输入以下命令来配置项目中所有的 IP 地址：

```
R1# configure terminal
R1(config)# interface f0/0
R1(config-if)# no shutdown
R1(config-if)# ip address 10.1.1.1 255.255.255.0
R1(config-if)# interface loopback1
R1(config-if)# ip address 172.16.1.1 255.255.255.0
R1(config-if)# interface loopback2
R1(config-if)# ip address 172.16.2.1 255.255.255.0
R1(config-if)# interface loopback3
R1(config-if)# ip address 172.16.3.1 255.255.255.0
```

接下来，启用 EIGRP 并广播所有 IP 网络。

```
R1(config-if)# router eigrp 10
R1(config-router)# no auto-summary
R1(config-router)# network 10.0.0.0
R1(config-router)# network 172.16.0.0
```

现在登录 NX-OSv，并配置与`R1`接口`f0/0`同一子网的 IP 地址。

```
vNX-OS-01# configure terminal
vNX-OS-01(config)# interface ethernet 2/1
vNX-OS-01(config-if)# ip address 10.1.1.2/24
vNX-OS-01(config-if)# no shutdown
```

你应该首先注意到，NX-OS 仅接受使用 CIDR 表示法的 IP 地址，因此此处子网掩码输入为`/24`而不是 IOS 中常用的`255.255.255.0`。现在使用`ping`命令测试从 NX-OSv 到路由器`R1`的连通性并退出配置模式。



```
vNX-OS-01(config-if)# do ping 10.1.1.1
PING 192.168.1.1 (110.1.1.1): 56 data bytes
64 bytes from 110.1.1.1: icmp_seq=0 ttl=254 time=19.494 ms
64 bytes from 110.1.1.1: icmp_seq=1 ttl=254 time=7.849 ms
64 bytes from 110.1.1.1: icmp_seq=2 ttl=254 time=7.511 ms
64 bytes from 110.1.1.1: icmp_seq=3 ttl=254 time=20.637 ms
64 bytes from 110.1.1.1: icmp_seq=4 ttl=254 time=8.524 ms
--- 110.1.1.1 statistics ---
5 packets transmitted, 5 packets received, 0.0% packet loss
round-trip min/avg/max = 7.511/8.803/20.637 ms
vNX-OS-01(config-if)# exit
```

现在让我们配置 NX-OSv，使其能够与路由器交换 EIGRP 路由。现在你已经预览了 NX-OSv，可以配置你的项目了。首先，你将配置路由器 `R1`。在路由器 `R1` 上打开控制台并输入以下命令来配置项目中所有的 IP 地址：

```
R1# configure terminal
R1(config)# interface f0/0
R1(config-if)# no shutdown
R1(config-if)# ip address 10.1.1.1 255.255.255.0
R1(config-if)# interface loopback1
R1(config-if)# ip address 172.16.1.1 255.255.255.0
R1(config-if)# interface loopback2
R1(config-if)# ip address 172.16.2.1 255.255.255.0
R1(config-if)# interface loopback3
R1(config-if)# ip address 172.16.3.1 255.255.255.0
```

接下来，启用 EIGRP 并广播所有 IP 网络。

```
R1(config-if)# router eigrp 10
R1(config-router)# no auto-summary
R1(config-router)# network 10.0.0.0
R1(config-router)# network 172.16.0.0
```

现在登录 NX-OSv，并配置与 `R1` 接口 `f0/0` 同一子网的 IP 地址。

```
vNX-OS-01# configure terminal
vNX-OS-01(config)# interface ethernet 2/1
vNX-OS-01(config-if)# ip address 10.1.1.2/24
vNX-OS-01(config-if)# no shutdown
```

你应该首先注意到，NX-OS 仅接受使用 CIDR 表示法的 IP 地址，因此此处子网掩码输入为 `/24` 而不是 IOS 中常用的 `255.255.255.0`。现在使用 `ping` 命令测试从 NX-OSv 到路由器 `R1` 的连通性并退出配置模式。

```
vNX-OS-01(config-if)# do ping 10.1.1.1
PING 192.168.1.1 (110.1.1.1): 56 data bytes
64 bytes from 110.1.1.1: icmp_seq=0 ttl=254 time=19.494 ms
64 bytes from 110.1.1.1: icmp_seq=1 ttl=254 time=7.849 ms
64 bytes from 110.1.1.1: icmp_seq=2 ttl=254 time=7.511 ms
64 bytes from 110.1.1.1: icmp_seq=3 ttl=254 time=20.637 ms
64 bytes from 110.1.1.1: icmp_seq=4 ttl=254 time=8.524 ms
--- 110.1.1.1 statistics ---
5 packets transmitted, 5 packets received, 0.0% packet loss
round-trip min/avg/max = 7.511/8.803/20.637 ms
vNX-OS-01(config-if)# exit
```

现在让我们配置 NX-OSv，使其能够与路由器交换 EIGRP 路由。现在你已经预览了 NX-OSv，可以配置你的项目了。首先，你将配置路由器 `R1`。在路由器 `R1` 上打开控制台并输入以下命令来配置项目中所有的 IP 地址：

```
R1# configure terminal
R1(config)# interface f0/0
R1(config-if)# no shutdown
R1(config-if)# ip address 10.1.1.1 255.255.255.0
R1(config-if)# interface loopback1
R1(config-if)# ip address 172.16.1.1 255.255.255.0
R1(config-if)# interface loopback2
R1(config-if)# ip address 172.16.2.1 255.255.255.0
R1(config-if)# interface loopback3
R1(config-if)# ip address 172.16.3.1 255.255.255.0
```

接下来，启用 EIGRP 并广播所有 IP 网络。

```
R1(config-if)# router eigrp 10
R1(config-router)# no auto-summary
R1(config-router)# network 10.0.0.0
R1(config-router)# network 172.16.0.0
```

现在登录 NX-OSv，并配置与 `R1` 接口 `f0/0` 同一子网的 IP 地址。

```
vNX-OS-01# configure terminal
vNX-OS-01(config)# interface ethernet 2/1
vNX-OS-01(config-if)# ip address 10.1.1.2/24
vNX-OS-01(config-if)# no shutdown
```

你应该首先注意到，NX-OS 仅接受使用 CIDR 表示法的 IP 地址，因此此处子网掩码输入为 `/24` 而不是 IOS 中常用的 `255.255.255.0`。现在使用 `ping` 命令测试从 NX-OSv 到路由器 `R1` 的连通性并退出配置模式。

```
vNX-OS-01(config-if)# do ping 10.1.1.1
PING 192.168.1.1 (110.1.1.1): 56 data bytes
64 bytes from 110.1.1.1: icmp_seq=0 ttl=254 time=19.494 ms
64 bytes from 110.1.1.1: icmp_seq=1 ttl=254 time=7.849 ms
64 bytes from 110.1.1.1: icmp_seq=2 ttl=254 time=7.511 ms
64 bytes from 110.1.1.1: icmp_seq=3 ttl=254 time=20.637 ms
64 bytes from 110.1.1.1: icmp_seq=4 ttl=254 time=8.524 ms
--- 110.1.1.1 statistics ---
5 packets transmitted, 5 packets received, 0.0% packet loss
round-trip min/avg/max = 7.511/8.803/20.637 ms
vNX-OS-01(config-if)# exit
```

现在让我们配置 NX-OSv，使其能够与路由器交换 EIGRP 路由。现在你已经预览了 NX-OSv，可以配置你的项目了。首先，你将配置路由器 `R1`。在路由器 `R1` 上打开控制台并输入以下命令来配置项目中所有的 IP 地址：

```
R1# configure terminal
R1(config)# interface f0/0
R1(config-if)# no shutdown
R1(config-if)# ip address 10.1.1.1 255.255.255.0
R1(config-if)# interface loopback1
R1(config-if)# ip address 172.16.1.1 255.255.255.0
R1(config-if)# interface loopback2
R1(config-if)# ip address 172.16.2.1 255.255.255.0
R1(config-if)# interface loopback3
R1(config-if)# ip address 172.16.3.1 255.255.255.0
```

接下来，启用 EIGRP 并广播所有 IP 网络。

```
R1(config-if)# router eigrp 10
R1(config-router)# no auto-summary
R1(config-router)# network 10.0.0.0
R1(config-router)# network 172.16.0.0
```

现在登录 NX-OSv，并配置与 `R1` 接口 `f0/0` 同一子网的 IP 地址。

```
vNX-OS-01# configure terminal
vNX-OS-01(config)# interface ethernet 2/1
vNX-OS-01(config-if)# ip address 10.1.1.2/24
vNX-OS-01(config-if)# no shutdown
```

你应该首先注意到，NX-OS 仅接受使用 CIDR 表示法的 IP 地址，因此此处子网掩码输入为 `/24` 而不是 IOS 中常用的 `255.255.255.0`。现在使用 `ping` 命令测试从 NX-OSv 到路由器 `R1` 的连通性并退出配置模式。

```
vNX-OS-01(config-if)# do ping 10.1.1.1
PING 192.168.1.1 (110.1.1.1): 56 data bytes
64 bytes from 110.1.1.1: icmp_seq=0 ttl=254 time=19.494 ms
64 bytes from 110.1.1.1: icmp_seq=1 ttl=254 time=7.849 ms
64 bytes from 110.1.1.1: icmp_seq=2 ttl=254 time=7.511 ms
64 bytes from 110.1.1.1: icmp_seq=3 ttl=254 time=20.637 ms
64 bytes from 110.1.1.1: icmp_seq=4 ttl=254 time=8.524 ms
--- 110.1.1.1 statistics ---
5 packets transmitted, 5 packets received, 0.0% packet loss
round-trip min/avg/max = 7.511/8.803/20.637 ms
vNX-OS-01(config-if)# exit
```

（注：此处为翻译正文内容）

现在你已经将 NX-OSv 设备添加到 GNS3 中，让我们在项目中使用它吧。创建一个包含一个 NX-OSv 设备和一个 IOS 路由器的拓扑结构，如图图 9-21 所示。该项目将使用 Cisco EIGRP 协议从 `R1` 向 `NX-OSv` 广播所有的 `172.16.0.0` 网络。

![使用 NX-OSv 的简单拓扑](img/httpatomoreillycomsourcenostarchimages2209151.png.jpg)

图 9-21. 使用 NX-OSv 的简单拓扑

创建项目后，启动所有设备并打开到 NX-OSv 的控制连接。在 PC 上运行的 NX-OS 启动需要长时间，并且经常会在 `SCSI disk detected` 处挂起一分钟，如图图 9-22 所示。这是正常现象，在启动期间请耐心等待。

![启动 NX-OSv](img/httpatomoreillycomsourcenostarchimages2209153.png.jpg)

图 9-22. 启动 NX-OSv

如果你没有看到启动信息，可能是某些配置有误。回去检查 VirtualBox 和 GNS3 中的所有设置。如果问题持续存在，可能是你的 `N7K.vmdk` 镜像文件有问题。

系统启动后，你应该会看到登录提示，如下所示：

```
User Access verification
vNX-OS-01 login:
```

默认登录名和密码应该是 `admin` 和 `admin`。使用这些凭据登录 NX-OSv。现在是输入几条命令的好时机。我会从 `show run`、`show version` 和 `show interface brief` 开始，但你可以尝试任何你熟悉的 IOS 命令。有些在 NX-OS 上是相同的，有些则不是。你可以使用问号（`?`）显示完整列表。

现在你已经预览了 NX-OSv，可以配置你的项目了。首先，你将配置路由器 `R1`。在路由器 `R1` 上打开控制台并输入以下命令来配置项目中所有的 IP 地址：

```
R1# configure terminal
R1(config)# interface f0/0
R1(config-if)# no shutdown
R1(config-if)# ip address 10.1.1.1 255.255.255.0
R1(config-if)# interface loopback1
R1(config-if)# ip address 172.16.1.1 255.255.255.0
R1(config-if)# interface loopback2
R1(config-if)# ip address 172.16.2.1 255.255.255.0
R1(config-if)# interface loopback3
R1(config-if)# ip address 172.16.3.1 255.255.255.0
```

接下来，启用 EIGRP 并广播所有 IP 网络。

```
R1(config-if)# router eigrp 10
R1(config-router)# no auto-summary
R1(config-router)# network 10.0.0.0
R1(config-router)# network 172.16.0.0
```

现在登录 NX-OSv，并配置与 `R1` 接口 `f0/0` 同一子网的 IP 地址。

```
vNX-OS-01# configure terminal
vNX-OS-01(config)# interface ethernet 2/1
vNX-OS-01(config-if)# ip address 10.1.1.2/24
vNX-OS-01(config-if)# no shutdown
```

你应该首先注意到，NX-OS 仅接受使用 CIDR 表示法的 IP 地址，因此此处子网掩码输入为 `/24` 而不是 IOS 中常用的 `255.255.255.0`。现在使用 `ping` 命令测试从 NX-OSv 到路由器 `R1` 的连通性并退出配置模式。

```
vNX-OS-01(config-if)# do ping 10.1.1.1
PING 192.168.1.1 (110.1.1.1): 56 data bytes
64 bytes from 110.1.1.1: icmp_seq=0 ttl=254 time=19.494 ms
64 bytes from 110.1.1.1: icmp_seq=1 ttl=254 time=7.849 ms
64 bytes from 110.1.1.1: icmp_seq=2 ttl=254 time=7.511 ms
64 bytes from 110.1.1.1: icmp_seq=3 ttl=254 time=20.637 ms
64 bytes from 110.1.1.1: icmp_seq=4 ttl=254 time=8.524 ms
--- 110.1.1.1 statistics ---
5 packets transmitted, 5 packets received, 0.0% packet loss
round-trip min/avg/max = 7.511/8.803/20.637 ms
vNX-OS-01(config-if)# exit
```

现在让我们配置 NX-OSv，使其能够与路由器交换 EIGRP 路由。现在你已经预览了 NX-OSv，可以配置你的项目了。首先，你将配置路由器 `R1`。在路由器 `R1` 上打开控制台并输入以下命令来配置项目中所有的 IP 地址：

（注：此处为翻译正文内容）

# 第 10 章：雨天可以做的酷玩事物

既然你已经了解了 GNS3 最常用的功能，让我们来探索一些可以在 GNS3 项目中完成的有趣技巧。首先，你将创建一个模拟的 Cisco 接入服务器，它的功能与真实的 Cisco 设备相当。



接下来，我将向你展示如何将 GNS3 项目从一个操作系统移动到另一个操作系统，以及如何将 GNS3 虚拟路由配置复制到真实的 Cisco 路由器上。最后，你将查看如何使用多台 PC 共享项目的资源负载、创建一些极客实验室并模拟一些真实的网络场景。

## 从接入服务器管理设备

`access server`（接入服务器）允许你从中央控制台管理所有网络设备，这样你可以同时登录到多个设备控制台并在它们之间轻松切换。这是管理大型 Cisco 网络设备的一种高效方法，只需花一点精力，你就可以创建一个功能完整的虚拟 Cisco 接入服务器（有时也称为 `terminal` 或 `comm server`）来管理你的 GNS3 设备。我发现使用虚拟接入服务器是管理和配置 GNS3 的快速方法，你也可以通过它来学习真实接入服务器的命令和按键操作。

一个 GNS3 虚拟接入服务器包含两个组件。第一个是配置了虚拟接口的 `Cloud` 节点；你在 Windows 中使用 `Loopback Adapter` 驱动，在 Linux 中使用 `TAP` 适配器。第二个是作为管理控制台的 `Cisco Dynamips` 路由器。虚拟接入服务器本身的配置根据你的操作系统略有不同。我将涵盖 Windows 和 Ubuntu Linux，但这些概念适用于其他 Linux 操作系统。遗憾的是，在本书期间不支持 OS X。

### 安装虚拟接口

无论你使用 Windows 还是 Linux，都需要安装一个虚拟网络适配器并为其分配 IP 地址。在 Windows 上，你将安装 `Loopback Adapter` 驱动，在 Linux 等 Unix 系统上，你将安装 `TAP` 驱动。如果你是 Linux 用户，可以跳到在 Linux 中配置 TAP 适配器。

### 在 Windows 中配置 Loopback 适配器

如果你还没有安装，请安装 `Microsoft Loopback Adapter` 驱动。（参考在 Windows 上使用 Loopback 适配器所示。

![配置 Microsoft Loopback 适配器驱动的属性](img/httpatomoreillycomsourcenostarchimages2209155.png.jpg)

图 10-1. 配置 Microsoft Loopback 适配器驱动的属性

右键点击 `Microsoft Loopback Adapter` 驱动并选择 `Properties`（属性）。在 `Properties` 窗口中，选择 `Internet Protocol Version 4 (IPv4)`，然后点击 `Properties` 按钮显示 IP 地址，如图 10-2 所示。

![使用 IP 地址配置你的 Loopback 适配器](img/httpatomoreillycomsourcenostarchimages2209157.jpg)

图 10-2. 使用 IP 地址配置你的 Loopback 适配器

选择 `Use following IP address`（使用下面的地址）并输入唯一的 IP 地址和子网掩码。我选择了 `9.9.9.9` `255.255.255.0`，但任何地址和掩码都可以，只要它们与分配给 PC 上任何以太网适配器的地址以及你计划在 GNS3 网络拓扑中使用的任何地址唯一即可。不需要包含默认网关地址或提供任何 DNS 服务器，因为接入服务器不会使用它们。完成后，点击 `OK` 完成配置。现在关闭所有打开的窗口并启动 GNS3。如果你是 Linux 用户，请继续阅读准备 GNS3 服务器。

### 在 Linux 中配置 TAP 适配器

在 Ubuntu Linux 上，你将使用虚拟 `TAP` 适配器作为接入服务器。打开终端并输入以下命令安装驱动：

```bash
sudo apt-get install uml-utilities
```

要启用 `tap0`，输入以下命令并将 `jneumann` 替换为你的 Linux 用户：

```bash
sudo tunctl -u jneumann -t tap0
```

接下来，为 `tap0` 分配唯一的 IP 地址。你选择的 IP 地址和子网掩码必须与 PC 上配置的网络适配器以及你计划在 GNS3 拓扑中使用的任何地址唯一。

```bash
sudo ifconfig tap0 9.9.9.9 netmask 255.255.255.0 up
```

为了确保 `tap0` 在重启后保持 IP 地址并可用，你需要修改 Linux 设置。

使用文本编辑器打开 `/etc/networks` 下的 `interfaces` 文件。你需要管理员权限才能修改该文件，因此使用 `sudo` 运行编辑器（如 `nano` 或 `vi`）。然后在文件末尾添加以下内容：

```
auto tap0
iface tap0 inet static
    pre-up tunctl -t tap0
    up ifconfig tap0 up
    down ifconfig tap0 down
    address 9.9.9.9
    netmask 255.255.255.0
```

有了这些命令，保存 `interfaces` 文件，关闭并重启。当 Ubuntu 重启时，`TAP` 驱动会自动加载，接口 `tap0` 将可以使用。

## 警告

编辑 `/etc/interfaces` 文件要小心。这里的错误会导致 Ubuntu 无法正常启动。

输入 `ifconfig` 命令验证 `tap0` 设置：

```bash
$ ifconfig
--snip--
  tap0    Link encap:Ethernet HWaddr 16:81:25:c1:cc:8c
         inet addr:9.9.9.9 Bcast:9.9.9.255 Mask:255.255.255.0
           UP BROADCAST MULTICAST MTU:1500 Metric:1
           RX packets:0 errors:0 dropped:0 overruns:0 frame:0
           TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
           collisions:0 txqueuelen:500
           RX bytes:0 (0.0 B) TX bytes:0 (0.0 B)
```

`ifconfig` 的输出显示 `tap0` 适配器已启用并配置了 IP 地址。安装并配置虚拟适配器后，你需要设置 GNS3 服务器。

## 准备 GNS3 服务器

在 Windows 上，以管理员身份运行 GNS3。首先将 GNS3 服务器绑定到虚拟接口的 IP 地址；否则你的接入服务器将无法工作。点击 `Edit ▸ Preferences` 从左列选择 `GNS3 server`。选择 `Host binding` 下拉菜单，然后选择分配给虚拟接口的 IP 地址，如图 10-3 所示。

在[图 10-3]中，IP 地址为 `9.9.9.9`。点击 `Apply` 和 `OK`，GNS3 服务器将使用新的主机绑定重启。

将您的 GNS3 服务器绑定到虚拟适配器的 IP 地址，您就可以创建虚拟接入服务器。该接入服务器由两个设备创建组成：一个 `Cloud` 节点和一个 `Dynamips IOS` 路由器。

### 配置 Cloud 节点

通过向您的工作区添加 `Cloud` 节点来开始项目。右键点击 `Cloud` 节点并选择 `Configure`。如果您正在运行 Windows，请选择 `NIO Ethernet` 选项卡（见图 10-4）。

点击 `Generic Ethernet NIO` 下方的下拉菜单，选择您的 Microsoft Loopback Adapter 驱动（在本例中为 `Loopback1`）；然后点击 `Add, Apply` 和 `OK` 完成配置。

如果您在 Ubuntu Linux 上运行 GNS3，请使用 `tap0` 配置 `Cloud` 节点。不要选择 `NIO Ethernet`，而是选择 `NIO TAP` 选项卡并在 TAP 接口字段中输入 `tap0`，如图 10-5 所示。

![在 Windows 中使用环回适配器驱动配置 Cloud 节点](img/httpatomoreillycomsourcenostarchimages2209161.png.jpg)

图 10-4. 在 Windows 中使用环回适配器驱动配置 Cloud 节点

![在 Ubuntu Linux 上使用 tap0 配置 NIO TAP](img/httpatomoreillycomsourcenostarchimages2209163.png.jpg)

图 10-5. 在 Ubuntu Linux 上使用 tap0 配置 NIO TAP

完成后，点击 `Add, Apply` 和 `OK` 完成 `Cloud` 节点的配置。

### 配置接入服务器路由器

配置好 `Cloud` 节点后，向您的工作区添加 `Dynamips` 路由器，并创建从路由器到 `Cloud` 节点的链接。这两个设备共同组成了虚拟接入服务器，如图 10-6 所示。它们不会连接到您的 GNS3 项目中的任何其他设备。

![虚拟接入服务器](img/httpatomoreillycomsourcenostarchimages2209165.png.jpg)

图 10-6. 虚拟接入服务器

将虚拟接入服务器组件连接后，向您的工作区添加更多路由器以创建一个简单的三路由器网络，如图 10-7 所示。这是将使用虚拟接入服务器管理的网络拓扑。

![使用虚拟 Cisco 接入服务器配置的网络](img/httpatomoreillycomsourcenostarchimages2209167.png.jpg)

图 10-7. 使用虚拟 Cisco 接入服务器配置的网络

图 10-7 显示您已使用路由器 `R1` 和 `Cloud` 节点（`Cloud 1`）创建了一个虚拟接入服务器，并创建了一个由名为 `R2`、`R3` 和 `R4` 的三个路由器组成的网络拓扑。

现在您已经创建了接入服务器和 GNS3 网络拓扑，可以配置接入服务器路由器。为路由器 `R1` 分配与您的 PC 虚拟适配器相同网络的 IP 地址，并测试从 `R1` 到虚拟适配器接口的连通性。例如，如果像我一样给虚拟适配器分配 IP 地址 `9.9.9.9 255.255.255.0`，您可以为接入服务器路由器 `R1` 分配该网络范围内的任何 IP 地址。我使用的是 IP 地址 `9.9.9.8` 和子网掩码 `255.255.255.0`。

要配置接口 `f0/0` 地址，打开到路由器 `R1` 的控制台连接并输入以下命令：

```
R1>enable
R1#configure terminal
R1(config)#interface f0/0
R1(config-if)#ip address 9.9.9.8 255.255.255.0
R1(config-if)#no shutdown
R1(config-if)#exit
R1(config)#exit
R1#ping 9.9.9.9
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 9.9.9.9, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/4 ms
```

在此配置中，路由器 `R1` 的接口 `f0/0` 连接到 `Cloud` 节点并配置了 IP 地址 `9.9.9.8 255.255.255.0`。使用 `ping` 命令测试 `R1` 与虚拟接口之间的连接。如果 ping 测试成功，您就可以继续下一步。如果 ping 测试失败，请验证您的所有接口是否已启用以及虚拟接口（loopback 或 back）是否正常。

虚拟访问服务器可以管理的设备存在局限性。由于 GNS3 服务器绑定到虚拟适配器并运行在你的 PC “本地”上，因此，虚拟访问服务器只能管理本地设备。

在 Windows PC 上，你无法管理 VirtualBox 虚拟机（包括 IOU），但你可以管理 QEMU 设备（如 Junos）。在 Ubuntu Linux 上，只要这些设备运行在你的 Linux PC 本，你就可以管理所有设备，包括 Dynamips、IOU、QEMU 和 VirtualBox。

要了解更多关于配置和使用真实 Cisco 访问服务器的信息，请访问 Cisco 网站（[`www.cisco.com/`](http://www.cisco.com/） ）并搜索 *configuring a comm server*。现在，你已经掌握了尝试虚拟访问服务器所需的所有信息。

#### 查看虚拟访问服务器的运行情况

在完全配置好访问服务器并启动项目路由器后，你应该能够使用该访问服务器管理这些路由器。你可以为几台路由器打开控制台连接，并在它们之间轻松切换。

### 打开控制台

首先为 `R1` 打开一个控制台连接。右键点击路由器 `R1` 并选择 `Console`。接下来，输入你想管理的主机名称并按回车

```
R1>R2
Translating "R2"
Trying R2 (9.9.9.9➊, 2002➋)... Open
Connected to Dynamips VM "R2" (ID 1, type c3600) - Console port
Press ENTER to get the prompt.

R2>➌
```

在此示例中，我通过在访问服务器命令行输入 `R2` 来与路由器 `R2` 会话。输出显示使用 IP 地址 `9.9.9.9` ➊ 和端口号 `2002` ➋ 建立了会话，且提示符 ➌ 已变为正在管理的路由器（在本示例中为 `R2`）。会话打开后，你可以像直接从 GNS3 打开控制台一样配置路由器。

当你完成路由器配置后，返回访问服务器控制台；只需按 `SHIFT-CTRL-6` 然后按 `X` 键。（Cisco 将这一组合动作称为 *escape sequence* 转义序列）。返回访问服务器控制台后，输入项目中的另一台路由器的名称以打开其控制台。现在尝试输入 `R3`，并按你意愿配置路由器。完成后，再次使用转义序列返回访问服务器。

尽管你当前登录在访问服务器控制台上，但另外两台路由器的会话仍然保持开启状态。要显示打开的会话列表及其对应的连接号，输入 `show sessions` 命令。

```
R1>show sessions
Conn Host                     Address          Byte  Idle  Conn Name
     1 R2                      9.9.9.9           0     0    R2
 ➊*  2 R3                     9.9.9.9           0     0    R3
```

你应该能看到两个活动连接（1 和 2）。`Conn 2` 旁的星号 ➊ 表示路由器 `R3` 是最后使用的会话。要返回上一个会话，请按 `ENTER`。要返回到不同的会话，输入连接号并按 `ENTER`；例如，输入 `1` 即可返回到路由器 `R2`。

### 关闭控制台

当你准备好断开打开的连接时，输入 `disconnect` 命令后跟连接号；然后按 `ENTER` 确认关闭会话。

```
R1>disconnect 2
Closing connection to R3 [confirm]
R1>
```

在此示例中，我已断开与路由器 `R3`（连接 2）。断开会话后，你必须重新输入主机名才能连接到设备。

### 设置连接超时

你可能希望调整路由器和访问服务器上的超时设置（通过控制台的 `exec-timeout` 参数），以确保在空闲期间（例如当你没有活动配置路由器时）不会自动注出。默认值为十分钟，但可以设置为更高、更低或更改为无限。

以下命令将控制台超时设置为 0 0 秒（无限）：

```
R1>enable
R1#configure terminal
R1(config)#line console 0
R1(config-line)#exec-timeout 0 0
```

GNS3 的默认 *startup-config* 应该已经为你完成了此操作，但要知道从安全角度来看，在生产环境中永远不允许路由器超时是一个坏主意。然而，在 GNS3 等实验环境中，这是非常方便的。

# 将配置部署到真实硬件

GNS3 的优点之一是它允许你创建并测试网络配置，这些配置稍后可以用于真实设备。你只需要在 GNS3 中导出路由器配置并将其加载到真实的 Cisco IOS 路由器上。

## 将 GNS3 配置导出到 Cisco 路由器

在 GNS3 内部彻底测试路由器配置后，你就可以准备将其导出并加载到真实的 Cisco 路由器上了。你可以导出项目中的所有路由器，也可以导出单个设备的配置。在导出 GNS3 IOS 路由器配置之前，登录该路由器并将其 *running-config* 文件保存到 *startup-config* 文件中。保存的 *startup-config* 即为 GNS3 导出的配置。

```
R1#copy running-config startup-config
```

如果你的项目中有任何 IOU 设备，你需要复制它们的配置。你还需要复制它们的 *running-config* 文件。

某一天，你可能希望将项目运行在与现有 PC 使用不同操作系统的 PC 上。如果你的 GNS3 项目仅包含 Dynamips IOS 路由器和交换机，你可以轻毫不费力地在 Windows 和 Linux 等不同平台之间复制它们。但如果你的项目由 IOU、QEMU 或 VirtualBox 等其他设备类型组成，该过程可能会变得复杂。无论如何，在平台之间移动项目大多只是将一个或多个项目从你旧的 GNS3 项目文件夹复制到新 PC 的项目文件夹中。



## 仅限 IOS 项目

如果你的项目仅由 Dynamips 路由器组成，只要目标计算机具有兼容的镜像文件，几乎不需要任何额外配置。如果目标 PC 配置了不同的 IOS 镜像文件，或者镜像存储在不同的目录中，GNS3 将提示你将原始镜像文件替换为目标计算机上已配置的镜像，如图 10-10（替换 IOS 镜像文件）所示。

![替换 IOS 镜像文件](img/httpatomoreillycomsourcenostarchimages2209173.png.jpg)

图 10-10 替换 IOS 镜像文件

在此示例中，你正在将项目从 Windows PC 移动到 Linux 主机。尽管`c3725-adventerprisek9-mz-124-15.T14.image`文件已在图 10-10（替换 IOS 镜像文件）中的 Linux 主机上配置，但 GNS3 无法找到它，因为 Windows 存储 IOS 镜像文件的路径与 Linux 不同。

在这种情况下，GNS3 应该显示已配置的 IOS 镜像列表并允许你选择其中一个。使用下拉菜单选择镜像并点击`OK`。选择镜像后，GNS3 应该更新目标 PC 项目文件中的路径信息。要使更改永久生效，你必须保存项目。所有的原始 IOS 配置都应保持完好，你的项目应该能按预期运行。如果没有运行，请重新开始并尝试使用不同的镜像文件。

## 带有 IOU 设备的项目

复制包含 IOU 设备的项目可能会复杂一些。简单的方法是在目标 PC 的项目上重新创建 IOU 设备，然后上传原始的 IOU 配置。在将项目复制到新平台之前，请遵循以下步骤：

1. 登录项目中的每个 IOU 设备，并将运行配置复制到`unix:initial-config.cfg`文件中。右键点击 IOU 设备并选择`Export config`以保存配置。在复制项目时，务必将导出的配置文件复制到新系统。

2. 在目标 PC 上打开项目并解决任何 IOS 镜像文件替换问题（参考图 10-10（替换 IOS 镜像文件））。

3. 在目标 PC 上，从项目中删除 IOU 设备，添加新设备，并使用与原始项目相同的接口将 IOU 设备链接到项目中的其他设备。

要导入配置，请遵循以下步骤：

1. 在目标 PC 上右键点击 IOU 设备并点击`Import config`。

2. 浏览到保存 IOU 配置的目录并选择文件。对项目中的每个 IOU 设备执行此操作。

3. 完成后，启动新项目中的所有设备并验证一切是否运行符合预期。登录每个 IOU 设备并检查其配置。如果一切正常，保存你更新后的项目。

最后，让我们来看传输使用 VirtualBox 的项目。

## 带有 VirtualBox 设备的项目

如果你在原始项目中使用 VirtualBox 设备，你将不得不导出为 OVA 文件。启动 VirtualBox 并选择`File` ▸ `Export Appliance`来保存设备文件。准备好 OVA 后，遵循以下步骤：

1. 将 OVA 文件复制到新 PC，启动 VirtualBox，并选择`File` ▸ `Import Appliance`来导入文件。

2. 启动 GNS3 并在`Preferences`（首选项）下添加 VirtualBox 虚拟机，如导入设备中讨论的那样。

3. 将设备添加到你的 GNS3 项目并将其链接到其他设备，选择与原始项目使用的相同的接口。

当你在新 PC 上启动项目时，你的 VirtualBox 设备应该具有与在旧 PC 上相同的配置。

# 探索 GNS3 控制台

GNS3 管理控制台提供命令行界面，你可以用它控制项目设备。基于为 Dynamips 编写的原始 Dynagen 控制台，管理控制台已针对 GNS3 进行了适配和更新。我在这里不会涵盖控制台的每一个方面，但我将向你展示一些可以使用它执行的更多有用操作。

默认情况下，启动 GNS3 时管理控制台应该是可见的。如果没有，请选择`View` ▸ `Docks` ▸ `Console`来显示控制台窗口。

在管理提示符（`=>`）下，输入`help`或问号（`?`）来查看命令列表。如如下列表所示，你可以在 CLI 执行熟悉的任务：

```
=> ?

已记录的命令（输入 help）：
========================================
console  debug  help  reload  show  start  stop  suspend  version
```

要显示命令的语法和用法，输入`help`后跟命令名称，如下所示：

```
=> help show
   Show detail information about device in current lab:
    show device

    Show detail information about a device:
    show device <device_name>

    Show whole topology:
    show run

    Show topology info of a device:
    show run <device_name>
```

`show`命令提供了许多不同的选项来显示有关你的虚拟机管理器、设备和配置的信息。例如，`show run`命令显示项目文件的全部内容。两个用于测试网络的有用命令是`suspend`和`start`。另一个有用的命令是`debug`。

# 使用多台 PC 创建项目

你可以使用多台 PC 运行设备，允许将资源负载分布到多台计算机上。共享资源允许你使用一台 PC 设计项目，而实际上在另一台 PC 上运行设备。这意味着你可以使用低端工作站（如旧笔记本电脑）创建和管理 GNS3 项目，而让高端服务器执行工作。

在本节中，我将向你如何在如何在客户端/服务器设置中共享资源，并涵盖创建超级实验室（uberlab）的策略。在配置客户端/服务器（多服务器）负载共享之前，禁用所有 PC 防火墙，让我们开始吧。

## Dynamips 客户端/服务器设置

在这种场景中，你在一个计算机上操作 GNS3，而另一台 GNS3 服务器运行在另一台 PC 上。如果你在 OS X 或 Windows 上运行 GNS3，这听起来很熟悉，因为这就是 IOU 虚拟机的工作方式。IOU 虚拟机运行在虚拟机上，而不是独立的 PC 上，但在其他方面概念是相同的。

### 准备你的工作站

在此示例中，我将使用 Windows 作为客户端 PC，Ubuntu Linux 作为服务器 PC。首先在两台工作站上安装 GNS3。一台作为客户端，用于配置和管理项目；另一台是服务器。服务器将仅运行 Dynamips 路由器，它应该具有更好的硬件，因为它将承担大部分工作。服务器的处理器性能和内存越大，你的设备性能就越好。

在每台计算机上启动 GNS3 并配置 IOS 镜像文件。这允许你同时运行本地和远程 Dynamips 路由器，并从客户端 PC 上通过 GNS3 将它们连接在一起。在服务器 PC 上配置 GNS3 时，请务必记录下你的 IOS 镜像文件的路径和文件名。在我的 Ubuntu 服务器上，我的镜像文件路径为`/home/jneumann/GNS3/images/IOS/c3725-adventerprisek9-mz.124-15.T14.image`。你需要这些信息来在客户端 PC 上配置远程 Dynamips 路由器。

接下来，找到你每台 GNS3 PC 的 IP 地址。在示例中，我的客户端 PC 配置的 IP 地址为`172.16.231.202`，服务器 PC 配置的 IP 地址为`172.16.231.205`。在配置好 GNS3 并记录 IP 和镜像路径信息后，你就可以开始了。

### 运行 gns3server

你必须从安装目录运行`gns3server`程序。登录到远程服务器 PC，在 Linux 或 OS X 上打开终端窗口，如果运行 Windows，则打开命令提示符。在 Windows 上，进入`C:\Program Files\GNS3`目录；在 OS X 上进入`/Applications/GNS3.app/Contents/Resources/Server/Contents/MacOS`目录。

启动服务器程序时，你必须指定服务器 PC 的 IP 地址以及服务器监听的端口号；输入命令`gns3server --host server-ip --port port-number`。如果你不知道服务器 PC 的 IP 地址，可以偷懒使用`0.0.0.0`，`gns3server`将监听所有配置的接口。在接下来的示例中，我在 Ubuntu Linux 上的`/usr/local/bin/`目录下启动了`gns3server`程序。

```
$ gns3server --host 172.16.231.205 --port 8000
2015-06-06 18:32:45 INFO main.py:145 GNS3 server version x.x
2015-06-06 18:32:45 INFO main.py:147 Copyright (c) 2007-2015 GNS3 Technologies Inc.
2015-06-06 18:32:45 INFO main.py:150 Config file /home/jneumann/.config/GNS3/gns3_server.conf loaded
2015-06-06 18:32:45 INFO main.py:163 Running with Python 3.4.2 and has PID 3436
2015-06-06 18:32:45 INFO main.py:72 Current locale is en_US.UTF-8
2015-06-06 18:32:45 WARNING project.py:397 Purge old temporary project f3b11fb8-82ed-42c1-b66a-226198ce6189
2015-06-06 18:32:45 INFO server.py:214 ➊ Starting server on 172.16.231.205:8000
```

启动服务器后，你应该能看到类似的输出，如果一切顺利，服务器将在`172.16.231.205:8000`➊启动，如输出的最后一行所示。这表示服务器程序正在 IP 地址`172.16.231.205`上的端口号`8000`处于监听状态。

### 注意事项

如果你想让 GNS3 服务器监听其他端口号（例如 8001），可以输入`gns3server --host 172.16.231.205 --port 8001`。要查看服务器选项的完整列表，请在命令行中输入`gns3server --help`。

### 配置客户端

服务器的配置就此完成，因此你可以将注意力转向 GNS3 客户端（在本示例中为了一台 Windows PC）。在 GNS3 中，选择`Edit`（编辑）▸ `Preferences`（首选项）并选择`GNS3 Server`，如图 10-11 所示。

![将主机绑定到以太网适配器的 IP 地址](img/httpatomoreillycomsourcenostarchimages2209175.png.jpg)

图 10-11. 将主机绑定到以太网适配器的 IP 地址

点击`Host binding`（主机绑定）下拉菜单并选择你的以太网接口的 IP 地址。在该 PC 上，地址为`172.16.231.202`。点击`Apply`（应用）完成配置。

接下来，将远程 GNS3 服务器的 IP 地址添加到客户端。点击`Remote Servers`（远程服务器）选项卡，如图 10-12 所示。

![配置 IP](img/httpatomoreillycomsourcenostarchimages2209175.png.jpg)

图 10-12. 配置 IP

在`Host`字段中输入远程服务器的 IP 地址。在本示例中，该 IP 为`172.16.231.205`。默认端口号应为`8000`，但如果你选择了其他端口也可以进行更改。点击`Apply`（应用）保存设置。接下来，在侧边菜单中选择`Dynamips`，如图 10-13 所示。

![Dynamips 设置](img/httpatomoreillycomsourcenostarchimages2209175.png.jpg)

图 10-13. Dynamips 设置

取消勾选`Use local server`（使用本地服务器）并点击`New`（新建）添加路由器，如图 10-14 所示。

![添加路由器](img/httpatomoreillycomsourcenostarchimages2209175.png.jpg)

图 10-14. 添加路由器

在`Name`字段中为你的路由器命名。我将其命名为`c3725_on_Ubuntu`，以便在工具栏中轻松识别，并且我知道它是配置为运行在远程服务器上的。点击`Next`（下一步）继续。在`IOS image`下，输入你从服务器记录的路径和文件名：`/home/jneumann/GNS3/images/IOS/c3725-adventerprisek9-mz.124-15.T14.image`。在`Server`下，选择服务器，如图 10-15 所示。

![选择服务器](img/httpatomoreillycomsourcenostarchimages2209175.png.jpg)

图 10-15. 选择服务器

点击`Next`（下一步）继续。像配置本地 Dynamips 路由器一样点击剩余选项。在要求时，务必输入一个 Idle-PC 值，如果你还没有计算过，请计算一个。完成添加路由器后，它应该显示在工具栏的 Routers 部分，如图 10-18 所示。

![工具栏中的 Routers 部分](img/httpatomoreillycomsourcenostarchimages2209175.png.jpg)

图 10-18. 工具栏中的 Routers 部分

此示例包含两台 c3725 路由器；一个是安装在 Windows PC 上的本地路由器，另一个安装在远程 Ubuntu 服务器上。当你创建一个项目时，你可以在同一个项目中使用这两个路由器，从而将客户端 PC 的 CPU 和内存消耗减少一半。

除了在远程服务器上运行`IOU`和`IOS`路由器外，你还可以在远程服务器上运行`QEMU`。只需在开始之前在服务器 PC 上安装`QEMU`即可。在客户端 PC 上设置远程`QEMU`设备的流程与任何其他远程设备几乎相同。然而，在新建 QEMU 虚拟机向导中，你需要为虚拟机选择`QEMU`二进制文件，如图 10-19 所示。

![配置 QEMU 二进制文件](img/httpatomoreillycomsourcenostarchimages2209191.png.jpg)

图 10-19. 配置 QEMU 二进制文件

GNS3 会查询远程服务器获取已安装的 QEMU 二进制文件列表，你创建的虚拟机将使用选择的二进制文件在远程服务器上运行。使用下拉菜单为你的虚拟机选择二进制文件，通常为`qemu-system-i386`或`qemu-system-x86_64`。调整 RAM 大小并点击`Next`。像虚拟机是本地设备一样配置其余选项。

# 创建 GNS3 Uberlab

GNS3 的核心在于扩展性，你可以用它创建包含几十个交换机和路由器的大型项目。创建 uberlab 的最佳方法之一是使用多个 GNS3 服务器。但如果你有一台非常快的电脑和另外几台性能没那么好的电脑怎么办？在这种情况下，你可能在一台机器上运行比另一台机器更多的设备。例如，你可以将大多数路由器运行在高端服务器上，而在性能较弱机器上运行较少设备。

uberlab 不需要局限于运行在局域网上的计算机。如果你在通过 VPN 连接的多个站点的企业网络上使用 GNS3，你可以使用客户端/服务器模型运行跨越城市甚至跨国家的各种虚拟化程序！你只需要在远程计算机（通过 VPN）上启动`gns3server`应用程序，并使用远程 PC 的 IP 地址配置你的本地客户端。这与普通客户端/服务器设置的唯一区别在于数据包将通过 VPN 发送到远程服务器。

# 用于乐趣和盈利的极客实验室

你已经探索了在 GNS3 中配置各种项目所需的工具，但获得这些新知识后你该做什么呢？你可以学习认证，或者只是玩玩！在这一节中，我将同时讨论这两者。这些项目中的许多是针对高级用户的，但请随时修改它们，以创建更适合你水平的项目和挑战。

## 准备 Cisco 考试

GNS3 是一个用于教育和认证的奇工具，它包含了获得 Juniper 或 Cisco 认证所需的所有内容，从入门级的`JNCIA`或`CCNA`直到 Cisco 认证的皇冠明珠——`CCIE`。

对于`CCNA`或`CCNP`等初级考试，可以从在线搜索寻找各种网络示例开始。你可能还想结合 GNS3 使用`CBT Nuggets`或`Bryant Advantage`的视频。他们的视频是很好的入门方式，而 GNS3 是实验他们所介绍的概念的绝佳工具。如果你正在学习`CCIE`，你可能想使用如`INE`练习册（[`www.ine.com/`](http://www.ine.com/)）。他们已经证明了自己是`CCIE`实验准备领域的领导者。

## 保护你的网络

如今，几乎每个人都在某种网络服务器上存储机密信息，因此拥有安全的网络基础设施不仅是一个好主意，它是防止重大财务损失、非预期诉讼以及与你公司的错误和遗漏（E&O）保险公司纠纷的方法。

在这一节中，我概述了一些与安全相关的挑战，这些挑战既有趣又有意义，并防止数据窃取或丢失。

### “破解我的机架”挑战



和朋友一起举办一场安全竞赛！每位挑战者在自己的 PC 上创建一个 GNS3 项目，并尽可能为他们的设备尽安全防护。挑战是让每个用户破解其他用户的安全防护。在每个用户在自己的 PC 上创建完网络后，他们被允许在朋友的 PC 上安装一个 `VirtualBox` 虚拟机，并带有任何他们想使用的系统破解工具。当挑战者完成网络创建后，他们交换电脑并计时。现在，大逃杀赛开始了！使用你的 `VirtualBox` 虚拟机破解另一位挑战者的 GNS3 网络。

## 创建 Cisco VPN

使用 Cisco 路由器和 `ASA` 设备创建 Cisco 站点到站点 VPN 或多站点 VPN。尝试配置一个具有 VPN 故障转移的多宿主 Cisco 路由器。在这种情况下，你的 WAN 边缘路由器可能配置了两个或多个带有 `BGP` 的接口以模拟到互联网提供商的 WAN 链路。某一天你可能需要一个，或者你的客户可能需要。在 GNS3 中学习如何这样做总比在客户的时间上摸索要好！

## 练习现实世界场景

以下项目想法旨在让你思考 GNS3 沙盒之外的生活。作为网络管理员或工程师，你需要理解多宿主网络、交换机块设计和多服务器集成的相互作用，这仅是其中之一。在 GNS3 中设计、运行和排错这些网络为现实世界做了良好的准备。

### 交换机块设计

理解交换是管理网络的重要部分。虽然 `EtherSwitch` 路由器 `IOU` 功能受限，但使用 `HSRP`、`VRRP` 和 `GLBP` 等协议配置冗余交换块是有用的。尝试创建一个具有互联网访问的全园区模型。

### 多宿主网络

许多小型企业使用单个 IP 连接互联网，但大型公司需要多个静态 IP 和 `BGP` 链路来维持其在互联网上的存在。通过使用几个 GNS3 路由器和 `BGP`，你可以模拟连接到多个互联网提供商的多宿主网络。添加额外的路由器以模拟如 [`www.google.com/`](http://www.google.com/) 或 [`www.gns3.com/`](http://www.gns3.com/) 的站点。然后从你的多宿主网络 ping 这些站点。

### 多厂商集成

使用 `Cisco`、`Juniper`、`Arista`、`Linux` 或任何你能想到的可路由设备创建一个项目。使用诸如 `RIP`、`OSPF`、`BGP` 或其他所有厂商支持的开放标准来配置设备，或使用路由重发布来翻译厂商设备之间的路由。目的是尽可能学习多厂商集成。

### 使用一切

这个项目涉及一切！方法很简单：构建一个你能想象的最大、最酷的项目。尽可能使用多个远程 PC 并运行 GNS3 提供的所有功能：`Cisco` 路由器、交换机、`ASA`、`IDS/IPS`、`Juniper`、`Firefly`、`Vyatta`、`Arista` 以及任何其他。应用所有的路由和交换协议，并使用 `ping` 或 `traceroute` 测试端到端连通性。确保设置至少一个 ATM 交换机、一个帧中云和两个 VPN。

### 多少个路由器会烧坏灯泡？

这是一个赢得自豪权的有趣方式。向朋友挑战，看谁的 PC 可以在 GNS3 中运行更多的路由器。通过正确的 `Idle-PC` 值，你可能会发现在 `Dynamips` 崩溃或 GNS3 开始变慢到无法使用之前，你可以运行超过 100 个。一个技巧是在 Linux 上运行 GNS3，因为 `Dynamips` 在 Linux 上的扩展性似乎比在 Windows 或 OS X 上更好。

### 失控的路由器

这种“画蛇添足”的挑战是与朋友一起玩游戏的另一种方式。每位挑战者都使用尽可能多的路由器来构建一个复杂的网络。越多越好！然后对这些网络进行配置和彻底测试。一旦两位挑战者都对自己的网络运行正常感到满意，他们就会交换电脑，通过更改几个配置设置来破坏对方的网络（即“画蛇添足”）。

破坏网络可能简单到只需关闭接口，也复杂到如过滤 BGP 路由。这完全取决于个人的技能和网络的复杂性。一旦网络被破坏，竞争者再次交换电脑，每个人都尝试成为第一个分析并修复自己的原始网络。

## 结语

设置虚拟 Cisco 接入服务器需要一些工作，但一旦配置完成，它就是管理设备的一种简便方法。如果你有一个只使用几个路由器的小型项目，那么可能没有必要。但如果你必须管理几十个设备，它会迅速成为一个无价之的工具。

GNS3 运行在多个 PC 操作系统上，但你并不局限于当前正在使用的系统。在系统之间迁移项目非常简单，因此不要害怕尝试新事物。GNS3 是使用 Linux 设计并移植到 Windows 和 OS X 的，因此它在 Linux 上运行良好，且通常比在 Windows 上运行时占用的资源更少。

如果你没有最新的 PC 硬件，可以在多个 PC 上对虚拟机进行负载均衡，并创建运行效果比单个 PC 更好的大型项目。这也是利用你家里或办公室闲置的旧 PC 的绝佳方法。

但关于 GNS3 最重要的一点是，它是有趣的，因为你可以创建其他可能无法实现的网络。所以，请发挥创意，享受其中！

# 附录 A. 命！我摔倒了起不起来

GNS3 是一个复杂的程序，和任何复杂程序一样，它偶尔会出现意料之外的行为。我已经在书中包含了故障排除技巧，因此在这个附录中我不会提供大量的修复信息。相反，我将为你提供解决问题的策略，并涵盖几个常见问题及其可能的解决方案。

# 识别问题

GNS3 问题大致分为两类。

* `突发问题`：发生在之前运行良好的项目中的问题。

* `功能问题`：在实现新功能时出现的问题。

突发问题凭空出现。你的项目可能已经运行良好了几周，然后突然就无法打开了，或者在打开时，设备拒绝启动。功能问题通常发生在创建新项目或在现有项目实现实现新功能时。这两类问题都可能令人沮丧，如果你使用 GNS3 足够长的时间，很可能会遇到其中一种。

# 突发问题

当一个项目运行良好并突然出现问题时，通常意味着发生了某些变化。变化可能发生在你的 PC 上、GNS3 内部或项目本身。对于 GNS3 来说，可能是你无意中更改了某个设置，或者对如 `Dynamips`、`QEMU` 或 `VirtualBox` 等辅助应用程序进行了更改。也可能意味着你升级到了有问题的 GNS3 版本。每当 GNS3 发布新版本时，在升级生产环境之前使用备用 PC 或虚拟机进行测试总是一个好主意。本节提供了帮助纠正一些突发问题的技巧。

## 停止 Dynamips 崩溃

不稳定的 Dynamips 程序可能导致与设备的连接丢失。在这种情况下，你可能会看到 GNS3 控制台错误消息，指示 `Dynamips` 已停止运行，如图 图 A-1 所示。

![Communication failure with Dynamips](img/httpatomoreillycomsourcenostarchimages2209193.png.jpg)

图 A-1. 与 Dynamips 通信失败

此消息可能表明你 PC 上运行的软件与 `Dynamips` 冲突，你拥有的是一个不稳定的 `Dynamips` 版本，或者你没有足够的 PC 资源（如内存或 CPU 周期）。尝试关闭任何非必要的应用程序、重启 PC、禁用所有防病毒/反垃圾邮件软件并禁用防火墙。如果 `Dynamips` 继续崩溃，你可能需要重新安装或从备份中恢复 `Dynamips` 或 `GNS3`。

## 当 IOS 镜像加载失败时

路由器内存是一个常见问题，会导致 `Dynamips` 路由器异常。当路由器拒绝启动时，检查你正在使用的 `IOS` 镜像精确版本的 Cisco RAM 要求——你可能分配的内存过多或不足。要验证这些要求，请访问 Cisco Feature Navigator 网站；浏览至 [`tools.cisco.com/ITDIT/CFN/jsp/index.jsp`](http://tools.cisco.com/ITDIT/CFN/jsp/index.jsp)。从这里，你可以使用 `Search by Software` 功能输入你的 `IOS` 详情，导航器将提供相应的要求。

如果 `IOS` 路由器的 RAM 设置得太低，路由器可能无法启动或在启动时崩溃，GNS3 Console 窗口可能会显示错误消息，如图 图 A-2 所示。

![Failed to load Cisco IOS error message](img/httpatomoreillycomsourcenostarchimages2209195.png.jpg)

图 A-2. 加载 Cisco IOS 镜像错误消息

此消息可能表明你 PC 上运行的软件与 `Dynamips` 冲突，你拥有的是一个不稳定的 `Dynamips` 版本，或者你没有足够的 PC 资源（如内存或 CPU 周期）。尝试关闭任何非必要的应用程序、重启 PC、禁用所有防病毒/反垃圾邮件软件并禁用防火墙。如果 `Dynamips` 继续崩溃，你可能需要重新安装或从备份中恢复 `Dynamips` 或 `GNS3`。

在这种情况下，停止设备并检查其配置。右键点击路由器并选择 `Configure` 以打开 GNS3 配置器。从左侧选择你的路由器并点击 `Memories and disks` 选项卡显示 RAM 设置。

如果你增加了内存但路由器仍然拒绝启动，你可能拥有一个损坏的 `IOS` 镜像文件，请尝试另一个。

当你拥有一个损坏的 `IOS` 镜像文件时，GNS3 窗口可能不会显示任何错误消息。相反，路由器控制台可能没有响应，或显示可能提供线索的信息，如图 图 A-3 所示。

![IOS image fails to load](img/httpatomoreillycomsourcenostarchimages2209197.png.jpg)

图 A-3. IOS 镜像加载失败

控制台输出显示 `IOS` 正以惊人的速度弹出异常错误。这可能表明镜像文件损坏或配置错误。使用 Cisco Feature Navigator 验证并并在必要更换镜像文件。

## 解决 IOS 内存错误

为 `Dynamips` 路由器添加过多的内存会导致路由器无法正常引导。例如，`c7200` 使用 `NPE-400` 处理的最大内存为 `512MB`。如果你添加更多，例如 `1024MB`，你可能会在 GNS3 Console 窗口中看到错误消息，或者在路由器控制台上显示以下消息：

```
Cisco IOS Software, 7200 Software (C7200-ADVENTPRISEK9-M), Version 15.2(4)
S2, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2012 by Cisco Systems, Inc.
Compiled Tue 11-Dec-12 13:32 by prod_rel_team

!!! WARNING - VM is not running, will be unresponsive (status=1) !!!
```

即使路由器看起来运行正常，你在配置 IOS 时也可能遇到错误。以下是一个有趣的情况：路由器虽然内存不足但成功启动了，但在配置时显示了错误信息：

```
R1(config-if)#ip nat inside
% NBAR ERROR: parsing stopped
% NBAR Error : Activation failed due to insufficient dynamic memory
% NBAR Error: Stile could not add protocol node
%NAT: Error activating CNBAR on the interface Vlan1
R1(config-if)#
*Mar 1 00:00:57.127: %LINEPROTO-5-UPDOWN: Line protocol on Interface NVI0,
changed state to up
*Mar 1 00:00:57.251: %SYS-2-MALLOCFAIL: Memory allocation of 10260 bytes
failed from 0x62915CD4, alignment 0
Pool: Processor Free: 18968 Cause: Memory fragmentation
Alternate Pool: None Free: 0 Cause: No Alternate pool
 -Process= "Exec", ipl= 0, pid= 195, -Traceback= 0x6148BFF8 0x60016604
0x6001C564 0x6001CBBC 0x636756E4 0x62915CDC 0x628F468C 0x628F88C 0x628F5968
0x628F87A0 0x628F5968 0x628F8344 0x628F5968 0x628F5B2C 0x62928FBC 0x62933A20
R1(config-if)#
*Mar 1 00:00:57.275: %NBAR-2-NOMEMORY: No memory available for StILE lmalloc,
-Traceback= 0x6148BFF8 0x62915CF8 0x628F468C 0x628F88C 0x628F5968 0x628F87A0
0x628F5968 0x628F8344 0x628F5968 0x628F5B2C 0x62928FBC 0x62933A20 0x62920BD0
0x6293DF70 0x6293E2F0 0x61C77C70
R1(config-if)#
```

在这个示例中，路由器 `R1` 在尝试配置网络地址转换之前一直运行良好。由于该路由器内存不足，Cisco IOS 立即显示内存分配错误信息。在 GNS3 中为路由器分配更多内存应该解决这个问题。

## 解决 NIO 错误

当你尝试使用 `Cloud` 节点将 GNS3 设备连接到 PC 物理以太网适配器时，最容易发生 NIO 错误。如果你在连接设备之间或 `Cloud` 节点时遇到困难，或者收收到如图 A-4 所示的 NIO 错误消息，你可能遇到了权限问题。

![image description](img/httpatomoreillycomsourcenostarchimages2209199.png.jpg)

图 A-4. 无法创建通用以太网 NIO 错误消息

在这种情况下，你可能需要给自己分配提升权限。如果你在 Windows 上运行 GNS3，请使用管理员帐户启动 GNS3：右键点击 GNS3 图标并选择 `以管理员身份运行`。如果你使用 OS X，你可能需要为 `/dev/tap` 或 `/dev/bpf` 设备文件分配所有权，如下例所示：

```
$ sudo chown $(id -un):$(id -gn) /dev/bpf*
$ sudo chown $(id -un):$(id -gn) /dev/tap*
```

这些命令将当前登录用户的用户 ID 分配给设备文件，允许你的用户账户在运行 GNS3 时使用这些文件。你必须每次重启 Mac 时都设置这些权限，因为 OS X 在启动时会重置所有设备文件的权限。

为了高安全性，请使用 `setcap` 命令提升 `dynamips` 文件的能力。在 Ubuntu 上，在输入 `setcap` 命令之前你可能需要安装 `libcap2`。

```
$ sudo apt-get install libcap2
$ sudo setcap cap_net_raw,cap_net_admin+eip /usr/local/bin/dynamips
```

### Linux 安全注意事项

如果你运行 Linux，可能需要以提升的权限运行 Dynamips。针对这种情况，根据你的 Linux 发行版有两种方法可供选择。

可以使用 Linux 的 `chown` 和 `chmod` 命令，或者使用 `setcap` 命令。这两种方法都可以解决权限问题，但 `chmod`/`chown` 方法的安全性较低。

当启动 Dynamips 路由器时控制台运行缓慢，可能是因为该路由器没有被分配最佳的 Idle-PC 值。选择不当的 Idle-PC 值对 CPU 造成的破坏可能与完全不设置值一样严重。要验证或设置您的 Idle-PC 值，请右键点击路由器，选择 `Configure` 打开节点配置器（Node Configurator），并在 `Advanced` 选项卡上检查您的 Idle-PC 值。如果路由器已经分配了 Idle-PC 值且设备正在消耗大量 CPU，那么您可能需要重新计算该值。（参见设置手动 Idle-PC 值）。

如果您更改了任何 Dynamips 的高级优化设置（例如 `Idlemax` 或 `Idlesleep`），您的控制台也可能运行缓慢。`Idlemax` 和 `Idlesleep` 与 Idle-PC 值配合使用；`Idlemax` 决定了在路由器代码中执行空闲循环时睡眠的频率，而 `Idlesleep` 值决定了睡眠时长。尝试点击 `Reset` 按钮将它们重置为默认值，如图 A-5 所示。

GNS3 开发团队已确定，`Idlemax` 和 `Idlesleep` 的默认值对大多数用户是最优的，但您可以按照节省资源中描述的方法修改它们，从而获得更好的 CPU 性能。

![Advanced router configuration](img/httpatomoreillycomsourcenostarchimages2209201.png.jpg)

图 A-5. 高级路由器配置

如果缓慢控制台是一个 IOU 设备且您正在使用 IOU 虚拟机（Windows 和 OS X 必需），尝试在 VirtualBox 中为 IOU 虚拟机分配更多内存。

# 功能问题

当您尝试实现以前未使用过的 GNS3 功能时就会发生功能问题，这些通常是由某种用户错误引起的。GNS3 拥有许多功能和选项，项目可能会变得复杂，特别是当您使用多台 PC 运行 GNS3，或者在项目中添加 QEMU 和 VirtualBox 虚拟机时。功能问题也可能存在于设备配置中。

## 配置问题



如果您在项目内部遇到网络路由问题，可能是因为您在配置设备的网络操作系统时犯了错；毕竟，`GNS3` 是一个学习工具，您在过程中难免犯错。在使用 `Arista`、`IOS` 和 `Junos OS` 等操作系统配置功能时，很容易犯导致网络中断的错误。检查您的设备配置，确保您没有为 IP 地址分配了错误的子网掩码，或者没有忘记启动接口。防止此类问题的一种方法是像配置实际网络一样配置您的 `GNS3` 项目设备。从几个设备开始，配置并测试它们，然后不断添加并测试设备，直到创建一个功能完备的项目。

## 使用不支持的 IOS 镜像

简而言之，不要尝试使用不支持的镜像。`Dynamips` 支持有限的 `Cisco` 路由器（参见附录 B）。

![Unsupported image](img/httpatomoreillycomsourcenostarchimages2209203.png.jpg)

图 A-6. 高级路由器配置

## 核武器选项

如果您在尝试了上述操作后仍然继续遇到 `GNS3` 的问题，可以采取“核武器选项”作为最后手段并清除 `GNS3` 设置。一旦删除了该文件，您将失去所有偏好设置并必须像第一次安装一样重新配置。

在开始之前，请备份现有的配置。进入 `Preferences` 并选择 `General` 选项卡；在新窗口中选择 `General`，如图 A-7 所示。

`GNS3` 设置文件显示在 `Configuration file` 下。要备份文件，请点击 `Export` 按钮。选择文件名和保存位置。注意原始文件的位置（在本示例中，为 `/home/neumann/.config/GNS3/gns3_gui.conf`），一旦导出完成，关闭 `GNS3` 并删除或重命名此原始文件。现在当您重新打开 `GNS3` 时，所有偏好将被清除，就像第一次安装一样。如果您认为清除文件是一个错误，可以使用 `Import` 恢复原始的 `GNS3` 设置。

![Exporting and clearing the GNS3 configuration](img/httpatomoreillycomsourcenostarchimages2209205.png.jpg)

图 A-7. 导出并清除 GNS3 配置

## 硬件过载

当 `GNS3` 运行缓慢且设备崩溃时，这可能是由于您用过多的设备使 PC 处理器过载了；这无疑会减慢控制台响应并可能导致 `Dynamips` 崩溃。如果是如此，请考虑精简项目、升级 PC 或使用多台 PC 运行 `GNS3`。

## 解决端口号冲突

在某个时刻，您计算机上的其他软件可能会与 `GNS3` 发生冲突。这通常发生在软件使用的端口号是 `GNS3` 需要的运行时。如果使用的端口号与您的 `GNS3` 服务器应用程序相同，`GNS3` 将加载，但服务器应该选择另一个端口号。

当这种情况发生时，使用 `netstat` 命令调查问题，该命令在 `Windows` 和如 `Linux` 和 `OS X` 的类 Unix 系统中都应包含。

```
$ netstat -an|more

Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:8000            0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:39191         127.0.0.1:80➊         TIME WAIT
tcp6       0      0 ::1:631                 :::*                    LISTEN
tcp6       1      0 ::1:53974               ::1:631                 CLOSE WAIT
udp        0      0 0.0.0.0:59759           0.0.0.0:*
udp        0      0 0.0.0.0:39309           0.0.0.0:*
udp        0      0 127.0.1.1:53            0.0.0.0:*
udp        0      0 0.0.0.0:68              0.0.0.0:*
udp        0      0 0.0.0.0:631             0.0.0.0:*
udp        0      0 0.0.0.0:5353            0.0.0.0:*
udp6       0      0 :::57463                :::*
udp6       0      0 :::45876                :::*
udp6       0      0 :::5353                 :::*
```

TCP 端口号 `8000` ➊ 是为 `GNS3` 服务器程序保留的默认端口号，但 `netstat` 输出显示另一个应用程序正在使用该端口。要解决此问题，请找到冲突的应用程序并将其关闭，或者更改 `GNS3` 使用的默认端口号。要更改端口号，前往 `Preferences`（首好） ▸ `Servers`（服务器） ▸ `Local Server Port`（本地服务器端口）并将端口号设置为 `8000` 的其他数字，例如 `8001`。

## ASA 故障排除

在 `GNS3` 中安装 `ASA` 时，请确保在安装向导的 `Type`（类型）下拉菜单中选择 `ASA 8.4(2)`。随后 `GNS3` 向导将用正确的信息填充所需的字段。

如果你的 `ASA` 配置正确但卡死或运行缓慢，可能是 `ASA` 导致了高 CPU 使用率，从而影响了 PC 的整体性能。你可以通过调整 `ASA` 的 CPU 限制百分比大大降低 CPU 使用率。进入 `Preferences`，选择你的 `ASA`，点击 `Edit` 并启用 `CPU throttling`（CPU 限制）。但要注意，过度限制 `ASA` CPU 使用也会导致 `ASA` 无响应。为了获得最佳效果，请尝试调整设置，直到找到一个既能降低 CPU 使用率又不对性能产生负面影响的平衡点。

## 节省资源

总的来说，只要你有适当硬件资源，`GNS3` 能够很好地处理几乎任何规模的项目，但项目越大，遇到问题的可能性就越高。避免这些问题的最佳方法是在创建项目时采用极简方法，并避免为设计增加不必要的复杂度。

### 小心选择设备

在 `GNS3` 中，始终选择内存和 CPU 消耗最少的设备。例如，如果可以使用仅需 `128MB` RAM 的 `c3700` 路由器，请避免使用需要 `512MB` RAM 的 `c7200` 路由器。在使用 `Dynamips` 设备时，项目中的所有路由器应使用相同的设备模型；这样 `GNS3` 可以在它们之间共享资源。使用多个不同的路由器模型会导致资源消耗和性能下降。你还可以使用仿真设备，例如使用以网交换机节点而不是 `EtherSwitch` 路由器，以节省内存和处理器。

### 优化 Idle-PC 值

为了减少系统资源占用，请调优 `Idle-PC` 值。当你运行少量 `IOS` 设备时，当前的值可能没问题，但较大的项目将从更优化的值中获益。

要找到最适合你的值，首先让你的电脑处于基本空闲状态：重启电脑并关闭所有程序（包括杀毒软件）。如果你使用 `Windows`，请尽可能关闭系统托盘中的应用程序。准备好后，向工作区添加一个路由器，启动它，右键点击路由器并选择 `Idle-PC` 开始计算 `Idle-PC` 值。在此过程中，在应用每个新值后仔细监控 CPU，并记录所有值。寻找消耗资源最少的那个值，一旦找到，将其应用到设备。

### 备份你的项目

备份 `GNS3` 项目非常重要，尤其是当它们变得越来越复杂且创建耗时更长时。没有人喜欢丢失花费数小时创建的工作！你可以备份整个 `GNS3` 文件夹、备份项目文件夹，或备份单个项目文件夹。

定期备份整个 `GNS3` 文件夹是确保你始终拥有所有项目和镜像的最新副本的最佳方法，但这可能非常耗时，并可能需要大量的磁盘空间。

如果你时间或资源紧张，至少从项目文件夹中备份单个项目。确保你已将整个 `GNS3` 文件夹备份到 U 盘或外部硬盘中。

### 欢迎来到丛林

当你无法独立解决问题时，不要害怕寻求帮助。`GNS3` 网站（[`www.gns3.com/`](http://www.gns3.com/)）提供了丰富的信息，并设有一个名为 *GNS3 Jungle* 的专用论坛。你可以在这里报告问题、提问并帮助其他用户解决问题。

在发布问题之前，请搜索网站查看你的问题是否已经过提出并解答。`GNS3 Jungle` 有非常活跃的社区，因此问题通常会得到快速回复。如果你发布了问题但没有按预期速度得到回复，请不要重复发布或回复自己的帖子来顶帖。重复发布相同的问题只会干扰尝试帮助你的人。通常，一个问题无人问津，是因为目前查看论坛的人没有答案。请耐心等待，很快会有人回复。

提问时，建议提供以下信息：

- `GNS3` 版本
- 操作系统名称和版本
- 平台细节（32 位或 64 位、处理器和内存）
- 问题的清晰描述
- 错误信息的截图（适用）
- 首选项设置的截图（适用）
- 拓扑结构（适用）
- 设备配置（适用）

详细的信息有助于其他 `GNS3` 用户判断你的问题并更快地给出解决方案。

### 结语

尽管 `GNS3` 通常运行良好，但偶尔还是会出现问题。在本附录中，你已经查看了一些常见问题以及纠正这些问题的基本排除策略。

你已经了解到防火墙、防病毒软件，以及偶尔基于 TCP/IP 的应用程序可能会对 `GNS3` 造成破坏。当不确定时，请在启动 `GNS3` 之前禁用防火墙、禁用防病毒软件并关闭任何不必要的程序。

你还了解到，修复损坏项目最快的方法通常是从备份恢复项目。你应该始终保留整个 `GNS3` 文件夹和 `GNS3` 设置文件的最新备份副本。从备份中恢复数据是灾难后恢复正常运行最可靠的方法。

## 附录 B. 与 GNS3 的 Cisco 硬件

本附录列出了 `Dynamips` 和 `GNS3` 支持的 `Cisco` 硬件。`Dynamips` 仅仿真使用 `MIPS` 架构的 `Cisco` 路由器，不支持所有的 `Cisco` 模型。在支持的路由器列表中，你会发现一个推荐的 `IOS` 镜像列表，`GNS3` 可以自动为它们应用正确的 `Idle-PC` 值，而无需执行 `Idle-PC` 计算。

### 支持的 Cisco 硬件

在 `GNS3` 中，你可以仿真来自五个不同系列（1700、2600、3600、3700 和 7200）的 `Cisco` 路由器，功能支持程度各异。

表 B-1. 1700 系列路由器

![1700 Series Routers](img/bfig01.png.jpg)

表 B-2. 2600 系列路由器

![2600 Series Routers](img/bfig02.png.jpg)

表 B-3. 3600 系列路由器

![3600 Series Routers](img/bfig03.png.jpg)

表 B-4. 3700 系列路由器

![3700 Series Routers](img/bfig04.png.jpg)

表 B-5. 7200 系列路由器

![7200 Series Routers](img/bfig05.png.jpg)

### IOS 兼容性

以下路由器不再接收 `Cisco` 的 `IOS` 更新。这里列出的 `IOS` 文件名是 `GNS3` 的推荐版本，尽管旧版本也可以正常工作。

表 B-6. c1700 系列路由器

![c1700 Series Routers](img/bfig06.png.jpg)

表 B-7. c2600 系列路由器

![c2600 Series Routers](img/bfig07.png.jpg)

表 B-8. c2691 系列路由器

![c2691 Series Routers](img/bfig08.png.jpg)

表 B-9. c3620 系列路由器

![c3620 Series Routers](img/bfig09.png.jpg)

表 B-10. c3640 系列路由器

![c3640 Series Routers](img/bfig10.png.jpg)

表 B-11. c3660 系列路由器

![c3660 Series Routers](img/bfig11.png.jpg)

表 B-12. c3725 系列路由器

![c3725 Series Routers](img/bfig12.png.jpg)

表 B-13. c3745 系列路由器

![c3745 Series Routers](img/bfig13.png.jpg)

`Cisco c7200` 系列路由器继续接收 `Cisco` 的 `IOS` 更新，并支持 `15.x` 版本 `IOS`。

表 B-14. c7200 系列路由器

![c7200 Series Routers](img/bfig14.png.jpg)

## 附录 C. NM-16ESW 和 IOU L2 局限性

`GNS3` `Dynamips NM-16ESW` 模块的操作与其真实的 `Cisco` 对应设备相同。与物理模块一样，`Dynamips` 模块不支持 `Cisco Catalyst` 交换机的所有功能，这意味着获得完整 `Catalyst` 交换机功能的唯一方法是将一个或多个真实交换机集成到你的 `GNS3` 项目中。我在列出了这些不支持的功能，以及 `IOU L2` 镜像可能不支持的功能。

如果你想使用特定的 `Catalyst` 交换机功能，请先检查这些列表，确认你是否需要使用物理交换机。

### 不支持的 NM-16ESW 功能

`NM-16ESW` 交换模块不支持以下功能：

- Access Switch Device Manager (SDM) Template
- ACL – 改进的合并算法
- ARP 优化
- BGP 对编号 as-path 访问列表的支持增加到 500
- BGP 在达到 max-prefix 限制后重启邻居会话
- BGP Route-Map 继续支持出站策略
- 每个端口清除计数器
- DHCP Snooping
- DHCP Snooping 计数器
- 启动时的诊断选项
- 每个端口的 ErrDisable 激活
- ErrDisable Timeout
- EtherChannel
- EtherChannel – 灵活 PAgP
- EtherChannel Guard
- Fallback Bridge
- Flex Link 双向快速收敛
- Flex Link VLAN 负载均衡
- Flex Links 接口抢占
- GOLD – 通用在线诊断
- IEEE 802.1ab，链路层发现协议 (LLDP)
- IEEE 802.1s – 多实例生成树 (MST) 标准兼容
- IEEE 802.1t – 快速生成树重配置
- IEEE 802.1w – 快速生成树 (RSTP)
- IEEE 802.1x – 生成树端口认证
- IEEE 802.3ad – 链路聚合
- IEEE 802.3af – 以太网供电 (PoE)
- IEEE 802.3x – 流控制
- IGMP Snooping
- ISL Trunks
- L3 Etherchannel
- MLS QoS
- Port-security
- Private VLAN
- QinQ
- SPAN/RSPAN/ERSPAN
- UDLD
- Voice VLANs

### IOU 镜像不支持的功能

`IOU` 据说支持实际 `Catalyst` 交换机功能的 90%。以下功能可能不支持。由于 `Cisco` 负责更新 `IOU` 镜像，实际情况可能会有所不同。

- DHCP snooping
- ISL trunks
- L3 Etherchannel
- MLS QoS
- Port-security
- Private VLAN
- QinQ
- SPAN/RSPAN/ERSPAN
- UDLD
- Voice VLANs

## 术语表

以下是书中使用的缩写词表。

**APT (Advanced Package Tool)** 用于基于 Debian 的 Linux 系统的软件包命令行工具。

**ARP (Address Resolution Protocol)** 用于将网络地址映射到链路地址的协议。通常用于 IP 到 MAC 地址的解析。

**AS (autonomous system)** 在单一组织管理下共享网络前缀的路由器组。

**ASA (adaptive security appliance)** Cisco 防火墙设备。

**ASDM (Adaptive Security Device Manager)** 用于管理和监控 Cisco 安全设备的软件。

**ASIC (application-specific integrated circuit)** 通常是特定厂商的专用电路。

**ATM (Asynchronous Transfer Mode)** 一种用于通过公共和私有网络传输语音、视频和数据的技术。很大程度上被 MPLS 取代。

**BGP (Border Gateway Protocol)** 互联网的路由协议。BGP 使用自治系统交换路由信息。

**BSD (Berkeley Software Distribution)** 在加州伯克利开发的 Unix 操作系统。

**CCIE (Cisco Certified Internetwork Expert)** Cisco 的专家级认证。

**CCNA (Cisco Certified Network Associate)** Cisco 的助理级认证。



**CCNP (Cisco Certified Network Professional)** Cisco 的专业级认证。

**CCP (Cisco Configuration Professional)** 用于管理和监控 Cisco 路由器的软件。

**CDP (Cisco Discovery Protocol)**

一种 Cisco 专用协议，用于从网络上直接连接的 Cisco 设备收集硬件和配置信息。

### CIDR（无类网间路由）

一种为 IP 地址分配子网掩码的简写方法。`CIDR` 使用斜杠，后跟 IP 地址中掩码部分的二进制位数；例如，`192.168.1.1` `255.255.255.0` 在 `CIDR` 记法中写为 `192.168.1.1 /24`。

### CPU（中央处理器）

计算机中负责执行代码和控制输入/输出操作的电路。

### DHCP（动态主机配置协议）

一种用于向主机动态应用 IP 地址和其他网络设置的协议。

### DLCI（数据链路连接标识符）

一种链路本地虚拟电路标识符，用于将帧分配给 `PVC` 或 `SVC`。

### DNS（域名系统）

一种分层的数据库服务器结构，用于将 Internet 主机名映射到 IP 地址。

### EIGRP（增强内部网关路由协议）

一种 Cisco 专用的高级距离矢量路由协议。

### FTP（文件传输协议）

一种用于通过 `TCP/IP` 将文件从一个主机传输到另一个主机的协议。也是允许用户与远程主机传输文件的程序的名称。

### GLBP（网关负载均衡协议）

一种支持负载均衡的 Cisco 专用冗余路由器协议。

### HSRP（热备备路由协议）

一种 Cisco 专用的冗余路由器协议，在默认网关处提供自动路由器故障转移。

### IDS/IPS（入侵检测系统/入侵防御系统）

一种监控网络活动以检测恶意代码的设备，通常与防火墙配合工作。异常活动会触发报警并报告给系统管理员。

### I/O（输入/输出）

用于描述任何向计算机或从计算机传输数据的程序、操作或设备。

### IOL（Linux 上的 IOS）

运行在 Linux 上并模拟 Cisco `IOS` 路由器或交换机功能的软件。

### IOS（网互域操作系统）

Cisco 主要路由器和交换机操作系统。

### IOU（Unix 上的 IOS）

运行在 Linux/Unix 上并模拟 Cisco `IOS` 路由器或交换机功能的软件。

### IP（网协议）

`TCP/IP` 栈中的网络层协议，提供路由和逻辑地址。

### IPv4（网际协议第四版）

`IP` 的第四版本。`IPv4` 使用 32 位地址方案。

### IPv6（网际协议第六版）

`IP` 的第六个版本。`IPv6` 使用 128 位地址方案。

### ISL（交换机链路）

一种 Cisco 专用的 VLAN 组干协议，在现代网络中已被 `802.1Q` 取代。

### ISP（互联网服务提供商）

为消费者和企业提供 Internet 接入公司。

### ISR（集成服务路由器）

一种用于小型企业或家庭办公室的 Cisco 路由器型号，通常通过 `DSL` 或电缆调制调器连接到 Internet。`ISR` 硬件通常使用专用集成设计。

### JNCIA（瞻远网络认证关联工程师）

针对 `Junos OS` 的 Juniper 入门关联工程师认证。

### LAN（局域网）

连接较小地理区域（如单栋建筑或一组建筑）内计算机和外围设备的网络。

### LMI（逻辑管理接口）

一种用于路由器和分帧传输交换机之间的信号标准。

### MAC（介质访问控制）

写入以太网网卡固件中的唯一标识符。`MAC` 地址用于物理网络网段上的通信。

### MPLS（多协议标签交换）

一种使用标签做出数据转发决策的封包转发技术。在现代网络中取代了 `ATM` 和分帧传输。

### MTU（最大传输单元）

协议数据单元的最大帧大小。以太网默认帧大小为 `1500` 字节，但可以根据你的以太网硬件和驱动程序进行缩小或增大。

### NAT（网络地址转换）

一种在边缘路由器或防火墙上使用单个 `IP` 地址的方法，使得边缘设备后的网络设备可以使用单个 `IP` 地址访问边缘设备之外的网络（如 Internet）。`NAT` 负责重写数据报文头部，以跟踪边缘设备与内部主机之间的数据包。

### NIO（网络输入/输出）

用于描述任何通过网络向计算机或从计算机传输数据的程序、操作或设备。

### NPE（网络处理引擎）

一种 Cisco 机框卡，为某些 Cisco 路由器型号（如 `c7200`）提供额外功能。

### NVRAM（非易失性随机访问存储器）

一种在掉电后仍保留内容的内存。

### OS（操作系统）

管理计算机内存、进程以及所有的软件和硬件。

### OSPF（开放最短路径优先）

一种内部网关协议，它使用链路状态数据库和最短路径优先 (`SPF`) 算法来计算到达网络的最佳路径。

### OVA（开放虚拟设备文件）

一种用于封装和分发虚拟设备的标准文件格式，可以使用 `VirtualBox` 和 `VMware` 等虚拟机软件运行。

### POS（SONET 上的封包传输）

一种用于在 `SONET` 上传输点对点协议 (`PPP`) 数据包的通信协议。

### PVC（永久虚拟电路）

在分帧传输或 `ATM` 网络中两个或多个节点建立建立永久连接。

### QEMU（快速仿真器）

一种开源机器模拟器和虚拟化工具。

### RAM（随机访问存储器）

一种在掉电后不保留内容的内存。

### RIP（路由信息协议）

一种距离矢量协议，使用跳数作为选择到达远程网络最佳路径的指标。通常被称为“传闻路由”。

### SSH（安全外壳）

用于安全地登录远程机器并在远程机器上执行命令。

### SONET（同步光纤）

一种用于在光纤网络上同步传输数据的协议。

### SVC（交换虚拟电路）

在分帧传输或 `ATM` 网络中两个或多个节点之间建立的动态连接。

### TAR（带归档的文件）

创建并操作流式归档文件。

### TCP（传输控制协议）

`TCP/IP` 栈中的面向连接传输层。`TCP` 负责创建可靠的端到端连接。

### TFTP（简单文件传输协议）

`TFTP` 允许用户在无身份验证或错误纠正的情况下与远程机器传输文件。

### UDP（用户数据报协议）

一种不使用握手的无连接传输层协议。`UDP` 在不确认的情况下交换数据报。

### VIRL（虚拟路由实验室）

Cisco 的网络仿真平台，包含运行 Cisco 核心网络系统的虚拟机。

### VLAN（虚拟局域网）

一种将二层网络划分为独立广播域的机制。

### VM（虚拟机）

一种模拟特定硬件并允许你安装和运行为该硬件设计的操作系统程序。

### VMDK（虚拟机磁盘）

一种虚拟机磁盘镜像文件，通常被 `VMware`、`VirtualBox` 和 `QEMU` 等虚拟机软件使用。

### VPS（虚拟 PC）

一种模拟 PC 基本网络功能和命令的简单程序。

### VPN（虚拟专用网络）

一组允许两个设备在公共网络（如 Internet）上共享加密信息的安全协议。

### VPNC（虚拟专用网络连接）

用于 Cisco `VPN3000` 集中器、`IOS` 设备和 `PIX` 设备的软件客户端。

### VRRP（虚拟路由器冗余协议）

一种在默认网关处提供路由器自动故障转移的开放冗余路由器协议。

## WAN（广域网）

覆盖地理范围广泛的网络，通常由通过一个或多个 VPN 连接的多个网络组成。

## WIC（WAN 接口卡）

一种思科专有的接口卡，通常为路由器提供串口接口。

# 资源

访问 *[`nostarch.com/gns3/`](http://nostarch.com/gns3/)* 获取资源、勘误及更多信息。

更多来自 ![](img/httpatomoreillycomsourcenostarchimages2209207.png.jpg) **NO STARCH PRESS** 的实务型书籍：

![无说明的图片](img/httpatomoreillycomsourcenostarchimages2209209.png.jpg)

**《PF 之书》，第三版**

**OpenBSD 防火墙实战指南**

作者：PETER N.M. HANSTEEN

2014 年 10 月，248 页，$34.95

ISBN 978-1-59327-589-1

![无说明的图片](img/httpatomoreillycomsourcenostarchimages2209211.png.jpg)

**《实战数据分析》，第二版**

**使用 Wireshark 解决现实网络问题**

作者：CHRIS SANDERS

2011 年 7 月，280 页，$49.95

ISBN 978-1-59327-266-1

![无说明的图片](img/httpatomoreillycomsourcenostarchimages2209213.png.jpg)

**《网络安全监控实践》**

**理解入侵检测与响应**

作者：RICHARD BEJTLICH

2013 年 7 月，376 页，$49.95

ISBN 978-1-59327-509-9

![无说明的图片](img/httpatomoreillycomsourcenostarchimages2209215.png.jpg)

**《TCP/IP 指南》**

**全面图解互联网协议参考**

作者：CHARLES M. KOZIEROK

2005 年 10 月，1616 页，$99.95

ISBN 978-159327-047-6

*精装*

![无说明的图片](img/httpatomoreillycomsourcenostarchimages2209217.png.jpg)

**《Linux 命令行》**

**完整入门教程**

作者：WILLIAM E. SHOTTS, JR.

2012 年 1 月，480 页，$39.95

ISBN 978-1-59327-389-7

![无说明的图片](img/httpatomoreillycomsourcenostarchimages2209219.png.jpg)

**《黑帽 Python》**

**面向黑客与渗透测试的 Python 编程**

作者：JUSTIN SEITZ

2014 年 12 月，192 页，$34.95

ISBN 978-1-59327-590-7

**电话：**

800.420.7240 或 415.863.9900

**邮箱：**

SALES@NOSTARCH.COM

**网址：**

[WWW.NOSTARCH.COM](http://WWW.NOSTARCH.COM)

# 关于作者

Jason C. Neumann 是 GNS3 项目的活跃参与者，负责提供代码、管理论坛并在多个平台上进行软件 Beta 测试。Neumann 还是一个拥有 20 多年经验的网络工程师，持有 Cisco、Juniper、Microsoft、Novell 和 VMware 的多项认证。他是 *Cisco Routers for the Small Business* (Apress) 的作者。

# 索引

### 关于数字索引的说明

索引条目中的链接显示为该条目所在的章节标题。由于某些章节有多个索引标记，一个条目拥有多个指向同一章节的链接并不稀见。点击任何链接都将带您直接到达正文中该标记出现的位置。

### 符号

2600 系列路由器，支持的思科硬件

32 位操作系统，IOS-XRv 虚拟机，为 IOS-XRv 配置 GNS3

64 位操作系统，IOS-XRv 虚拟机，为 IOS-XRv 配置 GNS3

7-zip 应用，运行 Juniper vSRX Firefly

802.1Q 中继，连接设备使用，Ubuntu Linux 上的 TUN/TAP 驱动，创建难以捉的突破交换机

?（问号），在 GNS3 控制台中，探索 GNS3 控制台

### A

缩写命令语法，在 VPCS 中，VPCS 命令

访问端口，更改，登录路由器

访问服务器，配置路由器（见访问服务器）

适配器，在 PC 中使用多个适配器，为 IOS-XRv 配置 GNS3，为 IOS-XRv 配置 GNS3，配置 GNS3，将 IOU 虚拟机导入 VirtualBox（见适配器类型）

用于 IOS-XRv 设备，为 IOS-XRv 配置 GNS3

用于 IOU 设备，配置 GNS3

用于 IOU 虚拟机，将 IOU 虚拟机导入 VirtualBox

多个，在 PC 中，使用设备，在 PC 中使用多个适配器

自适应安全设备，获取镜像（见自适应安全设备）

自适应安全管理器 (ASDM)，思科，思科 ASA、IDS/IPS 和 IOS-XRv，在 GNS3 中测试 ASA，术表

添加链接图标，工具栏，第四工具栏，操作路由器，在项目中使用 VirtualBox 主机

添加备注图标，GNS3 工具栏，第三工具栏

地址解析协议 (ARP)，术表

Adobe Flash Player，项目配置

高级包工具 (APT)，术表

高级设置选项卡，配置 Dynamips，创建许可证文件

Dynamips 偏好窗口，配置 Dynamips

UNIX 偏好窗口，创建许可证文件

所有设备图标，工具栏，第四工具栏

始终使用本地服务器（仅限 Linux），UNIX 偏好窗口，创建许可证文件

Apache 服务器，模拟操作系统

设备，导入 VirtualBox，在 Windows 上安装

专用集成电路 (ASIC)，术表

APT（高级包工具），术表

apt-get 工具，在 Windows 上安装

ARP（地址解析协议），术表

arp 命令，VPCS IP 地址

AS（自治系统），术表

ASA（自适应安全设备）防火墙，思科，思科 ASA、IDS/IPS 和 IOS-XRv，运行 CCP，获取镜像，获取镜像，获取镜像，为 GNS3 配置 ASA，在 GNS3 中测试 ASA，解决端口冲突，术表

获取镜像文件，获取镜像

ASDM 安装，在 GNS3 中测试 ASA

为 GNS3 配置，获取镜像

定义，术表

概述，思科 ASA、IDS/IPS 和 IOS-XRv，运行 CCP

为 GNS3 准备镜像，获取镜像

在 GNS3 中测试，为 GNS3 配置 ASA

故障排除，解决端口冲突

asa-initrd.gz 文件，获取镜像

asa-vmlinuz 文件，获取镜像

ASDM（自适应安全管理器），思科，思科 ASA、IDS/IPS 和 IOS-XRv，在 GNS3 中测试 ASA，术表

ASIC（专用集成电路），术表

ATM（异步传输模式），使用 IOS 创建帧中交换机

定义，术表

`switch`, 配置, 使用 IOS 创建帧继交换机

自治系统 (AS), 术语表

### B

备份, 让你的 Olive 运行起来, 在 GNS3 中验证 IDS/IPS, 配置问题, 节省资源

GNS3 配置文件, 配置问题

Juniper Olive, 让你的 Olive 运行起来

项目, 节省资源

QEMU 镜像文件, 在 GNS3 中验证 IDS/IPS

Berkeley 软件发行 (BSD), 术语表

BGP (边界网关协议), 术语表

二进制应用, QEMU, 在 GNS3 中配置 Juniper 路由器

二进制文件, QEMU 虚拟机, 为 ASA 配置 GNS3, 为 IDS/IPS 配置 GNS3, 为 IOS-XRv 配置 GNS3

bison 包, 安装 IOU

启动路由器, 设置手动 Idle-PC 值

边界网关协议 (BGP), 术语表

Boson NetSim, 介绍 GNS3

跳出线, 创建难以的跳出交换机

跳出交换机, 配置标准的 802.1Q Tr 干, 创建难以的跳出交换机, 创建一个简单的网络

创建, 配置标准的 802.1Q Tr 干

可选配置，用于, 创建难以的跳出交换机

概述, 创建一个简单的网络

网桥, Dynamips 权限, Dynamips 权限, 将 GNS3 IOU 虚拟机导入 VirtualBox

在环回地址和以太网适配器之间, Dynamips 权限

针对 IOU 虚拟机, 将 GNS3 IOU 虚拟机导入 VirtualBox

为 PC 准备工作, Dynamips 权限

Bryant Advantage 视频, 创建一个 GNS3 Uberlab

BSD (Berkeley 软件发行), 术语表

构建目录, 在 Linux 中创建 ISO, ASDM 安装

针对 IDS/IPS, ASDM 安装

在 QEMU 中准备, 在 Linux 中创建 ISO

内置设备节点, 内置设备节点

### C

使用 Wireshark 捕获数据包, 在 OS X 上安装

Cisco Catalyst 交换机, 有限仿真](#ch01.html_iddle1084), NM-16ESW 和 IOU L2 限制

CBT Nuggets 视频, 创建一个 GNS3 Uberlab

CCIE (Cisco 认证互联网专家)认证, 有限仿真, 创建一个 GNS3 Uberlab, 术语表

CCNA (Cisco 认证网络工程师)认证, 项目概述, 创建一个 GNS3 Uberlab, 术语表

CCNP (Cisco 认证网络专业人士)认证, 项目概述, 创建一个 GNS3 Uberlab, 术语表

CCP , Cisco ASA, IDS/IPS 和 IOS-XRv, Cisco ASA, IDS/IPS 和 IOS-XRv, Cisco ASA, IDS/IPS 和 IOS-XRv, 项目配置, 项目配置, 术语表

定义, 术语表

安装, 项目配置

概述, Cisco ASA, IDS/IPS 和 IOS-XRv, Cisco ASA, IDS/IPS 和 IOS-XRv

项目配置, Cisco ASA, IDS/IPS 和 IOS-XRv

运行, 项目配置

CD 镜像文件, 概述, ASDM 安装

Cisco IDS/IPS, ASDM 安装

Juniper Olive, 概述



# CDP (Cisco 发现协议)

创建难以的跳出交换机，术语表

# 中央处理器 (CPU)

将 IOS 镜像添加到 GNS3，为 ASA 配置 GNS3，解决冲突，术语表

# 定义

术语表

# 节流

针对 ASA，为 ASA 配置 GNS3，解决冲突

# 用法

为设置 Idle-PC 值，将 IOS 镜像添加到 GNS3

# 认证

准备，创建一个 GNS3 Uberlab（另见特定认证）

# 检查最小 RAM 需求

IOS 屏幕，将 IOS 镜像添加到 GNS3

# 针对 Junos OS 的检查

移除，完成 FreeBSD 安装

# `chmod` 命令

解决错误

# `chown` 命令

解决错误

# CIDR (无类域间路由)

VPCS 命令，NX-OS 实战，术语表

# Cisco 接入服务器

配置接入路由器（见虚拟接入服务器）

# Cisco 自适应安全防火墙

获取镜像（见 ASA (自适应安全防火墙)）

# Cisco 自适应安全设备 (ASDM)

Cisco ASA，IDS/IPS 和 IOS-XRv，在 GNS3 中测试 ASA，术语表

# Cisco ASDM-IDM 启动器

ASDM 安装

# Cisco Catalyst 交换机

有限仿真，NM-16ESW 和 IOU L2 限制

# Cisco 认证考试

设置手动 Idle-PC 值，创建一个 GNS3 Uberlab

# Cisco 认证互联网专家 (CCIE) 认证

有限仿真，创建一个 GNS3 Uberlab，术语表

# Cisco 认证网络工程师 (CCNA) 认证

项目概述，创建一个 GNS3 Uberlab，术语表

# Cisco 认证网络专业人士 (CCNP) 认证

项目概述，创建一个 GNS3 Uberlab，术语表

# Cisco 配置专家

术语表（见 CCP 软件）

# Cisco 控制台窗口

设置手动 Idle-PC 值

# Cisco 发现协议 (CDP)

创建难以的跳出交换机，术语表

# Cisco 增强内部网关协议

术语表（见 EIGRP）

# Cisco 功能导航网站

将 IOS 镜像添加到 GNS3，当 IOS 镜像加载失败时

# Cisco 硬件

支持，与 GNS3 兼容的 Cisco 硬件

# Cisco 入侵检测/防御系统

ASDM 安装（见 IDS/IPS (入侵防御系统/入侵检测系统)）

# Cisco IOS (网络操作系统)

介绍 GNS3，支持的 Cisco 硬件，术语表

## Cisco 设备与网络组件

- `Unix 上的 Cisco IOS`，介绍 GNS3（参见 IOU）
- `Cisco IOS-XRv`，为 IOS-XRv 配置 GNS3（参见 IOS-XRv）
- `Cisco IP 主机名表（hostname table）`，用于虚拟接入服务器，配置接入服务器路由器
- `Cisco ISL (交换机间链路)`，术语表
- `Cisco Learning Network`，Cisco IOU
- `Cisco NM-16ESW` 交换机模块，有限仿真，登录路由器
- `Cisco NPE (网络处理器引擎)`，术语表
- `Cisco NX-OSv`，将 NX-OSv 导入 VirtualBox（参见 NX-OSv）
- `Cisco 路由器`，在 Microsoft Windows 上安装，添加以太网接口，打开控制台，将 GNS3 配置导出到 Cisco 路由器，与 GNS3 的 Cisco 硬件，支持的 Cisco 硬件
- 将配置导入 GNS3，将 GNS3 配置导出到 Cisco 路由器
- IOS 兼容性，支持的 Cisco 硬件
- 支持的，与 GNS3 的 Cisco 硬件
- 测试 Juniper 路由器与之间的连接性，添加以太网接口
- `Cisco 交换机组设计`，“破解我的机架”挑战
- `Cisco 交换机`，CDP 隧道兼容性，创建难以捉摸的突破交换机
- `Cisco 虚拟互联网路由实验室 (VIRL)`，介绍 GNS3，术语表
- `Cisco VPNs`，“破解我的机架”挑战
- `Cisco WIC (WAN 接口卡)`，术语表

## 协议与服务器设置

- `无分类网域间路由 (CIDR)`，VPCS 命令，`NX-OSv 实战`，术语表
- 客户端/服务器设置，探索 GNS3 控制台，Dynamips 客户端/服务器设置，另一个 Dynamips 客户端/服务器设置，运行 `gns3server`，配置客户端
- 配置客户端，运行 `gns3server`
- 概述，探索 GNS3 控制台
- 准备工作站，Dynamips 客户端/服务器设置
- 运行 `gns3server`，Dynamips 客户端/服务器设置
- 建立 uberlab，配置客户端
- GNS3 客户端/服务器技术，模拟操作系统

## 虚拟化与网络

- `clock rate` 命令，使用 IOS 创建帧中继交换机
- 克隆功能，`VirtualBox`，VirtualBox 虚拟机设置，为你的虚拟机分配更多处理器
- 云节点，设备节点、实时交换机和互联网，云节点，在 Windows 上使用环回适配器，配置标准的 802.1Q 中继，创建难以捉摸的突破交换机，将 GNS3 设备连接到互联网，在 GNS3 中创建接入服务器
- 配置接入服务器，在 GNS3 中创建接入服务器
- 标准 802.1Q 中继，配置标准的 802.1Q 中继
- 使用 Linux 配置 VLAN，创建难以捉摸的突破交换机
- 使用环回适配器配置，在 Windows 上使用环回适配器，将 GNS3 设备连接到互联网
- 一般讨论，云节点
- 概述，设备节点、实时交换机和互联网
- 通信服务器，配置接入服务器路由器（参见接入服务器）
- 命令行界面，GNS3，屏幕布局，使用 IOU 设备的项目
- 命令行提示符，`IOS-XRv`，配置路由器

## GNS3

- 配置问题
- 配置按钮、CCP 管理界面、运行中的 CCP
- 连接超时、虚拟接入服务器、打开控制台
- 连通性、模拟操作系统，测试 Juniper 路由器，创建简单的网络，项目配置，为 ASA 配置 GNS3
- ASA、测试、为 ASA 配置 GNS3
- Windows 客户机与路由器之间、项目配置
- 互联网、创建简单的网络
- Juniper 路由器、测试 Juniper 路由器
- 虚拟、使用 GNS3 的、模拟操作系统
- 节省资源、节省资源
- 控制台应用程序标签页、GNS3 普通偏好窗口、手动设置 Idle-PC 值，手动设置 Idle-PC 值
- 连接到所有设备的图标、GNS3 工具栏、使用 GNS3 工具栏，登录路由器
- 控制台端口号、创建许可证文件，配置接入服务器路由器
- 配置 Cisco IP 主机名表、配置接入服务器路由器
- UNIX 上的 IOS 偏好窗口、创建许可证文件
- 控制台、手动设置 Idle-PC 值，屏幕布局，安装 VPCS，配置 Cisco IP 主机名表，带有 IOU 设备的项目，解决 NIO 错误
- Cisco、手动设置 Idle-PC 值
- GNS3、屏幕布局，带有 IOU 设备的项目
- 故障排除问题、解决 NIO 错误
- 虚拟接入服务器、配置 Cisco IP 主机名表
- VPCS、安装 VPCS
- 从路由器拷贝 IOS 镜像文件、获取 IOS 镜像
- 损坏的 IOS 镜像文件、IOS 镜像加载失败
- CPU（处理器）、将 IOS 镜像添加到 GNS3，为 ASA 配置 GNS3，解决端口冲突，术语表
- 定义、术语表
- 节流、针对 ASA、为 ASA 配置 GNS3，解决端口冲突
- 使用、为设置 Idle-PC 值、将 IOS 镜像添加到 GNS3
- `cpulimit`、为 ASA 配置 GNS3，为 ASA 配置 GNS3
- 崩溃、Dynamips、识别问题
- 创建虚拟机向导、运行 Juniper vSRX Firefly，NX-OSv

### D

- 数据链路连接连接标识符 (DLCI)、帧中继交换机，使用 IOS 创建帧中继交换机，术语表
- `debug` 命令、探索 GNS3 控制台
- 解压缩 IOS 镜像、配置 Dynamips
- 删除设备之间的链路、在路由器之间创建链路
- 依赖项、安装、从源码安装 GNS3
- `/dev/bpf` 设备文件、解决 IOS 内存错误，解决 IOS 内存错误
- 设备仪表板、ASDM、ASDM 安装
- 设备文件权限、OS X、解决 IOS 内存错误
- 设备管理器、CCP、项目配置
- 设备节点、设备节点、实时交换机和互联网，内置设备节点，内置设备节点，节点配置器，`EtherSwitch`路由器，帧中继交换机，使用 IOS 创建帧中继交换机，使用 IOS 镜像，云节点，配置 802.1Q 中继，配置 GNS3（见控制台交换机）
- ATM 交换机、内置设备节点
- 内置、云
- 云、连接到互联网
- 连接到硬件
- 以太网、节点配置器
- `EtherSwitch`路由器
- 交换机
- 概述、设备节点、实时交换机和互联网，内置设备节点，内置设备节点，节点配置器，`EtherSwitch`路由器，帧中继交换机，使用 IOS 创建帧中继交换机，使用 IOS 镜像，云节点，配置 802.1Q 中继，配置 GNS3（见控制台交换机）
- ATM 交换机、内置设备节点
- 内置、云
- 云、连接到互联网
- 连接到硬件
- 以太网、节点配置器
- `EtherSwitch`路由器
- 交换机
- 概述、设备节点、实时交换机和互联网

动态主机配置协议 (DHCP)，VPCS 命令，术语表

Dynamips，开源集成，在 Microsoft Windows 上安装，安装 Dynamips，获取 IOS 镜像，获取 IOS 镜像，获取 IOS 镜像，创建你的第一个项目，将 VirtualBox 主机节点连接到其他设备，云节点，为 IOS-XRv 配置 GNS3，UNIX 和 NX-OSv 上的 Cisco IOS，配置云节点，在平台之间拷贝 GNS3 项目，Dynamips 客户端/服务器设置，识别问题，解决 IOS 内存错误，修正控制台问题，与 GNS3 的 Cisco 硬件（参见路由器）

- 客户端/服务器设置，Dynamips 客户端/服务器设置
- 配置文件，创建你的第一个项目
- 配置，获取 IOS 镜像
- 控制台问题，修正控制台问题
- 在平台之间拷贝 GNS3 项目，在平台之间拷贝 GNS3 项目
- 将 IOS 镜像文件拷贝到，获取 IOS 镜像
- 崩溃，识别问题
- IOS-XRv 项目，为 IOS-XRv 配置 GNS3
- Linux VirtualBox 主机到路由器，将 VirtualBox 主机节点连接到其他设备
- 概述，开源集成
- 权限问题，解决 IOS 内存错误
- 权限设置，云节点
- 支持的 Cisco 硬件，与 GNS3 兼容的硬件
- 在 Linux 中验证路径，获取 IOS 镜像
- 虚拟访问服务器配置，配置云节点
- 对 IOU，UNIX 和 NX-OSv 上的 Cisco IOS
- Dynamips IOS 配置框，创建你的第一个项目
- Dynamips 偏好窗口，配置 Dynamips，配置客户端

### E

EIGRP (增强内部路由协议)，Cisco，配置路由器，配置 IOS-XR 设备，为 NX-OSv 配置 GNS3，NX-OSv 操作，NX-OSv 操作，术语表

- 定义，术语表
- IOS-XRv 项目，配置路由器，配置 IOS-XR 设备
- NX-OSv 项目，为 NX-OSv 配置 GNS3，NX-OSv 操作，NX-OSv 操作
- 省略号绘制，第三组工具栏
- 仿真硬件，介绍 GNS3，屏幕布局
- 启用 ghost IOS 支持选项，Dynamips 偏好窗口，配置 Dynamips
- 启用 mmap 支持选项，Dynamips 偏好窗口，配置 Dynamips
- 启用远程控制台选项，VirtualBox，VirtualBox 设置
- 启用稀疏内存支持选项，Dynamips 偏好窗口，配置 Dynamips
- 封装 frame-relay 命令，使用 IOS 创建帧中继交换机
- 终端设备图标，设备栏，第四组工具栏
- 内部路由协议，术语表（参见 EIGRP (增强内部路由协议)）
- `erase flash:` 命令，登录路由器
- 逃逸序列，配置 Cisco 主机
- `/etc/networks/interfaces` 文件，在 Linux 中配置 TAP 适配器
- 以太网适配器，Dynamips 权限，创建突破性连接，连接 GNS3 设备到互联网，解决 NIO 错误
- 连接设备到 PC，Dynamips 权限
- 将 GNS3 设备连接到互联网，连接 GNS3 设备到互联网
- MTU 大小，创建突破性连接
- NIO 问题，解决 NIO 错误
- 以太网连接数据捕获，在 GNS3 中捕获包
- 以太网集线器，节点配置器
- 以太网接口，添加到 Juniper 机器，在 GNS3 中配置 Juniper 路由器
- 以太网交换机节点，登录路由器，登录路由器，更改符号并组织你的设备，Ubuntu Linux TUN/TAP 驱动，创建突破性连接
- 使用突破性连接的配置，创建突破性连接
- 配置 802.1Q 中继，Ubuntu Linux TUN/TAP 驱动
- 节点配置器，登录路由器，更改符号并组织你的设备
- 概述，登录路由器
- EtherSwitch 路由器，EtherSwitch 路由器，Ubuntu Linux TUN/TAP 驱动
- 配置 802.1Q 中继，Ubuntu Linux TUN/TAP 驱动
- EXEC 模式权限，Cisco ASA、IPS 和 IOS-XRv
- `exec-timeout` 参数，登录路由器
- 导出选项，VirtualBox，IOU 设备
- 导出配置选项，将 GNS3 配置导出到路由器，IOU 设备
- 导出，配置 GNS3，登录路由器，问题
- GNS3 配置导出到路由器，登录路由器
- GNS3 设置文件，问题
- IOU 配置，配置 GNS3

### F

- FDISK 分区编辑器，入门
- 功能问题，故障排除，帮助！我摔倒了起不来，修正控制台问题
- 文件传输协议，在 GNS3 中测试 ASA（参见 FTP）
- 防火墙，禁用，VPCS IP 地址（参见 Juniper vSRX Firefly；ASA (自适应安全设备)防火墙）
- flex 包，安装 IOU
- 帧中继交换机节点，帧中继交换机
- `frame-relay intf-type dce` 命令，使用 IOS 创建帧中继交换机
- `frame-relay lmi-type` 命令，使用 IOS 创建帧中继交换机
- `frame-relay switching` 命令，使用 IOS 创建帧中继交换机

# F

FreeBSD，在 Linux 上安装 QEMU，介绍 Juniper，流程概述，在 Linux 中创建 ISO，在 Linux 中创建 ISO，在 Linux 中创建 ISO，Windows 和 OS X 的初步检查，入门指南，完成 FreeBSD 的安装，完成 FreeBSD 的安装

- 获取，流程概述
- 复制到构建目录，在 Linux 中创建 ISO
- 安装，完成 FreeBSD 的安装
- Juniper Olive 软件包，安装在，完成 FreeBSD 的安装
- Juniper Olive，安装在，介绍 Juniper
- 概述，在 Linux 上安装 QEMU
- 分区文件系统，入门指南
- 安装前的初步检查，在 Linux 中创建 ISO
- 创建 QEMU 虚拟机，在 Linux 中创建 ISO
- 创建虚拟硬盘，Windows 和 OS X 的初步检查

FTP (文件传输协议)，获取 IOS 镜像，获取镜像，在 GNS3 中测试 ASA，ASDM 安装，术语表

- 将 ASDM 软件复制到 ASA，在 GNS3 中测试 ASA，ASDM 安装
- 从 Cisco ASA 复制文件，获取镜像
- 将 IOS 镜像文件复制到，获取 IOS 镜像
- 定义，术语表

### G

网关负载均衡协议 (GLBP)，术语表

常规选项窗口，配置问题

通用设置选项卡，配置 Dynamips，VirtualBox 选项，创建许可证文件，配置 GNS3，为 IOU 配置 GNS3，配置客户端

- Dynamips 选项窗口，配置 Dynamips，配置客户端
- UNIX 上的 IOS 选项窗口，创建许可证文件，为 IOU 配置 GNS3
- 节点配置器，配置 GNS3



# VirtualBox 选项窗口

VirtualBox 选项

# Dynamips 的 ghost IOS 支持

配置 Dynamips

# GLBP (网关负载均衡协议)

术语表

# GNS3

- 介绍 GNS3
- 模拟操作系统
- 开源集成
- 安装基础 GNS3 系统
- 安装 GNS3 服务器和 GUI
- 安装 VPCS
- Cisco IOU
- 为 IOU 配置 GNS3
- 备份你的项目
- 兼容 GNS3 的硬件设备
- 安装

## 模拟硬件

介绍 GNS3

## 论坛

安装 VPCS，备份你的项目

## 安装包

安装基础 GNS3 系统

## IOU 的重要性

Cisco IOU

## 限制性

开源集成

## 开源集成

开源集成

## 概述

介绍 GNS3

## 使用原因

介绍 GNS3

## 可扩展性

模拟操作系统

## 模拟操作系统

介绍 GNS3

## 兼容 GNS3 的硬件

`apb.html_iddle1421`

## 升级

为 IOU 配置 GNS3

## 虚拟连接

模拟操作系统

## 网站

备份你的项目

# GNS3 IOU .ova 文件

在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机

# GNS3 Jungle 论坛

备份你的项目

# GNS3 服务器选项窗口

为 IOU 配置 GNS3，运行 `gns3server`

# GNS3 设置文件

配置问题

# GNS3 工具栏

项目管理，使用 GNS3 工具栏

# GNS3 Vault 网站

GNS3 WorkBench

# GNS3 WorkBench

- 优点与缺点
- 安装

## 概述

优点与缺点

# `gns3server` 程序

Dynamips 客户端/服务器设置，配置客户端

# 宽限期

EIGRP，NX-OSv 实战

# 图形用户界面 (GUI) 程序

模拟操作系统，安装 Dynamips

# GRUB 启动管理器

QEMU，破解硬件

# GRUB 启动菜单

Linux，创建支持 QEMU 的 IDS/IPS 系统

# GUI (图形用户界面) 程序

模拟操作系统，安装 Dynamips

# H

## “破解我的”挑战

创建 GNS3 Uberlab

## `halt` 命令

让你的 Olive 运行起来

## 硬盘设置

NX-OSv，将 NX-OSv 导入 VirtualBox

## 硬件

介绍 GNS3，屏幕布局，创建路由器之间的连接，配置接入服务器路由器，终极方案

（另见设备；特定硬件）

### 配置路由器

创建路由器之间的连接

### 模拟

介绍 GNS3，屏幕布局

### 故障排除

终极方案

## `hdiutil` 命令

在 Windows 中创建 ISO

## `help` 命令

探索 GNS3 控制台

## 主机绑定

GNS3 服务器，在 Linux 中配置 TAP 适配器，运行 `gns3server`

## 主机集成

模拟操作系统，主机集成与使用 Wireshark

（另见 VirtualBox）

### 概述

主机集成与使用 Wireshark

### 带有虚拟 PC 模拟器

主机集成与使用 Wireshark

## `hostname` 命令

创建许可证文件

## 热链接 IOU 设备

配置 GNS3

## HSRP (热备用路由协议)

术语表

## 星型拓扑帧链路网络

帧链路交换机

## 虚拟机监控程序

安装在 Microsoft Windows（见 Dynamips）

# I

## I/O (输入/输出)

术语表

## ICS (Internet 连接共享)

将 GNS3 设备连接到互联网

## Idle-PC 值

在 GNS3 中添加 IOS 镜像，配置客户端，修复控制台问题，节省资源

### 节省资源

节省资源

### 控制台问题

修复控制台问题

### 概述

在 GNS3 中添加 IOS 镜像，配置客户端

### 手动设置

在 GNS3 中添加 IOS 镜像

## Idlemax 设置

Dynamips，修复控制台问题

## Idlesleep 设置

Dynamips，修复控制台问题

## IDS/IPS (入侵检测系统/入侵防御系统)

Cisco ASA，IDS/IPS 和 IOS-XRv，ASDM 安装，创建一个支持 QEMU 的 IDS/IPS 系统，硬件劫持，为 IDS/IPS 配置 GNS3，在 GNS3 中验证 IDS/IPS，术语表

### 获取镜像文件

ASDM 安装

### 磁盘镜像文件的备份

在 GNS3 中验证 IDS/IPS

### 启动

ASDM 安装

### 为...配置 GNS3

硬件劫持

### 定义

术语表

### 概述

Cisco ASA，IDS/IPS 和 IOS-XRv，ASDM 安装

### 创建支持 QEMU 的系统

ASDM 安装

### 重启

硬件劫持

### 测试

硬件劫持

### 欺骗软件

创建一个支持 QEMU 的 IDS/IPS 系统

### 在 GNS3 中验证

为 IDS/IPS 配置 GNS3

## `ids_functions` 文件

创建一个支持 QEMU 的 IDS/IPS 系统

## `ifconfig` 命令

在项目中使用 VirtualBox 主机，OS X 上的 TUN/TAP 驱动，在 Linux 中配置 TAP 适配器

## `ifconfig eth0` 命令

上传 IOU 镜像文件

## 镜像

配置，第三工具栏组，流程概述，获取镜像，ASDM 安装，在 GNS3 中验证 IDS/IPS，IOU 镜像，配置 GNS3，将 GNS3 IOU 虚拟机导入 VirtualBox，为 IOU 配置 GNS3，NX-OSv（见 IOS 镜像）

### ASA 操作系统

获取镜像

### Cisco IOS-XRv 文件

在 GNS3 中验证 IDS/IPS

### IDS/IPS 获取

ASDM 安装

### 插入

第三工具栏组

### IOU

IOU 镜像，配置 GNS3，将 GNS3 IOU 虚拟机导入 VirtualBox，为 IOU 配置 GNS3

### ISO

流程概述，ASDM 安装

### NX-OSv

NX-OSv

### 导入设备到 VirtualBox

带有 IOU 设备

### 导入选项

将 GNS3 配置到 Cisco 路由器

### 导入虚拟设备

在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机

### 导入/导出对话

将 GNS3 配置到 Cisco 路由器

### 导入

在 Windows 上安装，配置 GNS3，NX-OSv，将 GNS3 配置到 Cisco 路由器，配置问题

### 设备到 VirtualBox

在 Windows 上安装

### Cisco 路由器配置到 GNS3

将 GNS3 配置到 Cisco 路由器

### GNS3 设置

配置问题

### IOU 配置

配置 GNS3

### NX-OSv 导入 VirtualBox

NX-OSv

## INE 教程

创建 GNS3 Uberlab

## Inipser 程序

安装 IOU

## RAM 磁盘

ASA 虚拟机，为 ASA 配置 GNS3

## 输入/输出 (I/O)

术语表

## 插入图标

GNS3 工具栏，第三工具栏组

## 安装启动管理器菜单

分区系统

## 安装媒体选择

完成 FreeBSD 安装

## Juniper 安装包

让你的 Olive 运行起来

## 安装

安装基础 GNS3 系统，通用要求，在 Microsoft Windows 上安装，在 OS X 上安装，安装 GNS3 服务器和 GUI，安装 VPCS，VPCS IP 地址，使用 Linux 虚拟机的简单 VirtualBox 项目，Juniper Olive 和 VSRX Firefly，介绍 Juniper，完成 FreeBSD 安装，OS X 上的 TUN/TAP 驱动，Ubuntu Linux 上的 TUN/TAP 驱动，项目配置，在 GNS3 中验证 IDS/IPS，ASDM 安装，在 Linux PC 上设置 IOU，从访问器管理设备

### CCP 软件

项目配置

### Cisco ASDM

在 GNS3 中验证 IDS/IPS

### Cisco IDS/IPS

ASDM 安装

### FreeBSD

完成 FreeBSD 安装

### GNS3 设备

安装 GNS3 服务器和 GUI

### GNS3 在 Windows 上

通用要求

### GNS3 在 OS X 上

在 Microsoft Windows 上安装

### GNS3 在 Ubuntu Linux 上

在 OS X 上安装

### GNS3 通用要求

通用要求

### GNS3 概述

安装基础 GNS3 系统

### IOU

在 Linux PC 上设置 IOU

### Juniper Olive

介绍 Juniper

### FreeBSD 中的 Juniper Olive 包

完成 FreeBSD 安装

### QEMU

Juniper Olive 和 VSRX Firefly

### TUN/TAP 驱动

OS X 上的 TUN/TAP 驱动，Ubuntu Linux 上的 TUN/TAP 驱动

### 虚拟访问服务器的虚拟接口

从访问器管理设备

## VirtualBox

VPCS IP 地址

## Wireshark

使用 Linux 虚拟机的简单 VirtualBox 项目

# 集成路由器 (ISR)

术语表

# 集成主机

模拟操作系统，主机集成与使用 Wireshark

（另见 VirtualBox）

## 概述

主机集成与使用 Wireshark

## 使用 Virtual PC 模拟器

主机集成与使用 Wireshark

# 交换机链路 (ISL)

Cisco，术语表

# 接口标签

使用 GNS3 工具栏

# 虚拟接口

用于虚拟接入服务器，从接入服务器管理设备

# `interface-nat` 命令

创建基于区域的防火墙项目

# `interface.conf` 文件

创建适用于 QEMU 的 IDS/IPS 系统，劫持硬件

# `interfaces` 文件

在 Linux 中配置 TAP 适配器

# Internet

获取 IOS 镜像，将 GNS3 设备连接到 Internet

## 连接设备到

将 GNS3 设备连接到 Internet

## 在查找 IOS 文件

获取 IOS 镜像

# Internet 连接共享 (ICS)

将 GNS3 设备连接到 Internet

# 网际协议 (IP)

在 Linux 中配置 TAP 适配器（见 IP；IPv4；IPv6）

# 网络服务提供商 (ISP)

术语表

# 网络操作系统

介绍 GNS3（见 IOS (网络操作系统)）

# 入侵检测系统/入侵防御系统 (IDS/IPS)

ASDM 安装（见 IDS/IPS (入侵检测系统/入侵防御系统)）

# IOL (Linux on IOS)

术语表

# IOS (网络操作系统)

Cisco，介绍 GNS3，支持的 Cisco 硬件，术语表

（另见 IOS 镜像；IOS 路由器；IOU）

# IOS 镜像

开源集成，配置，获取 IOS 镜像，配置 Dynamips，更改符号并组织设备，在平台间拷贝 GNS3 项目，Dynamips 客户端/服务器设置，识别问题，当 IOS 镜像加载失败时，配置问题

## 获取

配置

## 添加到 GNS3

配置 Dynamips

## 客户端/服务器设置

Dynamips 客户端/服务器设置

## 从路由器拷贝

获取 IOS 镜像

## 在平台间拷贝 GNS3 项目

在平台间拷贝 GNS3 项目

## 损坏

当 IOS 镜像加载失败时

## 解压缩

配置 Dynamips

## 加载失败故障排除

识别问题

## 局限性

开源集成

## 串口连接故障排除

更改符号并组织设备

## 稳定版本

获取 IOS 镜像

## 不支持

配置问题

# IOS 内存屏幕

将 IOS 镜像添加到 GNS3

# IOS on Linux

术语表

# IOS on Unix

介绍 GNS3（见 IOU (IOS on Unix)）

# IOS on UNIX 窗口

配置 IOU

# IOS 路由器

安装到 Windows，获取 IOS 镜像，配置 Dynamips，将 IOS 镜像添加到 GNS3，创建项目，将 VirtualBox 连接到设备，使用 IOS 创建交换链路，配置 GNS3，识别问题，当 IOS 镜像加载失败时

（另见 Dynamips）

## 将 IOS 镜像添加到 GNS3

配置 Dynamips

## 客户端/服务器设置

配置 GNS3

## 配置

创建第一个项目

## Dynamips 配置

获取 IOS 镜像

## 交换链路创建

使用 IOS

## Idle-PC 值手动设置

将 IOS 镜像添加到 GNS3

## 内存故障排除

识别问题，当 IOS 镜像加载失败时

## 将 VirtualBox 网络连接到

将 VirtualBox 连接到设备

## 首选项

配置 Dynamips

# IOS 路由器首选项

配置 GNS3

# IOS-XRv

Cisco，在 GNS3 中验证 IDS/IPS，配置 GNS3 使用 IOS-XRv，配置路由器

## 适配器用于

配置 GNS3 使用 IOS-XRv

## 配置 GNS3 用于

在 GNS3 中验证 IDS/IPS

## 配置 IOS-XR 设备

配置路由器

## 配置路由器

配置路由器

## 创建简单项目

配置 GNS3 使用 IOS-XRv

# IOU (Unix 上的 IOS)

Cisco

- GNS3 简介
- 模拟操作系统
- 有限仿真
- Unix 上的 Cisco IOS 和 NX-OSv
- Cisco IOU
- IOU 镜像
- 在 Linux PC 上设置 IOU
- 安装 IOU
- 创建许可证文件
- 配置 GNS3
- 在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机
- 将 GNS3 IOU 虚拟机导入 VirtualBox
- 上传 IOU 镜像文件
- 为 IOU 配置 GNS3
- 将 GNS3 配置导出到 Cisco 路由器
- 在平台间复制 GNS3 项目
- 解决 NIO 错误
- 修正控制台问题
- Cisco IOU L2 镜像中不支持的功能
- 术语表

## 配置设备

配置 GNS3

## 为 GNS3 配置

创建许可证文件，上传 IOU 镜像文件

## 控制台问题

修正控制台问题

## 在平台间复制 GNS3 项目

在平台间复制 GNS3 项目

## 创建配置文本文件

将 GNS3 配置导出到 Cisco 路由器

## 定义

术语表

## 导出/导入配置

配置 GNS3

## 镜像

IOU 镜像，将 GNS3 IOU 虚拟机导入 VirtualBox，为 IOU 配置 GNS3

## 对 GNS3 的重要性

Cisco IOU

## 安装

在 Linux PC 上设置 IOU

## L2 镜像

Cisco IOU L2 镜像中不支持的功能

## 许可证文件

安装 IOU，上传 IOU 镜像文件

## 连接设备

配置 GNS3

## NIO 问题

解决 NIO 错误

## 在 Linux PC 上

IOU 镜像

## 在 Windows 和 OS X 上

在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机

## 概述

Unix 上的 Cisco IOS 和 NX-OSv

## 简单项目

为 IOU 配置 GNS3

## 交换机

Cisco IOU，为 IOU 配置 GNS3

## 安装注意事项

IOU 镜像

## 上传镜像文件

将 GNS3 IOU 虚拟机导入 VirtualBox

## 虚拟机用于

IOU 镜像，在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机，为 IOU 配置 GNS3

# IOU 设备部分



IOU 设备部分，Unix 上的 IOS 好，配置 GNS3，为 IOU 配置 GNS3，为 IOU 配置 GNS3

## IOU 应用

IOU 应用，安装 IOU

## IP（互联网协议）

IP（互联网协议），VPCS 命令，在项目中使用 VirtualBox 主机，配置路由器，配置 IOS-XR 设备，上传 IOU 镜像文件，为 IOU 配置 GNS3，IOU 实战，NX-OSv 实战，从接入服务器管理设备，在 Windows 上配置环回适配器，在 Linux 上配置 TAP 适配器，配置 Cisco IP 主机表，Dynamips 客户端/服务器设置，运行 `gns3server`

## 将 GNS3 服务器绑定到虚拟接口

将 GNS3 服务器绑定到虚拟接口，在 Linux 上配置 TAP 适配器

## 客户端/服务器设置

客户端/服务器设置，Dynamips 客户端/服务器设置，运行 `gns3server`

## 在 VirtualBox 中配置

在 VirtualBox 中配置，在项目中使用 VirtualBox 主机

## 在 Windows 上配置环回适配器

在 Windows 上配置环回适配器，从接入服务器管理设备

## 在 Linux 上配置 TAP 适配器

在 Linux 上配置 TAP 适配器，在 Windows 上配置环回适配器

## NX-OSv 项目

对于 NX-OSv 项目，NX-OSv 实战

## IOS-XRv 项目

IOS-XRv 项目，配置路由器，配置 IOS-XR 设备

## IOU 虚拟机

IOU 虚拟机，上传 IOU 镜像文件，为 IOU 配置 GNS3

## 虚拟接入服务器

虚拟接入服务器，从接入服务器管理设备，配置 Cisco IP 主机表

## 使用 IOU 交换机进行 VLAN 路由

使用 IOU 交换机进行 VLAN 路由，IOU 实战

## VPCS

VPCS，VPCS 命令

## 在 VirtualBox 中配置

在 VirtualBox 中配置，在项目中使用 VirtualBox 主机

## 术语表

术语表，术语表

## IP 命令

IP 命令，VPCS 命令

## 虚拟接入服务器 IP 主机表

虚拟接入服务器 IP 主机表，配置路由器

## IP 状态命令

IP 状态命令，劫持硬件

## IPv4（互联网协议第 4）

IPv4（互联网协议第 4），VPCS 命令，术语表

## 在 VPCS 中手动配置地址

在 VPCS 中手动配置地址，VPCS 命令

## IPv6（互联网协议第 6）

IPv6（互联网协议第 6），VPCS 命令，术语表

## ISL（交换机链路）

ISL（交换机链路），Cisco，术语表

## ISO 镜像

ISO 镜像，概述，ASDM 安装

## IDS/IPS

IDS/IPS，获取，ASDM 安装

# ISO 记录器，过程概述

ISP（互联网服务提供商），术语表

ISR（集成服务路由器），术语表

## J

Java，项目配置

Juniper 网络认证助理 (JNCIA) 认证，在 Linux 上安装 QEMU，创建基于防火墙的项目，术语表

Juniper Olive，Juniper Olive 与 VSRX Firefly，在 Linux 上安装 QEMU，简介 Juniper，过程概述，在 Linux 中创建 ISO，Windows 和 OS X 的初步检查，入门指南，完成 FreeBSD 安装，让你的 Olive 运行，备份 Juniper Olive，在 GNS3 中配置 Juniper 路由器，添加以太接口，测试 Juniper 路由器，为你的虚拟机分配更多处理器

（另见 Juniper vSRX Firefly）

获取 FreeBSD，过程概述

获取软件，过程概述

在 GNS3 中添加虚拟机，在 GNS3 中配置 Juniper 路由器

备份，让你的 Olive 运行

在 GNS3 中配置 Juniper 路由器，备份 Juniper Olive

创建 CD 镜像文件，过程概述

在 QEMU 中创建虚拟硬盘，Windows 和 OS X 的初步检查

通用讨论，在 Linux 上安装 QEMU

安装，简介 Juniper

安装 FreeBSD，完成 FreeBSD 安装

在 FreeBSD 中安装包，完成 FreeBSD 安装

安装 QEMU，Juniper Olive 与 VSRX Firefly

概述，Juniper Olive 与 VSRX Firefly

在 QEMU 中划分文件系统，入门指南

FreeBSD 安装前的初步检查，在 Linux 中创建 ISO

语法，测试 Juniper 路由器

系统要求，简介 Juniper

测试路由器，添加以太接口

Juniper vMX，简介 Juniper

Juniper vSRX Firefly，测试 Juniper 路由器，运行 Juniper vSRX Firefly，为你的虚拟机分配更多处理器，将 vSRX Firefly 添加 GNS3

将虚拟机添加到 GNS3，为你的虚拟机分配更多处理器

使用 VirtualBox 创建 Firefly 虚拟机，运行 Juniper vSRX Firefly

提取并转换文件，运行 Juniper vSRX Firefly

增加虚拟机的处理器，为你的虚拟机分配更多处理器

概述，测试 Juniper 路由器

项目使用，将 vSRX Firefly 添加到 GNS3

Juniper 兼容分区，划分文件系统

`juniper-olive.iso` CD 镜像，挂载，完成 FreeBSD 安装

Junos OS，在 Linux 上安装 QEMU

## K

FreeBSD 内核配置，Windows 和 OS X 的初步检查，入门指南

内核镜像，ASA 虚拟机，为 ASA 配置 GNS3

## L

L2 镜像，Cisco IOU，Cisco IOU L2 不支持的功能

`l2protocol-tunnel cdp` 命令，创建突破交换机

LAN（局域网），术语表

层，操作，第四工具栏

`lib2`，解决 IOS 错误

`libcrypto`，设置 IOU

IOU 许可证文件，安装 IOU

许可证期限，NX-OS 实战

链接，第四工具栏

`linux`，与路由器工作

IOU 设备，第四工具栏

路由器，与路由器工作

VirtualBox 主机，使用 VirtualBox

VirtualBox，导入 NX-OSv

- CPU 使用率，设置 Idle-PC 值，向 GNS3 添加 IOS 镜像
- Dynamips 权限，设置，Dynamips 权限
- GNS3 WorkBench，一些优缺点
- `gns3server` 程序，Dynamips 客户端/服务器设置
- 安装 `cpulimit` 程序，为 ASA 配置 GNS3
- 在...上安装 GNS3 节点，在 OS X 上安装
- 安装 IOU，在 Linux PC 上设置 IOU
- 在...上安装 QEMU，在 Windows 和 OS X 上安装 QEMU
- 安装 VirtualBox，在 Windows 上安装
- 安装 VPCS 源文件，安装 VPCS
- 在...上安装 Wireshark，在 OS X 上安装
- Juniper Olive ISO 镜像制作，在 Windows 中创建 ISO
- IOU 许可证文件，安装 IOU
- NIO 连接，云节点
- 权限问题，解决 IOS 内存错误
- 为 GNS3 准备 ASA 镜像，获取镜像
- 在...上运行 GNS3 和 IOU，IOU 镜像
- Ubuntu Linux TUN/TAP 驱动，Ubuntu Linux TUN/TAP 驱动
- 验证 Dynamips 路径，获取 IOS 镜像
- 虚拟访问服务器限制，在...上，配置 Cisco IP 主机表
- VirtualBox 虚拟机项目，将 VirtualBox 主机节点到其他设备
- 实时交换机，连接设备到...，Ubuntu Linux TUN/TAP 驱动，配置标准 802.1Q Trunk 干链路，创建难以发现的跳出交换机，在 PC 中使用多个适配器，创建一个简单的网络
- 可选跳出交换机配置，创建难以发现的跳出交换机
- 概述，Ubuntu Linux TUN/TAP 驱动，创建一个简单的网络
- 在 PC 中使用多个适配器，在 PC 中使用多个适配器
- 使用跳出交换机，配置标准 802.1Q Trunk 干链路
- 使用标准 802.1Q Trunk 干链路，Ubuntu Linux TUN/TAP 驱动
- LMI（逻辑管理接口），术语表
- 所有可用远程服务器的负载均衡复选框，新 IOS 路由器对话框，配置客户端
- 局域网 (LAN)，术语表
- 登录路由器，配置虚拟硬件，登录路由器
- 逻辑管理接口 (LMI)，术语表
- 环回适配器驱动，Microsoft，Dynamips 权限，将 GNS3 设备连接到互联网，从访问服务器管理设备，在 GNS3 中创建虚拟访问服务器，配置云节点

### M

- MAC（介质访问），术语表
- OS X，向 GNS3 添加 IOS 镜像（参见 OS X）
- 管理设备屏幕，CCP，项目配置
- 管理控制台，GNS3，屏幕布局，带有 IOU 设备的项目
- 手动 Idle-PC 值，设置，向 GNS3 添加 IOS 镜像
- 在 VPCS 中手动配置 IP 地址，VPCS 命令
- 最大传输单元 (MTU)，术语表
- 介质访问 (MAC)，术语表
- 内存，通用要求，配置 Dynamips，向 GNS3 添加 IOS 镜像，为 ASA 配置 GNS3，为 IDS/IPS 配置 GNS3，为 IOS-XRv 配置 GNS3，将 GNS3 IOU 虚拟机导入 VirtualBox，NX-OSv，识别问题，IOS 镜像加载失败，解决控制台问题，节省资源
- Dynamips，配置 Dynamips
- 通用要求，通用要求
- IOS 路由器，向 GNS3 添加 IOS 镜像
- IOU 虚拟机，将 GNS3 IOU 虚拟机导入 VirtualBox
- NX-OSv，ch09.html_iddle1786
- QEMU 虚拟机，为 ASA 配置 GNS3，为 IDS/IPS 配置 GNS3，为 IOS-XRv 配置 GNS3，解决控制台问题
- 路由器，识别问题，IOS 镜像加载失败
- 内存设置，Dynamips 偏好，配置 Dynamips
- Microsoft 环回适配器驱动，Dynamips 权限，将 GNS3 设备连接到互联网，从访问服务器管理设备，在 GNS3 中创建虚拟访问服务器，配置云节点
- Microsoft Windows，通用要求，向 GNS3 添加 IOS 镜像，VPCS IP 址，在项目中使用 VirtualBox 主机，使用 Linux 虚拟机的 VirtualBox 项目，Juniper Olive 和 VSRX Firefly，流程概述，Dynamips 权限，将 GNS3 设备连接到互联网，Cisco ASA，IDS/IPS，和 IOS-XRv，在 GNS3 中测试 ASA，ASDM 安装，创建支持 QEMU 的 IDS/IPS 系统，IOU 镜像，在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机，从访问服务器管理设备，在 GNS3 中创建虚拟访问服务器，配置 Cisco IP 主机表，Dynamips 客户端/服务器设置，解决 IOS 内存错误，解决 NIO 错误
- CCP 项目配置，Cisco ASA，IDS/IPS，和 IOS-XRv
- Cisco ASDM，在 GNS3 中测试 ASA
- 配置云节点，在 GNS3 中创建虚拟访问服务器
- 在 VirtualBox 中配置 IP 地址，在项目中使用 VirtualBox 主机
- 在...中配置环回适配器，从访问服务器管理设备
- 连接设备到互联网，将 GNS3 设备连接到互联网
- CPU 使用率，设置 Idle-PC 值，向 GNS3 添加 IOS 镜像
- `gns3server` 程序，Dynamips 客户端/服务器设置
- 在...上安装 GNS3 节点，通用要求
- 在...上安装 QEMU，Juniper Olive 和 VSRX Firefly
- 在...上安装 VirtualBox，VPCS IP 址
- 在...上安装 Wireshark，使用 Linux 虚拟机的 VirtualBox 项目
- IOU 上，IOU 镜像，在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机
- Juniper Olive ISO 镜像创建，流程概述
- 环回环适配器驱动程序，Dynamips 权限
- NIO 问题，解决 IOS 内存错误，解决 NIO 错误
- QEMU 就绪 IDS/IPS 系统，ASDM 安装，创建 QEMU 就绪 IDS/IPS 系统
- 虚拟接入服务器限制在，配置 Cisco IP 主机主机表
- `mkisofs` 应用程序，在 Windows 中创建 ISO
- `mmap` 支持，Dynamips，配置 Dynamips
- `modprobe` 命令，创建难以捉摸的逃逸交换机
- `mount` 命令，完成 FreeBSD 安装
- MPLS（多协议标签交换），词汇表
- MTU（最大传输单元），OS X 上的 TUN/TAP 驱动，创建难以捉摸的逃逸交换机，词汇表
- 定义，词汇表
- 以太网适配器，创建难以捉摸的逃逸交换机
- 接口，OS X TUN/TAP 驱动
- 多协议路由，故障排除，更改符号并组织你的设备
- 多厂商集成，"黑客入侵机架"挑战
- 多宿主网络，"黑客入侵机架"挑战
- PC 中的多个适配器，用于设备连接，在你的 PC 中使用多个适配器
- 多个 PC，运行设备使用，探索 GNS3 控制台，Dynamips 客户端/服务器设置，配置客户端
- 客户端/服务器设置，Dynamips 客户端/服务器设置
- 概览，探索 GNS3 控制台
- uberlab 创建，配置客户端
- 多协议标签交换 (MPLS)，词汇表

### N

- NAT（网络地址转换），创建简单的网络，词汇表
- `netstat` 命令，登录路由器，解决端口冲突
- 网络适配器，桥接到 PC，将 GNS3 IOU 虚拟机导入 VirtualBox
- 网络适配器屏幕，向 GNS3 添加 IOS 镜像
- 网络地址转换 (NAT)，创建简单的网络，词汇表
- 网络连接性测试，ASA，配置 GNS3 以运行 ASA
- 网络收敛测试，在...中挂起路由器，配置虚拟硬件
- 网络输入/输出 (NIO)，云节点（参见 NIO）
- 网络性能，在 GNS3 中使用，有限仿真
- 网络处理引擎 (NPE)，Cisco，配置虚拟硬件，词汇表
- 网络设置，VirtualBox，VirtualBox 虚拟机设置
- 网络交换机模块，登录路由器
- 网络标签页，节点配置器，配置 GNS3
- 新建空白项目图标，GNS3 工具栏，使用 GNS3 工具栏



# 新 IOS 路由器对话框，配置客户端

# 新 IOU 设备向导，配置 GNS3, 配置 GNS3 以运行 IOU, 再次配置 GNS3 以运行 IOU

# 新项目窗口，创建你的第一个项目

# 新 QEMU 虚拟机，在 GNS3 中配置 Juniper, 配置 GNS3 以运行 ASA, 配置 GNS3 以运行 IOU, 在 GNS3 中验证 IDS/IPS

# 新 VirtualBox 虚拟机，VirtualBox 设置

# NIO (网络输入/输出)，云节点, 解决 IOS 内存错误

# NIO 错误，云节点, 词汇表

# NIO 标签页，节点配置器，在 GNS3 中配置访问服务器, 配置 GNS3 以运行 IOU

# NIO 标签页，节点配置器，在 GNS3 中运行 IOU

# 云节点

# NM-16ESW 交换机，在 GNS3 中运行 IOU

# NM-16ESW 交换机，在 GNS3 中运行 运行在 GNS3 中配置 Juniper

# NM-16ESW 交换机，在 GNS3 中运行 IOU 运行在 VirtualBox 中

`no shutdown` 命令，登录路由器

# 节点配置器，在 GNS3 中配置访问服务器

# 非易失性内存 (NVRAM)，词汇表

# 非易失性内存 (NVRAM)，词汇表

# NPE (网络处理引擎)，Cisco，配置虚拟硬件, 词汇表

# NX-OSv，Cisco，在 GNS3 中运行 IOU, NX-OSv

# NX-OSv，Cisco，在 GNS3 中运行 IOU

# NX-OSv，Cisco，在 GNS3 中运行 IOU

# NX-OSv，Cisco，在 GNS3 中运行 IOU

# 操作系统 (OSes), 介绍 GNS3, 在平台之间复制 GNS3 项目, 在平台之间复制 GNS3 项目, 术语表

(另参见特定的操作系统)

# 在平台之间复制 GNS3 项目，在平台之间复制 GNS3 项目

# 定义，术语表

# 模拟的，介绍 GNS3

# OS X, 在 Microsoft Windows 上安装, 向 GNS3 添加 IOS 镜像, 在 Windows 上安装, 在 OS X 上安装, Juniper Olive 和 VSRX Firefly, 在 Windows 中创建 ISO, 在 Linux 中创建 ISO, 云节点, OS X 上的 TUN/TAP 驱动程序, ASDM 安装, IOU 镜像, 在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机, Dynamips 客户端/服务器设置, 解决 IOS 内存错误

# CPU 使用，设置 Idle-PC 值，向 GNS3 添加 IOS 镜像

# 设置 Dynamips 权限，云节点

`gns3server` 程序，Dynamips 客户端/服务器设置

# 在...安装 GNS3 系统，在 Microsoft Windows 上安装

# 在...安装 QEMU，Juniper Olive 和 VSRX Firefly

# 安装 TUN/TAP 驱动程序，OS X 上的 TUN/TAP 驱动程序

# 在...上安装 VirtualBox，在 Windows 上安装

# 在...上安装 Wireshark，在 OS X 上安装

# 在...上运行 IOU，IOU 镜像, 在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机

# 创建 Juniper Olive ISO 镜像，在 Windows 中创建 ISO

# NIO 问题，解决 IOS 内存错误

# FreeBSD 安装前的初步检查，在 Linux 中创建 ISO

# QEMU 就绪 IDS/IPS 系统，ASDM 安装

# OSPF (开放最短路径优先)，术语表

# OVA (开放虚拟设备)文件，在 Windows 上安装, 运行 Juniper vSRX Firefly, 在 GNS3 中验证 IDS/IPS, 在 Windows 和 OS X 上使用 GNS3 IOU 虚拟机, 带有 IOU 设备的项目, 术语表

## P

# SONET 传输数据包 (POS)，术语表

# 数据包嗅探器，使用 Linux 虚拟机的简单 VirtualBox 项目

(另参见 Wireshark)

# 在 QEMU 中划分文件系统，入门指南

# UNIX IOS 偏好窗口中 `IOURC` 字段路径，创建许可证文件, 为 IOU 配置 GNS3

# UNIX IOS 偏好窗口中 `iouyap` 字段路径，创建许可证文件

# 暂停路由器，配置虚拟硬件

# 集成 PC 主，模拟操作系统, 集成主机并使用 Wireshark, 集成主机并使用 Wireshark

(另参见 VirtualBox)

# 概述，集成主机并使用 Wireshark

# 带有 Virtual PC 模拟器，集成主机并使用 Wireshark

`.pcap` 捕获文件，在 Linux PC 上设置 IOU

# 连接到...PC，云节点

# 运行多个设备的 PC，探索 GNS3 控制台, Dynamips 客户端/服务器设置, 配置客户端

# 客户端/服务器设置，Dynamips 客户端/服务器设置

# 概述，探索 GNS3 控制台

# uberlab，配置客户端

# 永久虚拟电路 (PVC)，帧中继交换, 使用 IOS 创建帧中继, 术语表

# 权限，云节点, 解决 IOS 内存错误

# 以及 NIO 错误，解决 IOS 内存错误

# 设置，云节点

# 连接到...物理硬件，云节点

(另参见硬件)

# 项目中的图片，第三个工具栏

`ping` 命令，VPCS IP 地址, 测试 Juniper 路由器, 项目配置, 为 ASA 配置 GNS3, 配置 IOS-XR 设备, IOU 实践, NX-OSv 实践, NX-OSv 实践, 配置接入服务器路由器

# ASA，为 ASA 配置 GNS3

# IOS-XR 设备，配置 IOS-XR 设备

# Juniper 路由器连接性，测试 Juniper 路由器

# NX-OSv 项目，NX-OSv 实践, NX-OSv 实践

# 虚拟接入服务器，配置接入服务器路由器

# VLAN 路由，VPCS IP 地址, IOU 实践

# Windows 访客和路由器之间的连接，项目配置

# 平台，在平台之间复制 GNS3 项目 (另参见操作系统 (OSes);特定的操作系统)

# 使用 ATM 交换机的点对点 WAN 连接，ATM 交换机

# 端口号，登录路由器, 终极方案

# 更改，登录路由器

# 冲突，故障，终极方案

# POS (SONET 传输数据包)，术语表

# 私有配置文件，创建第一个项目, 将 GNS3 配置导出到 Cisco 路由器

# 优先级设置，QEMU 虚拟机偏好窗口，为 ASA 配置 GNS3

# 处理器，为 Firefly 虚拟机增加处理器，给你的虚拟机处理器

# 项目管理，创建和管理项目, 项目管理概述, 项目管理概述, 项目管理概述, 使用 GNS3 工具栏, 第四个工具组, 第四个工具组, 创建第一个项目, 与路由器工作, 在你的路由器之间创建链接, 配置虚拟硬件, 配置虚拟硬件, 登录路由器, 登录路由器, 登录路由器, 更改符号并组织你的设备, 为 IOU 配置 GNS3

# 添加路由器，创建第一个项目

# 设备工具栏，第四个工具组

# 以太网交换机节点，登录路由器

# GNS3 工具栏，使用 GNS3 工具栏

# IOU 实践，IOU 实践

## 登录路由器，配置虚拟硬件, 登录路由器

## 新项目，创建，第四组工具组

## 概述，创建和管理项目

## 屏幕布局，项目管理概述

## 快照，项目管理概述

## 启动、停止和暂停路由器，配置虚拟硬件

## 设备符号，更改，更改符号和组织您的设备

## 终端设置，配置，登录路由器

## 术语，项目管理概述

## 虚拟硬件，配置，在路由器之间建立链接

## 项目，项目管理概述, VirtualBox 虚拟机设置, 将 VirtualBox 宿主机节点到其他设备, 在 GNS3 中添加 vSRX Firefly, Cisco ASA, IDS/IPS 和 IOS-XRv, 为 NX-OSv 配置 GNS3, 在平台之间复制 GNS3 项目, “破解我的机架”挑战, 节省资源

## 备份，节省资源

## Cisco NX-OSv，为 NX-OSv 配置 GNS3

## CCP 软件中的配置，Cisco ASA, IDS/IPS 和 IOS-XRv

## 在平台之间复制，在平台之间复制 GNS3 项目

## 定义，项目管理概述

## 练习真实场景，“破解我的机架”挑战

## 使用 Juniper vSRX Firefly，在 GNS3 中添加 vSRX Firefly

## 在中使用 VirtualBox 宿主机，VirtualBox 虚拟机设置

## 在 Linux 上使用 VirtualBox，将 VirtualBox 宿主机节点到其他设备

## PuTTY，通用要求

## PVC（永久虚拟电路），帧中继机, 使用 IOS 创建帧中继机, 术语表

### Q

## QEMU（快速模拟器），模拟操作系统, 开源集成, 通用要求, Juniper Olive 和 VSRX Firefly, Juniper Olive 和 VSRX Firefly, 过程概述, 在 Linux 中创建 ISO, 在 Linux 中创建 ISO, 在 Linux 中创建 ISO, Windows 和 OS 的初步检查, 入门, 入门, 在 GNS3 中配置 Juniper 路由器, 在 GNS3 中配置 Juniper 路由器, 在 GNS3 中配置 Juniper 路由器, 创建基于区域防火墙的项目, 获取镜像, 获取镜像, ASDM 安装, 在 GNS3 中验证 IDS/IPS, 在 GNS3 中验证 IDS/IPS, 控制台问题, 术语表

## ASA 镜像，准备，获取镜像

## 磁盘备份，在 GNS3 中验证 IDS/IPS

## 二进制应用程序，在 GNS3 中配置 Juniper 路由器

## 构建目录，准备，在 Linux 中创建 ISO

## 为 ASA 配置 GNS3，获取镜像

## 为 IOS-XRv 配置 GNS3，在 GNS3 中验证 IDS/IPS

## 控制台问题，控制台问题

## 定义，术语表

## 以太网接口，添加到 Juniper 虚拟机，在 GNS3 中配置 Juniper 路由器

## FreeBSD，安装，过程概述

## IDS/IPS 系统准备，创建，ASDM 安装

## 安装，Juniper Olive 和 VSRX Firefly

## Juniper 虚拟机，添加到 GNS3，在 GNS3 中配置 Juniper 路由器

## Juniper，运行，创建基于区域防火墙的项目

## 概述，开源集成, Juniper Olive 和 VSRX Firefly

## 分区文件系统，入门

## 前检查，在 Linux 中创建 ISO

## 虚拟硬盘，创建，Windows 和 OS 的初步检查

## FreeBSD 虚拟机，创建，在 Linux 中创建 ISO

## qemu 程序，在 Linux 中创建 ISO

## QEMU VM 窗口，备份 Olive, 获取镜像, 为 ASA 配置 GNS3, 破解硬件, 在 GNS3 中验证 IDS/IPS

## qemu-img 程序，在 Linux 中创建 ISO, Windows 和 OS 的初步检查

## qemu-system-i386 二进制应用程序，在 GNS3 中配置 Juniper 路由器

## qemu-system-x86 软件包，在 Windows 和 OS 上安装 QEMU

## qemu-system-x86_64 二进制应用程序，在 GNS3 中配置 Juniper 路由器

## 问号 (?)，在 GNS3 控制台中，探索 GNS3 控制台

## 模拟器，模拟操作系统（参见 QEMU（快速模拟器））

### R

## 机架租赁，虚拟化，介绍 GNS3

## RAM（随机访问存储），通用要求, 向 GNS3 添加 IOS 镜像, 让 Olive 运行, 为 ASA 配置 GNS3, 为 IDS/IPS 配置 GNS3, 为 IOS-XRv 配置 GNS3, 将 GNS3 IOU 虚拟机导入到 VirtualBox, 识别问题, 节省资源, 术语表

## 节省资源，节省资源

## 定义，术语表

## 安装 Juniper Olive，让 Olive 运行

## 通用要求，通用要求

## IOS 镜像，向 GNS3 添加 IOS 镜像

## IOU 虚拟机，将 GNS3 IOU 虚拟机导入到 VirtualBox

## QEMU 虚拟机，为 ASA 配置 GNS3, 为 IDS/IPS 配置 GNS3, 为 IOS-XRv 配置 GNS3

## 路由器，故障排除，识别问题

## 重置命令，破解硬件

## 圆形，绘制，第四组工具组

## 重载所有设备图标，GNS3 工具栏，第四组工具组

## 远程服务器类型，新建 IOS 路由器对话框，客户端

## 远程服务器标签页，GNS3 服务器首好窗口，为 IOU 配置 GNS3, 客户端

# 索引

- 资源，共享，Dynamips 客户端/服务器设置（参见使用运行设备的多个 PC）

- RIP（路由信息协议），术语表

- 根分区，创建，文件系统分区

- Linux 根级权限，解决 NIO 错误

- route 命令，在项目中使用 VirtualBox 主机

- 路由器，在 Microsoft Windows 上安装, 设置手动 Idle-PC 值, 项目管理概述, 创建你的第一个项目, 与路由器配合, 在路由器之间建立链接, 配置虚拟硬件, 配置虚拟硬件, 登录路由器, 登录路由器, 备份 Juniper Olive, 添加以太网接口, 在 GNS3 中添加 vSRX Firefly, EtherSwitch 路由器, Cisco ASA、IDS/IPS 和 IOS-XRv, 运行 CCP, 为 IOS-XRv 配置 GNS3, 为 IOS-XRv 配置 GNS3, 配置路由器, 为 IOU 配置 GNS3, 为 NX-OSv 配置 GNS3, 配置云节点, 配置 Cisco IP 主机表, 打开控制台, 将 GNS3 配置导出到 Cisco 路由器, 多厂商集成, 多厂商集成, 识别问题, 当 IOS 镜像加载失败时, 解决控制台问题, 与 GNS3 的 Cisco 硬件, 支持的 Cisco 硬件

- 启动，设置手动 Idle-PC 值

- 网络的破坏与修复，多厂商集成

- CCP 项目配置，Cisco ASA、IDS/IPS 和 IOS-XRv, 运行 CCP

- 控制台问题，解决控制台问题

- EtherSwitch，EtherSwitch 路由器

- 将 GNS3 配置导出到 Cisco，打开控制台

- 为 Cisco IOS-XRv 项目配置，为 IOS-XRv 配置 GNS3, 配置路由器

- 为虚拟访问服务器配置，配置云节点

- 硬件，配置，在路由器之间建立链接

- 将 Cisco 配置导入 GNS3，将 GNS3 配置导出到 Cisco 路由器

- IOS 兼容性，支持的 Cisco 硬件

- IOS-XRv 项目，为 IOS-XRv 配置 GNS3

- Juniper，备份 Juniper Olive, 添加以太网接口

- 在 GNS3 中配置，备份 Juniper Olive

- 测试，添加以太网接口

- 链接，与路由器配合

- 登录到，配置虚拟硬件, 登录路由器

- 内存，故障，识别问题, 当 IOS 镜像加载失败时

- NX-OSv 项目，为 NX-OSv 配置 GNS3

- 在 GNS3 中运行可能的，多厂商集成

- 启动、停止和暂停，配置虚拟硬件

- 支持的 Cisco 硬件，与 GNS3 兼容的 Cisco 硬件

- 升级虚拟，项目概述

- 虚拟访问服务器，配置 Cisco IP 主机表

- 使用 IOU 交换机的 VLAN 路由，为 IOU 配置 GNS3

- vSRX Firefly 项目，在 GNS3 中添加 vSRX Firefly

- 带有网络交换机，登录路由器

- 路由器图标，工具栏，第四组, 解决 IOS 内存错误，术语表, 创建基于防火墙的项目, 创建 GNS3 Uberlab, 配置 GNS3, 在 Linux 中配置 TAP 适配器, 解决 IOS 内存错误, 解决 NIO 错误, 探索 GNS3 控制台

- `show eigrp neighbors` 命令，配置 IOS-XR 设备

- `show flash command`，获取 IOS 镜像, 登录路由器

- `show frame-relay pvc command`，简单的帧中继中心型与星型配置

- `show hosts command`，配置 Cisco IP 主机表

- 显示接口标签图标，GNS3 菜单栏，使用 GNS3 菜单栏

- `show ip route command`，NX-OSv 实战

- `show route command`，配置 IOS-XR 设备

- `show run command`，探索 GNS3 控制台

- `show security nat source summary command`，创建基于区域的防火墙项目

- `show sessions command`，配置 Cisco IP 主机表

- 模拟设备，屏幕布局

- 模拟操作系统，介绍 GNS3

- 快照图标，GNS3 菜单栏，使用 GNS3 菜单栏

- 快照，项目管理概述, 备份你的项目



- 软件模拟程序，介绍 `GNS3`
- `SONET`（同步光网络），术语表
- 源代码，在 OS X 上安装，在 Windows 和 OS X 上安装 `QEMU`
- 从……安装 `GNS3`，在 OS X 上安装
- 从……安装 `QEMU`，在 Windows 和 OS X 上安装 `QEMU`
- 稀疏内存支持，`Dynamips`，配置 `Dynamips`
- `SSH`（安全外壳），术语表
- `start command`，探索 `GNS3` 控制台
- 无头模式启动虚拟机选项，`VirtualBox`，`VirtualBox` 虚拟机设置
- 启动/恢复所有设备图标，`GNS3` 菜单栏，第三组工具组
- 启动路由器，配置虚拟硬件
- `startup-config` 文件，创建你的第一个项目，与路由器交互，将 `GNS3` 配置导出到 `Cisco` 路由器
- 停止所有设备图标，`GNS3` 菜单栏，第三组工具组
- 停止路由器，配置虚拟硬件
- `sudo command`，在 Linux 中配置 TAP 适配器
- 挂起所有设备图标，`GNS3` 菜单栏，第三组工具组
- `suspend command`，探索 `GNS3` 控制台
- 挂起路由器，配置虚拟硬件
- `SVC`（交换虚拟电路），术语表
- `SVI`（交换接口），IOU 实战
- 交换机模块设计，`Cisco`，“破解我的机架”挑战
- 交换机模块，有限仿真，登录路由器，登录路由器，`NM-16ESW` 和 `IOU L2` 限制
- `NM-16ESW`，有限仿真，登录路由器，`NM-16ESW` 和 `IOU L2` 限制
- 概述，登录路由器
- 交换机，有限仿真，`EtherSwitch` 路由器，帧中继交换机，使用 `IOS` 创建帧中继交换机，Ubuntu 上的 `TUN/TAP` 驱动，标准 `802.1Q Trunk`，创建分出，`Cisco IOU`，为 `GNS3` 配置 `IOU`，`NM-16ESW` 和 `IOU L2` 限制（另见分出；以太网节点；连接设备）
- `ATM`，配置，使用 `IOS` 创建帧中继交换机
- `Catalyst`，有限仿真，`NM-16ESW` 和 `IOU L2` 限制
- `Cisco`，CDP 隧道传输，创建分出
- `EtherSwitch` 路由器，`EtherSwitch` 路由器，Ubuntu 上的 `TUN/TAP` 驱动
- 帧中继，帧中继交换机
- `IOU`，`Cisco IOU`，为 `GNS3` 配置 `IOU`
- 交换机图标，工具栏，第四工具组
- `switchport mode access`，在你的 PC 中使用适配器
- 符号选择，更改你的符号，更改你的符号
- 符号链接（symlink），Linux，在 Linux PC 上设置 `IOU`
- 设备的符号，更改，更改你的符号
- 同步光网络（`SONET`），术语表
- `sysinstall` 主菜单，FreeBSD，入门
- Tab 补全，`NX-OSv`，`NX-OSv` 实战
- 防止标签剥离，标准 `802.1Q Trunk`，创建分出
- TAP 适配器，用于虚拟接入服务器，在 Windows 中配置环回适配器，在 `GNS3` 中创建虚拟接入服务器，配置云节点
- TAP 接口，云节点，OS X 上的 `TUN/TAP` 驱动
- `TAR`（归档）文件，术语表
- `TCP`（传输控制协议），登录路由器，在项目中使用 `VirtualBox` 主机，术语表
- 在 `VirtualBox` 中配置，在项目中使用 `VirtualBox` 主机
- 定义，术语表
- 端口号，更改，登录路由器
- `Telnet` 客户端，在 Linux 中创建 ISO
- 终端，配置接入路由器（另见虚拟接入服务器）
- 终端程序和控制台问题，解决控制台问题
- 终端设置，配置，登录路由器
- 术语，`GNS3`，项目管理概述
- 测试，`VPCS` IP 地址配置，添加以太网接口，创建简单网络，为 `GNS3` 配置 `ASA`，破解硬件，为 `GNS3` 配置 `IDS/IPS`，配置接入路由器
- `GNS3` 中的 `ASA`，为 `GNS3` 配置 `ASA`
- `Cisco IDS/IPS`，破解硬件，为 `GNS3` 配置 `IDS/IPS`
- 互联网连接，创建简单网络
- `Juniper` 路由器，添加以太网接口
- 虚拟接入服务器，配置接入路由器
- `VPCS`，`VPCS` IP 地址配置
- 文本注释，创建，第三组工具组，第四工具组
- `TFTP`（简单文件传输协议），获取镜像，在 `GNS3` 中测试 `ASA`，`ASDM` 安装，术语表

## 超设置

虚拟访问服务器，打开控制台

## Titanium

将 `NX-OSv` 导入 `VirtualBox`（查看 `NX-OSv`）

## 工具栏

项目管理概述，屏幕布局，使用 `GNS3` 工具栏，第四工具栏组，创建你的第一个项目，`VirtualBox` 虚拟机设置，配置客户端

## 设备

屏幕布局，第四工具栏组，创建你的第一个项目，`VirtualBox` 虚拟机设置，配置客户端

## GNS3

项目管理概述，使用 `GNS3` 工具栏

## 拓扑文件

项目管理概述

## 拓扑摘要

屏幕布局

## 传输控制协议

在项目中使用 `VirtualBox` 宿主机（查看 `TCP`）

## 简单文件传输协议

在 `GNS3` 中测试 `ASA`（查看 `TFTP`（简单文件传输协议））

## 故障排除

更改符号并组织设备，`VirtualBox` 首选项，救命！我摔倒了起不起来，识别问题，`IOS` 镜像加载失败，解决 `IOS` 内存错误，解决 `NIO` 错误，修正控制台问题，配置问题，终极方案，解决端口号冲突，备份你的项目

## ASAs

解决端口号冲突

## 配置问题

修正控制台问题

## 控制台问题

解决 `NIO` 错误

## Dynamips

更改符号并组织设备，识别问题

## 功能问题

救命！我摔倒了起不起来，修正控制台问题

## GNS3 配置文件

配置问题

## 硬件

终极方案

## IOS 镜像加载失败

识别问题

## IOS 内存错误

`IOS` 镜像加载失败

## 多协议路由问题

更改符号并组织设备

## NIO 错误

解决 `IOS` 内存错误

## 概述

救命！我摔倒了起不起来

## 端口号冲突

终极方案

## 问题分类

救命！我摔倒了起不起来

## 资源用于

备份你的项目

## 突发问题

救命！我摔倒了起不起来

## 不支持的 IOS 镜像

配置问题

## VirtualBox

`VirtualBox` 首选项

## TUN/TAP 驱动

OS X 上的 `TUN/TAP` 驱动

## 隧道兼容性

`CDP`，创建隐藏的交换机

### uberlab

创建，配置客户端

## Ubuntu Linux

在 OS X 上安装，`GNS3 WorkBench`，设置 PC 值，设置 PC 值，在 OS X 上安装，在 Windows 和 OS X 上安装 `QEMU`，Ubuntu Linux 上的 `TUN/TAP` 驱动，将 `GNS3` 设备连接到互联网，为 `ASA` 配置 `GNS3`，在 Linux PC 上设置 `IOU`，将 `NX-OSv` 导入 `VirtualBox`，在 Windows 中配置环回适配器，在 `GNS3` 中创建虚拟访问服务器，配置 Cisco 主机名表，`Dynamips` 客户端/服务器设置，解决 `IOS` 错误

（另见 `IOU`）

## 云节点

配置，在 `GNS3` 中创建虚拟访问服务器

## 连接互联网

将 `GNS3` 设备连接到互联网（`#ch07.html_iddle2264`）

## 控制台应用

选择，设置 PC 值，设置 PC 值

## cpulimit 程序

安装，为 `ASA` 配置 `GNS3`

## GNS3 系统

在 OS X 上安装（`#ch02.html_iddle2268`）

## GNS3 WorkBench

安装，`GNS3 WorkBench`

## gns3server 程序

`Dynamips` 客户端/服务器设置

## IOU

安装，在 Linux PC 上设置 `IOU`

## 权限问题

解决 `IOS` 错误

## QEMU

安装，在 Windows 和 OS X 上安装 `QEMU`

## TAP 适配器

配置，在 Windows 中配置环回适配器

## TUN/TAP 驱动

Ubuntu Linux 上的 `TUN/TAP` 驱动

## 虚拟访问服务器限制

配置 Cisco 主机名表

## Wireshark

安装，在 OS X 上安装

## UDP

`UDP`（用户数据报协议），云节点，创建许可证文件，配置 `GNS3`，术语

## 定义

术语

## 套接字

云节点

## 隧道端口范围

创建许可证文件，配置 `GNS3`

## UNIX 套接字连接

云节点

（另见 `IOU`）

## unix:initial-config.cfg 文件

在平台之间拷贝 `GNS3` 项目

## 解包软件

获取镜像

## “UNSUPPORTED HARDWARE DETECTED”错误

劫持硬件

## 不支持的 IOS 镜像

配置问题

## 更新 Ubuntu 包管理器

从源码安装 `GNS3`（`#ch02.html_iddle2287`）

## 升级

项目管理概述，为 `IOU` 配置 `GNS3`

## GNS3

为 `IOU` 配置 `GNS3`

## 虚拟路由器

项目管理概述

## 上传 IOU 镜像文件

将 `GNS3 IOU` 虚拟机导入 `VirtualBox`

## 使用本地服务器设置

`Dynamips` 首选项窗口，配置客户端

## 用户数据报协议

项目管理概述（查看 UDP 用户文件夹）

### V

## VBoxManage 应用

导入设备，运行 `Juniper vSRX` 火狐

## vconfig 命令

创建隐藏的交换机

## 供应商

集成多个，“攻击我的机架”挑战

## vi 编辑器

创建支持 `QEMU` 的 `IDS/IPS` 系统（`#ch08.html_iddle2297`）

## VIRL

`VIRL`（虚拟路由实验室），Cisco，介绍 `GNS3`，术语

## 虚拟接入服务器

- 雨天可以做的酷事事
- 雨天可以做的酷事事
- 通过接入服务器管理设备
- 通过接入服务器管理设备
- 通过接入服务器管理设备
- 在 Windows 中配置环回适配器
- 在 Linux 中配置 TAP 适配器
- 在 `GNS3` 中创建虚拟接入服务器
- 配置云节点
- 配置接入服务器路由器
- 配置接入服务器路由器
- 配置 Cisco IP 主机表
- 配置 Cisco IP 主机表
- 打开控制台
- 打开控制台

### Cisco IP 主机配置

Cisco IP 主机表配置，配置接入服务器路由器

### 关闭控制台

关闭控制台，打开控制台

### 云节点配置

云节点配置，在 `GNS3` 中创建虚拟接入服务器

### 接入服务器的组件

组件部分，通过接入服务器管理设备

### 连接超时

连接超时设置，打开控制台

### 定义

定义，雨天可以做的酷事事

### 局限性

局限性，配置 Cisco IP 主机表

### 环回适配器配置

Windows 中的环回适配器配置，通过接入服务器管理设备

### 打开控制台

打开控制台，配置 Cisco IP 主机表

### 概述

概述，雨天可以做的酷事事

### 准备 GNS3 服务器

准备 `GNS3` 服务器，在 Linux 中配置 TAP 适配器

### 路由器配置

路由器配置，配置云节点

### TAP 适配器配置

Linux 中的 TAP 适配器配置，在 Windows 中配置环回适配器

### 测试

测试，配置接入服务器路由器

### 虚拟接口安装

虚拟接口安装，通过接入服务器管理设备

### 虚拟连接

`GNS3` 虚拟连接，模拟操作系统

### 虚拟磁盘镜像

`QEMU` 虚拟镜像文件，Windows 和 OS X 的初步检查，`ASDM` 安装

### 虚拟分布式以太网

虚拟分布式以太网设备连接，云节点

### 虚拟硬件配置

虚拟硬件配置，在路由器之间建立链接

### 虚拟接口驱动

虚拟接口驱动，`Dynamips` 权限，OS X 上的 `TUN/TAP` 驱动

### 虚拟接入服务器接口

用于虚拟接入服务器的虚拟接口，通过接入服务器管理设备

### 虚拟互联网路由实验室（VIRL）

Cisco 虚拟互联网路由实验室（`VIRL`），介绍 `GNS3`，术表

### 虚拟局域网

虚拟局域网，配置标准 `802.1Q` 中干链路（参见 `VLAN`）

### 虚拟机磁盘（VMDK）

虚拟机磁盘（`VMDK`）文件，在 `GNS3` 中验证 `IDS/IPS`，为 `IOS-XRv` 配置 `GNS3`，术表

### 虚拟机

虚拟机，模拟操作系统，开源集成，`VirtualBox` 偏好，获取镜像，`IOU` 镜像，在 Windows 和 OS X 上使用 `GNS3 IOU` 虚拟机，为 `IOU` 配置 `GNS3`，修复控制台问题，术表

（另 `IDS/IPS`；`IOS-XRv`；`Juniper Olive`；`Juniper vSRX Firefly`；`NX-OSv`）

### 控制台问题

控制台问题，修复控制台问题，修复控制台问题

定义，术表

### IOU

`IOU`，`IOU` 镜像，在 Windows 和 OS X 上使用 `GNS3 IOU` 虚拟机，为 `IOU` 配置 `GNS3`，为 `IOU` 配置 `GNS3`

概述，开源集成

### QEMU

`QEMU`，获取镜像

### VirtualBox 设置

`VirtualBox` 的设置，`VirtualBox` 偏好

### 虚拟 PC 模拟器

虚拟 PC 模拟器，通用要求

### 虚拟专用网络

虚拟专用网络，术表

### 虚拟专用网络

虚拟专用网络，黑客行为

### 虚拟冗余

虚拟冗余，术表

### 虚拟路由器

虚拟路由器，模拟操作系统

### 虚拟化

虚拟化，模拟操作系统

# GNS3 之书：使用 Cisco、Juniper 及其他设备构建虚拟网络

### Jason C. Neumann

版权 © 2015 *The Book of GNS3.*

## 索引术

- `VLANs`（虚拟局域网），配置标准 `802.1Q` 中继，配置标准 `802.1Q` 中继，配置标准 `802.1Q` 中继，为 `IOU` 配置 `GNS3`，术语表
- `breakout`（分出），配置标准 `802.1Q` 中继
- 使用以太网交换机节点配置 `802.1Q` 中继，配置标准 `802.1Q` 中继
- 使用 `EtherSwitch` 路由器配置 `802.1Q` 中继，配置标准 `802.1Q` 中继
- `defined`（定义），术语表
- 用于路由的 `IOU` 交换机，为 `IOU` 配置 `GNS3`
- `VMDK`（虚拟机磁盘）文件，在 `GNS3` 中验证 `IDS/IPS`，为 `IOS-XRv` 配置 `GNS3`，术语表
- `VMs`，在 `GNS3` 中验证 `IDS/IPS`（参见虚拟机（`VMs`）`VMware ESXi`）
- `VMware GNS3 WorkBench`，`GNS3 WorkBench`
- `vMX`，`Juniper`，介绍 `Juniper`
- `VPCS`（虚拟 PC 模拟器），通用要求，安装 `GNS3` 服务器和 GUI，集成主机并使用 `Wireshark`，安装 `VPCS`，安装 `VPCS`，`VPCS` 命令，术语表
- `commands`（命令），安装 `VPCS`
- `defined`（定义），术语表
- `installing`（安装），安装 `GNS3` 服务器和 GUI，安装 `VPCS`
- `IP addressing`（IP 地址分配），`VPCS` 命令
- `overview`（概述），集成主机并使用 `Wireshark`
- `VPNC`（虚拟专用网络连接），术语表
- `VPNs`（虚拟私有网络），配置客户端，“攻击我的机架”挑战，术语表
- `Cisco`，攻击我的机架”挑战
- `defined`（定义），术语表
- `uberlab using`（使用 uberlab），配置客户端
- `VRRP`（虚拟路由器冗余协议），术语表
- `vSRX Firefly`，为虚拟机提供更多处理器（参见 `Juniper vSRX Firefly`）

### W

- `WAN`（广域网），术语表
- `WAN interface card (WIC)`，Cisco，术语表
- `web browser`（网络浏览器），在 `GNS3` 中测试 `ASA`，`ASDM` 安装，上传 `IOU` 镜像文件
- 使用……安装 `ASDM`，在 `GNS3` 中测试 `ASA`，`ASDM` 安装
- 使用……上传 `IOU` 镜像文件，上传 `IOU` 镜像文件
- `Windows`，Microsoft，Cisco `ASA`，`IDS/IPS` 和 `IOS-XRv`（参见 `Windows`）
- `WinPCAP`，在 Windows 上安装
- `Wireshark`，通用要求，在 Linux 上使用 `VirtualBox`，在 OS X 上安装，在 `GNS3` 中捕获数据包，在 Linux PC 上设置 `IOU`
- and `IOU` on Linux，在 Linux PC 上设置 `IOU`
- `capturing packets in GNS3`（在 `GNS3` 中捕获数据包），在 OS X 上安装
- `installing`（安装），在 Linux 上使用 `VirtualBox`
- `overview`（概述），在 Linux 上使用 `VirtualBox`，在 `GNS3` 中捕获数据包



- **reviewing saved captures**（查看已保存的捕获文件），在 GNS3 中捕获数据包
- **saving captures**（保存捕获文件），在 GNS3 中捕获数据包
- **workspace**（工作空间），GNS3，布局, 更改符号和组织设备
- **workstations, client/server setup**（工作站，客户端/服务器设置），Dynamips/服务器设置

### X

- **XQuartz**，下载，在 OS X 上安装

### Z

- **Zoom in/out icons**（放大/缩小图标），GNS3 工具栏，第三工具栏组

## 出信息

**The Book of GNS3: Build Virtual Network Using Cisco, Juniper, and More**

### Jason C. Neumann

版权 © 2015 **The Book of GNS3.** 版权所有。未经版权所有者和出版者的事先书面许可，本书的任何部分不得通过任何手段（电子或机械方式，包括复印、录制或任何信息存储或检索系统）进行复制或传输。

第一次印刷 19 18 17 16 15 1 2 3 4 5 6 7 8 9

ISBN-10: 1-59327-554-4

ISBN-13: 978-1-59327-554-9

出版：William Pollock

制作编辑：Serena Yang

封面插：Tina Salameh

设计：Octopod Studios

开发编辑：Jennifer Griffith-Delgado

技术评审：Jeremy Grossmann

校对：Gillian McGvey and Kim Wimpsett

排字：Susan Ginert Stevens

校对：James Raleigh

索引编制：BIM Indexing & Proofreading Services

有关分销、翻译或批量销售的信息，请直接联系 No Starch Press, Inc.：

*美国国会目录出版数据*

Neumann, Jason C. The book of GNS3: build virtual network labs using Cisco, Juniper, and more / by Jason C. Neumann. 页 包含索引。摘要：“向读者展示如何使用流行的开源平台 GNS3 在 PC 上创建和管理虚拟网络，并提供基于教程的解释”——出版者提供。ISBN 978-1-59327-554-9 -- ISBN 1-59327-554-4. 1. 计算机网络--计算机仿真。I. 标题。TK5105.5.N4865 2015 004.6’8--dc23

No Starch Press 和 No Starch Press 标志是 No Starch Press, Inc. 的注册商标。此处提到的其他产品和公司名称可能是其所有者的商标。我们没有在每次出现商标时使用商标符号，仅以编辑方式使用这些名称，并造福商标所有者，无侵犯商标的意图。

本书中的信息按“现状”分发，不提供任何保证。在准备本作品时已采取一切预防措施，但作者或 No Starch Press, Inc. 对书中包含的信息直接或间接引起或据称引起的任何损失或损害，对任何个人或实体不承担任何责任。

No Starch Press 

2015

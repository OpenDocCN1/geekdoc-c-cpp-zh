
一种用于设计和测试新网络协议、架构或修改的有效工具。

- 真实环境测试：NS-3 可以与真实网络对接，从而支持“混合”仿真，即网络的一部分是仿真出来的，另一部分是真实运行的网络。这对于在将新协议或配置部署到真实网络之前进行测试非常有价值。
- C++ 和 Python API：NS-3 同时提供 C++ 和 Python 接口。这为设计仿真提供了灵活性，并允许你使用最适合自身需求的语言。对于大量使用 C++ 的网络专业人员来说，NS-3 提供了利用其现有技能和知识的机会。
- 模块：NS-3 中的功能按模块组织。每个模块封装网络功能的某个特定领域或某种特定网络协议。例如，有用于 TCP、UDP、以太网、WiFi、Internet 路由协议等的模块。
- 与其他工具集成：NS-3 可以与其他工具集成以进行进一步分析。例如，它可以生成 PCAP 文件，以便在 Wireshark 中进行数据包级分析。它还可以与可视化工具对接，以图形方式表示网络仿真。

## 使用 NS-3 进行网络仿真

### 网络仿真的流程

要在 C++ 中使用 NS-3 搭建网络仿真，通常需要遵循以下步骤：

#### 创建节点

首先，创建节点。在 NS-3 中，节点是能够在网络中发送或接收数据包的实体，充当终端系统或路由器。每个节点都是网络中一台计算机主机的抽象，能够运行网络协议。

#### 创建并配置网络设备

其次，创建并配置网络设备。网络设备（例如 Wi-Fi 设备、以太网设备或点对点设备）会连接到节点。这些设备使节点能够发送和接收数据包。根据你所建模网络的复杂程度，每个节点可以有一个或多个网络设备。

#### 创建并配置信道

第三步是创建并配置信道。NS-3 中的信道模拟数据包传输所经过的介质，例如无线射频频谱或有线电缆。你选择的信道取决于所仿真的网络类型。

#### 安装网络协议栈

接下来，你需要在每个节点上安装网络协议栈。网络协议栈包含支持网络通信的协议，例如 Internet 协议（IP）、传输控制协议（TCP）或用户数据报协议（UDP）。这些协议栈决定了数据在网络中如何发送和接收。

#### 分配 IP 地址

安装网络协议栈后，为每个网络设备分配唯一的 IP 地址。这个过程类似于实际网络中的设备被分配唯一标识符以促进通信。

#### 创建并安装应用

最后，在节点上创建并安装应用。NS-3 中的应用会生成网络流量，模拟网络中流动的真实数据。示例包括发送 ICMP 回显请求的简单 ping 应用，或模拟 VoIP 或视频流的更复杂应用。

NS-3 仿真非常灵活，既可以是只有几个节点的简单示例，也可以是对包含数百或数千个节点的大型网络进行复杂仿真。NS-3 为网络实验提供了受控、可复现的环境，是网络专业人员和研究人员的宝贵工具。

## 使用 NS-3 搭建网络仿真

让我们仿真一个由点对点链路连接两个节点的简单网络。

#### 安装 NS-3

在开始之前，请确保你的系统上已安装 NS-3。你可以从 NS-3 官方网站下载，并按照针对你所用操作系统的安装说明进行操作。

#### 创建新的仿真脚本

为你的仿真创建一个新的 C++ 文件。我们将其命名为 simple-network.cc。这个脚本将用于配置网络并运行仿真。

#### 包含必要的头文件

我们需要包含必要的 NS-3 头文件。对于这个简单仿真，我们需要以下内容：

```cpp
#include "ns3/core-module.h"
#include "ns3/network-module.h"
#include "ns3/internet-module.h"
#include "ns3/point-to-point-module.h"
#include "ns3/applications-module.h"
```

#### 设置主函数

所有 NS-3 仿真都从 main 函数开始，其形式如下：

```cpp
int main (int argc, char *argv[])
{
    // Simulation code here
    return 0;
}
```

#### 创建节点

创建两个节点，并在它们上面安装 Internet 协议栈：

```cpp
ns3::NodeContainer nodes;
nodes.Create (2);

ns3::InternetStackHelper stack;
stack.Install (nodes);
```

#### 创建点对点链路

我们将使用点对点链路连接节点：

```cpp
ns3::PointToPointHelper pointToPoint;
pointToPoint.SetDeviceAttribute ("DataRate", StringValue ("5Mbps"));
pointToPoint.SetChannelAttribute ("Delay", StringValue ("2ms"));

NetDeviceContainer devices;
devices = pointToPoint.Install (nodes);
```

#### 分配 IP 地址

我们将为节点分配 IP 地址：

```cpp
ns3::Ipv4AddressHelper address;
address.SetBase ("10.1.1.0", "255.255.255.0");
ns3::Ipv4InterfaceContainer interfaces = address.Assign (devices);
```

#### 设置应用

让我们设置一个简单的 UDP 回显服务器和客户端。服务器位于第一个节点上，客户端位于第二个节点上：

```cpp
UdpEchoServerHelper echoServer (9);
ApplicationContainer serverApps = echoServer.Install (nodes.Get (0));
serverApps.Start (Seconds (1.0));
serverApps.Stop (Seconds (10.0));

UdpEchoClientHelper echoClient (interfaces.GetAddress (0), 9);
echoClient.SetAttribute ("MaxPackets", UintegerValue (1));
echoClient.SetAttribute ("Interval", TimeValue (Seconds (1.0)));
echoClient.SetAttribute ("PacketSize", UintegerValue (1024));

ApplicationContainer clientApps = echoClient.Install (nodes.Get (1));
clientApps.Start (Seconds (2.0));
clientApps.Stop (Seconds (10.0));
```

### 运行仿真

最后，我们运行仿真：

```cpp
ns3::Simulator::Run ();
ns3::Simulator::Destroy ();
```

### 构建并运行

要构建并运行仿真，请在 NS-3 目录中使用 `./waf` 命令：

```
./waf --run simple-network
```

至此完成。这是一个简单易行的网络仿真：两个节点通过点对点链路通信。NS-3 框架极其灵活且强大，你可以通过添加更多节点、不同类型的链路、不同的应用等来创建复杂得多的仿真。

## 总结

本章深入探讨了网络测试与仿真领域，这些是网络管理员工具库中的关键工具，用于确保网络系统的可靠性、效率和稳健性。我们首先概述了网络测试方法及其在维护网络健康状况中的重要作用。我们进一步明确了使用 C++ 库如何有助于网络性能增强、压力测试和安全测试。

我们讨论并实际演示了两种关键测试方法：功能性测试和性能测试。我们学习了功能性测试如何确保网络各组件正确运行，从而提供坚实的基础。另一方面，性能测试评估网络在各种负载和条件下的效率，为优化提供洞见。我们学习了如何使用 C++ 中可用的工具和技术，实际应用这些方法。


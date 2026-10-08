

通用语言运行时 (CLR)，并通过利用 .NET 卓越环境的优势帮助您构建面向服务的应用程序。

WCF 提供了一个优秀的平台，将微软的分布式技术（Web 服务、远程调用、COM+ 等）统一在一个框架伞下。与 WCF 架构相关的三个重要概念包括服务、客户端和消息。本节将检查 WCF 架构的构建模块，如图 9-1 所示。

| WCF 客户端 | SOAP | WCF 服务 |
|---|---|---|
| WCF | | WCF |
| Microsoft .NET Framework | | Microsoft .NET Framework |

**图 9-1:** WCF 和 .NET Framework

在 WCF 中，你可以拥有三个合约：服务合约、数据合约和消息合约。任何 WCF 服务类都至少实现一个服务合约——该接口用于定义由 WCF 服务类暴露的操作。此类操作可能还包括数据操作——使用数据合约暴露。

实际上，WCF 服务类与任何其他类没有区别，区别在于它被标记了 `ServiceContract` 特性。服务类中的单个方法被标记为 `OperationContract` 特性，将其定义为服务的外部操作。消息合约的定义方式允许您更改消息的格式。注意，`ServiceContract`、`DataContract` 和其他特性定义在 `System.ServiceModel` 命名空间中。

由于使用了 `OperationContract` 特性，服务类中存在未标记该特性的方法。这将该方法从 WCF 服务内部的调用中隐藏。请记住，对于 DLL 引用等，方法的访问修饰符仍然将控制其对外部调用者的可用性。

在 WCF 中，绑定（binding）表示特定服务如何与其同类的其他服务通信，以及与其客户端通信。任何服务都可以随时通过一个或多个绑定变为可用。

表 9-1 显示了 WCF 中预定义的内置绑定。

## **表 9-1:** WCF 预定义的内置绑定

| 绑定 (BINDING) | 用途 |
|---|---|
| basicHttpBinding | 此绑定用于为基于 ASMX 的客户端提供后兼容支持。此绑定使用简单对象访问协议 (SOAP) 1.1 消息，当 WCF 服务必须与非基于 WCF 的系统通信时使用。 |
| wsHttpBinding | 此绑定发送 SOAP 1.2 消息并实现 ws* 规范，以支持安全性、可靠性、有序交付和事务。 |
| netTCPBinding | 此绑定发送 SOAP 1.2 消息，并在 Windows 网络上的 WCF 客户端和服务之间使用二进制编码和优化后的通信。此绑定仅在进行 WCF 到 WCF 通信时可用，这是可能的最快通信过程。它可以用于替换 COM+ 和 .NET 模型。 |
| netNamedPipeBinding | 此绑定为存储在同一台机器上的 WCF 服务和 WCF 客户端提供安全、可靠的管道通信。这种通信应用于同一服务器上进程之间的通信。 |
| netPeerTcpBinding | 此绑定用于建立点对点通信，详细信息请参阅 MSDN 文章 (http://microsoft.com/en-us/library/bb72691.aspx)。 |
| msmqIntegrationBinding | 此绑定允许应用程序使用微软消息队列 (MSMQ) 接收消息，并允许与已使用 MSMQ 的应用程序集成。 |
| wsDualHttpBinding | 此绑定允许客户端和服务器之间进行双向通信。虽然本质上与 `wsHttpBinding` 相似，但此方法将客户端的 IP 地址暴露给服务，并要求客户端通过公共 URI 可用。 |
| wsFederationHttpBinding | 此绑定通过实现 WS-Federation 协议，允许系统之间的无缝身份传递。 |
| netMsmqBinding | 此绑定允许应用程序通过 MSMQ 队列发送消息，提供了断连接通信和安全选项。 |

WCF 中的端点（Endpoints）用于将服务与其地址关联。通道（Channels）实际上是服务与其客户端之间的桥梁。以下是 WCF 支持的通道类型：

- 单向输入 (Simplex Input)
- 单向输出 (Simplex Output)
- 请求-响应 (Request-reply)
- 双工 (Duplex)

为了帮助直观理解端点和通道的概念，让我们用一个常见的问题来描述端点的功能。假设你正在进行一次前往目的地的旅行。到达目的地，你需要遵循一个简单的过程：乘坐车辆并通过必要的道路到达目的地。

以此场景为例，你要去的地方是端点，你的车辆是请求，而道路是通道。端点是用户可以调用的物理地址（例如 http://www.domain.com/service/get），而通道负责客户端与端点之间的数据接收和传输。

# 开始使用 WCF

一个典型的 WCF 实现包含一个 WCF 服务和一个 WCF 客户端。WCF 客户端消费由 WCF 服务提供的服务。WCF 服务基于三个概念：地址、绑定和合约。正如所述，WCF 服务和 WCF 客户端通过消息进行通信，如图 9-2 所示。

![](img/b5597c749e84b27b0d30513ae106_222)
图 9-2: WCF 服务与

本节介绍了如何开始使用 WCF。一个典型的 WCF 实现包含一个 WCF 服务和一个 WCF 客户端。WCF 客户端消费由 WCF 服务提供的服务。WCF 服务基于三个概念：地址、绑定和合约。正如所述，WCF 服务和 WCF 客户端通过消息进行通信，如图 9-2 所示。

本节介绍了如何开始使用 WCF。一个典型的 WCF 实现包含一个 WCF 服务和一个 WCF 客户端。WCF 客户端消费由 WCF 服务提供的服务。WCF 服务基于三个概念：地址、绑定和合约。正如所述，WCF 服务和 WCF 客户端通过消息进行通信，如图 9-2 所示。

本节介绍了如何开始使用 WCF。一个典型的 WCF 实现包含一个 WCF 服务和一个 WCF 客户端。WCF 客户端消费由 WCF 服务提供的服务。WCF 服务基于三个概念：地址、绑定和合约。正如所述，WCF 服务和 WCF 客户端通过消息进行通信，如图 9-2 所示。

本节介绍了如何开始使用 WCF。一个典型的 WCF 实现包含一个 WCF 服务和一个 WCF 客户端。WCF 客户端消费由 WCF 服务提供的服务。WCF 服务基于三个概念：地址、绑定和合约。正如所述，WCF 服务和 WCF 客户端通过消息进行通信，如图 9-2 所示。

本节介绍了如何开始使用 WCF。一个典型的 WCF 实现包含一个 WCF 服务和一个 WCF 客户端。WCF 客户端消费由 WCF 服务提供的服务。WCF 服务基于三个概念：地址、绑定和合约。正如所述，WCF 服务和 WCF 客户端通过消息进行通信，如图 9-2 所示。

# 创建服务

WCF 服务可以通过两种不同的方式进行托管——通过信息信息服务 (IIS)（类似于 ASMX），或者作为标准可执行文件。

注意，WCF 服务包含以下内容：
- 服务类
- 托管环境
- 一个或多个端点

服务类使用托管 CLR 编写的。托管环境是 WCF 服务执行的上下文。端点允许客户端访问服务。

可以选择两个模板来创建 WCF 服务：Visual Studio Service Library 模板和 Visual Studio Service Application 模板。

让我们使用 Visual Studio Service Library 模板创建 WCF 服务。按照以下步骤操作：

1. 打开 Visual Studio 2010。
2. 点击文件 -> 新建 -> 项目。
3. 从显示的模板中选择 WCF Service Application，如图 9-3 所示。
4. 为项目提供名称并点击 OK 保存。

![](img/b5597c749e84b27b0d30513ae106_233)
图 9-3: 创建应用程序

然后创建 WCF Service Application 项目。从外观上看，服务类如下：

```
using System;
namespace MyDataService
{
    // 注意：你可以使用“重构”菜单上的“重命名”命令
    // 一起更改代码文件中的类名“IService”。
    public class Service : IService
    {
        public string GetData(int value)
        {
            return string.Format("You entered: {0}", value);
        }
        public CompositeType GetDataUsingDataContract(CompositeType composite)
        {
            if (composite == null)
            {
                throw new ArgumentNullException("composite");
            }
            if (composite.BoolValue)
            {
                composite.StringValue += "Suffix";
            }
            return composite;
        }
    }
}
```

提供代码段中的服务类实现了 IService 接口，如下所示：

```
using System.Runtime.Serialization;
using System.ServiceModel;
namespace MyDataService
{
    // 注意：你可以使用“重构”菜单上的“重命名”命令
    // 同时配置代码和配置文件中的接口名称“IService”。
    [ServiceContract]
    public interface IService
    {
        [OperationContract]
        string GetData(int value);

        [OperationContract]
        CompositeType GetDataUsingDataContract(CompositeType composite);

        // TODO：在此处添加您的服务操作
    }
}
```


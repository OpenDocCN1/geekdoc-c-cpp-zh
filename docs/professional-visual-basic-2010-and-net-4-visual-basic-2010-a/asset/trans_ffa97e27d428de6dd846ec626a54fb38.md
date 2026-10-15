
要拥有一个服务，至少需要定义一个包含一个操作的 Service Contract（服务约定）。如果没有这最低限度的定义，就没有任何可调用的内容。ServiceContract 接口中的方法通过 <OperationContract> 特性来定义各个接口。

可选地，如果您的服务要接受除基元类型以外的数据类型，就需要提供元数据来定义这些数据类型。<DataContract> 特性可以与一个或多个类关联，以定义这些自定义数据结构。接口不需要暴露任何自定义数据结构，但如果需要暴露，就必须确定要将类的哪些属性包含在接口中。每个要暴露的属性都与一个 <DataMember> 特性关联，以将其标识为 DataContract 的一部分。

## 使用 WS-* 协议

WCF 可以理解和处理完整的 WS-* 规范集，并且可以启用这些规范来创建消息，以满足安全、可靠性和事务处理方面的既定方式。这些协议中的一部分，以及对消息管理方式的理解，都重要到值得仔细研究其实现细节。

消息（由 Messaging 层定义）依赖于 SOAP（以明文文本或二进制格式发送）。高级 WS-* 规范大量使用 SOAP 标头，使消息能够自包含，并且除了消息本身的简单传输外，不真正依赖传输协议来提供安全性、可靠性或任何其他能力。消息传输优化机制（MTOM）是一种替代直接 Internet 消息封装（DIME）的技术，用于随 SOAP 消息一起传输二进制对象。二进制对象的一个例子是您希望通过 WCF 服务公开的 JPEG 图像。

WCF 中的安全实现使您能够使用 WS-Security。在 WS-Security 出现之前，Web 服务中最初缺乏安全模型，这使得许多公司无法在整个公司范围内大规模采用这些服务，也无法转向面向服务的架构。WS-Security 解决了保持消息安全所需的主要领域——凭据交换、消息完整性和消息机密性。

为此，WS-Security 支持在两个级别实施安全性。第一个是消息级别。WS-Security 使实体能够在所交换的消息中提供和验证凭据。或者，WS-Security 还支持传输级别的安全性。这种安全形式侧重于基于传输协议建立凭据，例如使用 HTTPS 安全地传输数据。

借助消息级安全性，WS-Security 使两个实体能够在消息本身内部（实际上是从消息的 SOAP 标头）交换其安全凭据。WS-Security 的一大优点是它不要求使用特定类型的凭据集，而是允许使用任何类型的凭据。此外，消息还可以通过多个路由器发送。实际上，这使您的解决方案可以在消息到达最终目的地之前将其从一个地方转发到另一个地方，同时确保消息在传输过程中不被篡改。当消息从一个 SOAP 路由器移动到另一个路由器时，这些 SOAP 节点可以对消息进行添加或删除。如果这些 SOAP 节点落入恶意方之手，消息的完整性就可能受到损害。这正是 WS-Security 发挥作用的地方。

WS-Security 帮助的另一个领域是当您需要让 WS-Security 加密全部或部分 SOAP 消息时。当您的消息在虚拟世界中飞速传输时，有可能被不应查看其内容的一方截获并打开查看。因此，打乱消息的内容通常是有益的。当消息到达预期的接收者时，应用程序便可以使用您的加密密钥对消息进行解密，以读取内容。

WS-SecureConversation 用于建立连接，使实体能够交换多条消息并维持已建立的安全安排。相反，WS-Trust 与 WS-Security 配合使用，允许颁发安全令牌，并提供实体交换这些令牌的方式。该规范还涉及在两个实体之间建立信任关系。

WS-ReliableMessaging 允许消息进行可靠的端到端通信，以确保消息被送达。

“事务”部分允许使用 WS-Coordination 和 WS-AtomicTransaction。WS-Coordination 用于处理多个服务之间关系的描述。当一家公司开始在企业内部开发大量服务时，它会意识到开发出的许多服务彼此之间存在关系，这正是 WS-Coordination 发挥作用的地方。该规范旨在由其他规范进行扩展，以进一步定义特定的协调类型。

WS-AtomicTransaction 使用 WS-Coordination 和 WS-Security 来定义服务事务流程。原子事务是一种创建事务流程的方式，其基础是全有或全无。这些事务是短生命周期的事务，因此当您使用它们时，会锁定数据资源并占用物理资源（如连接、线程和内存）。

本讨论的主要目的是强调您可以利用大量的 WS-* 规范。更好的是，在使用 WCF 时，您甚至无需意识到这些规范的存在——您可以通过编程式或声明式编程来访问这些规范所提供的功能。

## 构建 WCF 服务

构建 WCF 服务并不困难。使用 Visual Studio 2010，您会看到图 13-2 所示的 WCF 新项目模板。不过要注意一点：要托管 WCF 服务，您需要以“以管理员身份运行”菜单链接启动 Visual Studio。在尝试复现示例中的所有步骤之前，请确保您已通过上下文菜单中的“以管理员身份运行”选项启动了 Visual Studio。

![](img/d99870e80390742f93963da7be0b2e61_527_0.png)

图 13-2

当您以这种方式构建 WCF 项目时，思路是构建一个传统的类库，将其编译为 DLL，然后可以添加到另一个项目中。代码的分离和多个项目的使用是在大型项目中管理复杂性的有力工具。话虽如此，您也可以同样轻松地直接在 .NET 项目中构建 WCF 服务，无论该项目是控制台应用程序还是 Windows 窗体应用程序。

本示例将首先在服务库中创建一个新的 WCF 服务。然后演示如何在控制台应用程序中托管 WCF 服务。首先创建一个名为 ProVB_WCFCalculatorService 的新服务库。

创建新的库项目后，Visual Studio 的样子将类似于图 13-3 所示。

![](img/d99870e80390742f93963da7be0b2e61_528_0.png)

图 13-3

本示例首先演示如何构建 WCF 服务，然后演示如何构建一个托管该服务的控制台应用程序，最后演示如何利用 Visual Studio 2010 测试此服务。

### 创建接口

要创建您的服务，您需要一个服务约定（Service Contract），即服务的接口。它由所有公开的方法以及调用这些方法所需的输入和输出参数组成。要完成此任务，请将文件 IService1.vb 重命名为 ICalculator.vb，然后用下面提供的代码替换生成文件的内容：

```
<ServiceContract()>
Public Interface ICalculator
    <OperationContract()>
    Function Add(ByVal a As Integer, ByVal b As Integer) As Integer
    <OperationContract()>
    Function Subtract(ByVal a As Integer, ByVal b As Integer) As Integer
    <OperationContract()>
    Function Multiply(ByVal a As Integer, ByVal b As Integer) As Integer
    <OperationContract()>
    Function Divide(ByVal a As Integer, ByVal b As Integer) As Integer
End Interface
```

来自 ICalculator.vb 的代码片段

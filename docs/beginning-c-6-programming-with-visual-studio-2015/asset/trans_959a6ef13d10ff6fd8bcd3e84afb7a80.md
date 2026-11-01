

如果你从 `<endpoint>` 元素中移除 `<bindings>` 节以及 `bindingConfiguration` 属性，那么客户端将使用默认的绑定配置。

包含名为 `BasicHttpBinding_IService1` 的 `<binding>` 元素，是为了让你可以用它来自定义绑定的配置。这里有许多你可能用到的配置设置，从超时设置到消息大小限制和安全设置。如果这些设置在服务项目中被指定为非默认值，那么你会在 `app.config` 文件中看到它们，因为它们会被复制过来。为了让客户端能够与服务通信，绑定配置必须匹配。本章不会深入探讨 WCF 服务配置。

这个示例涵盖了很多内容，在继续之前，值得总结一下你所学到的知识：

- WCF 服务定义：
  - 服务由包含操作协定成员的服务协定接口定义。
  - 服务在实现服务协定接口的类中实现。
  - 数据协定只是使用数据协定属性的类型定义。
- WCF 服务配置：
  - 你可以使用配置文件（`web.config` 或 `app.config`）来配置 WCF 服务。
- WCF Web 服务器托管：
  - Web 服务器托管使用 `.svc` 文件作为服务基地址。
- WCF 客户端配置：
  - 你可以使用配置文件（`web.config` 或 `app.config`）来配置 WCF 服务客户端。

下一节将更详细地探讨协定。

## WCF 测试客户端

在之前的“试一试”中，你同时创建了服务和客户端，以了解基本 WCF 架构的工作原理以及如何实现 WCF 服务的配置。但在实际中，你想要使用的客户端应用程序可能很复杂，并且正确测试服务可能很棘手。

为了简化 WCF 服务的开发，Visual Studio 提供了一个测试工具，你可以使用它来确保 WCF 操作正常工作。该工具会自动配置为与你的 WCF 服务项目一起使用，因此如果你运行项目，该工具就会出现。你只需确保要测试的服务（即 `.svc` 文件）被设置为 WCF 服务项目的启动页。或者，你也可以将测试客户端作为独立应用程序运行。在 64 位操作系统上，你可以在 `C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\WcfTestClient.exe` 找到测试客户端。

## 服务协定

服务协定是通过将 System.ServiceModel.ServiceContractAttribute 属性应用于接口定义来定义的。你可以使用表 22-5 中所示的属性来自定义服务协定。

表 22-5：ServiceContractAttribute 属性

| 属性 | 说明 |
|---|---|
| Name | 指定服务协定的名称，该名称在 WSDL 中的 `<portType>` 元素中定义。 |
| Namespace | 定义 WSDL 中 `<portType>` 元素使用的服务协定的命名空间。 |
| ConfigurationName | 配置文件中使用的服务协定的名称。 |
| HasProtectionLevel | 确定服务使用的消息是否具有显式定义的保护级别。保护级别使你可以对消息进行签名，或签名并加密。 |
| ProtectionLevel | 用于消息保护的保护级别。 |
| SessionMode | 确定是否为消息启用会话。如果使用会话，那么你可以确保发送到服务不同终结点的消息是关联的——也就是说，它们使用相同的服务实例，因此可以共享状态等。 |
| CallbackContract | 对于双工消息传递，客户端除了服务协定之外还会公开一个协定。这是因为，如前所述，双工通信中的客户端也充当服务器。此属性使你可以指定客户端使用哪个协定。 |

## 操作协定

在定义服务协定的接口中，你可以通过应用 System.ServiceModel.OperationContractAttribute 属性将成员定义为操作。此属性具有表 22-6 中所述的属性。

表 22-6：OperationContractAttribute 属性

| 属性 | 说明 |
|---|---|
| Name | 指定服务操作的名称。默认值是成员名称。 |
| IsOneWay | 指定操作是否返回响应。如果将此属性设置为 true，那么客户端将不会等待操作完成后再继续执行。 |
| AsyncPattern | 如果设置为 true，则该操作将实现为两个方法，你可以使用这两个方法异步调用该操作：`Begin<methodName>()` 和 `End<methodName>()`。 |
| HasProtectionLevel | 参见上一节。 |
| ProtectionLevel | 参见上一节。 |
| IsInitiating | 如果使用会话，那么此属性确定调用此操作是否可以启动新会话。 |
| IsTerminating | 如果使用会话，那么此属性确定调用此操作是否终止当前会话。 |
| Action | 如果你使用寻址（WCF 服务的一项高级功能），那么操作会有一个关联的操作名称，你可以使用此属性指定该名称。 |
| ReplyAction | 与 Action 类似，但指定操作响应的操作名称。 |

> **注意** 在 .NET 4.5 Framework 中，当你添加服务引用时，无论 AsyncPattern 是否设置为 true，Visual Studio 都会生成异步代理方法来调用服务。这些方法带有 Async 后缀，使用 .NET 4.5 中包含的新异步技术，并且仅从调用代码的角度来看是异步的。在内部，它们调用同步 WCF 操作。

## 消息协定

前面的示例没有使用消息协定规范。如果你使用这些规范，那么你需要定义一个表示消息的类，并将 MessageContractAttribute 属性应用于该类。然后，你将 MessageBodyMemberAttribute、MessageHeaderAttribute 或 MessageHeaderArrayAttribute 属性应用于此类的成员。所有这些属性都位于 System.ServiceModel 命名空间中。除非你需要对 WCF 服务使用的 SOAP 消息进行高度控制，否则你可能不会想要这样做，因此这里不提供详细信息。

## 错误协定

如果你有特定的异常类型（例如自定义异常）想要提供给客户端应用程序，那么你可以将 System.ServiceModel.FaultContractAttribute 属性应用于可能生成此异常的操作。

## 试一试 WCF 协定：Ch22Ex02Contracts

1. 在目录 C:\BegVCSharp\Chapter22 中创建一个名为 Ch22Ex02 的新 WCF 服务应用程序项目。
2. 向解决方案中添加一个名为 Ch22Ex02Contracts 的类库项目，并删除 Class1.cs 文件。
3. 向 Ch22Ex02Contracts 项目添加对 System.Runtime.Serialization.dll 和 System.ServiceModel.dll 程序集的引用。
4. 向 Ch22Ex02Contracts 项目添加一个名为 Person 的类，并按如下方式修改 Person.cs 中的代码：

```csharp
using System.Runtime.Serialization;
namespace Ch22Ex02Contracts
{
    [DataContract]
    public class Person
    {
        [DataMember]
        public string Name { get; set; }
        [DataMember]
        public int Mark { get; set; }
    }
}
```

5. 向 Ch22Ex02Contracts 项目添加一个名为 IAwardService 的接口，并按如下方式修改 IAwardService.cs 中的代码：

```csharp
using System.ServiceModel;
namespace Ch22Ex02Contracts
{
    [ServiceContract(SessionMode = SessionMode.Required)]
    public interface IAwardService
    {
        [OperationContract(IsOneWay = true, IsInitiating = true)]
        void SetPassMark(int passMark);
        [OperationContract]
        Person[] GetAwardedPeople(Person[] peopleToTest);
    }
}
```

6. 在 Ch22Ex02 项目中，添加对 Ch22Ex02Contracts 项目的引用。
7. 从 Ch22Ex02 项目中删除 IService1.cs 和 Service1.svc。
8. 向 Ch22Ex02 添加一个名为 AwardService 的新 WCF 服务。
9. 从 Ch22Ex02 项目中删除 IAwardService.cs 文件。
10. 按如下方式修改 AwardService.svc.cs 中的代码：

```csharp
using System.Collections.Generic;
using Ch22Ex02Contracts;
namespace Ch22Ex02
{
    public class AwardService : IAwardService
```


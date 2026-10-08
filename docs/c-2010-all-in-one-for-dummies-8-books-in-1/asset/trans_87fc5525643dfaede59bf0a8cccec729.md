

# 创建一个 WCF 服务 751

```csharp
public class Conference : SHARPService.IConference
{
    public int Id { get; set; }
    public String Title { get; set; }
    public String Description { get; set; }
    public int LocationId { get; set; }
}
```

我们希望将此作为服务的 DataContract。根据我们在模板中看到的，我们应该在类上方添加 [DataContract]，并在属性上方添加 [DataMember]。

# 3. 为服务添加 DataContract。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Runtime.Serialization;
```

```csharp
namespace SHARPService
{
    [DataContract]
    public class Conference : SHARPService.IConference
    {
        [DataMember]
        public int Id { get; set; }
        [DataMember]
        public String Title { get; set; }
        [DataMember]
        public String Description { get; set; }
        [DataMember]
        public int LocationId { get; set; }
    }
}
```

现在有了一个可以使用的类，是时候创建服务了。

# 4. 右单击 SHARPService 项目并添加一个新的 WCF 服务。

我将我的服务命名为 Registration.svc。

# 5. 删除方法模板并添加下面的代码。

与 ASMX 示例不同，这不是一个可以运行的示例；我们只是设置了一个模拟回复。

```csharp
namespace SHARPService
{
    public class Registration : IRegistration
    {
        public List<Conference> conferencesAtLocation(int locationId)
        {
            List<Conference> locationConferences = new List<Conference>();
            return locationConferences;
        }
    }
}
```

| 第七卷 | 第3章 |
| :--- | :--- |
| 使用 WCF 构建 Web 服务 | |

- 6. 右点击 Registration.svc 文件并选择“设为启动页”。
- 7. 按 F5 运行项目。

请注意，尽管 ASP.NET 开发服务器正在运行，但你的 Web 浏览器并没有运行。图 3-4 所示的 WCF 测试客户端取代了 ASMX 开发测试页。它允许你添加请求值并查看响应值，而无需依赖 HTTP。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_777_0.png)

为什么是这样？WCF 允许你使用 HTTP（Web 的骨干协议）之外的其他事物来传输消息细节。（你可以在侧边栏“使用不同的端点”中找到一些示例。）

# 配置

WCF 唯一的缺点是配置。因为 WCF 是 Windows 远程过程调用的终极解决方案，有足够的配置选项来处理一切。有时会让人有点抓狂。

幸运的是，有服务配置编辑器（Service Configuration Editor）。如图 3-5 所示，服务配置编辑器允许你管理 WCF 主要力量的复杂选项。

## 使用不同的端点

WCF 的核心意义在于你可以编写一个服务，并让 IIS 在相同的代码上接受许多不同的协议。当然，我们可以做 SOAP，就像在 ASMX 中做的那样。我们做许多其他协议。根据 MSDN，所有不同端点的分类说明如下：

- *BasicHttpBinding*: 适用于与符合 WS-Basic Profile 的 Web 服务通信的绑定（例如基于 ASMX 的服务）。该绑定使用 HTTP 作为传输，使用 text/XML 作为默认编码。
- *WSHttpBinding*: 一个安全且可操作的绑定，适用于非双工服务契约。
- *DualHttpBinding*: 一个安全且可操作的绑定，适用于双工服务契约或通过 SOAP 中间件通信。
- *WSFederationBinding*: 一个安全且可操作的绑定，支持 WS-Federation 协议，该协议允许联邦组织高效地对用户进行身份验证和授权。
- *NetTcpBinding*: 用于 WCF 应用程序之间跨机器通信的安全优化的绑定。
- *NetNamedPipeBinding*: 一个安全、可靠且优化的绑定，适用于 WCF 应用程序之间的机器内通信。
- *NetMmqBinding*: 一个安全、可靠且优化的绑定，适用于 WCF 应用程序之间的机器内通信。
- *NetMmqBinding*: 一个安全、可靠且优化的绑定，适用于 WCF 应用程序之间的跨机器通信。
- *NetPeerTcpBinding*: 一种启用安全多机器通信的绑定。
- *NetsmIntegrationBinding*: 适用于 WCF 应用程序与消息队列（Message Queuing）跨机器通信的绑定。
- *BasicHttpPostBinding*: 适用于与符合 WS-Basic Profile 的 Web 服务通信的绑定，允许使用 HTTP 用于交换上下文。
- *NetTcpBinding*: 用于 WCF 应用程序之间跨机器通信的安全优化绑定，允许使用 SOAP 用于交换上下文。
- *HttpBinding*: 用于配置通过 HTTP 而不是 SOAP 消息暴露的 WCF 服务端点的绑定。
- *WSHttpBinding*: 一个安全且可操作的绑定，适用于非双工服务契约，允许使用 SOAP 头用于交换上下文。

你何时使用哪一个？如果你想使用 .NET 应用程序或单个应用程序，请使用 NetTcpBinding。如果你是跨平台的，请使用 HttpBinding。只有当由于某些原因这些不起作用时，你才开始考虑其他的。或者，记住你可能对同一个服务有许多许多端点。如果你需要跨平台支持，就不要使用 SOAP 层。

| 第七卷 | 第3章 |
| :--- | :--- |
| 使用 WCF 构建 Web 服务 | |

# 754 创建一个 WCF 服务

![](img/36596fb11aa4233d5cab0d6ddd1d2e8_779_0.png)

图 3-5：服务配置编辑器。

使用服务配置编辑器添加服务似乎比应该的复杂。只需按照以下步骤操作：

1. 点击“文件...”，打开项目的 Web.config，导航到你的 Web.config。
2. 选择“文件” -> “添加新服务”。
3. 点击“浏览”，如果使用了了命名，则找到编译后的 SHARPService.dll。
4. 双击 DLL，服务就会显示出来。如图 3-6 所示，点击 Registration 服务。点击“打开”和“下一步”。
5. 确认服务契约（看吧，我告诉过你以后会很有用的！）。
6. 点击“下一步”。

在绑定配置窗口中，你会明白我所说的选项数量之多。选择“现有绑定（Existing Binding）”单选按钮并查看列表。列表中的项目在侧边栏“使用不同的端点”中有所介绍。现在，接受默认值。
7. 点击“下一步”。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_780_0.png)

图 3-6：相关的服务。

8. 在端点地址中，为了本次演示之目的，输入 http://localhost/。
9. 在确认窗口上点击“完成”。
10. 完成后，SHARPService.Registration 下会出现一个没有名称的端点。你可以点击此端点并添加名称，例如 SharpHttp。端点面板如图 3-7 所示。
11. 选择“保存”，然后关闭配置编辑器。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_780_1.png)

图 3-7：完成的端点。

| 第七卷 | 第3章 |
| :--- | :--- |
| 使用 WCF 构建 Web 服务 | |

# 756 创建一个 WCF 服务

回到 Visual Studio，通过双击解决方案管理器中的 Web.config 文件用代码编辑器打开。你会发现 ServiceModel 部分已根据你的新端点进行了编辑。代码如下：

```xml
<system.serviceModel>
  <services>
    <service name="SHARPService.Registration">
      <clear />
      <endpoint address="http://localhost" binding="basicHttpBinding" bindingConfiguration="SharpHttp" contract="SHARPService" />
    </service>
  </services>
  <behaviors>
    <behavior>
      <!-- 为了避免泄露元数据，将下面的值设置为 false 并在部署前移除元数据端点 -->
      <serviceMetadata endpointEnabled="true" />
      <!-- 为了调试接收异常详情，将下面的值设置为 true。部署前设置为 false 以避免显示异常信息。 -->
      <serviceDebug includeExceptionDetails="false" />
    </behavior>
  </behaviors>
</system.serviceModel>
```

现在，在代码中做这些会更容易吗？也许吧。为什么还需要服务编辑器？因为当你有很多绑定时，那里可能会变得非常混乱。查看其他绑定的侧边栏以了解。

# 部署

如果你使用 IIS 托管服务，WCF 的部署与 ASMX 相同。你可以有效地将 .svc 和配置文件与编译后的二进制文件一起拷贝到运行的 Web 应用程序中。

在 Visual Studio 2010 中更好的部署方法是使用发布工具。如果你右单击项目并选择“发布”，你就可以设置一个可重复的配置文件，这样你就不会忘记任何事情。（图 3-8）。

此面板执行了你必须手动完成的所有工作：

- 设置服务的 URL
- 命名应用程序（在 IIS 站点属性中）
- 设置凭据
- 拷贝正确的文件


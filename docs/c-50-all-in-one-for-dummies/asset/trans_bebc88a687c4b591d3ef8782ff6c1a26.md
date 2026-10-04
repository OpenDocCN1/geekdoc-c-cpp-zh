

# 772 创建一个 WCF 服务

```csharp
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
```

现在已经有一个类可以使用，是时候创建服务了。

- 6. 右键点击 SharpService 项目并添加一个新的 WCF 服务。

我将我的服务命名为 Registration.svc。

- 7. 删除模板方法并添加以下代码：

与 ASMX 示例不同，这并不是一个运行的版本；你只是在设置一个模拟（mock）回复。

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

- 8. 右键点击 Registration.svc 文件并选择“设为启动页”。

- 9. 按 F5 运行项目。

注意到 ASP.NET 开发服务器正在运行，但你的浏览器并没有打开。WCF 测试客户端取代了 ASMX 的开发测试页面。它允许你添加请求值并查看响应值是什么，而无需依赖 HTTP。

这是为什么呢？WCF 允许你使用 HTTP（Web 的基础协议）以外的其他协议传输消息细节。（你可以在侧边栏的“使用端点”中找到一些示例。）

# 配置

WCF 的唯一缺点是配置。因为 WCF 是 Windows 中远程过程调用的终极解决方案，有足够的配置选项来处理一切。有时会让人有点烦躁。

# 创建一个 WCF 服务

# 使用不同的端点

WCF 的核心意义在于你可以编写一个服务，并让 IIS 在同一代码上接受所有不同的协议。当然，我们可以像在 ASMX 中那样使用 SOAP。我们还可以使用许多其他协议。以下是根据 MSDN 对所有不同端点的分类说明：

- BasicHttpBinding：适用于与符合 WS-Basic Profile 的 Web 服务通信（例如 ASP.Net Web 服务或基于 ASMX 的服务）。该绑定使用 HTTP 作为传输，并使用 XML 作为默认编码。

- WSHttpBinding：一种安全且互操作的绑定，适用于双工（duplex）服务合约，且不需要双向通信的情况。

- WSDualHttpBinding：一种安全且互操作的绑定，适用于双工服务合约或通过 SOAP 中间件通信。

- WSFederationBinding：一种安全且互操作的绑定，支持 WCF-Federation 协议，该协议允许联盟中的组织高效地对用户进行身份验证和授权。

- NetTcpBinding：安全且优化的绑定，适用于 WCF 应用程序之间的跨机器通信。

- NetNamedPipeBinding：可靠且优化的绑定，适用于 WCF 应用程序之间的本机通信。

- NetMsmBinding：队列绑定，适用于 WCF 应用程序之间的跨机器通信。

- NetPeerTcpBinding：一种启用安全多机器通信的绑定。

- MsmIntegrationBinding：适用于 WCF 应用程序与现有消息队列（Message Queuing）应用程序之间的跨机器通信。

- BasicHttpContextBinding：适用于与符合 WS-Basic Profile 的 Web 服务通信，允许使用 HTTP Cookie 来交换上下文。

- NetTcpBinding：安全且优化的绑定，适用于 WCF 应用程序之间的跨机器通信，允许使用 SOAP 头来交换上下文。

- WebBinding：用于配置通过 HTTP 请求而非 SOAP 消息暴露的 WCF Web 服务端点。

- WSHttpClientBinding：一种安全且互操作的绑定，适用于非双工服务合约，允许使用 SOAP 头来交换上下文。

那么什么时候该用什么呢？如果你想让 .NET 应用程序进行通信，或者单个应用程序各层之间的通信，请使用 NetTcpBinding。如果你是在进行跨平台通信，请使用 WSHttpBinding。

只有当由于某些原因这些对你不起作用时，才考虑其他的。哦，请记住同一个服务可以有多个端点。不要在数据层使用 SOAP。如果你需要跨平台支持，只需单独建立一个 SOAP 层即可。

书籍第 3 章 使用 WCF 构建 Web 服务

![](img/6df7bb88e9302e98442acc219cfbd7fc_798_0.png)

# 774 创建一个 WCF 服务

幸运的是，有一个服务配置编辑器（Service Configuration Editor）。如图 3-5 所示，服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

![](img/6df7bb88e9302e98442acc219cfbd7fc_799_0.png)

图 3-5：
服务配置编辑器。

使用服务配置编辑器添加服务端点似乎比应有的要复杂。只需遵循步骤操作：

- 1. 通过选择“文件：打开”并导航到你的 Web.config 打开项目。
- 2. 在主窗口中，点击“新建服务”（New Service）。
- 3. 双击服务（Service）。
- 4. 如图 3-6 所示，点击端点（endpoint）。
- 5. 在端点地址中输入 `http://localhost/`。
- 6. 确认合约（contract）。
- 7. 点击下一步（Next）。
- 8. 点击端点。
- 9. 在绑定（binding）中输入 `SharpHttp`。
- 10. 点击完成（Finish）。
- 11. 点击端点并添加名称。
- 12. 选择“文件：保存”并关闭编辑器。

编辑器打开了。

它应该在 ServiceModel 中。这就是我说的选项。端点如图 3-7 所示。服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

端点位于 Model 中。

使用服务配置编辑器添加服务端点似乎比应有的要复杂。只需遵循这些步骤：

- 1. 通过选择“文件：打开”并导航到你的 Web.config 打开项目配置。
- 2. 在主窗口中，点击新建服务。
- 3. 双击服务。
- 4. 如图 3-6 所示，点击端点。
- 5. 在端点地址中输入 `http://localhost/`。
- 6. 确认合约。
- 7. 点击下一步。
- 8. 点击端点。
- 9. 在绑定中输入 `SharpHttp`。
- 10. 点击完成。
- 11. 点击端点并添加名称。
- 12. 选择“文件：保存”并关闭编辑器。

编辑器打开了。

它应该在 ServiceModel 中。这就是我说的选项。端点如图 3-7 所示。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

服务配置编辑器允许你管理 WCF 核心力量的复杂选项。

端点位于 Model 中。

# 776 创建一个 WCF 服务

回到 Visual Studio 世界，通过双击打开 Web.config 文件。你会看到 ServiceModel 已经随你的新端点包含进来。代码如下：

```xml
xml version="1.0"?>
<configuration>
  <appSettings>
    <add key="aspnet:UseFriendlySynchronizationContext" value="true" />
  </appSettings>
  <system.web>
    <compilation debug="true" targetFramework="4.5" />
    <httpRuntime targetFramework="4.5" />
  </system.web>
  <system.model>
    <services>
      <service name="SharpService.Registration">
        <endpoint address="http://localhost/" binding="basicHttpBinding" bindingConfiguration="SharpHttp" contract="SharpService.Registration" />
      </service>
    </services>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <!-- 为了避免披露元数据信息，部署前将以下值设置为 false -->
          <serviceMetadata enabled="true" httpGetEnabled="true" />
          <!-- 为了在调试时从故障中接收异常详细，将以下值设置为 true。部署前设置为 false 以避免异常信息 -->
          <serviceDebug includeExceptionFaults="false" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <behaviors>
      <protocolMappings>
        <protocolMapping>
          <add binding="basicHttpBinding" scheme="https" />
        </protocolMapping>
      </protocolMappings>
      <serviceHostEnvironment netCompatibilityEnabled="true" multipleSiteBindingEnabled="true" />
    </system.model>
  <system.webserver>
    <modules managedModulesForAllRequests="true" />
    <!---->
    <!-- 调试期间显示 Web 根目录，将以下值设置为 true。部署前设置为 false 以避免披露 文件夹信息 -->
    <directoryBrowse enabled="true" />
  </system.webserver>
</configuration>
```

# 775 创建一个 WCF 服务

![](img/6df7bb88e9302e98442acc219cfbd7fc_800_0.png)

**图 3-6:** 选择端点。

此属性唯一地标识给定合约的端点。每个定义必须是：

书籍第 3 章 使用 WCF 构建 Web 服务


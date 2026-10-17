
这个示例显然是非常不安全的，不会在生产环境中使用 —— 它仅仅检查用户名和密码是否相同。如果验证失败，则会抛出 `SecurityTokenException`，表示用户名和密码无法通过验证。

### 3. 一旦你有了自定义验证器，你就需要通过配置文件将其连接到 WCF 中。同样，配置设置是服务行为的一部分。服务项目和编辑器的 `web.config` 文件应如下：

```xml
<serviceBehaviors>
    <behavior name="WCFSecurity.EchoServiceBehavior">
        <serviceMetadata httpGetEnabled="false" httpsGetEnabled="true" />
        <serviceDebug includeExceptionDetailFaults="false" />
        <serviceCredentials>
            <userNameAuthentication userNameValidationMode="Custom" userNamePasswordValidatorType="
```

# 第 11 章 与 Windows 通信基础 共享数据

```
"WCFSecurity.CustomValidator, WCFSecurity/ \
<serviceCredentials>
</behavior>
</serviceBehaviors>
```

你可以看到，你已经添加了 `serviceCredentials` 部分，并使用全限定名及其包含的程序集指定了自定义的 `userNameValidatorType`。

### 4. 现在运行你的测试，看看当用户名和密码相同时，或者当不匹配时会发生什么。

你现在已经学习了面向 Internet 的服务的身份验证选项，但内网场景又是怎样的呢？对于内网，用户通常位于活动目录 `Active Directory` 中，使用 Web 服务的凭据是合理的，这与 IIS 中的集成身份验证工作方式是一样的。

# 尝试为内网服务添加身份验证

将身份验证类型更改为使用当前用户的 Windows 凭据涉及两处更改：服务器端和客户端各。

### 1. 在服务器端，你必须更改 `web.config` 文件中的绑定，并将消息的 `client-credentialType` 切换为 `Windows`，如下：

```xml
<wsHttpBinding>
  <binding name="wsHttp" hostComparisonMode="Exact">
    <security mode="TransportWithMessageCredential">
      <transport clientCredentialType="None" />
      <message clientCredentialType="Windows" />
    </security>
  </binding>
</wsHttpBinding>
```

### 2. 在客户端，你必须在它的 `app.config` 文件中进行相同的更改。一旦完成此操作，你就可以移除客户端应用程序中设置凭据的代码，因为将使用你的 Windows 凭据。运行测试应用程序，你将看到即使在代码中没有指定凭据，你也通过了 WCF 服务的验证。

当然，身份验证只是故事的一半。你可能需要实现良好的授权。一旦服务身份验证了用户，你就可以判断该用户是否允许执行所请求的操作。例如，你可以编写一个允许发布的 Web 服务。

# 尝试使用角色授权服务

将身份验证类型更改为使用当前用户的 Windows 凭据涉及两处更改：服务器端和客户端各。

### 1. 在服务器端，你必须更改 `web.config` 文件中的绑定，并将消息的 `client-credentialType` 切换为 `Windows`，如下：

```xml
<wsHttpBinding>
  <binding name="wsHttp" hostComparisonMode="Exact">
    <security mode="TransportWithMessageCredential">
      <transport clientCredentialType="None" />
      <message clientCredentialType="Windows" />
    </security>
  </binding>
</wsHttpBinding>
```

### 2. 在客户端，你必须在它的 `app.config` 文件中进行相同的更改。一旦完成此操作，你就可以移除客户端应用程序中设置凭据的代码，因为将使用你的 Windows 凭据。运行测试应用程序，你将看到即使在代码中没有指定凭据，你也通过了 WCF 服务的验证。

当然，身份验证只是故事的一半。你可能需要实现良好的授权。一旦服务身份验证了用户，你就可以判断该用户是否允许执行所请求的操作。例如，你可以编写一个允许发布的 Web 服务。

# 尝试使用角色授权服务

为了让 WCF 使用角色，你必须配置身份验证。

### 1. 在 `web.config` 中通过 `httpGetEnabled="false"` 和 `httpsGetEnabled="true"`，配置如下：

```xml
<serviceBehaviors>
    <behavior name="WCFSecurity.EchoServiceBehavior">
        <serviceMetadata httpGetEnabled="false" httpsGetEnabled="true" />
        <serviceDebug includeExceptionDetailFaults="false" />
        <serviceCredentials>
            <userNameAuthentication userNameValidationMode="Custom" userNamePasswordValidatorType="
```

### 2. 按照如下代码使用 `WCFSecurity.CustomValidator, WCFSecurity/` 所在的程序集：

```
"WCFSecurity.CustomValidator, WCFSecurity/ \
<serviceCredentials>
</behavior>
</serviceBehaviors>
```

你可以看到，你已经添加了 `serviceCredentials` 部分，并使用全限定名及其包含的程序集指定了自定义的 `userNameValidatorType`。

### 3. 现在运行你的测试，看看当用户名和密码相同时，或者当不匹配时会发生什么。

你现在已经学习了面向 Internet 的服务的身份验证选项，但内网场景又是怎样的呢？对于内网，用户通常位于活动目录 `Active Directory` 中，使用 Web 服务的凭据是合理的，这与 IIS 中的集成身份验证工作方式是一样的。

# 使用 WCF 消息签名

为了提供更细粒度的保护，可以在接口级别或数据合约级别通过对适当部分设置 `ProtectionLevel` 来配置 WCF 消息级保护。

在本章开始的原始示例中，你如下定义了服务合约：

```csharp
[ServiceContract]
public interface IEchoService
{
  [OperationContract]
  string Echo(string message);
}
```

要对服务的所有消息进行签名，可以在服务合约中添加 `ProtectionLevel` 设置（此时默认值为 `EncryptAndSign`）：

```csharp
[ServiceContract(ProtectionLevel = ProtectionLevel.Sign) ]
public interface IEchoService
{
  [OperationContract]
  string Echo(string message);
}
```

如果你想对消息的所有部分进行签名，可以将 `ProtectionLevel` 属性应用于 `OperationContract` 特性，所示：

```csharp
[ServiceContract(ProtectionLevel = ProtectionLevel.Sign)]
public interface IEchoService
{
  [OperationContract(ProtectionLevel = ProtectionLevel.Sign)]
  string Echo(string message);
}
```

如果你使用消息合约 `message contracts`，可以进行更细粒度的操作，对消息合约的不同部分进行签名或加密签名，所示：

```csharp
[MessageContract(ProtectionLevel = ProtectionLevel.EncryptAndSign)]
public class Order
{
  [MessageHeader(ProtectionLevel = ProtectionLevel.Sign)]
  public string From;
  [MessageBodyMember(ProtectionLevel = ProtectionLevel.EncryptAndSign)]
  public string PaymentDetails;
}
```

一旦你为合约装饰了 `ProtectionLevel` 特性，就必须选择正确的绑定、带有客户端身份验证的消息级传输。你可以通过 WCF 服务配置编辑器 `WCF Service Configuration Editor` 完成，或者在配置文件的绑定部分手动设置 `clientCredentialType`。你还必须为服务器选择一个要使用的证书，这与 IIS 使用的 HTTPS 配置无关。

证书的私钥必须对运行服务的账户可访问。你可以通过启动 `MMC` 并为本地计算机 `Local Computer` 添加证书单元来实现来实现。

右键点击证书，选择所有任务 `All Tasks` -> 管理私钥 `Manage Private Key`，并向适当的用户授予“读取” `Read` 权限。然后你可以在绑定配置中指定该证书。

默认情况下，WCF 会尝试将客户端映射到 Windows 账户，但对于面向公众的网站，这可能不是你想要的。你可以通过将 `clientCertificate` 行为的 `mapClientCertificate` 属性设置为 `false` 来控制这一点。

下面的配置文件显示了使用客户端证书进行消息安全的适当配置，其中禁用了 Windows 账户映射。服务器证书通过其名称（在本例中为 `wrox-vpc`）找到。

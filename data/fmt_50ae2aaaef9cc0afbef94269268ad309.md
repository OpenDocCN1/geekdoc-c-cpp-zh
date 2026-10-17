
```csharp
System.Web.ConfigurationManager.OpenWebConfiguration(webPath);

// 从文本框创建新的连接字符串
ConnectionStringSettings newConnSetting = new 
    ConnectionStringSettings(txtName.Text, txtValue.Text, txtProvider.Text);
try
{
    // 将连接字符串添加到集合中
    config.ConnectionStrings.ConnectionStrings.Add(newConnSetting);
    // 保存更改
    config.Save();
}
catch (ConfigurationErrorException cex)
{
    lblStatus.Text = "Status: " + cex.ToString();
}
catch (System.UnauthorizedAccessException uex)
{
    // ASP.NET 进程帐户必须对该目录具有读/写权限
    lblStatus.Text = "Status: " + "The ASP.NET process account must have" + 
    "read/write access to the directory";
}
catch (Exception eEx)
{
    lblStatus.Text = "Status: " + eEx.ToString();
}
// 重新加载列表框连接字符串
ShowConnectionStrings();
}
```

## 操作 machine.config 文件

`System.Configuration.ConfigurationManager` 类的 `OpenMachineConfiguration` 方法提供了一种操作 `machine.config` 文件的方法。`OpenMachineConfiguration` 方法是一个静态方法。

列表 33-36 显示了一个简单的示例，描述了 `machine.config` 文件中所有的节组（section groups）。所示，你使用 `OpenMachineConfiguration` 方法获取配置对象的实例。然后你将 `SectionGroups` 集合绑定到 `GridView` 控件。

### 列表 33-36：来自 machine.config 的配置组

```vbnet
Protected Sub Button2_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    ' 列出 machine.config 文件中所有的 SectionGroups
    Dim configSetting As Configuration = 
        System.Configuration.ConfigurationManager.OpenMachineConfiguration()
GridView.DataSource = configSetting.SectionGroups
GridView.DataBind()
End Sub
```

```csharp
protected void Button2_Click(object sender, EventArgs e)
{
    // 列出 machine.config 文件中所有的 Groups
    Configuration configSetting =
    System.Configuration.ConfigurationManager.OpenMachineConfiguration();
    GridView.DataSource = configSetting.SectionGroups;
    GridView.DataBind();
}
```

同样，你可以使用集合列出所有的配置节（sections），如列表 33-37 所示。

### 列表 33-37：来自 machine.config 的配置节

```vbnet
Protected Sub Button2_Click(ByVal sender Object, ByVal e As System.EventArgs)
    ' 列出 machine.config 文件中所有的 Groups
    Dim configSetting As Configuration =
    System.Configuration.ConfigurationManager.OpenMachineConfiguration()
    GridView.DataSource = configSetting.Sections
    GridView.DataBind()
End Sub
```

```csharp
protected void Button2_Click(object sender, EventArgs e)
{
    // 列出 machine.config 文件中所有的 Groups
    Configuration configSetting =
    System.Configuration.ConfigurationManager.OpenMachineConfiguration();
    GridView.DataSource = configSetting.Sections;
    GridView.DataBind();
}
```

## 从远程服务器操作 web.config

ASP.NET 管理对象提供了一种从远程服务器读取配置信息的方法。

例如，如果你想操作位于虚拟 `Optra.Microsoft.com` 站点的 `Expense` Web 配置文件，可以参考列表 33-38。

### 列表 33-38：操作远程服务器的 web.config 文件

```vbnet
// 连接到 Optra.Microsoft.com 服务器上的 Web 应用程序 Expense
Dim configSetting As Configuration =
System.Configuration.ConfigurationManager.OpenWebConfiguration("/*Expense", "1", "Optra.Microsoft.com")
Dim section As System.Configuration.ConfigurationSection =
configSetting.GetSection("AppSettings")
Dim element As KeyValueConfigurationElement =
CType(configSetting.AppSettings.Settings("keySection"),
KeyValueConfigurationElement)
If element Is Nothing Then
    Dim Value As String = "New Value"
    element.Value = value
    Try
        config.Save()
    Catch ex As Exception
        Response.Write(ex.Message)
    End Try
End If
```

### 列表 33-38（继续）

```csharp
// 连接到 Optra.Microsoft.com 服务器上的 Web 应用程序 Expense
Configuration configSetting = 
    System.Web.Configuration.WebConfigurationManager.OpenWebConfiguration(
    "/Expense", "1", "Optra.Microsoft.com");
ConfigurationSection section = configSetting.GetSection("appSettings");
KeyValueConfiguration element =
    configSetting.Settings["keySection"];
if (element == null)
{
    string value = "New Value";
    element.Value = value;
    try
    {
        configSetting.Save();
    }
    catch (Exception ex)
    {
        Response.Write(ex.Message);
    }
}
```

列表 33-38 中的代码演示了如何连接到远程服务器。然后你更改特定的 `appSettings` 为新值并保存更改。

## 配置设置

当 ASP.NET 1.0 引入时，所有配置都以明文格式存储。自 ASP.NET 1.1 起获得了一种使用数据保护 API（或 DPAPI）在注册表中存储配置的新方法。例如，列表 33-39 显示了如何在注册表中内部存储用户名和密码。

### 列表 33-39：在注册表中存储用户名和密码

```xml
<processModel
    userName="registry:HKLM\SOFTWARE\ExampleApp\Identity\ASPNET_SETREG"
    password="registry:HKLM\SOFTWARE\ExampleApp\Identity\ASPNET_SETREG"/>
```

ASP.NET 4 包含一个保护配置中敏感数据的系统。由于此原因，ASP.NET 将这些项存储为人类或机器都无法读取的格式。

配置文件中最需要加密的节之一是 `<connectionStrings>` 节。列表 33-40 显示了一个明文连接字符串的 `web.config` 示例。

### 列表 33-40：web.config 中暴露连接字符串

```xml
<?xml version="1.0"?>
<configuration>
  <appSettings />
  <connectionStrings>
    <add name="AdventureWorks"
      connectionString="Server=localhost;Integrated=True;Database=AdventureWorks"
      providerName="System.Data.SqlClient" />
  </connectionStrings>
  <system.web>
    <compilation debug="false" />
    <authentication mode="Forms">
      <forms name="Wrox" loginURL="Login.aspx" path="Clear" />
      <credentials>
        <user name="BillEvjen" password="Bubbles" />
      </credentials>
    </forms>
  </authentication>
  </system.web>
</configuration>
```

在这种情况下，你想加密此数据库连接字符串。为了实现这一点，ASP.NET 提供了一个工具 `aspnet_regiis.exe`。你可以在 `C:\WINDOWS\Microsoft\.NETFramework\v4.0.21006` 找到它。使用该工具加密节时，打开命令提示符并导航到 `C:\WINDOWS\Microsoft\.NETFramework\v4.0.21006`。另一个选项是打开 Visual Studio 2010 命令提示符。在进入这些环境之一后，使用列表 33-41 所示的语法来加密 `<connectionStrings>` 节。

### 列表 33-41：加密 <connectionStrings> 节

```bash
aspnet_regiis -pe "connectionString-app /EncryptionExample"
```

运行此构建脚本将产生图 33-6 所示的结果。

## 1276 | 第 33 章 配置

![](img/7040c21013b8e6c23c612d6da3599ff8_1335_0.png)

图 33-6

查看加密过程中使用的脚本，你可以看到 `-pe` 命令指定了 `web.config` 文件中需要加密的节，而 `-app` 命令则指定了实际要操作的应用程序。如果你回到 `web.config` 文件并检查已发生的加密操作，你将看到与列表 33-42 中的代码类似的内容。

### 列表 33-42：web.config 文件中加密的 <connectionStrings> 节

```xml
<?xml version="1.0"?>
<configuration>
<appSettings/>
<connectionStrings configProtectionProvider="RsaProtectedConfigurationProvider">
<EncryptedData Type="http://www.w3.org/2001/04/xmlenc#Element"
  xmlns="http://www.w3.org/2001/04/xmlenc#">
<EncryptionMethod
Algorithm="http://www.w3.org/2001/04/xmlenc#triples-cbc" />
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#" id="1">
<EncryptedKey xmlns="http://www.w3.org/2001/04/xmlenc#">
  Algorithms="http://www.w3.org/2001/04/xmlenc#rsa-1-5" />
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<KeyAlgorithm Name="RsaRSA"/>
</KeyInfo>
</EncryptedKey>
</KeyInfo>
<CipherData>
<CipherValue>
09BFXQ0CDXm0vaVO0crBFA65
UbYvUbNs77OSQ79YAAxcKGGT7Alqlgi
M2bZG0GZ1Elc7a93ggNCNn
hcYG8HOYF942HAYdCCR5
5KX5YLI7f869-KU
0oAGVHuCau8gBQWQEb13tFUS/8cLOWP8=</CipherValue>
</CipherData>
<EncryptedKey>
<CipherValue>03/PtxajkDVD/57JLGdd1cgRF81h7dls</CipherValue>
</EncryptedKey>
</EncryptedData>
</connectionStrings>
<system.web>
  <compilation debug="false" />
  <authentication mode="Forms">
    <forms name="root" loginURL="Login.aspx" path="/" />
    <credentials passwordFormat="Clear">
      <user name="Bill" password="Bubbles" />
    </credentials>
  </authentication>
</system.web>
</configuration>
```

现在当你在 ASP.NET 应用程序中使用连接字符串时，查看 `web.config` 文件，你可以看到 `<system.web>` 节内部有一个子节，以明文形式暴露了用户名和密码。这也是你可能想要保持加密的内容，以避免它们出现在你的视野中。因为它是一个子节，请使用列表 33-43 中的脚本。

### 列表 33-43：加密 <authentication> 节

```bash
aspnet_regiis -pe "system.web" -app "EncryptionExample"
```

此代码产生如列表 33-44 所示的结果。

### 列表 33-44：加密 web.config 文件的节

```xml
<authentication configProvider="RSAProtectedConfigurationProvider">
<EncryptedData Type="http://www.w3.org/2001/04/xmlenc#Element"
  xmlns="http://www.w3.org/2001/04/xmlenc#">
<EncryptionMethod
Algorithm="http://www.w3.org/2001/04/xmlenc#triples-cbc" />
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<EncryptedKey xmlns="http://www.w3.org/2001/04/xmlenc#">
  Algorithms="http://www.w3.org/2001/04/xmlenc#rsa-1-5" />

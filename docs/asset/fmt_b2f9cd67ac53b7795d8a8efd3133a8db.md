
# 列表 28-30：在 ExampleApplication 网站上安装 .NET 版本 2.0

```
C:\WINDOWS\Microsoft\Framework\v2.0.50729>asnet regiis -s W3SVC/ROOT/ExampleApplication
```

## 编程配置文件

ASP.NET 包含了 API（ASP.NET 管理对象），用于操作 `machine.config` 和 `web.config` 文件中的配置信息设置。ASP.NET 管理对象提供了一种强类型编程模型，用于处理 .NET Web 应用程序服务器的管理事务。它们管理着 ASP.NET Web 配置的创建和维护。使用 ASP.NET 管理对象，你可以操作存储在本地或远程计算机配置文件中的配置信息。这些对象可以用于任何常见管理任务的脚本编写或编写安装脚本。

所有的 ASP.NET 管理对象都存储在 `System.Configuration` 和 `System.Web.Configuration` 命名空间中。你可以使用 `WebConfigurationManager` 类访问配置。`System.Configuration.Configuration` 类表示来自机器和分级配置文件的配置设置的合并视图。`System.Configuration` 和 `System.Web` 命名空间包含多个类，允许你访问配置文件中提供的几乎所有设置。`System.Configuration` 和 `System.Web` 命名空间之间的主要区别是，`System.Configuration` 命名空间包含适用于所有 .NET 程序的类；而 `System.Web` 命名空间包含仅适用于 ASP.NET 应用程序的类。表 28-1 显示了 `System.Configuration` 中的重要类及其用途。

### 表 28-1

| 类名 | 用途 |
| --- | --- |
| `Configuration` | 允许你操作存储在本地或远程计算机中的配置 |
| `ConfigurationElementCollection` | 允许你枚举配置文件内部的子元素 |
| `AppSettingsSection` | 允许你操作配置文件的 `<AppSettings>` 部分 |
| `ConnectionStringsSettings` | 允许你操作配置文件的 `<connectionStrings>` 部分 |
| `ProtectedConfigurationSection` | 允许你操作配置文件的 `<protectedConfiguration>` 部分 |
| `ProtectedDataSection` | 允许你操作配置文件的 `<protectedData>` 部分 |

表 28-2 显示了来自 `System.Web.Configuration` 命名空间的的一些类及其用途。

### 表 28-2

| 类名 | 用途 |
| --- | --- |
| `AuthenticationSection` | 允许你操作配置文件的 `<authentication>` 部分 |
| `AuthorizationSection` | 允许你操作配置文件的 `<authorization>` 部分 |

## 常见配置设置

- `CompilationSection`：允许你操作配置文件的 `<compilation>` 部分
- `CustomErrorsSection`：允许你操作配置文件的 `<customErrors>` 部分
- `FormsAuthenticationConfiguration`：允许你操作配置文件的 `<forms>` 部分
- `GlobalizationSection`：允许你操作配置文件的 `<globalization>` 部分
- `HttpHandlersSection`：允许你操作配置文件的 `<httpHandlers>` 部分
- `HttpModulesSection`：允许你操作配置文件的 `<httpModules>` 部分
- `HttpRuntimeSection`：允许你操作配置文件的 `<httpRuntime>` 部分
- `MachineKeySection`：允许你操作配置文件的 `<machineKey>` 部分
- `MembershipSection`：允许你操作配置文件的 `<membership>` 部分
- `PagesSection`：允许你操作配置文件的 `<pages>` 部分
- `ProcessModelSection`：允许你操作配置文件的 `<processModel>` 部分
- `WebPartsSection`：允许你操作配置文件的 `<webParts>` 部分

所有的配置类都实现在一个简单的基于面向对象的架构上，该架构包含一个持有所有数据的实体类，以及一个具有添加、删除、枚举等方法的集合类。你可以从一个简单的连接字符串枚举开始你的配置文件编程，如下所示。

## 枚举连接字符串

在 Web 应用程序中，你可以存储多个连接字符串。其中一些由系统使用，另一些可能是特定应用程序使用的。你可以编写一个非常简单的 ASP.NET 应用程序来枚举存储在 `web.config` 文件中的所有连接字符串，如列表 28-32 所示。

### 代码列表 28-32: web.config 文件

```xml
<?xml version="1.0" ?>
<configuration>
  <appSettings>
    <add key="symbolServer" value="192.168.1.1" />
  </appSettings>
  <connectionStrings>
    <add name="ExampleApplication"
      connectionString="server=ExampleApplicationServer;database=ExampleApplicationDB;uid=WebUser;pwd=P$$swordD9"
      providerName="System.Data.SqlClient"; />
  </connectionStrings>
  <system.web>
    <compilation debug="false" targetFramework="4.5" />
    <authentication mode="None" />
  </system.web>
</configuration>
```

如列表 28-32 所示，一个应用程序设置指向符号服务器，有一个连接字符串存储在 Web.config 文件中。使用 `System.Web.ConfigurationManager` 的 `ConnectionStrings` 集合来读取连接字符串，如列表 28-33 所示。

### 代码列表 28-33: 将 ConnectionStrings 集合属性绑定到 GridView 控件

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    GridView1.DataSource = System.Web.ConfigurationManager.ConnectionStrings["localhost"];
    GridView1.DataBind();
}
```

`System.Web.ConfigurationManager` 的 `ConnectionStrings` 属性返回一个 `Configuration` 类的实例。因此，你只是将该属性绑定到 GridView 控件。图 28-4 显示了存储在 ASP.NET 中的连接字符串列表。在运行时添加连接字符串也是一项非常简单的任务。如果你像列表 28-33 所示那样操作，你将获得一个配置对象的实例。然后创建一个新的 `ConnectionStringSettings`。将新类添加到集合中并调用 `update` 方法。列表 28-34 显示了 VB 和 C# 的示例。

## 列表 28-34（续）

```csharp
// 将连接字符串添加到集合中
config.ConnectionStrings.ConnectionStrings.Add(new ConnSetting());

// 保存更改
config.Save();

} catch (ConfigurationErrorsException cEx) {
    lbl1Status.Text = "Status: " + cEx.ToString();
} catch (System.UnauthorizedAccessException uEx) {
    // ASP.NET 进程帐户必须对目录具有
    // 读写权限
    lbl1Status.Text = "status: " + "The ASP.NET process account must have " + 
        "read/write access to the directory";
} catch (Exception eEx) {
    lbl1Status.Text = "Status: " + eEx.ToString();
}

// 重新加载列表框中的连接字符串
ShowConnectionStrings();

protected void ShowConnectionStrings() {
    GridView1.DataSource = System.Web.Configuration.WebConfigurationManager.ConnectionStrings;
    GridView1.DataBind();
}
```

## 操作 machine.config 文件

`System.Configuration.ConfigurationManager` 类的 `OpenMachineConfiguration` 方法提供了操作 machine.config 文件的方法。`OpenMachineConfiguration` 方法是一个静态方法。

列表 28-35 显示了一个简单的示例，它列出了存储在 machine.config 文件中的所有节组。如列表所示，你使用 `OpenMachineConfiguration` 方法获取配置对象的实例。然后你将 `SectionGroups` 集合绑定到 `GridView` 控件。

## 列表 28-35：来自 machine.config 的配置组

VB

```vb
Protected Sub Page_Load(sender As Object, e As EventArgs)
    ' 列出 machine.config 中所有的 SectionGroups
    Dim configSetting As Configuration = 
    System.Configuration.ConfigurationManager.OpenMachineConfiguration()
    GridView1.DataSource = configSetting.SectionGroups
    GridView1.DataBind()
End Sub
```

C#

```csharp
protected void Page_Load(Object sender, EventArgs e)
{
    // 列出 machine.config 中所有的 SectionGroups
    Configuration configSetting = 
        System.Configuration.ConfigurationManager.OpenMachineConfiguration();
    GridView1.DataSource = configSetting.SectionGroups;
    GridView1.DataBind();
}
```

## 普通配置设置

## 保护配置设置

ASP.NET 使用数据保护 API（或 DPAPI）在注册表中存储配置信息。例如，列表 28-36 显示了你如何在注册表中存储进程模型的用户名和密码信息。

列表 28-36：在注册表中存储用户名和密码，然后在 machine.config 文件中引用这些设置

```xml
<processModel
  username="registry:HKLM\SOFTWARE\ExampleApp\Identity\ASNET_SETREG,username"
  password="registry:HKLM\SOFTWARE\ExampleApp\Identity\ASNET_SETREG,password"
/>
```

ASP.NET 4.5 包含了一套保护存储在配置系统中的敏感数据的系统。它使用行业标准的 XML 加密来加密包含任何敏感数据的配置节。

开发者通常对于将连接字符串、密码等敏感项目直接存放在 web.config 文件中感到忧虑。出于这个原因，ASP.NET 能够以一种格式存储这些项目，在不熟悉加密过程中所使用的加密技术和密钥的情况下，任何人类或机器进程都无法读取它们。

web.config 文件中加密程度最高的项目之一是 `<connectionStrings>` 节。列表 28-37 显示了一个暴露连接字符串的 web.config 文件示例。

列表 28-37：在 web.config 文件中暴露的标准连接字符串

```xml
<?xml version="1.0"?>
<configuration>
  <appSettings>
    <connectionStrings>
      <add name="AdventureWorks"
           connectionString="Server=localhost;Integrated Security=True;Database=AdventureWorks"
           providerName="System.Data.SqlClient" />
    </connectionStrings>
    <system.web>
      <compilation debug="false" />
      <authentication mode="Forms">
        <forms name="Wrox" loginUrl="Login.aspx" path="/" />
        <credentials password format="Clear" />
        <user name="JasonDaylord-Reindeer" />
      </credentials>
      </authentication>
    </system.web>
</configuration>
```

在这种情况下，你可能想要加密此数据库数据库字符串。为了实现这一点，你可以在 `C:\Windows\Microsoft\.Framework\v4.0.3019` 找到它。要使用此加密 `<connectionStrings>` 节，请打开命令提示符并使用 `cd C:\Windows\Microsoft\.Framework\v4.0.3019` 进入指定文件夹。另一个选项是以管理员身份使用 Visual Studio 2012 命令提示符。如果是其中之一，你可以使用列表 28-38 中显示的语法来加密 `<connectionStrings>` 节。

## 列表 28-38：加密 <connectionStrings> 节

```bash
aspnetregiis -pe "connectionStrings" -app /EncryptionExample
```

运行这段脚本会产生图 28-5 所示的结果。

```
Administrator Developer Command Prompt for VS2012
C:\>aspnetregiis -pe "connectionStrings" -app /EncryptionExample
distributed (C) Microsoft Corporation. All rights reserved.
The utility to install and uninstall ASP.NET was not found.
Encrypting connectionStrings. Success.
C:\>
```

查看加密过程中使用的脚本，可以看到 `-pe` 命令指定 web.config 文件中的节，而 `-app` 命令指定要操作的应用程序。查看 web.config 文件，你会看到类似于图 28-5 的内容。

## 列表 28-39：web.config 中加密的 <connectionStrings> 节

```xml
<?xml version="1.0"?>
<configuration>
  <connectionStrings configProvider="RSAProtectedProvider">
```

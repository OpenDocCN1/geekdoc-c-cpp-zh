

# 注释

您需要使用管理员权限打开 Visual Studio 2010 才能创建虚拟目录。

9. 打开 SimpleInterestService 应用程序的 web.config 文件，并在其中添加第 19.9 节所示的代码：

# 第 19.9 节：显示 SimpleInterestService 应用程序的 web.config 文件的代码

```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0" />
  </system.web>
  <system.serviceModel>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <!-- To avoid disclosing metadata information, set the value below to false and remove the metadata endpoint above before deployment -->
          <serviceMetadata httpGetEnabled="true" />
          <!-- To receive exception details in faults for debugging purposes, set the value below to true. Set to false before deployment to avoid disclosing exception information -->
          <serviceDebug includeExceptionDetailInFaults="false" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <serviceHostingEnvironment multipleSiteBindingsEnabled="true" />
  </system.serviceModel>
  <system.webServer>
    <modules>
      <add name="ScriptModule" preCondition="integratedMode" type="System.Web.Handlers.ScriptModule, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35" />
    </modules>
    <handlers>
      <remove name="WebServiceHandlerFactory-Integrated" />
      <add name="ScriptHandlerFactory" verb="*" path="*.asmx" preCondition="integratedMode" type="System.Web.Script.Services.ScriptHandlerFactory, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35" />
      <add name="ScriptHandlerFactoryAppServices" verb="*" path="*_AppService.axd" preCondition="integratedMode" type="System.Web.Script.Services.ScriptHandlerFactory, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35" />
      <add name="ScriptResource" preCondition="integratedMode" verb="GET,HEAD" path="ScriptResource.axd" type="System.Web.Handlers.ScriptResourceHandler, System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35" />
    </handlers>
    <directoryBrowse enabled="true" />
  </system.webServer>
</configuration>
```

10. 通过选择 Build→Build Solution（或按 Ctrl+Shift+B）来构建 SimpleInterestService 应用程序，以创建 WCF 服务。

11. 在运行命令框中输入 inetmgr 打开 IIS 管理器窗口。

12. 在连接窗格中展开 <machine_name>→Sites→Default Web Site，以查看 SimpleInterestService 应用程序，如图 19.32 所示：

# 第 19 章：使用 Windows Communication Foundation

![](img/e073a4882197be4ab61103cbe0bcb394_1027_0.png)

**图 19.32：显示 IIS 管理器窗口中的 SimpleInterestService 应用程序**

13. 在 IIS 管理器窗口的连接窗格中选择 `SimpleInterestService` 应用程序并双击目录浏览图标（图 19.32）。目录浏览窗格出现，如图 19.33 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1027_1.png)

**图 19.33：为 SimpleInterestService 应用程序启用目录浏览**

14. 在操作窗格中单击启用链接以启用浏览 `SimpleInterestService` 应用程序的目录或文件夹。

15. 打开位于 `C:\Windows\System32\inetsrv\config` 文件夹中的 `applicationHost.config` 文件并更改以下值：

+   - 在 `<section name="handlers" overrideModeDefault="Deny" />` 部分中，将 `overrideModeDefault` 的值更改为 `Allow`。
+   - 在 `<section name="modules" allowDefinition="MachineToApplication" overrideModeDefault="Deny" />` 中，将 `overrideModeDefault` 的值更改为 `Allow`。

16. 打开 Web 浏览器（Internet Explorer）并在浏览器的地址栏中输入 http://localhost/SimpleInterestService。输出如图所示 19.34：

![](img/e073a4882197be4ab61103cbe0bcb394_1028_0.png)

# 图 19.34：显示 SimpleInterestService 应用程序的输出

在图 19.34 中，您可以看到 SimpleInterestService 应用程序的内容以链接的形式显示。如果您单击 Service1.svc 链接，则会显示 WCF 服务，如图 19.35 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1028_1.png)

# 图 19.35：单击 Service1.svc 链接时显示的输出

# 注释

IIS 主机的 WCF 服务只能使用 HTTP 传输协议。

创建 WCF 服务后，让我们学习如何使用它。

# 调用 WCF 服务

在前面的章节中，您已经了解了可用于托管 WCF 服务的不同托管选项。如果您在客户端使用 WCF 服务，则可以使用 Svcutil.exe 工具生成代理类来调用 WCF 服务。要调用 WCF 服务，您需要创建并配置客户端。借助此客户端，您可以调用 WCF 服务的操作。现在，让我们先学习如何创建 WCF 客户端。

# 创建 WCF 客户端

WCF 客户端是调用 WCF 服务的应用程序。让我们执行以下步骤来创建 WCF 客户端：

+   1. 打开 Microsoft Visual Studio 2010。
+   2. 选择 File→New→Web Site 以打开新建网站对话框。
+   3. 从新建网站对话框的模板部分选择 ASP.NET Web Site 模板，并在 Web 位置组合框中输入网站的名称 MyFirstWCFClient（也可在 CD 上获得）及其位置。
+   4. 单击确定按钮创建新的 WCF 客户端，如图 19.36 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1029_0.png)

# 图 19.36：显示新建网站对话框

+   4. 打开 MyFirstWCFClient 网站的 Default.aspx 文件并用第 19.10 节所示的代码替换现有代码：

# 第 19.10 节：显示 Default.aspx 文件的代码

```
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
<h2>
<style type="text/css">
.style1 {
    width: 100%;
}
.style2
{
    width: 142px;
}
.style3
{
```

```
width: 75px;
}
.style4
{
    width: 96px;
}
.style5
{
    width: 111px;
}
</style>
</h2>
<div>
<table class="style1">
<tr>
<td class="style2">
<asp:Label ID="Label1" runat="server" Text="Enter a Number"></asp:Label>
</td>
<td>
<asp:TextBox ID="txtfirst" runat="server"></asp:TextBox>
</td>
</tr>
<tr>
<td class="style2">
<asp:Label ID="Label3" runat="server" Text="Output" Visible="False"></asp:Label>
</td>
<td>
<asp:Label ID="lbloutput" runat="server" Text="Label" Visible="False"></asp:Label>
</td>
</tr>
<tr>
<td class="style2">&nbsp;</td>
<td>&nbsp;</td>
</tr>
</table>
</div>
<table class="style1">
<tr>
<td class="style3">
<asp:Button ID="btnsqr" runat="server" onclick="btnsqr_Click" Text="Square" Width="103px" />
</td>
<td class="style4">
<asp:Button ID="btncube" runat="server" style="margin-left: 0px" Text="Cube" Width="103px" onclick="btncube_Click" />
</td>
<td class="style5">&nbsp;</td>
<td>&nbsp;</td>
</tr>
</table>
</asp:Content>
```

7. 打开 Default.aspx.cs 文件并添加 System.ServiceModel 命名空间，如以下代码片段所示：

```
using System.ServiceModel;
```

使用 WCF 服务需要在您想要调用服务的应用程序中添加 WCF 服务的引用，并为客户端生成代理代码和 .config 文件，我们接下来将探讨这一点。

# 添加 WCF 服务的引用

创建 WCF 客户端后，您可以向客户端添加 WCF 服务的引用。在我们的例子中，我们通过在 MyFirstWCFClient 网站中添加服务的 .svc 文件来添加 WCF 服务的引用。为此，在解决方案资源管理器中右键单击 MyFirstWCFClient 网站并选择添加服务引用选项。这将打开添加服务引用对话框。

在添加服务引用对话框的地址文本框中，输入您的 WCF 服务的 URL 并单击转到按钮。您可以在服务框中看到您的 WCF 服务，并在操作框中看到其方法列表。现在，将服务引用的名称从 ServiceReference1 更改为 MyWCFServiceReference 并单击确定按钮，如图 19.37 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1031_0.png)

图 19.37：显示添加服务引用对话框

> 注释
> 在应用程序中添加服务引用之前，您需要先构建应用程序。

现在，您需要使用 svcutil.exe 文件生成代理代码。

# 生成代理代码

.NET Framework 3.5 和 4.0 服务器开发工具包（SDK）提供了一种通过 Svcutil.exe 文件构建客户端代理（从服务提供的元数据自动生成的代码）的方法。使用 Svcutil.exe 文件，您可以生成代表客户端代理代码的 .cs 文件和包含客户端配置详细信息的 .config 文件。让我们执行以下步骤来使用 Svcutil.exe 文件：

+   1. 打开 Visual Studio 2010 命令提示符并输入以下命令：

```
svcutil.exe /language:cs /out:MyWCFClient.cs /config:MyWCFClient.config http://localhost:6485/MyFirstWCFService/Service.svc
```

+   2. 按 ENTER 键。上述命令生成两个文件，MyWCFClient.cs 和 MyWCFClient.config，如图 19.38 所示：




```
minRequiredNonAlphanumericCharacters="0" passwordAttemptWindow="10" applicationName="/"/>
</providers>
</membership>
<profile>
  <providers>
    <clear/>
    <add name="AspNetSqlProfileProvider"
         type="System.Web.Profile.SqlProfileProvider"
         connectionStringName="ApplicationServices" applicationName="/"/>
  </providers>
</profile>
<roleManager enabled="false">
  <providers>
    <clear/>
    <add name="AspNetSqlRoleProvider"
         type="System.Web.Security.SqlRoleProvider"
         connectionStringName="ApplicationServices" applicationName="/"/>
    <add name="AspNetWindowsTokenRoleProvider"
         type="System.Web.Security.WindowsTokenRoleProvider"
         applicationName="/"/>
  </providers>
</roleManager>
</system.web>
<system.webServer>
  <modules runAllManagedModulesForAllRequests="true"/>
</system.webServer>
<system.serviceModel>
  <behaviors>
    <serviceBehaviors>
      <behavior name="MyServiceTypeBehaviors">
        <serviceMetadata httpGetEnabled="true"/>
      </behavior>
    </serviceBehaviors>
    <endpointBehaviors>
      <behavior name="OperationServiceAspNetAjaxBehavior">
        <enableWebScript/>
      </behavior>
    </endpointBehaviors>
  </behaviors>
  <serviceHostingEnvironment aspNetCompatibilityEnabled="true" multipleSiteBindingsEnabled="true"/>
  <services>
    <service name="OperationService" behaviorConfiguration="MyServiceTypeBehaviors">
      <endpoint address="" behaviorConfiguration="OperationServiceAspNetAjaxBehavior" binding="webHttpBinding" contract="OperationService"/>
      <endpoint contract="IMetadataExchange" binding="mexHttpBinding" address="mex"/>
    </service>
  </services>
</system.serviceModel>
</configuration>
```

5. 运行 OperationService 服务。运行 OperationService 服务时，会出现一条消息“You have created a service”，如图 19.44 所示；

## OperationService 服务

你已创建了一个服务。要测试此服务，你需要创建一个客户端并使用它调用该服务。你可以使用命令行中的 svcurl.exe 工具来完成此操作

```
svcurl.exe http://localhost:1980/MyAjaxEnableWCFService/OperationService.svcws
```

这将生成一个配置文件和一个包含客户端类的代码文件。将这两个文件添加到你的客户端应用程序中，并使用生成的客户端类调用服务。

```
class Test
{
    static void Main()
    {
        HelloClient client = new HelloClient();
        client.ClientCredentials.UserName.UserName = "value";
        client.ClientCredentials.UserName.Password = "value";
        client.Close();
    }
}
```

## 图 19.44：创建 ASP.NET AJAX 启用的 WCF 服务

创建 WCF 服务后，需要调用它以使用其指定的操作。你可以通过创建客户端并使用客户端脚本调用 OperationService 服务来调用 WCF 服务。

## 从客户端脚本调用 WCF 服务

创建 WCF 服务后，你可以从客户端脚本（如 JavaScript）调用它。让我们执行以下步骤从客户端脚本调用 WCF 服务。

- 1. 将如清单 19.15 所示的代码添加到 Default.aspx 页面，以设计客户端页面的接口，并添加用于调用 WCF 服务方法的脚本：

## 清单 19.15：显示调用 WCF 服务方法的代码

```
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<%@ Import Namespace="System.ServiceModel" %>
<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <style type="text/css">
        .style1
        {
            width: 95%;
        }
        .style5
        {
            width: 115px;
        }
        #button1
        {
            width: 56px;
        }
    </style>
```

```
.style7
{
    width: 449px;
}
</style>
<div>
<h1>AJAX-Enable WCF Service </h1>
    <table class="style1">
        <tr>
            <td class="style5">
                First Number:</td>
            <td class="style7">
                <input type="text" id="Number1" /></td>
        </tr>
        <tr>
            <td class="style5">
                Second Number:</td>
            <td class="style7">
                <input type="text" id="Number2" /></td>
        </tr>
        <tr>
            <td class="style5">
                Result:</td>
            <td class="style7">
                <input type="text" id="result" /></td>
        </tr>
        <tr>
            <td class="style5">
                <input id="Button1" type="button" value="Add" onclick="return callAdd()" />
            </td>
            <td class="style7">
                <input id="Button2" type="button" value="Subtract" onclick="return callSub()" /></td>
        </tr>
        <tr>
            <td class="style5">
                <input id="Button3" type="button" value="Multiply" onclick="return callMul()" /></td>
            <td class="style7">
                <input id="Button4" type="button" value="Divide" onclick="return callDiv()" /></td>
        </tr>
    </table>
&nbsp;
</div>
<asp:ScriptManager ID="ScriptManager1" runat="server">
    <services>
        <asp:servicereference Path="OperationService.svc" />
    </services>
</asp:ScriptManager>
<script language="javascript" type="text/javascript">
    function callAdd() {
        var Number1 = document.getElementById("Number1").value;
        var Number2 = document.getElementById("Number2").value;
        var service = new tempuri.org.OperationService();
        service.Add(parseFloat(Number1), parseFloat(Number2), onsuccess, null, null);
    }
    function callSub() {
```

```
var Number1 = document.getElementById("Number1").value;
var Number2 = document.getElementById("Number2").value;
var service = new tempuri.org.OperationService();
service.Subtract(parseFloat(Number1), parseFloat(Number2), onSuccess, null, null);
}
function callMul() {
var Number1 = document.getElementById("Number1").value;
var Number2 = document.getElementById("Number2").value;
var service = new tempuri.org.OperationService();
service.Multiply(parseFloat(Number1), parseFloat(Number2), onSuccess, null, null);
}
function callDiv() {
var Number1 = document.getElementById("Number1").value;
var Number2 = document.getElementById("Number2").value;
var service = new tempuri.org.OperationService();
service.Divide(parseFloat(Number1), parseFloat(Number2), onSuccess, null, null);
}
function onSuccess(result) {
document.getElementById("result").value = result;
}
</script>
</asp:Content>
```

Default.aspx 页面的设计视图出现，如图 19.45 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1040_0.png)

图 19.45：显示 Default.aspx 文件的设计视图

- 2. 将 MyAjaxEnableWCFService 网站的 Default.aspx 文件设为你的主页。

- 3. 按 F5 键或从菜单栏中选择 Debug→Start Debugging 选项来运行应用程序。MyAjaxEnableWCFService 网站的输出出现，如图 19.46 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1041_0.png)

图 19.46：显示 MyAjaxEnableWCFService 网站的输出

现在，你可以执行 OperationService 服务中指定的操作，例如加法、减法、乘法和除法。

## 摘要

在本章中，你学习了 WCF 服务。你还学习了 WCF 服务的实例化模型。接下来，你学习了 WCF 架构。此外，你学习了 WCF 端点，包括端点地址、绑定、服务契约、行为、WCF 服务配置、WCF 客户端、WCF 服务标识以及 WCF 与 ASP.NET AJAX 的集成。最后，你学习了如何创建 WCF 服务并使用 ASP.NET AJAX 调用它。

在下一章中，你将学习 Windows 服务。


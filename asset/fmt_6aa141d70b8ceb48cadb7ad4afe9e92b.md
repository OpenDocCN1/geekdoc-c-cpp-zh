
```xml
<xml version="1.0"?>

<configuration>
  <configSections>
    <sectiongroup name="web.extensions"
      type="System.Web.Configuration.SystemWebExtensionsSectionGroup,
System.Web.Extensions,Version=3.5.0,Culture=neutral,
PublicKeyToken=31B3F856AD3643E35">
      <sectiongroup name="scripting"
        type="System.Web.Configuration.ScriptingSectionGroup,
System.Web.Extensions,Version=3.5.0,Culture=neutral,
PublicKeyToken=31B3F856AD3643E35">
        <section name="scriptResourceHandler"
          type="System.Web.Configuration.ScriptingHttpResourceHandlerSection,
System.Web.Extensions,Version=3.5.0,Culture=neutral,
PublicKeyToken=31B3F856AD3643E35"
          allowDefinitions="false"/>
      </sectiongroup>
      <sectiongroup name="webServices"
        type="System.Web.Configuration.ScriptingServicesSectionGroup,
System.Web.Extensions,Version=3.5.0,Culture=neutral,
PublicKeyToken=31B3F856AD3643E35">
        <section name="jsonSerialization"
          type="System.Web.Configuration.ScriptingJsonSerializationSection,
System.Web.Extensions,Version=3.5.0,Culture=neutral,
PublicKeyToken=31B3F856AD3643E35"
          requirePermission="false"
          allowDefinition="Everywhere" />
        <section name="profileService"
          type="System.Web.Configuration.ScriptingProfileServiceSection,
System.Web.Extensions,Version=3.5.0,Culture=neutral,
PublicKeyToken=31B3F856AD3643E35"
          requirePermission="false"
          allowDefinitions="MachineToApplication" />
      </sectiongroup>
      <section name="authenticationService"
        type="System.Web.Configuration.ScriptingAuthenticationServiceSection,
System.Web.Extensions,Version=3.5.0,Culture=neutral;
PublicKeyToken=31BF3856AD364E35"
        requirePermission="false"
        allowDefinition="MachineToApplication" />
      <section name="roleService"
        type="System.Web.Configuration.
ScriptingRoleServiceSection,
System.Web.Extensions, Version=3.5.0.0,
Culture=neutral;
PublicKeyToken=31BF3856AD364E35"
        requirePermission="false"
        allowDefinition="MachineToApplication" />
    </section>
  </configSections>

<!-- 为了清晰起见删除了配置 -->

</configuration>
```

`web.config` 文件就绪后（由 ASP.NET Web Site 类型提供），下一步是构建一个不使用 AJAX 的简单 ASP.NET 页面。

## 构建不使用 AJAX 的简单 ASP.NET 页面

要构建一个不使用 ASP.NET 3.5 提供的 AJAX 能力的简单页面，你的页面只需要一个 `Label` 控件和一个 `Button` 服务器控件。页面代码位于列表 19-2 中。

### 列表 19-2：一个不使用 AJAX 的简单 ASP.NET 3.5 页面

```vb
<@ Page Language="VB" %>

<script runat="server">
Protected Sub Button1_Click(ByVal sender As Object,
ByVal E As System.Events.EventArgs)

	Label1.Text = DateTime.Now.ToString()
End Sub</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
	<title>My Normal ASP.NET Page</title>
</head>
<body>
	<form id="form1" runat="server">
	<div>
		<asp:Label ID="Label1" runat="server"></asp:Label>
		<br />
	<br />
		<asp:Button ID="Button1" ID="Button1" runat="server" 
            Text="Click to get machine time" 
            onclick="Button1_Click" />
	</div>
	</form>
</body>
</html>
```

```csharp
<%@ Page Language="C#" %>

<script runat="server">
protected void Button1_Click(object sender, EventArgs e)
{
    Label1.Text = DateTime.Now.ToString();
}
</script>
```

# 第 19 章：ASP.NET AJAX

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_940_0.png)

图 19-9

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_940_1.png)

图 19-10

当你首次从列表 19-4 提取页面时，该页面的代码与不使用 AJAX 构建的代码有很大不同。列表 19-5 显示了你将看到的页面结果。

# 列表 19-5：使用页面的输出

```
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>
My ASP.NET AJAX Page
</title></head>
<body>
<form name="form1" method="post" action="Default.aspx"
id="form1">
<div>
<input type="hidden" name="__EVENTTARGET" id="__EVENTTARGET"
value="" />
<input type="hidden" name="__EVENTARGUMENT" id="__EVENTARGUMENT"
value="" />
<input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE"
value="fEPDWULLTE4NZe5Ntc5mRkEZRIHzHPQg4Ga09Hox9A/RnOf1m" />
</div>

<script type="text/javascript">
//<![CDATA[
var form = document.forms['form1'];
if (form) {
Form = document.form;
}

doPostBack(eventTarget, eventArgument)
if (!form.onsubmit || (form.onsubmit !== false)) {
form__EVENTTARGET.value = eventTarget;
form__EVENTARGUMENT.value = eventArgument;
}
form.submit();
}
//]]>
</script>

<script src="AJAXWebsite/WebResource.axd?d=084nEjJ-
4cYI0WgPFXCg2amp;t=633825032854684000
type="text/javascript"></script>

<script src="AJAXWebsite/ScriptResource.axd?d=dETFHs584D5pxXqHI6EM05YqRK2K0YMoAgraYEDUS
gISumL2lGTQRaWB56SI50jJRQe01VI8SIYDjmYmpFP0
CoW8fKKJKw2MeI1amp;t=63328503850530400
type="text/javascript"></script>
<script type="text/javascript">
//<![CDATA[
if (typeof(Sys) === 'undefined') throw Error('ASP.NET AJAX
client-side
framework failed to load.');
}
//]]>
</script>
```

```
<script src="AJAXWebSite/Resource.axd
d=FEtH554Dpx8XqhM5SYKYR2GkMoAYYEDUS
gilSum2qc7rQRTRBA6617AYfRVaIRCo023xw23JTIC
t92e-U0qfrP30mEjYjs90UUIxl89jPTJKLRI0k0ap;t=63328053850304000*
type="javascript"></script>
<div>
<script type="javascript">
//<![CDATA[>
Sys.Forms.PageRequest.initialize('ScriptManager1',
document.getElementById('form'));
Sys.Forms.PageRequest.getInstance().updateControls(['UpdatePanel'],
[], 90);
//]]>
</script>
<span id="Label2"></span>
<br />
<input type="submit" name="Button1"
value="Click to get machine time"
id="Button1" />
<br />
<div id="UpdatePanel1">
<span id="Label2"></span>
<br />
<input type="submit" name="Button2"
value="Click to get machine
time using AJAX" id="Button2" />
</div>
<div>
<input type="hidden" name="__EVENTVALIDATION"
id="__EVENTVALIDATION"
value="wEWAWLktbDDGGkMr4GBb7qN57VIQM2sRDfn0sgWQK" />
</div>
<script type="javascript">
//<![CDATA[>
Sys.Application.initialize();
//]]>
</script>
</form>
</body>
</html>
```

在这里，如果你点击 `Button1` 执行全页回传（postback），你会在响应中得到这段代码，尽管你只想更新页面的部分！但是，如果你点击 `Button2` —— AJAX 按钮——你会发送列表 19-6 所示的请求。

# 列表 19-6：来自 ASP.NET 页面的异步请求

```
POST /AJAXWebSite/Default.aspx HTTP/1.1
Accept: */
Accept-Language: en-US
Referer: http://localhost:62203/AJAXWebSite/Default.aspx
AXAX: true
Content-Type: application/x-www-form-encoded; charset=utf-8
Content-Cache: no
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 7.0; Windows 6.0); .NET 2.0.5072; .NET 1.1.1432; .NET 3.5.21004; .NET 3.0.0456
host: localhost:62203
Content-Length: 33
Connection: Keep-Alive
Pragma: no-cache
ScriptManager|UpdatePanel|Button2__EVENTTARGET=__EVENTARGUMENT=__VIEWSTATE=UpdatePanel|5MtCQBYCAQZEAEPGMDxCHGRUZh0QQMSMS8zIwDMcmQjXNo1SB0TRWHKZIzQQGz25E87libYbruJuk1MyMDA5AwCdkXNojAgYg1b847as3g=Click to get time AJAX
```

该请求的响应如列表 19-7 所示。

# 列表 19-7：来自 ASP.NET AJAX 的异步响应

```
HTTP/1.1 200 OK
Server: ASP.NET Developer/9.0.0
Date: Sat, 03 Nov 2007 19:17:58 GMT
X-Aspnet-Version: 2.0.5027
Cache-Control: private
Content-Type: text/plain; charset=utf-8
Content-Length: 796
Connection: Close
updatePanel|<span id="panel2">11/3/2007 2:17:58 PM</span>
<br />
<input type="submit" name="Button2"
value="Click to get time using AJAX" id="Button2" />
```

（注：列表 19-6 和 19-7 的 OCR 文本包含大量的交叉/乱码；这些基于标准的 HTTP 请求/响应结构以及文中提供的上下文重建的。）

下表描述了随 ASP.NET 3.5 提供的新的 ASP. AJAX 服务器控件。

| ASP.NET AJAX 控件 | 描述 |

| --- | --- |

| ScriptManager | 管理向需要部分更新的页面部分服务器标记消息的组件。每个 ASP.NET 页面都需要一个 ScriptManager 控件才能工作。注意的是，一个页面上只能有一个 ScriptManager 控件。 |

| ScriptManagerProxy | 作为内容页的 ScriptManager 控件的组件。位于内容页（或子页）上的 ScriptManagerProxy 控件与位于主页上的必需 ScriptManager 控件协同工作。 |

| Timer | Timer 控件会间隔执行客户端事件，并允许页面的特定部分在这些时刻进行更新或刷新。 |

| UpdatePanel | 定义页面上启用与 ScriptManager 工作的特定区域。这些区域反可以执行部分页面回并在并在 ASP.NET 页面之外更新自身。 |

# ASP.NET AJAX 的服务器端控件

当你在 Visual Studio 2008 工具箱中查看 AJAX 扩展服务器时，你会发现有很多控件可供使用。控件侧重于允许你启用 ASP.NET 应用程序。它们是启用控件。如果你正在寻找利用新 AJAX 模型的更具体的服务器控件，请查看 ASP.NET AJAX Control Toolkit —— 这是下一章将介绍的独立下载项目。

从列表 19-7 中，你可以看到响应比整个 Web 页面小得多！事实上，响应的主要部分仅包含在 `UpdatePanel` 服务器控件中的代码，不再更多。底部的项目处理页面的状态（因为它现在已经改变）以及一些其他页面变化。

# 第19章：ASP.NET AJAX


# PasswordStrength 控件

`PasswordStrength` 控件允许你检查 `TextBox` 中的密码内容并验证其强度。它还会向用户提供有关强度是否合理的消息。列表 19-41 展示了 `PasswordStrength` 控件的一个简单示例。

文件名 `NoBot.aspx.vb` 和 `NoBot.aspx.cs`

## 示例 19-41：在 TextBox 控制中使用 PasswordStrength 控制

```csharp
<@ Page Language="C# %>

<@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Password Strength Control</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ToolkitScriptManager ID="ToolkitScriptManager1" runat="server" />
<asp:ToolkitScriptManager />
<asp:PasswordStrength ID="PasswordStrength" runat="server"
TargetControlID="TextBox1">
<asp:TextBox ID="TextBox1" runat="server" />
</asp:PasswordStrength>
</div>
<br />
</form>
</body>
</html>
```

这个非常简单的页面显示了一个文本框，当用户开始在文本框中输入内容时，他们将根据输入情况实时收到提交内容的强度通知。这如图 19-42 所示。

在这里使用的一些重要属性包括：
`MinimumLowerCaseCharacters`（最小小写字母数）、`MinimumNumericCharacters`（最小数字数）、`MinimumSymbolCharacters`（最小符号数）、`MinimumUppercaseCharacters`（最小大写字母数）以及 `PreferredLength`（理想长度）。

## 评分控制 (Rating Control)

评分控制允许用户查看和设置评分（如星级评分）。你可以控制评分的数量、填充评分的外观、空闲评分的外观等。
示例 19-42 显示了一个五星评分系统，赋予用户自己设置评分的能力。

| | |
|---|---|
| aaa | 强度弱 |
| aa123 | 强度中等 |
| aaa1234K | 强度不可破解 |

图 19-42

## 示例 19-42：用户可以操作的评分控制

```csharp
<@ Page Language="C# %>

<@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Rating Control</title>
<style type="text/css">
.ratingStar {
font-size: 0pt;
width: 12px;
height: 12px;
margin: 0px;
padding: 0px;
cursor: pointer;
display: block;
background-repeat: no-repeat;
}
.filledRating {
  background-image: url(Images/FilledStar.png);
}
.emptyRating {
  background-image: url(Images/EmptyStar.png);
}
.savedRating {
  background-image: url(Images/SavedStar.png);
}
</style>
</head>
<body>
<div>
  <form id="form" runat="server">
    <asp:ToolkitScriptManager ID="ToolkitScriptManager1" runat="server">
    </asp:ToolkitScriptManager>
    <asp:Rating ID="Rating1" runat="server"
    StarClassName="savedRating"
    FilledStarClassName="filledStar"
    EmptyStarClassName="emptyRating">
    </asp:Rating>
  </div>
</form>
</body>
</html>
```

在这里，`Rating` 控制使用一组 CSS 类来定义其在不同区域的视觉效果。通过 `StarCssClass`、`FilledStarClass` 和 `EmptyCssClass`，你还可以指定评分、评分数量（默认为 5）、当前评分等。示例 19-42 中提供的代码生成的结果如图 19-43 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_860_0.png)

图 19-43

## TabContainer 控制

`TabControl` 和 `TabPanel` 控制使得标签页界面（tabbed UI）的呈现变得简单。用户跨越面板查看一组标签的内容。当用户选择一个标签时，内容会发生变化。Tabs 非常适合控制具有一组标签页的页面。`TabControl` 可以包含一个或多个 `TabPanel`，每次显示一组标签的内容。

`TabControl` 允许你触发 `ActiveTabChanged` 事件，该事件在回传（Postback）期间触发。你也可以使用 `OnClientTabChanged` 事件在用户选择不同标签时触发 JavaScript。`ScrollBars` 属性允许你决定控件应该是水平（Horizontal）、垂直（Vertical）、无（None）或自动（Auto），这控制了滚动行为。

`TabPanel` 拥有用于标签的 `<HeaderTemplate>` 和用于正内容的 `<ContentTemplate>`。你可以省略 `HeaderText` 属性。它还有一个在标签被选中时触发的 `OnClick` 事件。Tabs 的一个特别有趣的功能是在 JavaScript 中通过将 `Enabled` 属性设置为 `False` 来禁用标签。

示例 19-43 显示了一个带有三个 `TabPanel` 控件的 `TabContainer` 示例。

## 示例 19-43：在 TabContainer 控制中显示三个标签

```csharp
<@ Page Language="C#" %>
<% Register Assembly="AjaxControlToolkit" 
Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>TabContainer Control</title>
</head>
<body>
<form id="form" runat="server">
<div>
  <asp:ToolkitScriptManager Id="ToolkitScriptManager1" runat="server"></asp:ToolkitScriptManager>
  <asp:TabContainer Id="TabContainer1" runat="server"
    Height="300px">
    <asp:TabPanel runat="server">
      <HeaderTemplate>标签 1</HeaderTemplate>
      <ContentTemplate>
        这是标签1的内容。
      </ContentTemplate>
    </asp:TabPanel>
    <asp:TabPanel runat="server">
      <HeaderTemplate>标签 2</HeaderTemplate>
      <ContentTemplate>
        这是标签2的内容。
      </ContentTemplate>
    </asp:TabPanel>
    <asp:TabPanel runat="server">
      <HeaderTemplate>标签 3</HeaderTemplate>
      <ContentTemplate>
        这是标签3的内容。
      </ContentTemplate>
    </asp:TabPanel>
  </asp:TabContainer>
</div>
</form>
</body>
</html>
```

图 19-44 展示了此操作的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_861_0.png)

图 19-44

## 20 安全

本章包含内容：

- 使用基于 Windows 和基于表单的身份验证
- 管理程序化授权
- 通过 IIS 实现安全

并不是用 ASP.NET 构建的每个页面都要向所有人开放并可访问。有时，你希望构建只有特定群体可以访问的页面或应用程序部分。因此，你需要本章解释的安全措施。它们可以帮助保护应用程序数据以及应用程序本身免受欺诈使用。

安全是一个非常广泛的术语。在应用程序构建的每一步，你都必须意识到恶意用户可能会尝试绕过你的锁定措施。你必须采取措施确保没有人可以接管应用程序或访问其资源。无论是涉及基本服务器控件的操作还是访问数据库，都应该考虑你想要使用的安全级别。

如何将安全应用于你的应用程序确实是一个权衡的过程。例如，互联网上一个公开访问的 ASP.NET 页面与仅供特定个人使用的或处理信用卡号、医疗信息的 ASP.NET 应用程序具有不同的安全要求。

第一步是为当前任务应用适当的安全级别。由于你可以采取许多操作来保护你的应用程序和资源，你必须决定采用哪些措施。本章介绍了保护应用程序的可能性。

请注意，书中范围内都在讨论安全问题。此外，还有几个章节关注 ASP.NET 提供的特定安全框架，这些内容在本章中未讨论。第 14 章和第 15 章讨论了 ASP.NET 的成员和角色管理框架，以及此版本的个性化功能。这些主题是让构建安全应用程序变得更容易的安全方面。尽管最新版本的 ASP.NET 提供了这些安全框架，但你仍然可以像以前的 ASP.NET 版本那样构建自己的措施。本章讨论了如何这样做。

### 总结

ASP.NET AJAX 控制使得添加丰富的动画和交互性变得简单。除了可以使用 `UpdatePanel` 向用户显示正在进行异步处理外，Toolkit 还有助于模糊桌面应用程序和 Web 应用程序之间的区别。

如你所见，有许多控件供你选择。可用 AJAX 控件列表将继续增长。

本章探索了许多 ASP.NET AJAX 控件以及如何在你的应用程序中使用它们。记得经常访问微软关于这些控件的页面，并利用最新的产品。

你可以在应用程序的 `web.config` 文件中使用 `<authentication>` 节点来设置 ASP.NET 应用程序所需的验证类型：

```xml
<system.web>
  <authentication mode="Windows|Forms|Passport|None">
  </authentication>
</system.web>
```

`<authentication>` 节点使用 `mode` 属性来设置要使用的验证形式。选项包括 Windows、Forms、Passport 和 None。每个选项在表 20-1 中均有解释。

## 表 20-1

| 提供程序 | 描述 |
|---|---|
| Windows | Windows 验证与 IIS 验证一起使用。验证由 IIS 通过以下方式执行：基本（basic）、摘要（digest）或集成验证（Integrated）。ASP.NET 使用验证后的身份来授权访问。这是默认设置。 |
| Forms | 未验证的请求将重定向到使用 HTTP 客户端重定向的 HTML 表单，用户在其中提供登录信息并提交表单。如果应用程序验证了请求，系统将创建一个包含凭据或身份所需的密钥的问题。 |
| Passport | Microsoft 提供的集中验证服务为成员站点提供单点登录和核心配置文件服务。这种验证模式在 2005 年底被微软不再重视。 |
| None |此设置下无任何验证。 |

如你所见，你有几种方法可以为 ASP.NET 应用程序构建验证/授权模型。下一节将检查 Windows 验证模式。

## 基于 Windows 的验证

基于 Windows 的验证处理在 ASP.NET 应用程序所在的服务器和客户端计算机之间。在基于 Windows 的验证模型中，请求发送到 IIS 以提供验证过程。这种验证在内网环境中非常有用，你可以让服务器完全处理验证过程——特别是在用户已经登录的环境中。在这种情况下，你只需获取并使用已有的凭据进行验证过程即可。

IIS 从域登录中获取用户的凭据。如果此过程失败，IIS 将显示弹出对话框，让用户输入或重新输入其登录信息。要设置你的 ASP.NET 应用程序与基于 Windows 的验证工作，请从创建用户和组开始。

你可以使用基于 Windows 的验证允许具有域登录的特定用户访问你的应用程序或部分应用程序。由于可以使用这种验证，ASP.NET 与部署在内网环境中的应用程序配合非常容易。如果用户已以域用户身份登录本地计算机，那么当他访问该计算机上的网络计算机时，无需验证。

以下步骤显示了如何创建用户。如果你有权创建用户，创建用户的步骤如下：

- 1. 在你的 Windows XP 或 Windows Server 2003 服务器上，选择“开始 > 控制面板 > 管理工具 > 计算机管理”。如果你使用的是 Windows 7，选择“开始 > 控制面板 > 系统和安全 > 管理工具 > 计算机管理”。这会打开计算机管理实用程序。它管理并控制本地 Web 服务器上的资源。你可以使用此工具完成许多工作，但这里的重点是创建用户。
- 2. 展开“系统工具”节点。
- 3. 展开“本地用户和组”节点。
- 4. 选择“用户”文件夹。你会看到类似于图 20-2 所示的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_867_0.png)

图 20-2

- 5. 右键点击“用户”文件夹并选择“新建用户”。
出现“新建用户”对话框，如图 20-3 所示。
- 6. 给用户用户名、密码，并在描述中说明这是一个测试用户。在此示例中，该用户名为 Bubbles。
- 7. 取消勾选“用户下次登录时更改密码”的框框。
- 8. 点击按钮。你的测试用户被创建并呈现在计算机管理实用程序的“用户”文件夹中，如图 20-4 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_867_1.png)

图 20-3

![](img/7040c21013b8e6c23c612d6da3599ff8_867_2.png)

图 20-4

现在创建一个与此用户配合的页面。

## 验证和授权用户

现在创建一个允许用户进入的应用程序。你通过应用程序的 `web.config` 文件来控制哪些用户允许访问站点，哪些用户不允许访问。

将代码列表 20-1 中的部分添加到你的 `web.config` 文件中。

## 代码列表 20-1：通过 web.config 文件拒绝所有用户

```xml
<system.web>
  <authentication mode="Windows" />
  <authorization>
    <deny users="*" />
  </authorization>
</system.web>
```

在此示例中，`web.config` 文件正在配置应用程序采用基于 Windows 的验证。`<authorization>` 元素属性用于定义哪些用户或组允许访问应用程序。在这种情况下，`<deny>` 元素指定了拒绝哪些用户（即使他们已经通过了验证）。如你所见，你有几种方法可以为你的 ASP.NET 应用程序构建验证/授权模型。下一节将检查 Windows 验证模式。

# 应用身份验证措施

![](img/7040c21013b8e6c23c612d6da3599ff8_870_0.png)

20-6

右键点击“组”（Groups）文件夹选择“新建组”（New Group）。出现新建组对话框（见图 20-7）。

要创建一个组，请提供名称和描述；然后点击“添加”（Add）按钮并选择你想加入该组的用户。创建组后，你可以这样将其允许用于应用程序：

```xml
<allow roles="MyGroup" />
```

你可以在 `<allow>` 或 `<deny>` 元素中使用 `roles` 属性来处理你创建的组或已存在的特定组。

![](img/7040c21013b8e6c23c612d6da3599ff8_870_1.png)

# 对 HTTP 传输方法进行验证和授权

除了验证和授权特定用户或用户组外，你还可以对通过特定 HTTP 传输协议的请求进行授权或拒绝。你可以使用 `<allow>` 和 `<deny>` 元素中的动词来实现这一点。

```xml
<deny verbs="GET, DEBUG /">
```

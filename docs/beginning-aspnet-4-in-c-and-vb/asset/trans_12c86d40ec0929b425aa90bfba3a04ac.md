
```
<div id="nav">
  <div class="navTree">
    <asp:TreeView ID="TreeView1" runat="server"
      DataSourceID="SiteMapDataSource" ShowLines="True" />
    <br />
    <br />
    <asp:LoginView ID="LoginView1" runat="server">
      <LoggedInTemplate>
        You are currently logged in as
        <b><asp:LoginName ID="LoginName1" runat="server" /></b>.
        <asp:LoginStatus ID="LoginStatus1" runat="server" />
      </LoggedInTemplate>
    </asp:LoginView>
  </div>
  <div id="body">
    <asp:ContentPlaceHolder ID="ContentPlaceHolder1" runat="server" />
  </div>
</form>
<asp:SiteMapDataSource ID="SiteMapDataSource1" runat="server" />
</body>
</html>

*code snippet PCSDemoSite/MasterPage.master*
```

*代码片段 PCSDemoSite/MasterPage.master*

这里的许多控件是你尚未查看过的，你很快就会回来查看它们。

这里需要注意的重要事项是包含各个内容部分（页眉、导航栏和正文）的 <div> 元素，以及使用 <%$ AppSettings:SiteTitle %> 从 web.config 文件中获取站点标题：

```
<appSettings>
  <add key="SiteTitle" value="Professional C# Demo Site"/>
</appSettings>

*code snippet PCSDemoSite/web.config*
```

*代码片段 PCSDemoSite/web.config*

还有一个指向 StyleSheet.css 的样式表链接：

```
<link rel="stylesheet" href="StyleSheet.css" type="text/css" />
```

此样式表包含此页面上 <div> 元素的基本布局信息，以及会议室预订控件的一个部分。 请注意，此文件中的样式信息不包括颜色、字体等。 这是通过主题中的样式表实现的，你将在本章后面看到。 这里的唯一信息是布局信息，例如 <div> 大小。

> 请注意，本章在可能的情况下已遵守网站最佳实践。 使用 CSS 进行布局而不是表格，正在迅速成为网站布局的行业标准，值得学习。 在前面的代码中，# 符号用于格式化具有特定 id 属性的 <div> 元素，而 .mrbEventList 将格式化具有特定 class 属性的 HTML 元素。

## 网站导航

SiteMapPath、Menu 和 TreeView 这三个导航 Web 服务器控件可以与你为网站提供的 XML 站点地图一起工作，或者如果你实现替代站点地图提供程序，也可以与以不同格式提供的站点地图一起工作。 当你创建了这样的数据源后，这些导航 Web 服务器控件能够自动为用户生成位置和导航信息。

Menu 和 TreeView 控件通过将它们的 DataSourceID 设置为 SiteMapDataSource 的 ID 来简单地使用此数据源的数据。 两个控件都包含许多样式属性，并且可以进行主题化，如本章后面所示。

## 在 PCSDemoSite 中导航

PCSDemoSite 的站点地图如下：

```
<?xml version="1.0" encoding="utf-8" ?>
<siteMap>
  <siteMapNode url="~/Default.aspx" title="Home">
    <siteMapNode url="~/About/Default.aspx" title="About" />
    <siteMapNode url="~/HRB/Default.aspx" title="Meeting Room Booker"
    roles="RegisteredUser,SiteAdministrator" />
  </siteMapNode>
  <siteMapNode url="~/Configuration/Default.aspx" title="Configuration"
    roles="RegisteredUser,SiteAdministrator" />
  <siteMapNode url="~/Configuration/Themes/Default.aspx" title="Themes"
    roles="RegisteredUser,SiteAdministrator"/>
  </siteMapNode>
  <siteMapNode url="~/Users/Default.aspx" title="User Area"
    roles="SiteAdministrator" />
  <siteMapNode url="~/Login.aspx" title="Login Details" />
</siteMapNode>
</siteMap>
```

*code snippet PCSDemoSite/Web.sitemap*

*代码片段 PCSDemoSite/Web.sitemap*

PCSDemoSite 网站使用自定义提供程序从 Web.sitemap 获取信息——这是必要的，因为默认提供程序会忽略 roles 属性。 提供程序在网站的 web.config 文件中定义如下：

```
<siteMap defaultProvider="CustomProvider">
  <providers>
    <add name="CustomProvider"
      type="System.Web.XmlSiteMapProvider"
      siteMapFile="Web.sitemap" securityTrimmingEnabled="true" />
  </providers>
</siteMap>
```

*code snippet PCSDemoSite/web.config*

*代码片段 PCSDemoSite/web.config*

这与默认提供程序的唯一区别是添加了 securityTrimmingEnabled="true"，它指示提供程序仅为当前用户允许查看的那些节点提供数据。 此可见性由用户的角色成员身份决定，如下一节所示。

PCSDemoSite 中的 MasterPage.master 页面包含 SiteMapPath 和 TreeView 导航显示以及数据源，如下所示：

```
<div id="header">
  <h1><asp:literal ID="Literal1" runat="server"
    text="<%$ AppSettings:SiteTitle %>" /></h1>
  <asp:SiteMapPath ID="SiteMapPath1" runat="server"
    CssClass="breadcrumb" />
</div>
<div id="nav">
  <div class="navTree">
    <asp:TreeView ID="TreeView1" runat="server"
      DataSourceID="SiteMapDataSource1" ShowLines="True" />
  </div>
  <br />
  <br />
```

- 3. 点击“使用安全设置向导逐步配置安全”链接。
- 4. 在向导的步骤 1 中阅读相关信息后点击下一步。
- 5. 在向导的步骤 2 中，选择“来自互联网”以选择窗体身份验证，然后点击下一步。
- 6. 在确认你将使用默认的“高级提供程序设置”提供程序来存储安全信息后再次点击下一步。

> 此提供程序信息可通过 Provider 选项卡配置，你可以选择将信息存储在其他位置，例如 SQL Server 数据库，但默认的 SQL Server Express 数据库对于说明目的来说已经足够了。

- 7. 选中“为此网站启用角色”选项并点击下一步。
- 8. 添加两个角色 Administrator 和 User，然后点击下一步。
- 9. 添加两个用户帐户，也称为 Administrator 和 User。 请注意，密码的默认安全规则（在 machine.config 中定义）相当严格； 最小长度为七个字符，包括至少一个符号字符以及大小写字母的混合。

> 在本章的可下载代码中，用户和管理员帐户的密码均为 PaSsW0rd。

- 10. 点击下一步，然后再次点击下一步，跳过添加新访问规则页面。

> 默认情况下，所有用户和角色都将有权访问你网站的所有区域。 从添加新访问规则页面，你可以根据角色、用户或匿名用户限制区域。 你可以为网站中的每个目录执行此操作，因为这是通过目录中的 web.config 文件实现的，如你稍后将看到的那样。

- 11. 点击完成。
- 12. 在安全选项卡的主页面上，点击管理用户。
- 13. 依次为每个用户点击编辑角色，并将管理员用户添加到两个角色，将用户用户仅添加到用户角色。

完成所有这些操作后，你就基本完成了。 你已经建立了用户系统，以及角色和用户

为了说明这使得什么成为可能，你必须向网站添加一些控件以使其正常工作。 以下各节中的示例代码假定网站已按本节所述配置了用户和管理员角色和用户。

## 实现登录系统

如果在运行安全向导后打开 web.config，你会看到它已被以下内容修改：

```
<roleManager enabled="true" />
```

和：

```
<authentication mode="Forms" />
```

对于你所付出的努力来说，这似乎不多，但请记住，大量信息存储在 SQL Server Express 数据库中，你可以在 App_Data 目录中看到它（你可能需要在解决方案资源管理器中点击刷新按钮才能看到此文件，名为 ASPNETDB.MDF。 你可以使用任何标准数据库管理工具，包括 Visual Studio，检查存储在此文件中的数据。 如果小心，你甚至可以直接向此数据库添加用户和角色。

默认情况下，登录是通过网站根目录中的 Login.aspx 页面实现的。 如果用户尝试导航到他们无权访问的位置，他们将被自动重定向到此页面，并在成功登录后返回到所需位置。

向 PCSAuthenticationDemo 站点添加两个 Web 窗体 Default.aspx 和 Login.aspx，并从工具箱将登录控件拖到 Login.aspx 窗体上。

这是启用用户登录网站所需做的全部工作。 在浏览器中打开站点，并导航到 Login.aspx（目前你必须手动执行此操作，因为你尚未限制对 Default.aspx 的访问）。 输入你在安全设置向导中添加的用户详细信息，如图 41-5 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1264_0.png)

FIGURE 41-5

图 41-5

登录后，你将被发送到 Default.aspx，目前是一个空白页面。

## 登录 Web 服务器控件

工具箱的登录部分包含多个控件，如下表所示。

| 控件 | 描述 |
|---|---|
| Login | 如你所见，此控件允许用户登录到你的网站。 此控件的大多数属性用于设置提供的模板的样式。 你还可以使用 DestinationPageUrl 在登录后强制重定向到特定位置，并使用 VisibleWhenLoggedIn 确定控件是否对已登录用户可见。 此外，你可以使用各种文本属性，例如 CreateUserText，向用户输出有用的消息。 |
| LoginView | 此控件使你能够显示根据用户是否已登录或用户所属角色而变化的内容。 你可以将内容放在 <AnonymousTemplate> 和 <LoggedInTemplate> 中，以及 <RoleGroups> 以控制此控件的输出。 |
| PasswordRecovery | 此控件使用户能够将密码通过邮件发送给他们，并且可以使用为用户定义的密码恢复问题。 同样，大多数属性用于显示格式，但也有诸如 MailDefinition-Subject 之类的属性用于配置发送到用户地址的电子邮件，以及 SuccessPageUrl 用于在用户请求密码后重定向用户。 |
| LoginStatus | 此控件根据用户是否已登录向用户显示登录或注销链接，其文本和图像可自定义。 |




示例代码包含一个名为 **Membership** 的网站项目，我们将用它作为本节的示例。它基于 Empty 网站项目模板。在项目创建后，添加了一些页面来帮助演示 Membership 提供程序的安全功能。如果你想构建自己的项目，你需要创建一个名为 Secret 的文件夹，然后在此文件夹中创建一个名为 **Payroll.aspx** 的页面。此外，在根文件夹中创建一个 **Default.aspx** 页面。在工资单和默认页面中各添加一行文本（例如“这是工资单页面”）。

如前所述，membership 和角色管理提供程序通过查找名为 `LocalSqlServer` 的连接字符串来访问其数据。Web Site Administration Tool 使用这些提供程序，因此在使用该工具之前必须正确配置连接字符串。还请记住，如果 `web.config` 文件中没有 `LocalSqlServer` 的条目，该工具将创建一个并使用本地数据库作为应用程序的存储。本书中的示例应用程序使用了一个在配置 membership 时自动创建的本地数据库。它名为 `aspnetdb.mdb`，位于 `App_Data` 文件夹中。

让我们逐步了解如何使用 ASP.NET Web Site Administration Tool 设置安全性和用户角色。你可以通过 Solution Explorer 中的按钮启动此工具，或在主菜单中选择 Website（Web site 项目）或 Project（Web 应用程序项目）下的 ASP.NET Configuration。当工具打开时，单击 Security 选项卡，然后单击链接开始 Security Setup Wizard，如图 22-17 所示。

![](img/d99870e80390742f93963da7be0b2e61_773_0.png)

## FIGURE 22-17

你将被欢迎页迎接向导。该页面描述了向导将如何帮助你为站点设置安全。单击 Next 按钮将带你进入可以选择使用哪种身份验证的页面。

所提供的选项询问你的应用程序是否将在公共互联网上可用或托管在内网中。这些选项具有误导性，因为无论站点托管在哪里，你都可以使用其中任何一个。向导真正询问的是你希望使用哪种类型的身份验证。如果你选择 Internet，则你的网站将启用表单身份验证。如果你选择本地网络，则你的站点将配置为使用 Windows Integrated Authentication 工作。对于我们的示例，选择 Internet 选项，如图 22-18 所示。

![](img/d99870e80390742f93963da7be0b2e61_774_0.png)

## FIGURE 22-18

在向导中继续操作时，还会询问你是否要使用角色管理。通过选中适当的复选框启用角色管理并添加一个名为 Manager 的角色。此步骤之后，你可以开始向系统中输入用户。填写你希望系统中存在的每个用户的相关信息，如图 22-19 所示。示例应用程序中使用的数据库有三个用户：Rob Windsor、Bill Sheldon 和 Billy Hollis。所有用户的密码都相同：pass@word1。

![](img/d99870e80390742f93963da7be0b2e61_774_1.png)

## FIGURE 22-19

下一步是为你的站点创建访问规则。你可以选择特定的文件夹并为该文件夹应用规则。单击左侧的 Membership 文件夹，然后添加一条拒绝匿名用户访问该文件夹的访问规则（见图 22-20）。现在单击 Secret 文件夹并添加两条访问规则，一条允许 Manager 角色中的人员，另一条拒绝所有用户（见图 22-21）。顺序很重要，因为规则按其在 web.config 文件中出现的顺序应用。如果规则的顺序被颠倒，Manager 角色中的用户将被拒绝访问 Secret 文件夹。

![](img/d99870e80390742f93963da7be0b2e61_775_0.png)

**FIGURE 22-20**

![](img/d99870e80390742f93963da7be0b2e61_775_1.png)

**FIGURE 22-21**

单击 Finish 按钮退出向导。你应该被重定向回 Security 选项卡。最后一步是将你创建的用户中的至少一个添加到 Manager 角色。单击 Manage users 链接，然后单击一个或多个用户的 Edit roles 链接并将他们添加到 Manager 角色，如图 22-22 所示。

![](img/d99870e80390742f93963da7be0b2e61_775_2.png)

**FIGURE 22-22**

添加到根文件夹中 `web.config` 文件的内容包括以下内容：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <system.web>
        <authorization>
            <allow roles="Manager" />
```

```xml
<deny users="?" />
</authorization>
<roleManager enabled="true" />
<authentication mode="Forms" />
</system.web>
</configuration>
```

这显示了向导添加的所有设置。`<authorization>` 部分允许属于 Manager 角色的用户，并拒绝所有匿名用户（用问号定义）。`<roleManager>` 元素打开角色管理系统，而 `<authentication>` 元素打开表单身份验证。

请注意，Secret 文件夹中还有第二个 web.config。这定义了该文件夹及其内部页面的安全性：

```xml
<configuration>
    <system.web>
        <authorization>
            <allow roles="Manager" />
            <deny users="*" />
        </authorization>
    </system.web>
</configuration>
```

现在，添加一个名为 Login.aspx 的页面。此页面将在用户需要输入其凭据时使用。在登录页面放置一个 Login 服务器控件。这是许多服务器控件之一，旨在与 Membership 和 Role 提供程序一起使用。每个控件都需要很少或不需要配置，因为它们知道它们所连接的提供程序的方法和属性。例如，Login 控件天生就知道如何要求 Membership 提供程序验证用户输入的凭据。

现在运行应用程序尝试访问 Default.aspx 页面。你将以匿名用户身份开始。由于已拒绝匿名用户访问站点中的所有页面，因此你将被重定向到 Login.aspx 页面以便输入你的凭据，如图 22-23 所示。

![](img/d99870e80390742f93963da7be0b2e61_776_0.png)

输入你之前创建的任何用户的凭据都应使你进入 Default.aspx 页面。然而，只有属于 Manager 角色的用户凭据才足以允许你导航到 Payroll.aspx 页面。

## PROFILE PROPERTIES

许多 Web 应用程序具有允许某种个性化的功能。这可能像用名字向用户问候一样简单，也可能涉及更高级的问题，例如内容放置。不管怎样，个性化技术一直很棘手。开发人员使用从 cookie、会话或数据库条目等任何东西来控制用户可以对其页面执行的个性化。

ASP.NET 包含一个易于使用的个性化系统。它只需在 web.config 文件中进行条目即可启动个性化系统。与 membership 和角色管理系统一样，个性化系统使用提供程序模型，因此可以根据你的需要进行自定义。

继续在上一节中创建的 Membership 项目，我们将创建两个配置文件属性 FirstName 和 LastName，两者均为 String 类型。要开始，请按如下所示修改根文件夹中的 web.config 文件：

```xml
<?xml version="1.0"?>
<configuration>
  <system.web>
    <profile>
      <properties>
        <add name="FirstName" type="System.String" />
        <add name="LastName" type="System.String" />
      </properties>
    </profile>
  </system.web>
</configuration>
```

Code snippet from web.config

当你使用使用动态编译的 Web site 项目时，ASP.NET 将在后台创建一个类，其中包含与你刚刚定义的那些匹配的强类型属性。当你使用 Web 应用程序项目时，你必须使用当前 HttpContext 的 Profile 属性的方法来获取和设置属性。

通过添加控件和代码来更新 Default.aspx 页面，以允许用户输入名字和姓氏，然后将这些值保存到相应的 Profile 属性中。此外，添加控件和代码以在页面加载时以及其值更新时显示 Profile 属性的值。你应该得到类似以下内容的结果：

```xml
<%@ Page Language="VB" %>

<script runat="server">
  Protected Sub Page_Load(ByVal sender As Object, _
    ByVal e As System.EventArgs)

    If Not IsPostBack Then
      ' Web Application projects
      'Dim prof = HttpContext.Current.Profile
      'TextBox1.Text = prof.GetPropertyValue("FirstName")
      'TextBox2.Text = prof.GetPropertyValue("LastName")

      ' Web Site projects
      TextBox1.Text = Profile.FirstName
      TextBox2.Text = Profile.LastName
    End If
    PopulateLabel()
  End Sub

  Protected Sub Button1_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs)

    ' Web Application projects
    'Dim prof = HttpContext.Current.Profile
```


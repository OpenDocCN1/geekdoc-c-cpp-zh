
## 第35 章：仪表化

```vb
<%@ Language="VB" %>
<% Import Namespace="System.Web.Management" %>

<script runat="server">
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
        Dim mail As MailEventNotificationInfo =
            TemplatedMailEventProvider.CurrentNotification
        Label1.Text = "Events Discarded By Buffer: " & _
            mail.Events.DiscardedByBuffer.ToString()
        Label2.Text = "Events Discarded Due Message Limit: " & _
            mail.Events.DiscardedDueMessageLimit.ToString()
        Label3.Text = "Events In Buffer: " & mail.EventsInBuffer.ToString()
        Label4.Text = "Events In Notification: " & 
    End Sub
</script>
```

```vb
meni.EventsInNotificationToString()
Label5.Text = "剩余事件: " & meni.EventsRemaining.ToString()
Label6.Text = "上次通知 UTC 时间: " & 
meni.LastNotificationUtc.ToString()
Label7.Text = "通知中的消息数: " & 
meni.MessagesInNotification.ToString()
```

```vb
DetailsView.DataSource = meni.Events
DetailsView.DataBind()
End Sub
```

```html
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head></head>
<body>
```

```html
<form id="form" runat="server">
<asp:label id="Label1" runat="server"></asp:label><br />
<asp:label id="Label2" runat="server"></asp:label><br />
<asp:label id="Label3" runat="server"></asp:label><br />
<asp:label id="Label4" runat="server"></asp:label><br />
<asp:label id="Label5" runat="server"></asp:label><br />
<asp:label id="Label6" runat="server"></asp:label><br />
<asp:label id="Label7" runat="server"></asp:label><br />
```

```html
<br />
<asp:DetailsView Id="DetailsView" runat="server" Height="50px"
Width="500px" BorderColor="White" Border="None" BorderStyle="Horizontal"
BorderSize="1px" CellPadding="3" GridLines="Horizontal">
<FooterStyle BackColor="#B5CFDE" ForeColor="#4A3C8C" />
<EditRowStyle BackColor="#F7B3A6" Font-Bold="True"
ForeColor="#F7F7F7" />
<CellStyle BackColor="#F7F7F7" ForeColor="#4A3C8C" />
<PagerStyle BackColor="#F7F7F7" ForeColor="#4A3C8C" />
HorizontalAlign="Right"
<HeaderStyle BackColor="#4A3C8C" Font-Bold="True"
ForeColor="#F7F7F7" />
<AlternatingRowStyle BackColor="#F7F7F7" />
</asp:DetailsView>
</form>
</body>
</html>
```

```csharp
<% Page Language="C#" %>
<% Import Namespace="System.Web.Management" %>
<script runat="server">
protected void Load(object sender, EventArgs e)
{
MailEventNotificationInfo meni = 
TemplatedMailEventProvider.CurrentNotification;
Label.Text = "缓冲区丢弃的事件: " + 
meni.EventsDiscardedByBuffer.ToString();
```

```csharp
Label2.Text = "因消息限制丢弃的事件: " +
meni.EventsDiscardedDueMessageLimit.ToString();
Label3.Text = "缓冲区中的事件: " + meni.EventsInBuffer.ToString();
Label4.Text = "通知中的事件: " +
meni.EventsInNotification.ToString();
Label5.Text = "剩余事件: " + meni.EventsRemaining.ToString();
Label6.Text = "上次通知 UTC 时间: " +
meni.LastNotificationUtc.ToString();
Label7.Text = "通知中的消息数: " +
meni.MessagesInNotification.ToString();

DetailsView.DataSource = meni.Events;
DetailsView.DataBind();

<script>
```

要使用 `TemplatedWebEventProvider`，你首先需要导入 `System.Web.Management` 命名空间。你可以通过 `MailEventNotificationInfo` 和 `TemplatedMailEventProvider` 对象来实现。你首先创建一个 `MailEventNotificationInfo` 对象的实例，并为 `TemplatedMailEventProvider.CurrentNotification` 属性赋值。现在，你就可以访问来自监控的 Web 事件的一整系列值了。

这封电子邮件显示在图 35-15。

如你在图中所示，这种格式的电子邮件更具可读性。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1626_0.png)

图 35-15

## 总结

虽然说 ASP.NET 1.x 真正关注的是开发者，但 ASP.NET 2.0 和 3.5 在简化部署的 ASP.NET 应用程序管理员的工作方面取得了巨大进展。除了许多基于 GUI 的管理和维护工具（在下一章中介绍）外，你现在可以使用 ASP.NET 健康监控功能记录并发送有关你的 ASP.NET 应用程序健康状况（良好或不良）的通知。

## 第36 章：管理与维护

你已经接近这本书的末尾；你已经接触了 ASP.NET 3.5 以及它旨在帮助你成为更好、更高效的程序员的精彩功能。然而，所有的进步都伴随着复杂性，在 ASP.NET 配置和管理领域也是如此。好消息是，ASP.NET 开发团队意识到了这一点，并提供了工具和 API，让开发者能够可靠且舒适地配置和管理基于 ASP.NET 的应用程序。

本章将详细介绍这些工具，旨在向你介绍可以为你提供的一些选项。本章探索了两个强大的配置工具：基于 Web 的应用程序 ASP.NET 站点管理工具，以及用于配置你的 ASP.NET 应用程序的 IIS 管理器。

### ASP.NET 站点管理工具

当 ASP.NET 发布时，它引入了许多帮助你成为更好、更高效程序员的精彩功能。然而，所有的进步都伴随着复杂性，在 ASP.NET 配置和管理领域也是如此。好消息是，ASP.NET 开发团队意识到了这一点，并提供了工具和 API，让开发者能够可靠且舒适地配置和管理基于 ASP.NET 的应用程序。

本章将详细介绍这些工具，旨在向你介绍可以为你提供的一些选项。本章探索了两个强大的配置工具：基于 Web 的应用程序 ASP.NET 站点管理工具，以及用于配置你的 ASP.NET 应用程序的 IIS 管理器。

When ASP.NET was first released, it introduced the concept of configuration for that. The tool allows you to access the of the settings. The `web.config` is located in the same directory as the application.

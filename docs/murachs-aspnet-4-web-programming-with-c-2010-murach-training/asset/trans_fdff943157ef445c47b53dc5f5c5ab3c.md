

## 如何强制页面使用安全连接

当你构建一个完整的 Web 应用程序时，通常会包含导航功能，例如菜单或超链接，用于引导用户从一个页面跳转到另一个页面。不幸的是，用户有时会绕过你的导航功能并直接访问应用程序中的页面。例如，用户可能会为应用程序中的某个页面添加书签并稍后返回。其他用户可能只是简单地在浏览器地址栏中输入应用程序中各个页面的 URL。有些用户是无意为之；另一些用户则试图绕过应用程序的安全功能。

因此，应该使用 SSL 发送或接收敏感信息的页面不应假设已建立安全连接。相反，它应检查是否存在安全连接，并在必要时建立连接。为此，你可以使用图 18-7 中所示的 HttpRequest 类的属性。

要检查安全连接，你使用 IsSecureConnection 属性。然后，如果连接不安全，你可以使用 Url 属性检索页面的 URL 并修改该 URL，使其使用 HTTPS 协议。完成此操作后，你可以使用 Redirect 方法使用新 URL 重定向浏览器。请注意，你通常会在页面的 Load 方法开头包含此代码。这样，你就可以确保在建立安全连接之前不会执行任何其他代码。

强制页面使用安全连接的另一种方法是设置 IIS 中页面的属性。当你使用此技术时，用户将无法在不使用安全连接的情况下访问该页面。换句话说，他将无法绕过应用程序提供的导航功能。有关如何使用此技术的更多信息，请参阅附录 B（Windows 7 和 Windows Vista）或附录 C（Windows XP）。

## Halloween Store 应用程序如何使用安全

Cart.aspx

CheckOut1.aspx

Secure

CheckOut2.aspx

Order.aspx

Confirmation.aspx

Unsecure

### 描述

- 当用户从 Cart 页面（或 Order 页面）点击 Check Out 按钮时，浏览器会使用安全连接重定向到第一个 Check Out 页面。
- 当用户从第一个 Check Out 页面点击 Continue Checkout 按钮时，浏览器会重定向到第二个 Check Out 页面并保持安全连接。
- 当用户从第二个 Check Out 页面点击 Accept Order 按钮时，浏览器会重定向到 Confirmation 页面并保持安全连接。
- 当用户从 Confirmation 页面点击 Return to Order Page 按钮时，浏览器会以非安全连接重定向到 Order 页面。

图 18-8   Halloween Store 应用程序使用 SSL 的操作

## Cart 页面的部分 C# 代码

```
public partial class Cart : System.Web.UI.Page
{
    .
    .
    protected void btnCheckOut_Click(object sender, EventArgs e)
    {
        string url = "https:"
            + ConfigurationManager.AppSettings["AppPath"]
            + "Checkout1.aspx";
        Response.Redirect(url);
    }
}
```

## 第一个 Check Out 页面的部分 C# 代码

```
public partial class Checkout1 : System.Web.UI.Page
{
    .
    .
    protected void Page_Load(object sender, EventArgs e)
    {
        if (!Request.IsSecureConnection)
        {
            string url = Request.Url.ToString().Replace("http:", "https:");
            Response.Redirect(url);
        }
    }

    protected void btnCheckOut_Click(object sender, EventArgs e)
    {
        if (Page.IsValid)
        {
            .
            .
            Response.Redirect("Checkout2.aspx");
        }
    }

    protected void btnCancel_Click(object sender, EventArgs e)
    {
        Session.Remove("Cart");
        String url = "http:"
            + ConfigurationManager.AppSettings["AppPath"]
            + "Order.aspx";
        Response.Redirect(url);
    }

    protected void btnContinue_Click(object sender, EventArgs e)
    {
        string url = "http:"
            + ConfigurationManager.AppSettings["AppPath"]
            + "Order.aspx";
        Response.Redirect(url);
    }
}
```

## 第二个 Check Out 页面的部分 C# 代码

```
public partial class CheckOut2 : System.Web.UI.Page
{
    .
    .
    protected void Page_Load(object sender, EventArgs e)
    {
        if (!Request.IsSecureConnection)
        {
            String url = Request.Url.ToString().Replace("http:", "https:");
            Response.Redirect(url);
        }
    }

    protected void btnAccept_Click(object sender, EventArgs e)
    {
        if (Page.IsValid)
        {
            .
            .
            Response.Redirect("Confirmation.aspx");
        }
    }

    protected void btnCancel_Click(object sender, EventArgs e)
    {
        Session.Remove("Cart");
        String url = "http:"
            + ConfigurationManager.AppSettings["AppPath"]
            + "Order.aspx";
        Response.Redirect(url);
    }

    protected void btnContinue_Click(object sender, EventArgs e)
    {
        String url = "http:"
            + ConfigurationManager.AppSettings["AppPath"]
            + "Order.aspx";
        Response.Redirect(url);
    }
}
```

## Confirmation 页面的部分 C# 代码

```
public partial class Confirmation : System.Web.UI.Page
{
    .
    .
    protected void btnReturn_Click(object sender, EventArgs e)
    {
        string url = "http:"
            + ConfigurationManager.AppSettings["AppPath"]
            + "Order.aspx";
        Response.Redirect(url);
    }
}
```

## 观点

现在你已完成本章，你应该能够使用 SSL 加密来保护客户端和服务器之间的数据传输。那是保护应用程序的一部分。另一部分是确保只有授权用户才能使用你的应用程序，你将在下一章学习如何提供该功能。

顺便说一下，如果你有兴趣查看本章中 Halloween Store 应用程序的其余代码，你应该知道你可以从我们的网站（www.murach.com）下载本书中的所有应用程序。有关详细信息，请参阅附录 A。

## 术语

- Secure Sockets Layer (SSL)
- secure connection
- authentication
- server authentication
- client authentication
- digital secure certificate
- certification authority (CA)
- registration authority (RA)
- SSL strength
- single root certificate
- chained root certificate
- self-signed certificate
- binding

## 如何验证和授权用户

在上一章中，你学习了如何保护客户端和服务器之间的数据传输。现在，你将学习如何限制对应用程序某些页面的访问，但让授权用户访问这些页面。为了在不编写一行代码的情况下提供此功能，你可以使用 Web Site Administration Tool 和登录控件。

- 对身份验证的介绍 .................................... 628
- 三种身份验证类型 ............................................. 628
- 基于表单的身份验证的工作原理 .................................... 630
- 如何设置身份验证和授权 ........... 632
- 如何启动 Web Site Administration Tool ....................... 632
- 如何启用基于表单的身份验证 ............................... 634
- 如何创建和管理角色 ........................................... 636
- 如何创建和管理用户 ........................................... 638
- 如何创建和管理访问规则 ................................... 640
- 如何修改成员资格和角色提供程序....................... 642
- 如何使用登录控件 ........................................... 644
- 如何使用 Login 控件 ............................................. 644
- 如何使用 LoginStatus 和 LoginName 控件 ................... 646
- 如何使用 CreateUserWizard 控件 ............................... 648
- 如何使用 PasswordRecovery 控件 ............................... 650
- 如何使用 ChangePassword 控件 .................................. 652
- 如何使用 LoginView 控件 ....................................... 654
- Authentication 应用程序 ........................................ 656
- 页面 ................................................................ 656
- 目录结构 ................................................ 660
- 访问规则 ........................................................ 660
- web.config 文件 .................................................... 662
- 观点 .............................................................. 664


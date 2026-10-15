

```
BorderStyle="None" BorderWidth="1px" CellPadding="3" CellSpacing="2"
Height="100px" style="margin-left: 136px" Width="191px">
<FooterStyle BackColor="#F7DF85" ForeColor="#8C4510" />
<RowStyle BackColor="#FFF7E7" ForeColor="#8C4510" />
<PagerStyle ForeColor="#8C4510" HorizontalAlign="Center" />
<SelectedRowStyle BackColor="#738A9C" Font-Bold="True" ForeColor="white" />
<HeaderStyle BackColor="#A55129" Font-Bold="True" ForeColor="white" />
</asp:Gridview>
</div>
</form>
</body>
</html>
```

4. 在 Default.aspx 页面的代码隐藏文件中添加以下代码。清单 36.11 显示了该应用程序的 Default.aspx 页面代码隐藏文件的代码：

## 清单 36.11：显示 Default.aspx 页面代码隐藏文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Configuration;
using System.Web.Security;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        Dropgetallroles.DataSource = Roles.GetAllRoles();
        Dropgetallroles.DataBind();
    }
    protected void BtnCreate_Click(object sender, EventArgs e)
    {
        try
        {
            Label1.Visible = true;
            Roles.CreateRole(TextBox1.Text);
            Dropgetallroles.DataSource = Roles.GetAllRoles();
            Dropgetallroles.DataBind();
            //Label1.Visible = false;
            Label1.Text="Role " + TextBox1.Text+" is Created" ;
        }
        catch
        {
            Label1.Visible = true;
            Label1.Text = "Unable to create role, as this role exists. Please try another role name.";
        }
    }
    protected void BtnDelete_Click(object sender, EventArgs e)
    {
        Label1.Visible = true;
        Roles.DeleteRole(TextBox1.Text);
        Dropgetallroles.DataSource = Roles.GetAllRoles();
        Dropgetallroles.DataBind();
        Label1.Text = "Roles " + TextBox1.Text + " is deleted";
    }
    protected void BtnAdd_Click(object sender, EventArgs e)
    {
        try
        {
            Label2.Visible = false;
            Roles.AddUserToRole(Txtusername.Text, TxtRolename.Text);
            Gridview1.DataSource = Roles.GetUsersInRole(TxtRolename.Text);
            Gridview1.DataBind();
        }
        catch
        {
            Label2.Visible = true;
            Label2.Text = "User Already exist";
        }
    }
    protected void BtnDelUser_Click(object sender, EventArgs e)
    {
        try
        {
            Roles.RemoveUserFromRole(Txtusername.Text, TxtRolename.Text);
            Gridview1.DataSource = Roles.GetUsersInRole(TxtRolename.Text);
            Gridview1.DataBind();
        }
        catch
        {
            Label2.Visible = true;
            Label2.Text = "User not exist";
        }
    }
}
```

- 5. 按键盘上的 F5 键运行应用程序并查看输出。
- 6. 在“Enter Role Name”文本框中输入角色，然后单击“Create Roles”按钮（图 36.23）。页面将显示消息“Role User is Created”（图 36.23）。
- 7. 单击下拉列表查看创建的角色，如图 36.23 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1714_0.png)

图 36.23：创建角色

- 8. 在“Enter Role Name”文本框中输入角色名称，然后单击“Delete Roles”按钮（图 36.24）。页面将显示消息“Role User is deleted”（图 36.24）。
- 9. 单击下拉列表查看剩余角色，如图 36.24 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1715_0.png)

# 图 36.24：删除用户

10. 在“Enter user name”文本框中输入用户名，并在“Enter Role”文本框中输入已创建的角色（图 36.25）。

11. 单击“Add User”按钮添加用户，并将其显示在 Admin 角色的网页上，如图 36.25 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1715_1.png)

# 图 36.25：添加用户

12. 在相应的文本框中输入用户和角色的名称，然后单击“Delete User”按钮（图 36.26）。

已删除的用户不会显示在网页上，如图 36.26 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1716_0.png)

图 36.26：删除用户

在 Roles 应用程序中，您学习了如何在网站中创建和删除角色，还学习了如何创建和删除与角色对应的用户。现在，让我们学习匿名身份验证。

## 在 ASP.NET 中使用匿名身份验证

匿名身份验证在 IIS 中默认启用。这意味着，尝试访问 ASP.NET 应用程序网页的用户会被 IIS 视为匿名用户。对于匿名用户，IIS 不要求任何类型的凭据。许多网站和 Web 应用程序允许用户匿名访问大部分 Web 内容，即无需任何身份验证。

可以通过设置应用程序或站点的 web.config 文件中 `<authentication>` 元素的 `mode` 属性，在 ASP.NET 应用程序中实现匿名身份验证。让我们执行以下步骤创建一个 ASP.NET 网站，并将其保存为 AnonymousAuth（在 CD-ROM 上）：

- 1. 向 AnonymousAuth Web 应用程序添加一个 Web 页面 Default.aspx。
- 2. 打开 Default.aspx 页面，并添加清单 36.12 中给出的代码，以在应用程序中添加所需的控件：

## 清单 36.12：显示 Default.aspx 页面的代码

```
<%@ page language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
<title>using Anonymous Authentication in ASP.NET</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<table style="z-index: 150; left: 250px; position: absolute; top: 75px; width: 361px; height: 114px;">
<tr style=" font-weight: bold">
<td>Movies</td>
<td>Available</td>
<td>Price (in Rs.)</td>
</tr>
<tr style=" background:LightGreen; height: 25px">
<td>Kung Fu Panda</td>
<td>Yes</td>
<td>150</td>
</tr>
<tr style=" background:LightYellow; height: 25px">
<td>Hancock</td>
<td>Yes</td>
<td>175</td>
</tr>
<tr style=" background:LightGreen; height: 25px">
<td>Amistad</td>
<td>No</td>
<td>110</td>
</tr>
<tr style=" background:LightYellow; height: 25px">
<td>Ice Age</td>
<td>Yes</td>
<td>150</td>
</tr>
<tr style=" background:LightGreen; height: 25px">
<td>Shrek</td>
<td>No</td>
<td>170</td>
</tr>
<tr style=" background:LightYellow; height: 25px">
<td>Jerry McGuire</td>
<td>Yes</td>
<td>155</td>
</tr>
</table>
</div>
</form>
</body>
</html>
```

需要启用匿名身份验证，以允许任何用户访问 AnonymousAuth 网站的 Default.aspx 页面。匿名身份验证已在 IIS 中启用，您只需在 ASP.NET 应用程序中启用它。

- 3. 打开应用程序的 web.config 文件，并按以下代码修改 `<authentication>` 元素的设置：

```xml
<authentication mode="None" />
```

通过这种对 `<authentication>` 元素 `mode` 属性的设置，用户在 IIS 和应用程序中都被视为匿名用户。

如果用户尝试在 Web 浏览器中访问 Default.aspx 页面，如图 36.27 所示，IIS 和 ASP.NET 网站不需要进行身份验证即可授予用户查看页面的访问权限：

![](img/e073a4882197be4ab61103cbe0bcb394_1718_0.png)

# 图 36.27：显示网页

学习完匿名身份验证后，让我们学习 Windows 身份验证。

## 在 ASP.NET 中使用 Windows 身份验证

如您所知，当您希望在本地计算机或 Intranet 上托管 ASP.NET 应用程序时，Windows 身份验证是一种理想的选择。默认情况下，ASP.NET 应用程序使用当前登录用户的 Windows 凭据进行身份验证。您可以在 IIS 中启用以下任一身份验证模式，以在 ASP.NET 应用程序中实现 Windows 身份验证：

- 匿名身份验证
- Windows 身份验证（集成）
- 基本身份验证
- 摘要身份验证

在许多情况下，IIS 中的默认身份验证（匿名身份验证）与 ASP.NET 中的 Windows 身份验证结合使用。在这种情况下，IIS 将用户识别为匿名用户，而 ASP.NET 将用户识别为 Windows 用户。您可以禁用 IIS 中的匿名身份验证，或者使用 web.config 文件中的 `<authorization>` 元素来拒绝匿名用户的访问。

现在，让我们创建一个 ASP.NET 网站，并将其保存为 WindowsAuth（在 CD-ROM 上）。

该网站包含两个 Web 页面：Default.aspx 和 AddEvent.aspx。Default.aspx 页面显示事件列表，AddEvent.aspx 页面允许您添加新事件。请执行以下步骤创建 WindowsAuth 网站：

- 1. 在 Web 应用程序中添加两个 Web 页面：Default.aspx 和 AddEvent.aspx。
- 2. 打开 Default.aspx 文件的“设计”视图，首先在 Default.aspx 页面中添加一个 GridView 控件。然后，在项目中添加一个名为 EventsData 的 SQL Server 数据库项，并在数据库中指定一个名为 events 的表。该表包含五列：ID、EventName、Place、Time 和 CreatedBy。现在，将 GridView 控件绑定到一个表示 EventsData 数据库中 events 表的新数据源。此外，使用 GridView 任务启用分页和排序。
- 3. 在 Default.aspx 页面中添加清单 36.13 中给出的代码，以添加所需的控件：

## 清单 36.13：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
```


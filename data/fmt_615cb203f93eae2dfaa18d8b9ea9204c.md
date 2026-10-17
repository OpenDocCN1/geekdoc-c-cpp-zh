
您也可以通过使用 `PrincipalPermissionAttribute` 对象在要保护的类或方法之前使用声明式安全检查来执行相同的授权。例如，在 `Album` 应用程序中，您可以在 `EditImage_Click()` 方法之前添加 `PrincipalPermissionAttribute` 对象，如以下代码所示：

```
[PrincipalPermissionAttribute(SecurityAction.Demand, Name = "Avantika-pc\\Avantika", Role = "BUILTIN\\Administrators")]
private void EditImage_Click(object sender, RoutedEventArgs e)
{
    :
    :
}
```

或者，您可以在 `Album` 应用程序的 `Window1` 类之前使用 `PrincipalPermissionAttribute` 对象。在声明式安全检查的情况下，即使在调用或初始化方法或类之前也会进行检查。如果用户没有授权，则会发生未处理的异常。

## Managing Roles and Users

在 ASP.NET 中，角色由一组用户组成。您将能够通过管理角色来将用户分配到指定的角色，例如 `manager` 和 `admin`。一个用户可以被分配到具有不同权限的多个组。现在，让我们创建一个网站并将其保存为 `Roles`（在 CD-ROM 上）。现在，让我们通过执行以下步骤创建一个网站来管理角色和相应的用户：

+   1. 打开 `Visual Studio 2010` IDE 并选择 `File→New→Web Site` 以打开“新建网站”对话框。在对话框中，选择 `ASP.NET Web Site` 选项并指定 `Roles` 作为网站名称，然后单击“确定”按钮。

+   2. 打开 `web.config` 文件并在 `<system.web>` 标签下添加以下代码行：

```
<roleManager enabled = "true" />
```

前面的代码行启用了网站的角色管理器。角色管理器简化了在应用程序中管理角色和执行基于角色的授权的任务。您也可以通过 Web 管理工具（WAT）执行相同的功能。在 Web 站点管理工具的安全选项卡下，启用 `RoleManager`（有关 WAT 的更多详细信息，请参阅第 16 章，ASP.NET 4.0 中的登录和 Web Parts 控件）。它将自动把前面的代码行添加到 `web.config` 文件中。

+   3. 在应用程序中添加一个 Web 页面 `Default.aspx`，并用清单 36.10 中给出的代码替换 `Default.aspx` 页面的代码，以添加应用程序所需的控件：

### Listing 36.10: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
<title>Managing Roles and User</title>
</head>
<body>
<form id="form1" runat="server">
<div>
Enter Role Name:<br />
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
<asp:Label ID="Label1" runat="server" Text="Label" Visible="False" width="304px"></asp:Label><br />
<asp:Button ID="BtnCreate" runat="server" onclick="BtnCreate_Click" Text="Create Roles" />
&nbsp;<asp:Button ID="BtnDelete" runat="server" onclick="BtnDelete_Click" style="margin-left: 81px" Text="Delete Roles" />
<br />
<br />
<asp:DropDownList ID="Dropgetallroles" runat="server">
</asp:DropDownList>
<br />
<br />
<hr style="background-color:Black"/>
<span style="color: #000000">
<br />
Enter user name:<br />
</span>
<asp:TextBox ID="Txtusername" runat="server"></asp:TextBox><br />
<span style="color: #000000">Enter Role:</span><br />
<asp:TextBox ID="TxtRolename" runat="server"></asp:TextBox>
<asp:Label ID="Label2" runat="server"></asp:Label><br />
<br />
<asp:Button ID="BtnAdd" runat="server" onclick="BtnAdd_Click" Text="Add User" Width="103px" />
<asp:Button ID="BtnDeluser" runat="server" style="margin-left: 63px" Text="Delete User" onclick="BtnDeluser_Click" />
<br />
<br />
<asp:Gridview ID="Gridview1" runat="server" BackColor="#DEBA84" BorderColor="#DEBA84"
```

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

4. 在 `Default.aspx` 页面的代码隐藏文件中添加以下代码。清单 36.11 显示了该应用程序的 `Default.aspx` 页面代码隐藏文件的代码：

### 清单 36.11：显示 Default.aspx 页面代码隐藏文件的代码

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

- 5. 按键盘上的 `F5` 键运行应用程序并查看输出。

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

在 `Roles` 应用程序中，您学习了如何在网站中创建和删除角色，还学习了如何创建和删除与角色对应的用户。现在，让我们学习匿名身份验证。

## 在 ASP.NET 中使用匿名身份验证

匿名身份验证在 IIS 中默认启用。这意味着，尝试访问 ASP.NET 应用程序网页的用户会被 IIS 视为匿名用户。对于匿名用户，IIS 不要求任何类型的凭据。许多网站和 Web 应用程序允许用户匿名访问大部分 Web 内容，即无需任何身份验证。

可以通过设置应用程序或站点的 `web.config` 文件中 `<authentication>` 元素的 `mode` 属性，在 ASP.NET 应用程序中实现匿名身份验证。让我们执行以下步骤创建一个 ASP.NET 网站，并将其保存为 `AnonymousAuth`（在 CD-ROM 上）：

- 1. 向 `AnonymousAuth` Web 应用程序添加一个 Web 页面 `Default.aspx`。

- 2. 打开 `Default.aspx` 页面，并添加清单 36.12 中给出的代码，以在应用程序中添加所需的控件：

### 清单 36.12：显示 Default.aspx 页面的代码


`using System;`

`using System.Collections.Generic;`

`using System.Linq;`

`using System.Web;`

`using System.WebServices;`

```xml
<summary>
/// Web 服务的描述
[WebServiceBinding(Namespace = "http://tempuri.org/")]
</summary>
// 要允许从脚本调用此 Web 服务（使用 ASP.NET AJAX），请取消
// 下行的注释
[System.Web.Script.Services.WebService]
public class webService : WebService
{
    // 如果使用设计组件，请取消下面的注释
    //[InitializeComponent();
    [WebMethod]
    public string HelloWorld() {
        return "Hello world";
    }
    [WebMethod]
    public string GetMachineName() {
        return Server.MachineName;
    }
}
```

- 2. 运行 Web 服务。输出如图 15.25 所示。
- 3. 点击 `GetMachineName` 链接，如图 15:25 所示。

![](img/17af790174c480761404624aeed9b30b_784_0.png)

图 15.25：执行 Web 服务

- 4. 点击“调用”（Invoke）查看 Web 服务的输出，如图 15:26 所示：

![](img/17af790174c480761404624aeed9b30b_785_0.png)

图 15.26：调用 Web 服务

Web 服务的输出现在出现，如图 15:27 所示：

![](img/17af790174c480761404624aeed9b30b_785_1.png)

图 15.27：Web 服务输出

在图 15.27 中，Web 服务显示的服务器名称为 DESKTOP-PC。

# 使用 Web 服务

你需要创建一个 ASP.NET Web 应用程序，允许客户端访问 Web 服务。代理类是 Web 服务类的本地副本，代表 Web 服务。你可以通过向 Web 服务添加 Web 引用来为 Web 服务生成代理类。让我们创建一个名为 `UsingInterestWebService` 的 Web 应用程序。现在按照以下步骤操作：

- 1. 向解决方案管理器添加 ASP.NET Web，右键点击 `UsingInterestWebService` 解决方案并选择“添加→现有 Web 项目”（Add→Existing Web），如图 15:28 所示：

![](img/17af790174c480761404624aeed9b30b_786_0.png)

图 15.28：向新网站添加现有网站

- 2. 打开 `UsingInterestWebService` Web 应用程序中 `Default.aspx` 页的设计视图。
- 3. 将以下控件添加到 `Default.aspx` 页面以设计 `UsingInterestWebService` 应用程序的界面。按照图 15:29 所示的布局安排控件：
  - 五个 Label 控件——分别选择四个标签文本为 Principal（本金）、Rate（利率）、Duration（时长）和 Simple Interest（单利）。将四个 TextBox 控件的 ID 为 Principal、Rate、Duration 和 SimpleInterest。
  - 一个 Button 控件——将其文本设置为 Calculate Interest。

![](img/17af790174c480761404624aeed9b30b_786.png)

图 15.29：`Default.aspx` 的设计界面

- 4. 将列表 15:13 所示的代码添加到 `UsingInterestWebService` 的 `Default.aspx` 页面中：

**列表 15:13：Default.aspx 代码**
```xml
@page language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs">
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <title>Calculate Interest</title>
</head>
<body>
  <form id="form1" runat="server">
    <div>
      <span>Calculate interest using the Web Service</span>
      <br />
      <asp:Label ID="Label1" runat="server" Text="Principal" width="60px" />
      <asp:TextBox ID="txtPrincipal" runat="server" />
      <br />
      <asp:Label ID="Label2" runat="server" Text="Rate" width="60px" />
      <asp:TextBox ID="txtRate" runat="server" />
      <br />
      <asp:Label ID="Label3" runat="server" Text="Duration" width="63px" />
      <asp:TextBox ID="txtDuration" runat="server" />
      <br />
      <asp:Label ID="Label4" runat="server" Text="Simple Interest" />
      <asp:TextBox ID="txtSimpleInterest" runat="server" />
      <br />
      <asp:Label ID="Label5" runat="server" width="66px" />
      <asp:Button ID="Button1" runat="server" Text="Calculate Interest" width="220px" OnClick="Button1_Click" />
    </div>
  </form>
</body>
</html>
```

- 5. 在解决方案管理器窗口中右键点击 `UsingInterestWebService`，从从键菜单中选择“添加引用”（Add Reference）以显示引用对话框（图 15.30）。
- 6. 出现引用对话框。点击“高级”（Advanced）按钮，如图 15:30 所示：

![](img/17af790174c480761404624aeed9b30b_787_0.png)

图 15.30：引用对话框

- 7. 打开引用对话框。点击“添加 Web 引用”（Add Web Reference）按钮，如图 15:31 所示：

![](img/17af790174c480761404624aeed9b30b_788_0.png)

图 15.31：引用对话框

你可以通过在 URL 框中指定位置来定位 Web 服务，或者在“浏览到”面板中选择相应的链接。例如，如果 Web 服务存在于应用程序中，请选择解决方案中的 Web 服务。由于我们的服务位于 Web 应用程序中，我们点击相应的超链接，如图 15.32 所示。

![](img/17af790174c480761404624aeed9b30b_788_1.png)

图 15.32：浏览 Web 服务

## 8. 从此解决方案的 Web 服务“Services”列中选择 `CalculateSimpleInterest` 链接，如图 15.33 所示：

![](img/17af790174c480761404624aeed9b30b_789_0.png)

图 15.33：添加引用

只有当成功定位 Web 服务时，“添加引用（Add Reference）”按钮才会可用。

9. 点击“添加引用”按钮，在解决方案管理器（Solution Explorer）中添加该引用，如图 15.33 所示。

10. 在 Web 应用程序的 `Default.aspx` 后置代码中添加代码以创建 Web 引用的实例，如列表 15.14 所示：

列表 15.14：访问 Web 服务 Web方法的 `Default.aspx.cs` 代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;
public partial class _Default : System.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
    }
    protected void Button1_Click(object sender, EventArgs e)
    {
        localhost.WebService ws = new localhost.WebService();
        ws.IsEnabled = true;
        Double Si = 0;
        if (txtPrincipal.Text == "" || txtRate.Text == "" || txtDuration.Text == "")
        {
            Label5.Text = "无法计算单利";
        }
        else
        {
            Si = ws.CalculateSimpleInterest(Convert.ToDouble(txtPrincipal.Text), Convert.ToDouble(txtRate.Text), Convert.ToInt32(txtDuration.Text));
            txtSimpleInterest.Enabled = true;
            txtSimpleInterest.Text = Si.ToString();
        }
    }
}
```

11. 现在运行 SimpleInterest 应用程序。输出结果见图 15.34）。你应该注意 `default.aspx` 页面是项目的启动页面。

12. 在 Principal、Rate 和 Duration 中输入相应的数字，并点击 Simple Interest 按钮计算单利，如图 15.34 所示：

![](img/17af790174c480761404624aeed9b30b_790_0.png)

图 15.34：显示 Web 服务的结果

现在，让我们学习跨服务共享数据。

## 跨服务共享数据

假设你想创建一个 Web 应用程序，需要两个 Web 服务 `SharingWebService1` 和 `SharingWebService2` 来执行业务逻辑。`WebService1` 获取并更新员工姓名，而 `WebService2` 获取员工 ID。让我们创建名为 `SharingWebService` 和 `SharingWebService2` 的两个 Web 服务，以理解数据如何在之间共享。按照以下步骤完成 `SharingWebService` 和 `SharingWebService2` 之间的数据共享：

- 1. 使用列表 15.15 编写 `SharingWebService` 的后置代码。

列表 15.15：`SharingWebService` 的后置代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Services;
/// <summary>
/// SharingWebService 的摘要
/// </summary>
[WebService(Namespace = "http://tempuri.org/")]
[WebServiceBinding(By = "BasicProfile1")]
// 使用 ASP.NET AJAX 从脚本调用此服务，请取消下行的注释
// [System.Web.Services.ScriptService]
public class SharingWebService : System.Web.Services.WebService
{
    public SharingWebService()
    {
        // 使用设计组件时取消下行的注释
        InitializeComponent();
    }
    public class EmpDetails
    {
        public string FirstName;
        public string EmpName;
        public string LastName;
        public string EmpID;
        public string Designation;
    }
    [WebMethod]
    public EmpDetails obtainEmpDetails(string fName, string mName, string lName)
    {
        EmpDetails name = new EmpDetails();
        name.FirstName = fName;
        name.EmpName = mName;
        name.LastName = lName;
        return name;
    }
    [WebMethod]
    public string HelloWorld()
    {
        return "Hello world";
    }
}
```

- 2. 在添加上述获取员工名称列表后，使用列表 15.16 中的代码在 `WebService2` 的后置字段中获取员工的 ID 和职位：

列表 15.16：`SharingWebService` 服务后置文件的代码

```csharp
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Services;
/// <summary>
/// SharingWebService2 的摘要
/// </summary>
[WebService(Namespace = "http://tempuri.org/")]
[WebServiceBinding(By = "BasicProfile1")]
// 使用 ASP.NET AJAX 从脚本调用此服务，请取消下行的注释
// [System.Web.Services.ScriptService]
public class SharingWebService2 : System.Web.Services.WebService
{
    public SharingWebService2()
    {
        // 使用设计组件时取消下行的注释
        InitializeComponent();
    }
    public class EmpDetails
    {
        public string FirstName;
        public string EmpMiddleName;
        public string EmpLastName;
        public string EmpID;
        public string Designation;
    }
    [WebMethod]
    public EmpDetails UpdateEmpDetail(EmpDetails name, string FID, string FDesignation)
    {
        name.EmpID = FID;
        name.Designation = FDesignation;
        return name;
    }
    [WebMethod]
    public string HelloWorld()
    {
        return "Hello world";
    }
}
```

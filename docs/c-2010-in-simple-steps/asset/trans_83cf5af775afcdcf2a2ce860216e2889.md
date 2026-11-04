
3 在“已安装模板”窗格下选择 Visual C#→Web，并在“新建项目”对话框的中部窗格中选择 ASP.NET 空 Web 应用程序（图 C#13.1）。

4 在“名称”文本框中将 Web 应用程序的名称输入为 AddNumbers，并在“位置”组合框中选择保存应用程序所需的路径（图 C#13.1）。

5 单击“确定”按钮创建 AddNumbers Web 应用程序，如图 C#13.1 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_359_0.png)

图 C#13.1

创建了一个空的 Web 应用程序。

6 在“解决方案资源管理器”中右键单击 AddNumbers→添加→新建项。

“添加新项”对话框打开（图 C#13.2）。

7 从中部窗格中选择“Web 服务”选项（图 C#13.2）。

8 为 Web 服务输入名称。在本例中，我们输入的名称为 MyWebService.asmx（图 C#13.2）。

9 单击“添加”按钮将 MyWebService Web 服务添加到您的应用程序中，如图 C#13.2 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_359_1.png)

图 C#13.2

您可以在“解决方案资源管理器”中看到 Web 服务的默认文件，如图 C#13.3 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_360_0.png)

图 C#13.3

10 向 MyWebService Web 服务的代码隐藏文件 MyWebService.asmx.cs 添加一个 Web 方法 Add()，如列表 13.1 所示：

### 列表 13.1：向 AddNumbers Web 服务添加的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Services;

namespace AddNumbers
{
    /// <summary>
    /// Summary description for MyWebService
    /// </summary>
    [WebService(Namespace = "http://tempuri.org/")]
    [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
    [System.ComponentModel.ToolboxItem(false)]
    // To allow this Web Service to be called from script, using ASP.NET AJAX,
    // uncomment the
    //following line
    // [System.Web.Script.Services.ScriptService]
    public class MyWebService : System.Web.Services.WebService
    {
        [WebMethod]
        public Decimal Add (Decimal a, Decimal b)
        {
            Decimal dc;
            dc = a + b;
            return dc;
        }
    }
}
```

在列表 13.1 中，Add() 方法将两个 Decimal 数字相加，然后将 Decimal 数字作为输出返回给调用方法。

11 按 F5 键执行 MyWebService Web 服务。Web 页面出现（图 C#13.4）。

12 单击 Web 页面上的 Add 超链接，如图 C#13.4 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_361_0.png)

图 C#13.4

输出出现（图 C#13.5）。

- 13. 为 a 和 b 参数输入值（图 C#13.5）。
- 14. 单击“调用”按钮，如图 C#13.5 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_361_1.png)

图 C#13.5

出现一个新 Web 页面，显示分配给 a 和 b 参数的两个值的加法结果，如图 C#13.6 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_362_0.png)

现在要访问 **MyWebService** Web 服务，您需要先将其 Web 引用添加到应用程序中。接下来，使用代理类使您的应用程序能够访问 **MyWebService** Web 服务。代理类是表示 Web 服务的类的本地副本。您可以通过向 Windows 应用程序添加 Web 引用来为 Web 服务生成代理类。在本例中，我们提供两个数字作为加法的输入。

> **注意**
>
> 在本例中，我们正在创建 Windows 窗体应用程序以访问 Web 服务应用程序。Windows 窗体应用程序和 Web 服务应用程序都在同一系统上创建。因此，为了使 Windows 窗体应用程序能够正确访问 Web 服务应用程序，您需要保持运行 Web 服务应用程序的 Visual Studio 2010 实例处于打开状态。

现在，让我们执行以下步骤创建一个名为 **WebServiceExample** 的 Windows 窗体应用程序以访问 **MyWebService** Web 服务。

- 1. 打开 **Visual Studio 2010** 并创建 Windows 窗体应用程序项目 **WebServiceExample**。
- 2. 将 Windows 窗体窗体的 **Text** 属性设置为 **Web Service Example**。
- 3. 向 Windows 窗体窗体添加两个标签、两个文本框和一个按钮，并更改其 **Text** 属性，如图 C#-13.7 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_362_1.png)

- 4. 通过在 **Solution Explorer** 中右键单击 **WebServiceExample** 项目并从上下文菜单中选择 **Add Service Reference** 选项，为 **WebServiceExample** 应用程序添加 **MyWebService** Web 服务的 Web 引用，如图 C#-13.8 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_363_0.png)

图 C#-13.8

“添加服务引用”对话框出现（图 C#-13.9）。

5 单击“高级”按钮，如图 C#-13.9 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_363_1.png)

图 C#-13.9

“服务引用设置”对话框出现（图 C#-13.10）。

6 单击“添加 Web 引用”按钮，如图 C#-13.10 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_363_2.png)

图 C#-13.10

“添加 Web 引用”对话框出现。

7 通过在 URL 文本框中指定其位置（URL 应为托管 Web 服务的 Web 服务的 URL）或在“浏览到：”选项下选择适当的链接来定位 MyWebService Web 服务（图 C#13.11）

8 单击“转到”按钮，如图 C#13.11 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_364_0.png)

图 C#13.11

在指定位置找到的 Web 服务显示出来（图 C#13.12）。

9 在“Web 引用名称”文本框中将 Web 引用的名称输入为 AddTwoNumbers（图 C#13.12）。

10 单击“添加引用”按钮将 MyWebService Web 服务添加到您的应用程序中，如图 C#13.12 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_364_1.png)

图 C#13.12

将 Web 引用添加到 WebServiceExample 应用程序后，您需要创建 Web 引用的实例。您可以使用此实例访问 Web 服务的 Web 方法。

11 在 WebServiceExample 应用程序的 Form1.cs 文件中，在 Add 按钮的 Click 事件中添加列表 13.2 中显示的突出显示的代码以访问 Add() Web 方法：

### 列表 13.2：显示访问 Web 服务的代码

```csharp
private void button1_Click(object sender, EventArgs e)
{
    decimal a, b, result;
    AddTwoNumbers.MyWebService ad = new AddTwoNumbers.MyWebService();
    a = Convert.ToDecimal(textBox1.Text);
    b = Convert.ToDecimal(textBox2.Text);
    result = ad.Add(a, b);
    MessageBox.Show("The addition of the two numbers is " + result.ToString());
}
```

在列表 13.2 中，已使用 AddTwoNumbers 命名空间访问 MyWebService Web 服务。MyWebService Web 服务的 Add() 方法接受两个数字作为加法参数。两个数字相加的结果存储在 result 变量中，并在消息框中显示。

12 按 F5 键运行应用程序。输出出现（图 C#-13.13）。

13 在两个文本框中输入两个数字并单击 Add 按钮。消息框出现，如图 C#-13.13 所示。

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_365_0.png)

图 C#-13.13

14 单击“确定”按钮关闭消息框。

您已了解 Web 服务。现在，让我们在以下部分学习创建 WCF 服务和客户端以使用 WCF 服务。

## 创建和使用 WCF 服务

在 Visual Studio 2010 中创建 WCF 服务是一项轻松的任务，因为 Visual Studio 2010 内置了对 WCF 的支持。但是，在 Visual Studio 2008 之前的版本中，您需要安装 WCF 组件才能创建 WCF 服务。现在，让我们使用 Visual Studio 2010 提供的模板通过执行以下步骤创建 WCF 服务：

- 1. 打开 Microsoft Visual Studio 2010。
- 2. 从菜单栏中选择 文件→新建→项目。新建项目对话框出现。
- 3. 在“已安装模板”窗格下选择 Visual C#，并在“新建项目”对话框的中部窗格中选择 WCF 服务应用程序。

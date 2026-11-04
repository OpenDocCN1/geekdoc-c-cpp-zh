
4 为 WCF 服务应用程序输入名称 WCFService，并在 Location 下拉组合框中选择所需的位置以保存应用程序。

5 单击 OK 按钮创建 WCFService WCF 服务。

WCF 服务的默认文件会出现在解决方案资源管理器中，如图 C#-13.14 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_366_0.png)

### 图 C#-13.14

可以通过执行两个步骤来构建 WCF 服务；首先，您需要创建服务契约。其次，您需要创建数据契约。服务契约指定接口及其相应消息的规则，而数据契约指定通过输入和输出操作交换的数据的规则。

6 在 WCFService 服务的 IService1.cs 文件中添加列表 13.3 中显示的突出显示的代码：

### 列表 13.3：显示 IService1.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.ServiceModel.Web;
using System.Text;

namespace WCFService
{
    // NOTE: You can use the "Rename" command on the "Refactor" menu to change the interface
    //name "IService1" in both code and config file together.
    [ServiceContract]
    public interface IService1
    {
        [OperationContract]
        string GetData(string value);

        [OperationContract]
        string GetDataUsingDataContract(UserInfo users);

        // TODO: Add your service operations here
    }

    // Use a data contract as illustrated in the sample below to add composite types to service
    //operations.
    [DataContract]
    public class UserInfo
{
    string fName;
    string lName;

    [DataMember]
    public string FirstName
    {
        get { return fName; }
        set { fName = value; }
    }

    [DataMember]
    public string LastName
    {
        get { return lName; }
        set { lName = value; }
    }
}
```

在列表 13.3 中，IService1 接口使用 [ServiceContract] 属性标记，并明确将 IService1 接口标记为携带 WCF 的契约元数据。IService1 接口中使用 [OperationContract] 属性标记的方法在 WCF 中被标记为公共方法。数据契约使用 [DataContract] 属性和 [DataMember] 属性分别为 UserInfo 类及其成员定义。服务契约定义服务的行为，而数据契约定义在服务边界之间流动的信息，并在提供者和消费者端使用额外逻辑处理。

7 在 WCFService 服务的 Service1.svc.cs 文件中添加列表 13.4 中给出的突出显示的代码：

### 列表 13.4：显示 Service1.svc.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.ServiceModel.Web;
using System.Text;

namespace WCFService
{
    // NOTE: You can use the "Rename" command on the "Refactor" menu to change the
    // class name in code, svc and config file together.
    public class Service1 : IService1
    {
        public string GetData(string MyValue)
        {
            return "Hello: " + MyValue;
        }

        public string GetDataUsingDataContract(UserInfo dcValue)
        {
            return "Hello: " + dcValue.FirstName + " " + dcValue.LastName;
        }
    }
}
```

8 按 F5 键执行 WCFService 服务。WCF 测试客户端窗口出现，如图 C#-13.15 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_368_0.png)

图 C#-13.15

9 复制 WCF 服务应用程序的 URL 并将其粘贴到您的 Web 浏览器中。输出显示，如图 C#-13.16 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_368_1.png)

图 C#-13.16

现在，需要一个客户端应用程序来使用此 WCF 服务。在创建 WCF 客户端之前，您必须生成帮助 WCF 客户端应用程序调用 WCF 服务的代理类。在 Visual Studio 2010 命令提示符中执行以下代码片段中给出的命令以生成代理类：

```
svcutil.exe /language:cs /out:Service1.cs /config:app.config
http://localhost:49544/Service1.svc?wsdl
```

在前面的代码片段中，svcutil.exe 命令生成一个配置文件（app.config）和一个包含代理类的代码文件（Service1.cs）。

> 注
> 在创建 WCF 服务的位置的命令提示符中执行 svcutil.exe 命令。

执行前述代码片段中给出的命令后的输出显示在图 C#-13.17 中：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_369_0.png)

图 C#-13.17

图 C#-13.17 显示了执行 svcutil.exe 命令后生成的 Service.cs 和 app.config 文件。

### 注

端口号 49544 可能根据您的系统而有所不同。

现在，让我们执行以下步骤来创建一个 WCF 客户端应用程序：

- 1. 打开 Visual Studio 2010 并创建 Windows 窗体应用程序 WCFClient。
- 2. 将窗体的 Text 属性设置为 WCF Client。
- 3. 在解决方案资源管理器中右键单击项目名称，并在创建 WCFClient 应用程序后从上下文菜单中选择 Add Service Reference 选项以添加 WCFService WCF 服务的引用。
- 4. 输入 WCFService WCF 服务的地址，并在 Add Service Reference 对话框中单击 Go 按钮。服务列表显示（图 C#-13.18）。
- 5. 单击 OK 按钮添加服务引用，如图 C#-13.18 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_369_1.png)

6. 添加三个 Label 控件、两个 TextBox 控件和一个 Button 控件，并设置其 Text 属性，如图 C#-13.19 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_370_0.png)

图 C#-13.19

7 将 Service1.cs 文件（使用 svcutil.exe 生成）在向 Windows 窗体添加控件后添加到 WCFClient 应用程序。

8 在 WCFClient 应用程序文件夹中用使用 svcutil.exe 生成的 app.config 文件替换原始 app.config 文件。

9 在 Form1.cs 文件中 Call Service 按钮的 Click 事件上添加列表 13.5 中给出的突出显示的代码：

### 列表 13.5：调用 WCFService 服务

```
private void button1_Click(object sender, EventArgs e)
{
    Service1Client client = new Service1Client();
    WCFService.UserInfo users= new WCFService.UserInfo ();
    users.FirstName = textBox1.Text;
    users.LastName = textBox2.Text;
    label3.Text = client.GetDataUsingDataContract(users);
    client.Close();
}
```

10 按 F5 键执行 WCFClient 应用程序（图 C#-13.20）。

11 在相应的文本框中输入名字和姓氏（图 C#-13.20）。

12 单击 Call Service 按钮调用 WCF 服务。调用 WCF 服务后的输出显示在图 C#-13.20 中：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_370_1.png)

图 C#-13.20

在图 C#-13.20 中，当单击 Call Service 按钮时，会调用 WCFService 服务，该服务返回一个字符串 Hello: <FirstName> <LastName>。

接下来，让我们回顾一下本章中学到的主要要点。

## 摘要

在本章中，您已了解：

- WCF 4.0、Web 服务和 WCF 服务中的新功能
- 云服务及其使用目的
- 在 Visual Studio 2010 中 Web 服务和 WCF 服务的创建和使用

## 第 14 章

### C# 2010 应用程序的部署

本章内容：

- 使用 Windows Installer 部署应用程序
- 使用 ClickOnce 部署应用程序

11 在设计视图中再次双击 Timer 控件，并在计时器的 Tick 事件上添加以下代码片段：

```
progressBar1.Value += 10;
if (progressBar1.Value == progressBar1.Maximum) {
    pictureBox1.BackColor = colorDialog1.Color;
    timer1.Enabled = false;
}
```

前面的代码片段在计时器启用时触发计时器的 Tick 事件。在计时器的 Tick 事件处理程序中，我们将进度条值递增 10。当进度条值达到最大值 100 时，所选颜色加载到图片框中，计时器被禁用。

12 按 F5 键执行应用程序。输出出现。

13 单击 Pick Color 按钮打开颜色对话框。

14 从颜色对话框中选择一种颜色并单击 OK 按钮。

15 FillColor 应用程序已创建。让我们通过以下步骤学习部署此应用程序：

16 选择 File→Add→New Project 打开 Add New Project 对话框（图 C#-14.1）。

17 在 Installed Templates 窗格下选择 Other Project Types→Setup and Deployment→Visual Studio Installer（图 C#-14.1）。

18 在中间窗格中选择 Setup Wizard 选项（图 C#-14.1）。

19 在 Name 文本框中输入项目的名称。在我们的例子中，我们输入了 FillColorSetup（图 C#-14.1）。

单击 OK 按钮，如图 C#-14.1 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_374_0.png)

图 C#-14.1

Setup Wizard 出现并显示 Welcome to the Setup Project Wizard 页面，如图 C#-14.2 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_374_1.png)

图 C#-14.2

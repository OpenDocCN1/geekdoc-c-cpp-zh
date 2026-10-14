

## 如何创建使用 WCF 服务的网站

创建托管 WCF 服务的网站后，可以创建使用该服务的客户端网站。由于任何网站都可以作为客户端网站，你可以使用本书中学到的任何技能来开发该网站。然后，你可以向客户端网站添加对服务的引用，并编写使用该服务的代码。

### 如何向客户端网站添加服务引用

要使 WCF 服务可供网站使用，可以使用如图 23-11 所示的“添加服务引用”对话框添加对服务的引用。首先，需要输入指向该服务 .svc 文件的 URL。最简单的方法是从类似于上一张图中显示服务的 Web 浏览器中复制 URL。实际上，要添加这样的服务引用，宿主网站必须正在运行。为此，你需要打开两个 Visual Studio 实例，在一个实例中打开并运行宿主网站，在另一个实例中打开客户端网站，以便添加引用。

输入 URL 后，可以单击“转到”按钮在“服务”列表中显示该服务。最后，可以输入要为服务使用的命名空间名称，并单击“确定”按钮。在此示例中，我为命名空间输入了名称 HalloweenServices。

当你向网站添加对 WCF 服务的引用时，Visual Studio 会在解决方案资源管理器的 App_WebReferences 文件夹下为服务引用创建一个文件夹。此文件夹的名称与你在“添加服务引用”对话框中输入的命名空间名称相同。如果展开此文件夹，可以看到该服务的配置文件。由于这些文件是自动生成的，你不需要理解它们包含的代码。不过，如果你对这些文件的工作方式感到好奇，可以在文本编辑器中显示它们。

在继续之前，你应该意识到，如果用于运行宿主网站的开发服务器端口号与服务引用使用的端口号不同，客户端网站将无法定位到该服务。例如，如果你尝试运行本章中可从我们的网站下载的客户端网站，它将无法工作。要解决此问题，你需要从 App_WebReferences 文件夹中删除服务引用文件夹。然后，你需要启动宿主网站，并使用其 URL 将服务引用重新添加到客户端网站。

### 添加了对 WCF 服务的引用之后的网站

![](img/c024ccf88e28c30c07dd410d4342288f_792_0.png)

### 说明

- 要启动将使用 WCF 服务的网站，可以使用本书中学到的任何技术。
- 要使 WCF 服务可供网站使用，请添加对服务的引用。为此，请使用“网站→添加服务引用”命令显示“添加服务引用”对话框。然后，输入服务的 URL，单击“转到”按钮，输入服务的命名空间名称，并单击“确定”按钮。
- 当你添加对 WCF 服务的引用时，Visual Studio 会在解决方案资源管理器的 App_WebReferences 文件夹下为服务引用创建一个文件夹。如果展开此文件夹，可以看到该服务的配置文件。

图 23-11 如何向客户端网站添加服务引用

### 如何使用 WCF 服务

图 23-12 显示了如何从客户端网站使用 WCF 服务。此处显示的应用程序由一个简单的网页组成，该网页允许用户显示所选产品的信息。为此，用户输入产品代码并单击“获取产品数据”按钮。然后，应用程序使用你在图 23-5 中看到的 ProductService 服务来获取产品的名称、单价和类别。最后，应用程序将检索到的值显示在窗体上的标签中。

要为这样的应用程序编写代码，通常首先要为包含服务的命名空间添加 using 语句，以便更容易引用。此处指定的名称与你在“添加服务引用”对话框中输入的名称相同。在本例中，它是 HalloweenServices。

接下来，为服务创建客户端对象。由于此对象提供对服务定义的操作和数据类型的访问，因此它被称为服务的代理。要创建代理，请使用由定义服务的类名加上“Client”组成的类型名。例如，名为 ProductService 的服务的类型名是 ProductServiceClient。

创建代理后，可以使用它调用服务提供的操作。为此，可以使用与执行对象方法相同的技术。例如，在此图中，代码调用代理的 GetProduct 操作，并传递用户在文本框中输入的产品 ID。然后，它将此操作返回的 Product 对象存储在 Product 类型的变量中。接下来，关闭代理。最后，将 Product 对象的属性显示在网页上的标签中。

### 浏览器中的网页

![](img/c024ccf88e28c30c07dd410d4342288f_794_0.png)

### 网页的代码隐藏文件

```
using System;
using HalloweenServices;

public partial class _Default : System.Web.UI.Page
{
    protected void btnGetProduct_Click(object sender, EventArgs e)
    {
        // Create a proxy for the service
        ProductServiceClient client = new ProductServiceClient();

        // Get the data from the service
        Product p = client.GetProduct(txtProductID.Text);

        // Close the proxy
        client.Close();

        // Display the data
        lblName.Text = p.Name;
        lblUnitPrice.Text = p.UnitPrice.ToString("c");
        lblCategory.Text = p.CategoryID;
    }
}
```

### 说明

- 要使用 WCF 服务，请为该服务创建客户端对象或代理。为此，请使用由定义服务的类名加上“Client”组成的类型。
- 创建服务对象后，可以使用与执行任何对象方法相同的技术来执行其操作。
- 为了更容易地使用服务，可以为包含服务的命名空间包含 using 语句。

### 展望

虽然本章介绍的 WCF 服务很简单，但它展示了你可以用来开发更大型 WCF 服务的技术。因此，你在这里学到的基本技能足以让你开始开发自己的 WCF 服务。此外，当需要时，你也将准备好学习 WCF 服务编程的更复杂方面。

例如，在部署 WCF 服务之前，你可能想了解更多关于配置其端点的信息，以改进服务的功能或安全性。或者，如果你想使用 REST 而不是 SOAP，可以学习更多关于创建支持 REST 的 WCF 服务的信息。或者，如果你不想使用网站作为 WCF 服务的宿主或客户端，可以了解更多关于提供和使用 Web 服务的其他选项。

* * *

在本书中，我们尽力呈现了开发电子商务 Web 应用程序所需的所有技能。现在，如果你已经阅读了全部 23 章，我们希望你觉得已经为此做好了充分准备。你还应该觉得，在开发 Web 应用程序时，你已经拥有了学习任何其他所需知识所需的概念、技能和视角。如果是这样，这本书就完成了它的任务。感谢你的阅读。

### 术语

- web service：Web 服务
- ASMX web service：ASMX Web 服务
- WCF (Windows Communication Foundation)：WCF（Windows 通信基础）
- service-oriented development：面向服务的开发
- service：服务
- provide a service：提供服务
- consume a service：使用服务
- WAS (Windows Process Activation Service)：WAS（Windows 进程激活服务）
- endpoint：端点
- SOAP (Simple Object Access Protocol)：SOAP（简单对象访问协议）
- binding：绑定
- MTOM (Message Transmission Optimization Mechanism)：MTOM（消息传输优化机制）
- TCP (Transmission Control Protocol)：TCP（传输控制协议）
- named pipes：命名管道
- MSMQ (Microsoft Message Queuing)：MSMQ（Microsoft 消息队列）
- metadata exchange (mex) binding：元数据交换（mex）绑定
- mex endpoint：mex 端点
- REST (Representational State Transfer)：REST（表述性状态转移）
- JSON (JavaScript Object Notation)：JSON（JavaScript 对象表示法）
- POX (plain old XML)：POX（普通旧 XML）
- operation：操作
- attribute：属性
- member：成员
- proxy：代理


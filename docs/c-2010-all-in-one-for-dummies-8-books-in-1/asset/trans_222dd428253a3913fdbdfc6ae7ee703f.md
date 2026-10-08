

## Net 类如何融入框架

System.Net 命名空间包含 62 个类和 6 个较小的命名空间。在我写这些内容时，我感到目不应接。然而，如果你仔细观察，可以发现其中的模式。

如果你在使用类方面需要帮助，可以在第二本书中找到更多信息。

这些类的命名非常规范，你会注意到某些协议各对应若干类。在翻译后，你可以根据协议的命名方式缩小你需要的范围：

-   Authentication and Authorization（身份验证与授权）：这些类提供安全性。
-   Cookie：此类类管理来自 Web 浏览器的 Cookie，并用于 ASP.NET 页面。
-   DNS（域名服务）：这些类帮助将域名解析为 IP 地址。
-   EndPoint（端点）：此类类帮助定义网络节点。
-   FileWeb：这组精妙的类将网络文件服务器描述为本地类。
-   FtWeb：此类是一个简单的文件传输协议实现。
-   Http（超文本传输协议）：此类是 Web 协议。
-   IP（网协议）：此类类帮助定义专门与互联网相关的网络端点。
-   IrDA：此类是红外端点。红外端口也是网络！
-   NetworkCredential（网络凭据）：此类类帮助管理网络实现。
-   Service（服务）：此类类帮助管理网络连接。
-   Socket（套字）：此类类处理最原始的网络连接。
-   Upload（上传）：这组类帮助你将信息上传到互联网。
-   Web：这些类协助万维网——很大程度上是基于 http 类相互构建的实现。更面向任务。

这个列表之所以详尽，是因为类之间是相互构建的。Endpoint 类被 socket 类用于定义特定的网络细节，而 IP 类使它们特定于互联网。Web 类则专门用于万维网。你很少会使用最高级别的类，而且通常很难看出何时需要它们。

## 458 使用 System.Net 命名空间

尽管如此，你每天使用的大多数函数都封装在 System.Net 命名空间下的七个主要命名空间中：

-   Cache（缓存）：此函数有许多枚举器，用于管理命名空间内置的浏览器和网络缓存函数。
-   Configuration（配置）：此函数允许访问你需要设置的属性，以使许多其他 System.Net 类能够工作。
-   Mail（邮件）：此函数接管了 System.Web.Mail，以便于发送电子邮件。
-   MIME：此函数将文件附件与 Mail 命名空间捆绑。
-   NetworkInformation（网络信息）：此函数获取有关应用程序周围网络的详细信息。
-   Security（安全）：此函数实现了由 System.Net 许多类管理的网络安全。
-   Sockets（套接字）：此函数利用到 Windows 最基本的网络连接。

## 使用 System.Net 命名空间

System.Net 命名空间是面向代码的，这意味着很少实现是专门针对用户界面的。你使用这些类进行的所有操作都在后台完成。你很少拖放用户控件——System.Net 命名空间是在视图（Code View）中使用。

为了演示这一点，在本章的其余部分，我将介绍构建一个具有以下要求的 Windows Forms 应用程序：

-   检查网络状态。
-   从互联网获取特定文件。
-   发送到特定的电子邮件地址。
-   记录整个事务过程。

这并不是一组无关紧要的需求。事实上，即使在 C# 的 1.0 和 1.1 版本中，这也会很困难。该版本 System.Net 命名空间的主要目标之一是让常见任务变得简单得多。你可以从加载示例代码开始，或者启动新项目并按照后续章节中的步骤。

## 检查网络状态

首先，你需要按照以下步骤告知用户网络连接情况：

-   1. 在 Visual Studio 中创建一个新的 Windows Forms Application 项目。我将我的项目命名为 NetworkTools。
-   2. 从工具箱中拖入 StatusStrip 控件到表单上。
-   3. 选择出现的智能标记（SmartTag）并添加一个 StatusLabel。
-   4. 双击表单以获取 Form_Load 事件处理器并移动到代码。
-   5. 通过在代码顶部添加行 `using System.Net.NetworkInformation;` 来引用 System.Net 命名空间。
-   6. 添加以下加粗代码：

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Drawing;
using System.Linq;
using System.Net;
using System.Text;
using System.Windows.Forms;

namespace NetworkTools
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            if (NetworkInterface.IsAvailable())
            {
                toolStripStatus1.Text = "Connected";
            }
            else
            {
                toolStripStatus1.Text = "Disconnected";
            }
        }
    }
}
```

就这些。

## 从互联网下载文件

要从互联网获取文件，请遵循以下步骤：

-   1. 将按钮拖到表单上。
-   2. 双击按钮以获取 Click 事件处理器。
-   3. 在处理器中使用以下代码：

Streams 代表某种类型的数据流，以及来自互联网的信息流。当你从互联网获取 Web 页面或文件时，你所做的就是收集数据流，应用程序中的状态栏显示完成百分比。就像向杯子里倒水，数据流是一个流，因此该概念被命名为 Stream。

这个概念适用于从万维网获取文件，而且 HTTP 作为 Web 协议只是另一种定义文档从服务器通过互联网移动到你本地机器的协议。

## 使用 System.Net 命名空间

要从互联网获取文件，请遵循以下步骤：

```csharp
private void button_Click(object sender, EventArgs args)
{
    DownloadFile(@"http://ftp.punnies.net/sample.bmp", @"c:\sample.bmp");
}
```

## 列表 4-1: DownloadFile(string remoteFile, string localFile)

```csharp
{
    FileStream localFileStream = new FileStream(localFile, FileMode.Create);
    FtpWebRequest ftpRequest = (FtpWebRequest)remoteFile;
    ftpRequest.Method = WebRequestMethods.DownloadFile;
    ftpRequest.Credentials = new NetworkCredential("Anonymous", "bill@example.com");
    FtpResponse ftpResponse = ftpRequest.GetResponse();
    Stream buffer = ftpResponse.GetResponse();
    byte[] buffer = new byte[1024];
    int bytes = ftpResponse.Read(buffer, 0, 1024);
    while (bytes > 0)
    {
        localFileStream.Write(buffer, 0, bytes);
        bytes = ftpResponse.Read(buffer, 0, 1024);
    }
    localFileStream.Close();
    ftpResponse.Close();
}
```




# 458 走进 System.Net

- 日志传输
- 检查运行的应用程序周围的网络状态

请记住，我并不是说 socket、IPv6 以及各种高级 Internet 协议并不重要。本章介绍的是你每天都会用到的命名空间部分。一如既往，System.Net 仍有更多值得发现的内容。

# 认识 System.Net

System.Net 命名空间充满了许多类，这些类在文档中查看可能令人困惑，但在应用程序中使用时却非常有意义。该命名空间消除了处理 Internet 上使用的各种协议的复杂性。

Internet 协议有 2000 多个 RFC（RFC 是意见请求，是一种在成为标准之前发送给标准组织进行同行评审的文档）， 如果你必须单独学习所有的 RFC，你将无法完成你的项目。System.Net 命名空间让这个过程变得不那么痛苦。

System.Net 不仅用于 Web 项目。就像基类库中的其他所有内容一样，你可以在各种类型的项目中使用 System.Net。你可以：

- 从互联网上的网页获取信息并将其用于你的程序。
- 通过 FTP 在互联网传输文件。
- 轻松地发送电子邮件。
- 使用更高级的网络结构。
- 使用 SSL 协议通过互联网进行安全通信。

如果你需要从 Windows 应用程序检查计算机的连通性，可以使用 System.Net。如果你需要构建一个从网站下载文件的类，System.Net 正是你所需要的命名空间。由于大多数类都与 Internet 相关，但这并不意味着只有 Web 应用程序可以使用它。这就是 System.Net 的魔法之处。任何应用程序都可以是连接型应用程序。虽然命名空间的某些功能是为了让 Web 应用程序的开发更简单，但整个命名空间的设计是为了让任何应用程序都能与 Web 工作。

# Net 类如何融入框架

System.Net 命名空间包含 62 个类和 6 个较小的命名空间。即使在我写这些内容时，我也感到目不暇。不过，如果你仔细观察，可以发现其中的模式。

如果你在使用这些类方面需要帮助，可以在第二本书中找到更多信息。

这些类的命名很好，你会注意到某些协议各对应许多类。在翻译后，你可以根据协议的命名方式缩小范围到你需要的类：

- **认证 (Authentication)** 和 **授权 (Authorization)**：这些类提供安全性。
- **Cookie**：此类管理来自 Web 浏览器的 Cookie，并用于 ASP.NET 页面。
- **DNS** (域名系统服务)：这些类帮助将域名解析为 IP 地址。
- **下载 (Download)**：此类用于从服务器获取文件。
- **端点 (Endpoint)**：此类帮助定义网络节点。
- **FileWeb**：这组精妙类将网络文件服务器描述为本地类。
- **FtpWeb**：此类是一个简单的文件传输协议实现。
- **Http** (超文本传输协议)：此类是 Web 协议。
- **IP** (网际协议)：此类帮助定义专门与 Internet 的网络端点。
- **IrDA**：此类是一个红外线端点。红外端口也是网络！
- **NetworkCredential (网络凭据)**：此类是另一个安全实现。
- **Service (服务)**：此类帮助管理网络连接。
- **Socket**：此类处理最原始的网络连接。
- **上传 (Upload)**：这组类帮助你将信息上传到互联网。
- **Web**：这些类帮助处理世界维网——大部分是更具方向性的 http 类的实现。

这个列表非常详尽，是因为类是相互构建的。Endpoint 类被 socket 类用于定义特定的网络细节，

![](img/6df7bb88e9302e98442acc219cfbd7fc_484_0.png)

# 460 使用 System.Net 命名空间

并且 IP 类使它们专门用于 Internet。Web 类则专门用于世界维网。你很少会使用最高级别的类，但在确定何时需要它们时通常是很困难的。

不过，你每天使用的大多数函数都封装在 System.Net 命名空间下的七个大部分新的命名空间中：

- **Cache (缓存)**：此功能包含许多枚举器，用于管理命名空间内置的浏览器和网络缓存功能。
- **Configuration (配置)**：此功能允许访问使任何其他 System.Net 类正常工作所需的属性。
- **Mail (邮件)**：此功能接管了 System.Web.Mail 以方便发送电子邮件。
- **MIME**：此功能将文件附件与 Mail 命名空间包在一起。
- **NetworkInformation (网络信息)**：此功能获取有关你应用程序周围的网络详细信息。
- **Security (安全)**：此功能实现了由 System.Net 许多类管理的网络安全。
- **Sockets (套接字)**：此功能利用 Windows 提供的最基础的网络连接。

# 使用 System.Net 命名空间

System.Net 命名空间是面向代码的，这意味着很少有实现是专门针对用户界面的。你通过这些类进行的所有操作都在后台进行。你很少有拖放的用户控件——System.Net 命名空间是在代码视图（Code View）中使用。你通过这些类进行的所有操作都在后台进行。你很少有拖放的用户控件——System.Net 命名空间是在代码视图中使用。

为了演示这一点，你需要在代码视图中使用这些类来执行：

- 检查连接。
- 从网站下载文件。
- 使用 SSL 协议通过互联网进行安全通信。
- 轻松发送电子邮件。

你通过这些类进行的所有操作都在后台进行。你很少有拖放的用户控件——System.Net 命名空间是在代码视图中使用。

为了演示这一点，你需要在代码视图中使用这些类来执行。为了实现这些功能，请执行以下步骤：

1. 在 Windows 应用程序中，添加一个拖放的用户控件。
2. 从工具箱中拖入一个控件。
3. 双击该控件以获取事件处理程序。
4. 在代码顶部添加所需的引用。
5. 在代码视图中，使用 `System.Net`。
6. 在代码顶部添加 `System.Net`。

为了实现这些功能，请执行以下步骤：

1. 在 Windows 应用程序中，添加一个拖放的用户控件。
2. 从工具箱中拖入一个控件。
3. 双击该控件以获取事件处理程序。
4. 在代码顶部添加所需的引用。
5. 在代码视图中，使用 `System.Net`。
6. 在代码顶部添加 `System.Net`。

为了实现这些功能，请执行以下步骤：

1. 在 Windows 应用程序中，添加一个拖放的用户控件。
2. 从工具箱中拖入一个控件。
3. 双击该控件以获取事件处理程序。
4. 在代码顶部添加所需的引用。
5. 在代码视图中，使用 `System.Net`。
6. 在代码顶部添加 `System.Net`。

为了实现这些功能，请执行以下步骤：

1. 在 Windows 应用程序中，添加一个拖放的用户控件。
2. 从工具箱中拖入一个控件。
3. 双击该控件以获取事件处理程序。
4. 在代码顶部添加所需的引用。
5. 在代码视图中，使用 `System.Net`。
6. 在代码顶部添加 `System.Net`。

为了检查状态，请执行以下步骤：

1. 从工具箱中拖入一个 `StatusLabel` 控件。
2. 双击该控件以获取 `Load` 事件处理程序。
3. 使用 `System.Net` 命名空间。

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Drawing;
using System.Linq;
using System.Net;
using System.Text;
using System.Threading.Tasks;
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
                toolStrip1.Text = "Connected";
            }
            else
            {
                toolStrip1.Text = "Disconnected";
            }
        }
    }
}
```

# 462 使用 System.Net 命名空间

这就是全部内容。NetworkInformation 类包含了关于网络、IP 地址和网关的信息。

![](img/6df7bb88e9302e98442acc219cfbd7fc_487_0.png)

请记住，NetworkInformation 类仅适用于本地机器。如果你在 ASP.Net Web 应用程序中使用此类，将获取服务器的信息。

# 从互联网下载文件

你可以通过多种方式从互联网获取文件，最常用的方法是使用 FTP。FTP 协议受到青睐，是因为它是安全的并且支持许多系统。

要构建使用 FTP 的应用程序，请执行以下步骤：

1. 从工具箱中拖入一个按钮。
2. 双击该按钮以获取 Click 事件处理程序。
3. 在代码顶部添加所需的导入：`System.Net`、`System.Net.Mail` 和 `System.IO`。
4. 创建一个名为 `DownloadFile` 的新方法，接受远程文件名和文件名作为字符串。
5. 在新方法中，创建一个 `FileStream`（命名为 `localFileStream`）和 `FTPWebRequest`（命名为 `ftpRequest`），如列表 4-1 所示。

FileStream 引用本地文件并接受传入方法的本地文件。FtpWebRequest 是用于远程文件的。

# 列表 4-1：Download 方法

```csharp
private void DownloadFile(string remoteFile, string localFile)
{
    FileStream localFileStream = new FileStream(localFile, FileMode.OpenCreate);
    FTPWebRequest ftpRequest = (FTPWebRequest)WebRequest.Create(remoteFile);
    ftpRequest.Method = WebRequest.Methods.DownloadFile;
    ftpRequest.Credentials = new NetworkCredential("Anonymous", "bill@sempf.net");
    Stream ftpResponse = ftpRequest.GetResponseStream();
    byte[] buffer = new byte[1024];
    int bytesRead = ftpResponse.Read(buffer, 0, 1024);
    while (bytesRead > 0)
    {
        localFileStream.Write(buffer, 0, bytesRead);
        bytesRead = ftpResponse.Read(buffer, 0, 1024);
    }
    localFileStream.Close();
    ftpResponse.Close();
}
```


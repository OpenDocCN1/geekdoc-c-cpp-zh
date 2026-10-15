

```
foreach (IChannelReceiver chan in ChannelServices.RegisteredChannels)
{
    lbServices.Items.Add(chan.ChannelName);
}
UpdateDesc();
}
private void UpdateDesc()
{
    TextBox1.Text = "";
    if (lbServices.Items.Count > 0)
    {
        if (lbServices.SelectedItems.Count > 0)
        {
            IChannelReceiver chan =
                (IChannelReceiver)ChannelServices.GetChannel(
                System.Convert.ToString(lbServices.SelectedItem));
            string strDesc = null;
            foreach (string UriName in
                ((ChannelDataStore)chan.ChannelData).ChannelUris)
            {
                strDesc += UriName + System.Environment.NewLine;
            }
            TextBox1.Text = strDesc;
            TextBox1.Text += "Priority : " + chan.ChannelPriority.ToString();
        }
    }
}
private void Form1_Load(object sender, EventArgs e)
{
    ListServices();
}
private void btnStopSelected_Click(object sender, EventArgs e)
{
    if (lbServices.Items.Count > 0)
    {
        if (lbServices.SelectedItems.Count > 0)
        {
            IChannelReceiver chan =
                (IChannelReceiver)ChannelServices.GetChannel(
                System.Convert.ToString(lbServices.SelectedItem));
            ChannelServices.UnregisterChannel(chan);
            chan.StopListening(null);
            ListServices();
            txtStatusBar.Text = "Disconnected";
        }
    }
}
private void rbtnHttpChannel_CheckedChanged(object sender, EventArgs e)
{
    if (rbtnHttpChannel.Checked)
    {
        rbtnSoap.Checked = true;
        GroupBox1.Enabled = false;
    }
}
private void rbtnTcpChannel_CheckedChanged(object sender, EventArgs e)
{
    GroupBox1.Enabled = true;
}
private void lbServices_SelectedIndexChanged(object sender, EventArgs e)
{
    UpdateDesc();
}
private void btnRefresh_Click(object sender, EventArgs e)
{
}
private void btnStartServer_Click(object sender, EventArgs e)
{
	Start();
}
}
```

> **注意**
> 要运行 DBServer 应用程序以及其他任何应用程序，您需要添加以下程序集的引用：
> System.Runtime.Remoting;
> System.Runtime.Serialization;
> System.ServiceModel.Channels.Formatters.Soap

构建 DBServer 应用程序，然后执行 DBServer.exe 文件。图 35.7 显示了 DBServer 主机应用程序的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1647_0.png)

- 枚举已注册的通道
- 注销通道
- 注册对象
- 指定格式化程序

## 枚举已注册的通道

注册通道会在客户端系统和服务器系统之间创建一个隧道。当通道被注册后，所有的通信都将通过该通道进行。通道可以是 HTTP 通道、TCP 通道或自定义通道。以下代码片段显示了如何在 DBServer 应用程序中注册 TCP 通道：

```
ChannelServices.RegisterChannel(new TcpChannel(), false);
```

在前面的代码片段中，我们使用了 RegisterChannel() 方法来注册 TCP 通道。此方法接受两个参数，一个通道对象和一个布尔值，用于指定是否对调用保持协议安全设置开启或关闭。在我们的例子中，第二个参数设置为 False。

您可以通过使用 ChannelServices 类的 RegisteredChannels() 方法来创建所有已注册通道的枚举，如以下代码片段所示：

```
foreach (IChannelReceiver chan in ChannelServices.RegisteredChannels)
{
    lbServices.Items.Add(chan.ChannelName);
}
```

要检索与通道关联的通道名称和 URI 列表，如以下代码片段所示：

```
IChannelReceiver chan =
(IChannelReceiver)ChannelServices.GetChannel(System.Convert.ToString(lbServices.SelectedItem));
string strDesc = null;
foreach (string UriName in ((ChannelDataStore)chan.ChannelData).ChannelUris)
{
    strDesc += UriName + System.Environment.NewLine;
}
TextBox1.Text = strDesc;
TextBox1.Text += "Priority : " + chan.ChannelPriority.ToString();
```

## 注销通道

如果您已注册一个通道，并且稍后想要注销它以便使用其他通道，您可以轻松地注销该通道，如以下代码片段所示：

```
if (lbServices.SelectedItems.Count > 0)
{
    IChannelReceiver chan=
    (IChannelReceiver)ChannelServices.GetChannel(System.Convert.ToString(lbServices.SelectedItem));
    ChannelServices.UnregisterChannel(chan);
    chan.StopListening(null);
    ListServices();
    txtStatusBar.Text = "disconnected";
}
```

## 注册对象

如“深入探讨”部分所述，可远程对象有三种类型——SingleCall、Singleton 和 CAO。您可以使用 RemotingConfiguration 类的 RegisterWellKnownServiceType() 方法来注册 SingleCall 对象，如以下代码片段所示：

```
RemotingConfiguration.RegisterWellKnownServiceType(
    typeof(Sharedobject.Sharedobject), "HiServerApp/HiServer", WellKnownObjectMode.SingleCall);
```

您可以使用 RemotingConfiguration 类的 RegisterWellKnownServiceType() 方法来注册 Singleton 对象，如以下代码片段所示：

```
RemotingConfiguration.RegisterWellKnownServiceType(typeof(Sharedobject.Sharedobject), "HiServerApp/HiServer", WellKnownObjectMode.Singleton);
```

您可以使用 RemotingConfiguration 类的 RegisterActivatedServiceType() 方法来注册 CAO 对象，如以下代码片段所示：

## 指定格式化程序

指定格式化程序意味着指定消息的格式，例如二进制或 SOAP。这些格式化程序由通道用于在网络上传输二进制或 SOAP 格式的消息。默认情况下，TcpChannel 类使用二进制格式化程序，HttpChannel 类使用 SOAP 格式化程序。然而，这两个通道都可以使用两种格式化程序中的任何一种。以下代码片段显示了 TcpChannel 类如何使用 SOAP 格式化程序：

```
IChannel chan;
IServerChannelSinkProvider SProvider;
IClientChannelSinkProvider CProvider;
...
SProvider = new BinaryServerFormatterSinkProvider();
CProvider = new BinaryClientFormatterSinkProvider();
chan = new TcpChannel(props, CProvider, SProvider);
...
ChannelServices.RegisterChannel(chan, false);
```

在前面的代码片段中，我们创建了提供格式化程序 sink 的提供程序的实例，以使用格式化程序类将格式化程序与通道关联。BinaryServerFormatterSinkProvider 和 BinaryClientFormatterSinkProvider 对象分别提供 IServerChannelSinkProvider 对象和 IClientChannelSinkProvider 对象，它们使用 BinaryFormatter 类以二进制格式对消息进行编码。

创建 sink 提供程序后，您可以指定格式化程序，如以下代码片段所示：

```
private void Start()
{
    try
    {
        IDictionary props = null;
        props = new Hashtable();
        props["port"] = TextBox2.Text;
        if (rbtnBinary.Checked)
        {
            SProvider = new BinaryServerFormattersSinkProvider();
            CProvider = new BinaryClientFormattersSinkProvider();
            if (cbtnFullTrust.Checked)
            {
                ((BinaryServerFormattersSinkProvider)SProvider).TypeFilterLevel = TypeFilterLevel.Full;
            }
        }
        else if (rbtnSoap.Checked)
        {
            SProvider = new SoapServerFormattersSinkProvider();
            CProvider = new SoapClientFormatterSinkProvider();
            if (cbtnFullTrust.Checked)
            {
                ((SoapServerFormattersSinkProvider)SProvider).TypeFilterLevel = TypeFilterLevel.Full;
            }
        }
        if (rbtnTcpChannel.Checked)
        {
            chan = new TcpChannel(props, CProvider, SProvider);
        }
        else if (rbtnHttpChannel.Checked)
```

```
{
	chan = new HttpChannel(CProvider, SProvider);
}
ChannelServices.RegisterChannel(chan, false);
if (rbtnSingleCall.Checked)
{
	RemotingConfiguration.RegisterWellKnownServiceType(
		typeof(SharedObject.SharedObject), "HiServerApp/HiServer",
		WellKnownObjectMode.SingleCall);
}
else if (rbtnSingleTon.Checked)
{
	RemotingConfiguration.RegisterWellKnownServiceType(
		typeof(SharedObject.SharedObject), "HiServerApp/HiServer",
		WellKnownObjectMode.Singleton);
}
else if (rbtnActivated.Checked)
{
	RemotingConfiguration.RegisterActivatedServiceType(
		typeof(SharedObject.SharedObject));
}
Thd = System.Threading.Thread.CurrentThread;
	txtStatusBar.Text = "Connected";
}
catch (Exception ex)
{
	txtStatusBar.Text = ex.Message;
}
}
```

现在让我们学习如何创建一个 SingleCall 客户端对象。

## 创建 SingleCall 客户端对象

在本节中，您将学习如何创建一个 SingleCall 客户端应用程序，该应用程序充当 DBServer 主机应用程序的客户端。每次为客户端的调用服务时都会创建一个新的 SingleCall 对象，并在服务后销毁。让我们创建一个名为 WellKnownSingleCallClient 的 Windows 窗体应用程序，以学习如何创建 SingleCall 客户端对象。此应用程序的设计和源代码可在光盘上获得。

### 列表 35.6：显示 WellKnownSingleCallClient 应用程序的 Form1.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Runtime.Remoting;
using System.Runtime.Remoting.Channels;
using System.Runtime.Remoting.Channels.Tcp;
using System.Runtime.Remoting.Activation;
using SharedObject;

namespace WellKnownSingleCallClient
{
	public partial class Form1 : Form
	{
		public Form1()
		{
			InitializeComponent();
		}
	}
}
```

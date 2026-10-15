

```csharp
last = new Point(e.X, e.Y);
Array.Resize(ref Points, NumberPoints + 1);
Points[NumberPoints] = last;
NumberPoints += 1;
if (NumberPoints >= 2)
{
try
{
if (bConnected)
{
Obj.confer(down, last);
}
}
catch (Exception ex)
{
txtStatusBar.Text = ex.Message;
}
g.DrawLine(MyPen, down, last);
}
down = last;
}
}
private void rbtnTcpChannel_CheckedChanged(object sender, EventArgs e)
{
GroupBox4.Enabled = true;
}
private void rbtnHttpChannel_CheckedChanged(object sender, EventArgs e)
{
if (rbtnHttpChannel.Checked)
{
rbtnSoap.Checked = true;
GroupBox4.Enabled = false;
}
}
```

注意：你可以通过安装 microsoft.directx.dll 程序集来导入 Microsoft.DirectX 命名空间。

5. 构建 WellKnownSingleTonClient 应用程序并执行其 WellKnownSingleTonClient.exe 文件。图 35.10 显示了 WellKnownSingleTonClient 应用程序的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1656_0.png)

## 图 35.10：显示 WellKnownSingleTonClient 应用程序的输出

现在，让我们一起执行 DBServer.exe 和 WellKnownSingleTonClient.exe 文件，如图 35.11 所示：

> 图 35.11：显示连接到共享数据的 Singleton 对象的应用程序

在执行 DBServer 应用程序期间，你需要在服务类型组中选择 WellKnown SingleTon 单选按钮。这将启动你的主机应用程序。单击刷新按钮并在控制面板组中选择通道类型。这将返回机器地址，你需要将其复制到 WellKnownSingleTonClient 应用程序的文本框中。请注意，这些应用程序需要在建立连接前以完全信任运行。

> 注意

如果你尝试连接跨网络运行的应用程序，你可能会遇到应用程序执行某些操作的问题。这是由权限不足造成的。为避免这种情况，你需要设置系统安全以允许这些应用程序正常运行。

要编译 WellKnownSingleTonClient 应用程序，你需要在计算机上安装一些 DirectX 程序集。图 35.11 显示了连接到 DBServer 中 Singleton 对象的两个 WellKnownSingleTonClient 应用程序实例，并模仿彼此的绘画笔触：

让我们现在学习创建 CAO 对象。

## 创建客户端激活对象

如“深入”部分所述，CAO 对象在每次新客户端需要访问它时都会被激活，并且每个对象为其各自的客户端保存会话状态。在本节中，你将学习创建名为 ClientActivatedClient 的 Windows 窗体应用程序，该应用程序展示了如何创建 CAO 对象。此应用程序的设计和源代码可在光盘上获得。列表 35.9 显示了 ClientActivatedClient 应用程序的 Form1.cs 文件的代码：

## 列表 35.9：显示 ClientActivatedClient 应用程序的代码

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
using System.Runtime.Remoting.Channels.Http;
using System.Runtime.Remoting.Activation;
using System.Runtime.Serialization;
using System.Runtime.Serialization.Formatters;
using System.Collections;
using SharedObject;

namespace ClientActivatedClient
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private TimeSpan TimeSp = new TimeSpan(0);
        private bool bConnected = false;
        private IChannel chan;
        private IServerChannelSinkProvider SProvider;
        private IClientChannelSinkProvider CProvider;
        private IDictionary props;
        private SharedObject.Sharedobject Obj;
        public EventSink sink;
        private void Button1_Click(object sender, EventArgs e)
        {
            try
            {
                string URI = null;
                IDictionary props = null;
                props = new Hashtable();
                props["port"] = "0";
                if (rbtnBinary.Checked)
                {
                    SProvider = new BinaryServerFormatterSinkProvider();
                    CProvider = new BinaryClientFormatterSinkProvider();
                    if (cbtnFullTrust.Checked)
                    {
                        ((BinaryServerFormatterSinkProvider)SProvider).TypeFilterLevel = TypeFilterLevel.Full;
                    }
                }
                else if (rbtnSoap.Checked)
                {
                    SProvider = new SoapServerFormatterSinkProvider();
                    CProvider = new SoapClientFormatterSinkProvider();
                    if (cbtnFullTrust.Checked)
                    {
                        ((SoapServerFormatterSinkProvider)SProvider).TypeFilterLevel = TypeFilterLevel.Full;
                    }
                }
                if (rbtnTcpChannel.Checked)
                {
                    if (!cbtnFullTrust.Checked)
                    {
                        chan = new TcpChannel();
                    }
                    else
                    {
                        chan = new TcpChannel(props, CProvider, SProvider);
                    }
                    URI = "tcp://localhost:" + TextBox2.Text;
                }
                else if (rbtnHttpChannel1.Checked)
                {
                    if (!cbtnFullTrust.Checked)
                    {
                        chan = new HttpChannel();
                    }
                    else
                    {
                        chan = new HttpChannel(props, CProvider, SProvider);
                    }
                    URI = "http://localhost:" + TextBox2.Text;
                }
                ChannelServices.RegisterChannel(chan, false);
                RemotingConfiguration.RegisterActivatedClientType(
                    typeof(SharedObject.SharedObject), URI);
                Obj = new SharedObject.SharedObject();
                if (cbtnFullTrust.Checked)
                {
                    MessageBox.Show("FullTrust");
                    StatusEvent StMtd = new StatusEvent(this.StausMethod);
                    sink = new EventSink(StMtd);
                    Obj.Status += new StatusEvent(sink.OnStatus);
                }
                txtStatusBar.Text = "Connected";
                bConnected = true;
            }
            catch (Exception ex)
            {
                txtStatusBar.Text = ex.Message;
            }
        }
        private void Button2_Click(object sender, EventArgs e)
        {
            if (bConnected)
            {
                Obj.Greeting(TextBox1.Text);
            }
        }
        private void Button3_Click(object sender, EventArgs e)
        {
            if (bConnected)
            {
                MessageBox.Show(Obj.GetCount().ToString());
            }
        }
        private void Button4_Click(object sender, EventArgs e)
        {
            if (chan != null)
            {
                ChannelServices.UnregisterChannel(chan);
                SProvider = null;
                CProvider = null;
                chan = null;
                Obj = null;
                bConnected = false;
                txtStatusBar.Text = "Disconnected";
            }
        }
        public void StausMethod(string msg)
        {
            System.Diagnostics.Debug.WriteLine(msg);
        }
        private void rbtnTcpChannel_CheckedChanged(object sender, EventArgs e)
        {
            GroupBox1.Enabled = true;
        }
        private void rbtnHttpChannel_CheckedChanged(object sender, EventArgs e)
        {
            if (rbtnHttpChannel.Checked)
            {
                rbtnSoap.Checked = true;
                GroupBox1.Enabled = false;
            }
        }
        private void timer1_Tick(object sender, EventArgs e)
        {
            TimeSp.Add(TimeSpan.FromSeconds(1));
        }
        private void Button5_Click(object sender, EventArgs e)
        {
            if (bConnected)
            {
                obj.ClimbTheCliff();
                System.Diagnostics.Debug.WriteLine("Call Complete");
            }
        }
    }
}
```

构建 ClientActivatedClient 应用程序并执行 ClientActivatedClient.exe 文件。图 35.12 显示了 ClientActivatedClient 应用程序的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1660_0.png)

## 图 35.12：显示 ClientActivatedClient 应用程序的输出

现在，让我们一起执行 DBServer.exe 和 ClientActivatedClient.exe 文件，如图 35.13 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1661_0.png)

## 图 35.13：显示连接到 CAO 的两个应用程序

在执行 DBServer 应用程序期间，你需要在服务类型组中选择 WellKnown SingleTon 单选按钮、合适的通道和格式化程序 sink 提供程序，然后单击启动服务器按钮。这将启动你的主机应用程序。单击刷新按钮并在控制面板组中选择通道类型。这将返回主机应用程序正在运行的机器地址。

你可以运行多个 ClientActivatedClient 应用程序实例并将它们连接到服务器。在 ClientActivatedClient 应用程序中，选择合适的通道和格式化程序 sink 提供程序，然后单击连接按钮以将客户端与服务器连接。请注意，ClientActivatedClient 应用程序中选择的通道和格式化程序 sink 提供程序不应与 DBServer 应用程序中选择的通道和格式化程序 sink 提供程序不同。当你单击连接按钮时，客户端将连接到主机应用程序。问候按钮的功能与它在 WellKnownSingleCallClient 和 WellKnownSingleTonClient 应用程序中执行的功能相同。单击计数按钮会显示连接到对象的客户端数量。同样，单击攀登悬崖按钮会调用 SharedObject 程序集的 ClimbTheCliff() 方法，并在从睡眠模式出来时返回指定的消息。断开连接按钮将客户端与主机应用程序断开。

> 注意
> 如果你尝试连接跨网络运行的应用程序，你可能会遇到应用程序执行某些操作的问题。这是由权限不足造成的。为避免这种情况，你需要设置系统安全以允许这些应用程序正常运行。

让我们现在在下一节中回顾本章的主要要点。

## 摘要

在本章中，你学习了用于在应用程序之间建立通信的 .NET 远程处理。本章首先解释了 .NET 远程处理的架构，其中包括应用程序域、通道和格式化程序等各种概念。接下来，你学习了远程对象的托管以及为对象设置租约时间。你还学习了如何在“即时解决方案”部分中创建应用程序域、托管服务器和包括 SingleCall、SingleTon 和 CAO 对象在内的客户端应用程序。

在下一章中，你将学习 .NET 4.0 中的安全性。


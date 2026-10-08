
- 4. 将列表 29.8 提供的代码添加到 `WellKnownSingleClient` 应用程序的 `Form1.cs` 文件中：

列表 29.8：`WellKnownSingleClient` 应用程序的代码

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Runtime.Remoting;
using System.Runtime.Remoting.Channels;
using System.Runtime.Remoting.Channels.Http;
using System.Runtime.Remoting.Activation;
using System.Runtime.Serialization;
using System.Runtime.Serialization.Formatters;
namespace WellKnownSingleClient
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
```

## 解决方案

```csharp
cProvider = null;
chan = null;
Ob = null;
bConnected = false;
txtStatusBar.Text = "disconnected";
}
```

```csharp
private void button4_Click_1(object sender, EventArgs e)
{
    if (NumberPoints > 0)
    {
        System.Array.Clear(Points, 0, NumberPoints);
        NumberPoints = 0;
    }
    panel1.Invalidate();
}
private void rbtnTcpChannel_CheckedChanged_1(object sender, EventArgs e)
{
    groupbox4.Enabled = true;
}
private void rbtnTcpChannel_CheckedChanged(object sender, EventArgs e)
{
    if (rbtnSoap_Checked)
    {
        rbtnSoap.Checked = true;
        groupbox4.Enabled = false;
    }
}
private void panel1_MouseDown_1(object sender, MouseEventArgs e)
{
    if (NumberPoints > 0)
    {
        System.Array.Clear(Points, 0, NumberPoints);
        NumberPoints = 0;
    }
}
private void panel1_MouseMove_1(object sender, MouseEventArgs e)
{
    if (e.Button == System.Windows.Forms.MouseButtons.Left)
    {
        last = new Point(e.X, e.Y);
        Array.Resize(Points, NumberPoints + 1);
        Points[NumberPoints] = last;
        NumberPoints++;
        if (NumberPoints >= 2)
        {
            try
            {
                if (bConnected)
                {
                    Obj.Confer(down, last);
                }
            }
            catch (Exception ex)
            {
                txtStatusBar.Text = ex.Message;
            }
            g.DrawLine(MyPen, down, last);
            down = last;
        }
    }
}
private void Form1_Load_1(object sender, EventArgs e)
{
    g = panel1.CreateGraphics();
    MyPen = new Pen(Color.Black, 5F);
}
```

1319

## 第 29 章：C# 5.0 中的 .NET Remoting

```csharp
}
    private void Form1_Paint(object sender, PaintEventArgs e)
{
    if (NumberLines >= 2)
    {
        g.DrawLines(MyPen, Points);
    }
}
```

注意
你可以通过安装 `Microsoft.DirectX.dll` 汇集来导入 `Microsoft.DirectX` 命名空间。

- 5. 构建 `WellKnownSingleTonClient` 并执行其 `WellKnownSingleTonClient.exe` 文件。图 29.11 显示了 `WellKnownSingleTonClient` 程序的输出：

![](img/17af790174c480761404624aeed9b30b_1359_0.png)

图 29.11：`WellKnownSingleTonClient` 程序的输出

现在，让我们执行 `DBServer` 和 `WellKnownSingleTonClient` 文件，如图 29.12 所示：

![](img/17af790174c480761404624aeed9b30b_1359_1.png)

图 29.12：连接到共享事件数据的单例对象的应用程序

1320

## 解决方案

在执行 `DbServer` 程序期间，你需要在 Service Type 组中选择 `WellKnown SingleTon` 单选按钮、适当的通道和格式化器接收器提供程序，并点击 `Start Server` 按钮。这将启动你的应用程序。点击 `Refresh` 按钮并在 Control Panel 组中选择通道类型。这将返回机器地址，你需要将地址复制到 `WellKnownSingletonClient` 应用程序的文本框中。注意，这些应用程序需要全信任模式运行；因此，在建立连接之前，请在 `WellKnownSingletonClient` 应用程序的表单中勾选 `Full trust` 选框。

注意

如果你尝试跨网络使用 Remoting，可能会遇到权限问题。由于这些应用程序需要全信任模式运行；因此在建立连接之前，请在 `WellKnownSingletonClient` 应用程序的表单中勾选 `Full trust` 选框。

创建单例对象的状态

在执行 `DbServer` 程序期间，你需要在 Service Type 组中选择 `WellKnown SingleTon` 单选按钮、适当的通道和格式化器接收器提供程序，并点击 `Start Server` 按钮。这将启动你的应用程序。点击 `Refresh` 按钮并在 Control Panel 组中选择通道类型。这将返回机器地址，你需要将地址复制到 `WellKnownSingletonClient` 应用程序的文本框中。注意，这些应用程序需要全信任模式运行；因此在建立连接之前，请在 `WellKnownSingletonClient` 应用程序的表单中勾选 `Full trust` 选框。

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Threading;
using System.Windows.Forms;
using System.Runtime.Remoting;
using System.Runtime.Remoting.Channels;
using System.Runtime.Remoting.Channels.Tcp;
using System.Runtime.Remoting.Channels.Http;
using System.Runtime.Serialization;
    private void button1_click(object sender, EventArgs e)
    {
        try {
            string URI = null;
            IDictionary props = null;
            props = new Hashtable();
            props["port"] = "0";
            if (rbSoap_Checked)
            {
                props["port"] = "WellKnown.Client";
            }
            if (rbtnTcpChannel.Checked)
            {
                props["port"] = "tcp://localhost:8080";
            }
            if (rbtnHttpChannel.Checked)
            {
                props["port"] = "http://localhost:8080";
            }
            if (chan == null)
            {
                if (rbtnTcpChannel.Checked)
                {
                    chan = new TcpChannel(props, false);
                }
                else if (rbtnHttpChannel.Checked)
                {
                    chan = new HttpChannel(props, false);
                }
            }
            if (chan != null)
            {
                ChannelServices.Register(chan);
                RemotingConfiguration.RegisterDelegate(typeof(SharedObject), "Object");
            }
        }
        catch (Exception ex)
        {
            txtStatusBar.Text = ex.Message;
        }
    }
```

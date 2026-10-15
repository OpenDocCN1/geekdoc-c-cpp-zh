

## NOTE

在执行 AppOne.exe 和 AppTwo.exe 期间，如果你在任务管理器窗口中检查进程条目，你会发现那里只列出了一个名为 AppOne.exe 的进程。这表明两个应用程序都在单个应用程序域中运行。

你可以点击显示消息框的 Access Object Created in the Default AppDomain 按钮，如图 35.3 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1642_0.png)

图 35.3：显示消息框以创建 Access 对象实例

点击此消息框中的 OK 按钮后，会显示另一个消息框，如图 35.4 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1642_1.png)

图 35.4：在应用程序默认 AppDomain 中访问对象

图 35.4 所示的消息框表明，该对象上的方法仅在默认 AppDomain 中被调用。

让我们现在学习在额外的应用程序域中使用对象。

## Using Objects in another Application Domain

你可以使用 AppDomain 类的 CreateDomain() 方法在除应用程序默认域之外的域中创建对象。

让我们执行以下步骤来创建一个额外的域：

- 1. 在 AppOne 应用程序的 Form1 中添加一个额外的 Button 控件，其文本设置为 Click the Access Object Created in the Secondary AppDomain。
- 2. 在 AppOne 应用程序中添加 System.Reflection 和 System.Runtime.Remoting 命名空间：
- 3. 在 Button 控件 button3 的 Click 事件中添加以下代码片段：

```
private void button3_Click(object sender, EventArgs e)
{
AppDomain SecondAppDomain = AppDomain.CreateDomain("Second AppDomain");
ObjectHandle objH=SecondAppDomain.CreateInstance("AppTwo", "AppTwo.AClassInAppTwo",
true, BindingFlags.CreateInstance, null, new object[]{" - " +
AppDomain.CurrentDomain.FriendlyName+ " says Hi! -"}, null, null, null);
object obj=objH.Unwrap();
((AppTwo.AClassInAppTwo)obj).ASimpleMethod();
}
```

- 4. 构建 AppTwo 应用程序并将 AppTwo.exe 文件复制到 AppOne 应用程序的 Debug 文件夹中。
- 5. 构建 AppOne 应用程序并执行 AppOne.exe 文件。现在，点击 Click the Access Object Created in the Secondary AppDomain 按钮，它会显示一个消息框，如图 35.5 所示：

### Figure 35.5: Displaying a Message Box to Show an Instance of Secondary Application Domain

点击此消息框中的 OK 按钮后，会显示另一个消息框，如图 35.6 所示：

### Figure 35.6: Accessing an Object Created in Secondary Application Domain

让我们现在创建一个可远程对象。

## Creating a Remotable Class

要创建可远程类，你需要继承 MarshalByRefObject 类。让我们创建一个名为 SharedObject 的类库应用程序（也在 CD 上提供）来创建可远程类 SharedObject。SharedObject 类派生自 MarshalByRefObject 类，以便该类的对象可以远程使用。SharedObject 应用程序的 Class1.cs 文件的代码在清单 35.4 中给出：

### Listing 35.4: Showing the Code of the Class1.cs File of the SharedObject Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Runtime.Remoting.Lifetime;
using System.Runtime.Remoting.Messaging;
using System.Drawing;

namespace SharedObject
{
    public delegate void StrokeEvent (Point from, Point till);
    public delegate void StatusEvent(string msg);
    [Serializable()]
    public class SharedObject:MarshalByRefObject
    {
        private static int Count = 0;
        public event StatusEvent Status;
        public event StrokeEvent Stroke;
        public SharedObject()
        {
            Count += 1;
```

![](img/e073a4882197be4ab61103cbe0bcb394_1643_0.png)

![](img/e073a4882197be4ab61103cbe0bcb394_1643_1.png)

```
public int GetCount()
{
    return Count;
}
public void Greeting(string name)
{
    System.Diagnostics.Debug.Write("SharedObject says Hi: " + name);
    if (Status != null)
        Status("SharedObject says Hi : " + name);
}
public void Confer(Point from, Point Till)
{
    if (Stroke != null)
        Stroke(from, Till);
}
public override object InitializeLifetimeService()
{
    ILease myLease = (ILease)base.InitializeLifetimeService();
    myLease.InitialLeaseTime = TimeSpan.FromMinutes(10);
    myLease.RenewOnCallTime = TimeSpan.FromMinutes(50);
    return myLease;
}
}
```

现在，使用 Build→Build SharedObject 菜单项构建 SharedObject 应用程序。请注意，SharedObject 应用程序在整个本章中用于远程访问 SharedObject 类的对象。让我们现在创建一个主机应用程序。

## Creating a Host Application

在本节中，你将学习创建主机应用程序 DBServer 来表示主机服务器。DBServer 是一个 Windows Forms 应用程序，它注册远程对象并将其保留在内存中，同时为其客户端提供服务。DBServer 应用程序的设计和源代码可在 CD 上获得。清单 35.5 显示了 DBServer 应用程序的 Form1.cs 文件的完整代码：

### Listing 35.5: Showing the Code of the Form1.cs File of the DBServer Application

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
using System.Runtime.Serialization.Formatters;
using SharedObject;
using System.Collections;

namespace DBServer
{
public partial class Form1 : Form
{
    IChannel chan;
    IServerChannelSinkProvider SProvider;
    IClientChannelSinkProvider CProvider;
    System.Threading.Thread Thd;
    public Form1()
    {
        InitializeComponent();
```

```
}
private void Start()
{
    try
    {
        IDictionary props = null;
        props = new Hashtable();
        props["port"] = TextBox2.Text;
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
            chan = new TcpChannel(props, CProvider, SProvider);
        }
        else if (rbtnHttpChannel.Checked)
        {
            chan = new HttpChannel(props, CProvider, SProvider);
        }
        ChannelServices.RegisterChannel(chan, false);
        if (rbtnWSingleCall.Checked)
        {
            RemotingConfiguration.RegisterWellKnownServiceType(
                typeof(SharedObject.SharedObject), "HiServerApp/HiServer",
                WellKnownObjectMode.SingleCall);
        }
        else if (rbtnWSingleton.Checked)
        {
            RemotingConfiguration.RegisterWellKnownServiceType(
                typeof(SharedObject.SharedObject), "HiServerApp/HiServer",
                WellKnownObjectMode.Singleton);
        }
        else if (rbtnCActivated.Checked)
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
private void ListServices()
{
    lbServces.Items.Clear();
```


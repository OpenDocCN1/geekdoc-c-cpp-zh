
## 20.6.2.3 将父窗体传递给子窗体

设计无模式窗体的另一种方式是将整个父窗体（上例中的 Form1）传递给子窗体（MsgDlg）的构造函数。

然后，子窗体的构造函数将使用以下代码，把其“发送消息”按钮的委托设置为父窗体中的某个函数。

```csharp
public MsgDlg(Form1 fm)
{
    InitializeComponent();
    this.btnSendMsg.Click +=
        new System.EventHandler(fm.GetChildMessage);
    // set the delegate to a func. in parent form
}
```

要实现上述功能，需要将 Form1 中“GetChildMessage”函数的私有属性改为公共。

父窗体中以无模式方式调用子窗体的代码（“显示消息对话框”处理程序）现在如下所示：

```csharp
private void btnShowMsgDlg_Click(object sender, System.EventArgs e)
{
    mdlg = new MsgDlg(this); // sending parent form to child
    mdlg.Show();
}
```

## 20.6.2.4 消息框作为模态对话框和关闭事件

- 1. 除了以模态方式向用户显示消息外，MessageBox 还用于从用户那里收集少量信息。
- 2. 它能够向用户显示由 MessageBoxButtons 枚举定义的若干按钮，以及不同种类的图标。这些图标由 MessageBoxIcon 枚举定义。（警告消息框）
- 3. 当应用程序的主窗体关闭时，可以询问用户是否确实要关闭应用程序。
- 4. 解决方案是编写 Form_Closing 事件处理程序，并通过 MessageBox 询问用户。如果用户取消关闭主应用程序，则将窗体的 Cancel 属性设置为 true，以避免应用程序终止。

示例：向上面的应用程序中的 Form1 添加一个关闭事件处理程序。在其中编写以下代码。

```csharp
private void Form1_Closing(object sender,System.ComponentModel.CancelEventArgs e)
{
    DialogResult d1 = MessageBox.Show("OK to quit",
```

## 7. 创建 OpenFileDialog 对话框。

- - 在工具箱中双击 **OpenFileDialog**，这会向窗体添加一个 menuStrip1 对象。
- - 窗体上不会显示其他内容，因为对话框控件在视图中是隐藏的。
- - 可以通过“属性”窗口更改 **openFIDlg** 的 **Name** 来重命名该对话框。窗体上的控件也会随之改变。

![](img/3005a4307e6d8f3bb7e76eea28a92357_658_0.png)

![](img/3005a4307e6d8f3bb7e76eea28a92357_658_1.png)

- - 打开文件对话框实际上并不打开文件，而是通过获取文件名来帮助打开文件；其他对话框控件也是如此。打开文件需要编写单独的代码。

## 8. 模态和无模式对话框

- 1. 模态对话框是要求用户作出响应后才能继续执行程序的对话框。WordPad 的“段落”对话框就是一个很好的例子：当它显示时，用户无法使用 WordPad 的任何其他部分，除非先关闭此对象。
- 2. 无模式对话框是屏幕保持稳定并可供所有用户随时使用的对话框，但它不会阻止用户，允许其他用户的工作不受任何干扰地进行。例如，MSWord 的“查找”对话框或“查找和替换”对话框。
- 3. 模态对话框和无模式对话框的主要区别：
- i) 模态对话框会捕获消息循环，并且在当前对象关闭之前不会转移到其他对象；而无模式对话框不会捕获消息循环。
- ii) 模态对话框在所有其他窗口关闭之前不允许访问其父窗口，而无模式对话框则允许。模态对话框的例子是 MS Word 中的“保存”和“另存为”，在它们打开期间，直到窗口关闭前用户不能做任何事；而“查找和替换”可以同时执行。

## 20.8 事件处理基础

### 概念

### 1. 事件

操作和事件在每个基于 GUI 的应用程序中都起着重要作用。这些操作指示程序在发生某事时该做什么。

例如，当用户执行鼠标单击或键盘操作时，某种事件正在发生。如果用户不执行该操作，则什么也不会发生。

### 2. 委托

委托是一种 C# 语言元素，它允许引用方法。委托本质上是一个函数指针。

### 说明

### 3. C# 事件处理

- 1. 事件是一种机制，类可以通过它在发生某事时通知其客户端。
- 2. C# 事件是一个类成员，每当为其设计的事件被触发时，它就会被激活。事件触发时，将调用相应的已注册方法。

### 3. C# 事件模型

- - C# 事件模型基于“发布-订阅”模式，其中一个类（发布者）触发事件，而另一个类（订阅者）接收该事件。事件处理程序是订阅者，包含处理特定事件的代码。
- - 例如，事件处理程序可用于处理在 UI 中单击命令按钮时发生的事件。

![](img/3005a4307e6d8f3bb7e76eea28a92357_660_0.png)

### 4. 事件源

它负责通知其他对象某事已发生变化。

### 5. 事件处理程序是在事件触发时被调用的例程/方法。

- - .NET Framework 中的事件处理程序返回 void，并接受两个参数。

- - 第一个参数是事件源；即发布对象。
- - 第二个参数是派生自 EventArgs 的对象。
- - 事件是发布事件的类的属性。
- - 关键字 event 控制订阅类如何访问事件属性。

### 6. 在 C# 中处理事件包括两个步骤：

步骤 1：实现事件处理方法

事件处理方法如 btn_Click。它具有所需的签名（两个参数：类型为 object 的 sender 和类型为 EventArgs 的 e），并且按要求返回 void。

事件处理方法主体中的代码执行响应事件所需的任何编程任务。

步骤 2：将事件处理方法分配给事件

具体做法是实例化一个 EventHandler 委托，该委托封装 btn_Click 方法，然后使用 += 运算符将该委托添加到按钮的 Click 事件中。

```csharp
btn.Click += new System.EventHandler(btn_Click);
```

### 7. 声明事件：

- - 首先声明一个委托，然后按如下方式声明事件：

```
//delegate
public delegate void TimeToSleep();
//Associate event
private event TimeToSleep PowerOff;
```

- - 处理/订阅事件：

假设我的 PG 类有一个方法“plssleep”，它在断电时触发，如下所示：

```
myPG obj = new myPG();
PowerOff = new TimeToSleep(obj.plsSleep);

public class myPG
{
public void plsSleep()
{
//code
}
}
```

### 8. 事件和委托协同工作以提供程序的功能。

首先创建一个声明了*事件*的类。任何类，包括*在其中声明了该事件*的同一个类，都可以为*事件*注册其方法之一。这是通过*委托*完成的，*委托*指定了为*事件*注册的方法的签名。*委托*可以是预定义的 .NET *委托*之一，也可以是程序员声明的委托。*委托*被分配给*事件*，这实际上注册了将在*事件*触发时被调用的方法。

### 9. 在 C# 中创建事件处理程序

- 1. C# 中的事件处理程序是具有特殊签名的委托，如下所示。

```csharp
public delegate void MyEventHandler(object sender, MyEventArgs e);
```

- 1. 上述声明中的第一个参数（sender）指定触发事件的对象。上述声明中的第二个参数（e）保存可在事件处理程序中使用的数据。

- 2. MyEventArgs 类派生自 EventArgs 类。EventArgs 是更专用类的基类，如 MouseEventArgs、ListChangedEventArgs 等。

- 3. 对于 GUI 事件，可以使用这些专用 EventArgs 类的对象，而无需创建自己的专用 EventArgs 类。然而，对于非 GUI 事件，需要创建自己的专用 EventArgs 类，以保存需要传递给委托对象的数据。

- 4. 专用 EventArgs 类通过从 EventArgs 类派生来创建。

```csharp
public class MyEventArgs : EventArgs{
public string m_myEventArgumentdata;
}
```

- 5. 对于事件处理程序，使用关键字 event 引用委托对象，如下所示，

```csharp
public event MyEventHandler MyEvent;
```

### 10. 事件参数

### 概念

- - 按照惯例，.NET Framework 中 C# 的事件处理程序需要返回 void，并接受两个参数。第一个参数是事件的“源”：**发布对象**。第二个参数是**派生自 EventArgs 的对象**。

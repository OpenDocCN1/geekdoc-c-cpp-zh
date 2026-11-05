

6. 添加分隔符后，菜单如下所示。这里添加了 2 个分隔符。

![](img/3005a4307e6d8f3bb7e76eea28a92357_648_0.png)

图 20.5.9 窗体菜单视图

7. 另请注意，要添加访问键，请插入与号字符（&）。

8. 可以通过输入一个短横线并按 Enter 来插入菜单分隔符。

8. 在窗体上创建 Menu 后，双击每个菜单项，并根据应用程序要求编写作为菜单后台代码的操作部分。在本示例中，在相应菜单项的单击事件中添加了消息框。双击菜单项以为它们创建事件过程。以下是本示例添加的代码。

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
```
```csharp
namespace WindowsFormsApplicationMenus
{
    public partial class FrmMenu : Form
    {
        public FrmMenu()
        {
            InitializeComponent();
        }

        private void lineToolStripMenuItem_Click(object sender, EventArgs e)
        {
            MessageBox.Show("Insert Line Menu is selected");
        }

        private void circleToolStripMenuItem_Click(object sender, EventArgs e)
        {
            MessageBox.Show("Insert Circle Menu is selected");
        }

        private void cubeToolStripMenuItem_Click(object sender, EventArgs e)
        {
            MessageBox.Show("Insert Cube Menu is selected");
        }
    }
}
```

# 输出

![](img/3005a4307e6d8f3bb7e76eea28a92357_649_0.png)

图 20.5.10 窗体菜单视图

![](img/3005a4307e6d8f3bb7e76eea28a92357_650_0.png)

图 20.5.11 菜单单击输出

## 20.6 C# MDI 窗体

### 20.6.1 MDI 和 SDI 概念

### 概念

- 1. 多文档界面（MDI）是一种规范，它定义了应用程序的用户界面，使用户能够在一个父窗体（窗口）下同时处理多个文档。

### 说明

- 2. C# 多文档界面（MDI）程序可以在其中显示多个子窗口。这与单文档界面（SDI）应用程序形成对比，后者一次只能操作一个文档。
- 
- 3. C# 多文档界面（MDI）程序可以在其中显示多个子窗口。这与单文档界面（SDI）应用程序形成对比，后者一次只能操作一个文档。

4. Visual Studio 环境是多文档界面（MDI）的一个示例，而记事本是 SDI 应用程序的一个示例。MDI 应用程序通常有一个“窗口”菜单项，其子菜单用于在窗口或文档之间切换。

5. 通过将 IsMdiContainer 属性设置为 True，可以将任何窗口设为 MDI 父窗口。

```
IsMdiContainer = true;
```

6. 以下 C# 程序显示一个带有两个子窗体的 MDI 窗体。创建一个新的 C# 项目，以获得默认窗体 Form1。然后在项目中再添加两个窗体（Form2、Form3）。在窗体上创建一个 Menu，并在菜单单击事件中调用这两个窗体。如果希望 MDI 父窗体自动调整子窗体大小，可以按如下方式编写代码：

```
form.MdiParent = this;
form.Dock = DockStyle.Fill;
form.Show();
```

![](img/3005a4307e6d8f3bb7e76eea28a92357_651_0.png)

图 20.6.1 MDI 窗体

### 20.6.2 模式窗体和无模式窗体

### 20.6.2.1 模式窗体

### 概念

- 1. 模式窗体是指必须先处理它，然后才能继续应用程序中的后续处理的窗体。

### 说明

- 2. 示例
- 1. 在 VS.NET 中创建一个名为“ModalModeless”的 C# Windows 窗体类型应用程序。
- 2. 在主窗体（Form1）中添加一个按钮，名称为“btnShowLogin”，文本属性为“显示登录对话框”。右键单击项目，向项目中添加另一个窗体（Add->Add New Item..）。
- 3. 将此窗体命名为“LoginDlg.cs”。在此登录对话框中放置两个标签、两个文本框和两个按钮，如下所示。

![](img/3005a4307e6d8f3bb7e76eea28a92357_652_0.png)

- 4. 分别将文本框命名为“txtUsername”和“txtPassword”。将密码文本框的密码字符设置为 *。
- 5. 将第一个按钮命名为“btnLogin”，第二个按钮命名为“btnCancel”。
- 6. 由于父窗体需要知道用户在登录对话框中输入的用户名和密码，因此需要在 LoginDlg 类（LoginDlg.cs 文件）中添加两个属性，如下所示。应注意，get 方法仅用于这些属性，因为父窗体只会读取用户输入的数据。

### 7. Logging Dlg. 类文件

```
public class LoginDlg : System.Windows.Forms.Form
{
    private string username;
    public string Username
    {
        get { return username; }
    }
```

```
}
private string pword;
public string PWord
{
    get { return pword; }
}
private System.Windows.Forms.TextBox txtUsername;
...
```

### 8. LoginDlg 中“Login”和“Cancel”按钮处理程序的代码

```
private void btnLogin_Click(object sender, System.EventArgs e)
{
    this.username = txtUsername.Text;
    this.pword = txtPassword.Text;
    this.DialogResult = DialogResult.OK; // also closes the dialog
}

private void btnCancel_Click(object sender, System.EventArgs e)
{
    this.DialogResult = DialogResult.Cancel; // also closes the dialog
}
```

### 9. 对于 Form1——为“Show Login Dialog”按钮添加以下处理程序

```
private void btnShowLogin_Click(object sender, System.EventArgs e)
{
    LoginDlg ldg = new LoginDlg();
    if (ldg.ShowDialog() == DialogResult.OK)
    {
        string unm = ldg.Username;
        string pw = ldg.PWord;
        if ((unm == "India") && (pw == "1234"))
            MessageBox.Show("Correct login");
        else
            MessageBox.Show("Incorrect login");
    }
}
```

### 20.6.2.2 无模式窗体

### 概念

- 1. 无模式窗体与父应用程序共存。显示无模式窗体的调用是 Show( )。当用户通过某种操作（例如单击按钮）对无模式窗体进行更改时，父窗体中的事件处理程序会被调用。这可以通过将委托（指向父窗体中的成员函数）传递给子窗体的构造函数来轻松处理。然后，构造函数的代码可以将其设置为本地按钮。

### 说明

- 2. 示例

- 1. 在项目中添加窗体（将此窗体命名为“MsgDlg.cs”）。
- 2. 按如下所示设计此对话框中的用户界面。

![](img/3005a4307e6d8f3bb7e76eea28a92357_654_0.png)

图 20.6.3

- 3. 将文本框命名为“txtMsg”。两个按钮分别命名为“btnSendMsg”和“btnClose”。

- 4. 在 MsgDlg 中添加一个名为 msg 的属性

```
public string Msg
{
    get { return txtMsg.Text; }
}
```

- 5. 向 MsgDlg.cs 类中添加另一个构造函数。

```
public MsgDlg(System.EventHandler del)
{
    InitializeComponent();
    this.btnSendMsg.Click += del;
    // set the delegate to a func. in parent form
}
```

- 6. 在 MsgDlg 类中为“Close”按钮处理程序添加以下代码。

```
private void btnClose_Click(object sender, System.EventArgs e)
{
    this.Close();
}
```

上述函数将“send Message”按钮的单击事件处理程序设置为父窗体中的一个函数。这里发生的情况是，每当用户单击此按钮时，它就可以调用父窗体中的一个函数，该函数随后可以读取 Msg 属性，以找出子窗体正在发送什么消息。

- 7. 现在，通过在 Form1 类中添加以下代码，在父窗体中添加“Send Message”按钮处理程序。

```
private void GetChildMessage(object sender, System.EventArgs e)
{
    MessageBox.Show(mdlg.Msg);
}
```

- 8. 在 Form1 类的开头添加声明。

```
private MsgDlg mdlg; // child modeless dialog
```

- 9. 向 Form1 类中添加一个按钮。将按钮命名为“btnShowMsgDlg”。为其指定文本属性“显示消息对话框”。在“显示消息对话框”处理程序中键入以下代码。

```
private void btnShowMsgDlg_Click(object sender, System.EventArgs e)
{
    System.EventHandler pDel = new System.EventHandler
        (this.GetChildMessage);
    // delegate to GetChildMessage
    mdlg = new MsgDlg(pDel);
    mdlg.Show();
}
```

![](img/3005a4307e6d8f3bb7e76eea28a92357_655_0.png)

图 20.6.4 对话框窗口


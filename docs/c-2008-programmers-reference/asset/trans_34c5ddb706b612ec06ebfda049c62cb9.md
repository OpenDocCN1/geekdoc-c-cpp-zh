
user.config 文件的内容如下所示：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <userSettings>
    <PhotoViewer.Properties.Settings>
      <setting name="FTP_SERVER" serializeAs="String">
        <value>ftp://127.0.0.1/</value>
      </setting>
      <setting name="UserName" serializeAs="String">
        <value>anonymous1</value>
      </setting>
      <setting name="Password" serializeAs="String">
        <value></value>
      </setting>
    </PhotoViewer.Properties.Settings>
  </userSettings>
</configuration>
```

（您计算机上的）每个用户都会维护自己的 user.config 文件副本。

## 编写应用程序

现在开始编写应用程序。切换到 Form1 的后台代码，导入以下命名空间：

```csharp
using System.Net;
using System.IO;
```

定义 WebRequestMethod 枚举：

```csharp
namespace PhotoViewer
{
    enum WebRequestMethod
    {
        MakeDirectory,
        DownloadFile,
        ListDirectoryDetails,
        RemoveDirectory,
        DeleteFile
    }
}
```

声明以下常量和成员变量：

```csharp
public partial class Form1 : Form
{
    //---constants for the icon images---
    const int ico_OPEN = 0;
    const int ico_CLOSE = 1;
    const int ico_PHOTO = 2;
}
```

在 Form1 中，选中用于输入 FTP 服务器名称、用户名和密码的三个 TextBox 控件（可以按住 Ctrl 并逐个单击它们）（参见图 16-9）。在“属性”窗口中，双击 Leave 属性，为 Leave 事件生成事件处理程序存根。

## 构建目录树并显示图像

窗体加载时，首先将应用程序设置的值加载到 TextBox 控件中，然后在 TreeView 控件中显示一个表示 FTP 服务器根目录的节点：

```csharp
private void Form1_Load(object sender, EventArgs e)
{
    try
    {
        //---load the application settings values
        // into the textbox controls---
        txtFTPServer.Text = Properties.Settings.Default.FTP_SERVER;
        txtUserName.Text = Properties.Settings.Default.UserName;
        txtPassword.Text = Properties.Settings.Default.Password;

        //---create the root node for the TreeView---
        TreeNode node = new TreeNode();
        node.ImageIndex = ico_CLOSE;
        node.SelectedImageIndex = ico_OPEN;
        node.Text = @"//";

        //---add the root node to the control---
        TreeView1.Nodes.Add(node);

        //---add the dummy child node to the root node---
        node.Nodes.Add("");

        //---select the root node---
        TreeView1.SelectedNode = node;
    }
    catch (Exception ex)
    {
        MessageBox.Show(ex.ToString());
    }
}
```

创建节点后，始终会在 TreeView 控件中添加一个虚拟节点，以确保当前节点可以展开以显示子目录（即使没有子目录）。如图 16-10 所示。

![](img/a977a875c7c627b45d939729705a252e_538_0.png)

```
new StreamReader(ftpRespStream, System.Text.Encoding.UTF8);

//---obtain the result as a string array---
string[] result = reader.ReadToEnd().Split(
    Environment.NewLine.ToCharArray(),
    StringSplitOptions.RemoveEmptyEntries);
FTPResp.Close();
return result;
}
catch (Exception ex)
{
    MessageBox.Show(ex.ToString());
    return null;
}
}
```

要查看 FTP 服务器的目录列表，可使用 PerformWebRequest() 辅助函数，其定义如下：

```csharp
private FtpWebResponse PerformWebRequest(
    string path, WebRequestMethod method)
{
    //---display the hour glass cursor---
    Cursor.Current = Cursors.WaitCursor;

    FtpWebRequest ftpReq = (FtpWebRequest)WebRequest.Create(path);
    switch (method)
    {
    case WebRequestMethod.DeleteFile:
        ftpReq.Method = WebRequestMethods.Ftp.DeleteFile;
        break;
    case WebRequestMethod.DownloadFile:
        ftpReq.Method = WebRequestMethods.Ftp.DownloadFile;
        break;
    case WebRequestMethod.ListDirectoryDetails:
        ftpReq.Method = WebRequestMethods.Ftp.ListDirectoryDetails;
        break;
    case WebRequestMethod.MakeDirectory:
        ftpReq.Method = WebRequestMethods.Ftp.MakeDirectory;
        break;
    case WebRequestMethod.RemoveDirectory:
        ftpReq.Method = WebRequestMethods.Ftp.RemoveDirectory;
        break;
    }
    ftpReq.Credentials = new NetworkCredential(
        Properties.Settings.Default.UserName,
        Properties.Settings.Default.Password);

    FtpWebResponse ftpResp = (FtpWebResponse)ftpReq.GetResponse();

    //---change back the cursor---
    Cursor.Current = Cursors.Default;
    return ftpResp;
}
```

PerformWebRequest() 函数包含两个参数：

- 表示完整 FTP 路径的 path
- 表示正在执行的请求类型的 WebRequestMethod 枚举

在 PerformWebRequest() 函数中，执行以下操作：

- 使用 WebRequest 类的 Create() 方法创建 FtpWebRequest 类的实例。Create() 接受一个 URI 参数（包含完整 FTP 路径）。
- 使用 FtpWebRequest 对象的 Method 属性，设置要发送到 FTP 服务器的命令。
- 使用 NetworkCredential 类指定登录到 FTP 服务器的凭据。
- 使用 FtpWebRequest 类的 GetResponse() 方法获取 FTP 服务器的响应。

PerformWebRequest() 函数返回一个 FtpWebResponse 对象。

回到 GetDirectoryListing() 函数，在 PerformWebRequest() 调用返回后，使用 FtpWebResponse 类的 GetResponseStream() 方法获取包含 FTP 服务器发送的响应数据的流。然后使用 StreamReader 对象读取目录列表：

```csharp
//---Get the file/dir listings and return them as a string array---
private string[] GetDirectoryListing(string path)
{
    try
    {
        //---get the directory listing---
        FtpWebResponse FTPResp = PerformWebRequest(
            path, WebRequestMethod.ListDirectoryDetails);

        //---get the stream containing the directory listing---
        Stream ftpRespStream = FTPResp.GetResponseStream();
        StreamReader reader =
            new StreamReader(ftpRespStream, System.Text.Encoding.UTF8);

        //---obtain the result as a string array---
        string[] result = reader.ReadToEnd().Split(
            Environment.NewLine.ToCharArray(),
            StringSplitOptions.RemoveEmptyEntries);
        FTPResp.Close();
        return result;
    }
    catch (Exception ex)
    {
        MessageBox.Show(ex.ToString());
        return null;
    }
}
```

目录列表被拆分为字符串数组。目录列表项由换行符分隔。如果您的 FTP 服务器配置为 MS-DOS 目录列表样式（参见图 16-11），则目录列表大致如下所示：

```
12-11-06  10:54PM        2074750  DSC00098.JPG
12-11-06  10:54PM        2109227  DSC00099.JPG
12-11-06  10:49PM        <DIR>    George
12-11-06  10:49PM        <DIR>    James
12-11-06  10:58PM        <DIR>    Wei-Meng Lee
```

![](img/a977a875c7c627b45d939729705a252e_542_0.png)

**图 16-11**

因为所有子目录都有 `<DIR>` 字段，所以在 `BuildDirectory()` 函数中，可以通过在每一行中查找 `<DIR>` 来轻松区分目录和文件：

```csharp
///---Build the directory in the TreeView control---
private void BuildDirectory(TreeNode ParentNode)
{
    string[] listing = GetDirectoryListing(
        Properties.Settings.Default.FTP_SERVER +
        ParentNode.FullPath);
    foreach (string line in listing)
    {
        if (line == String.Empty) break;

        TreeNode node = new TreeNode();
        if (line.Substring(24, 5) == "<DIR>")
        {
```

（续）

```csharp
//---this is a directory; create a new node to be added---
node.Text = line.Substring(39);
node.ImageIndex = ico_CLOSE;
node.SelectedImageIndex = ico_OPEN;

//---add the dummy child node---
node.Nodes.Add("*");
ParentNode.Nodes.Add(node);
}
else
{
    //---this is a normal file; create a new node to be added---
    node.Text = line.Substring(39);
    node.ImageIndex = ico_PHOTO;
    node.SelectedImageIndex = ico_PHOTO;
    ParentNode.Nodes.Add(node);
}
}
```

选中节点时，首先获取其当前路径；如果它是文件夹，则将该路径显示在状态栏中。如果它是图像节点，则使用 DownloadImage() 函数下载并显示照片。所有这些都在 TreeView1_AfterSelect 事件中处理。代码如下：

```csharp
private void TreeView1_AfterSelect(object sender, TreeViewEventArgs e)
{
    //---always ignore the first '/' char---
    string FullPath =
        Properties.Settings.Default.FTP_SERVER +
        e.Node.FullPath.Substring(1).Replace("\\", "/");

    //---display the current folder selected---
    if (e.Node.ImageIndex != ico_PHOTO)
    {
        ToolStripStatusLabel1.Text = FullPath;
        return;
    }

    //---download image---
    DownloadImage(FullPath);
}
```


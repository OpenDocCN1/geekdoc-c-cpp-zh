
对于基本的删除操作，`System.IO`命名空间中的`.Delete`方法提供了与基本 VB 语法相当的功能。

```csharp
// 目录将被永久删除。该
// 第二个参数在目标
// 不为空时也会删除。
System.IO.Directory.Delete(targetFile, true);
```

C# 不包含你调用的功能。相反，你必须访问 Win32 API 并调用相应的函数。对于基本的删除操作，`System.IO`命名空间中的`.Delete`方法提供了与基本 VB 语法相当的功能。在区域删除和类似操作的情况下，你可以调用`SHFileOperation` API。

# DeleteFile 方法（删除文件）

- - `My.Computer.FileSystem.DeleteFile`

删除文件或将其移动到回收站。

```VISUAL BASIC
' 基础语法。文件将被永久删除。
```

```csharp
```

# Deployment 属性（部署）

- - `My.Application.Deployment`

返回当前应用程序 ClickOnce（安装）部署。

```VISUAL BASIC
Dim result As System.Deployment.Application.
Deployment
```

```csharp
System.Deployment.Application.ApplicationDeployment
result = System.Application.Current;
```

# Description 属性（描述）

- - `My.Application.Info.Description`

返回程序集中存储的应用程序描述。

```VISUAL BASIC
Dim result As String = My.Application.Info.Description
```

```csharp
string result;
System.Reflection.Assembly currentAssembly =
System.Reflection.Assembly.GetEntryAssembly();
if (currentAssembly == null) currentAssembly =
System.Reflection.Assembly.GetCallingAssembly();
object[] attrSet = currentAssembly.GetCustomAttributes(
typeof(System.Reflection.AssemblyDescriptionAttribute),
inherit:true);
if (attrSet.Length == 0)
result = "";
```

```csharp
result = ((System.Reflection.
AssemblyDescriptionAttribute)
attrSet[0]).Description;
```

# Desktop 属性（桌面）

- - `My.Computer.FileSystem.SpecialDirectories.Desktop`

返回当前用户“桌面”文件夹的路径。

```VISUAL BASIC
Dim result As String = My.Computer.FileSystem.
SpecialDirectories.Desktop
```

```csharp
string result = System.Environment.GetFolderPath(
System.Environment.SpecialFolder.DesktopDirectory);
```

# DirectoryExists 方法（目录是否存在）

- - `My.Computer.FileSystem.DirectoryExists`

表示目录路径是否存在。

```VISUAL BASIC
Dim result As Boolean = My.Computer.FileSystem.
DirectoryExists("C:\temp");
```

```csharp
bool result = System.IO.Directory.Exists("C:\\temp");
```

# DirectoryPath（目录路径）

- - `My.Application.Info.DirectoryPath`

返回包含当前应用程序的目录路径。

```VISUAL BASIC
Dim result As String = My.Application.Info.DirectoryPath
```

```csharp
System.Reflection.Assembly currentAssembly =
System.Reflection.Assembly.GetEntryAssembly();
if (currentAssembly == null) currentAssembly =
System.Reflection.Assembly.GetCallingAssembly();
string result = System.IO.Path.GetDirectoryName(
Assembly.Location);
```

# DoEvents 方法（处理事件）

- - `My.Application.DoEvents`

在 Windows Forms 应用程序中，临时暂停当前代码，以允许其他线程和进程处理消息。

```VISUAL BASIC
```

## `My.Application.DoEvents()`
```
// --- 仅 Windows Forms 代码：
System.Windows.Forms.Application.DoEvents();
```

基于 XAML 的应用程序使用“调度器（dispatcher）”或“后台工作线程”来实现相同的目的。

## DownloadFile 方法

+   ◆ `My.Computer.Network.DownloadFile`

从网络地址下载文件到本地计算机。

```
VISUAL BASIC
My.Computer.Network.DownloadFile(sourceAddress,
destinationFile, userName, password);
```

```csharp
System.Net.WebClient client = new System.Net.WebClient();
System.Uri sourceUri = new System.Uri(sourceAddress);
```

```csharp
// --默认凭据。
client.UseDefaultCredentials = true;
```

```csharp
// 或者，提供特定的凭据。
client.UseDefaultCredentials = false;
client.Credentials = new System.Net.NetworkCredential(
userName, password);
```

```csharp
// --- 同步复制。
client.DownloadFile(sourceUri, destinationFile);
```

```csharp
// --- 或者，异步复制，提供你自己的
//自定义完成/取消事件处理程序。
client.DownloadFileCompleted += new
AsyncCompletedFileEventHandler(CompletedCallback);
client.DownloadFileAsync(sourceUri, destinationFile);
```

如果目标文件存在，`WebClient`类方法将覆盖它。如果你不想覆盖该文件，则必须手动检查。此外，它没有提供关于传输状态的视觉提示。如果需要，你必须提供自己的进度对话框。

要覆盖默认超时值，请从`WebClient`类派生新类，并手动配置`HttpRequest`的`TimeOut`属性。使用此类 own标准的`WebClient`类来执行下载。

```csharp
class WebClientTimeout : System.Net.WebClient
{
    public int Timeout { get; set; }
    public WebClientTimeout(int timeoutOverride)
    {
        // ---- 保存用户指定的超时时间。
        this.Timeout = timeoutOverride;
    }
    protected override System.Net.WebRequest
    GetWebRequest(System.Uri sourceAddress)
    {
        // ---- 使用超时时间修改请求。
        System.Net.WebRequest coreRequest =
            base.GetWebRequest(sourceAddress);
        if (coreRequest != null)
            coreRequest.Timeout = this.Timeout;
        return coreRequest;
    }
}
```

## Drives 属性

+   ◆ `My.Computer.FileSystem.Drives`

返回一个描述工作站逻辑驱动器的对象的集合。

```VISUAL BASIC
' 此代码返回一个只读驱动器集合。
Dim result As System.Collections.ObjectModel.
    ReadOnlyCollection(Of System.IO.DriveInfo) =
    My.Computer.FileSystem.Drives
```

```csharp
// ---- 此代码返回一个普通的驱动器数组。
System.IO.DriveInfo[] result =
    System.IO.DriveInfo.GetDrives();
```

## DynData 属性

+   ◆ `My.Computer.Registry.DynData`

返回指向 `HKEY_DN_DATA` Windows注册表位置的引用。

```VISUAL BASIC
' 此代码已过时。
Dim result As Microsoft.Win32.RegistryKey =
    My.Computer.Registry.DynData
```

```csharp
// ---- 此代码已过时。
Microsoft.Win32.RegistryKey result =
    Microsoft.Win32.Registry.DynData;
```

此代码仅在 Windows 98 和 Windows ME 平台上有效。在基于 Windows NT 或更高版本的系统上无效。

## FileExists 方法

+   - `My.Computer.FileSystem.FileExists`

指示文件路径是否存在。

```VISUAL BASIC
Dim result As Boolean = My.Computer.FileSystem.FileExists(
"C:\temp\WorkFile.txt")
```

```csharp
bool result = System.IO.File.Exists(
"C:\temp\WorkFile.txt")
```

## FileSystemObject

+   - `My.Computer.FileSystem`

参见
`CombinePath` 方法, `CopyDirectory` 方法, `CopyFile` 方法,
`CreateDirectory` 方法, `CurrentDirectory` 属性, `DeleteDirectory`
方法, `DeleteFile` 方法, `DirectoryExists` 方法, `Drives` 属性,
`FileExists` 方法, `FindFiles` 方法, `GetDirectories` 方法,
`GetDirectoryInfo` 方法, `GetDriveInfo` 方法, `GetFileInfo` 方法,
`GetFiles` 方法, `GetName` 方法, `GetPath` 方法,
`GetTempFileName` 方法, `MoveDirectory` 方法, `MoveFile` 方法,
`OpenTextFieldParser`, `OpenTextFileReader` 方法,
`OpenTextWriter` 方法, `ReadAllBytes` 方法, `ReadAllText` 方法,
`RenameDirectory` 方法, `RenameFile` 方法, `SpecialDirectories` 对象,
`WriteAllBytes` 方法, `WriteAll` 方法

## FindFiles 方法

+   - `My.Computer.FileSystem.FindFiles`

从目标目录返回包含特定搜索字符串的文件路径集合。

```VISUAL BASIC
Dim result As System.Collections.ObjectModel.
ReadOnlyCollection(Of String) =
My.Computer.FileSystem.FindFiles(targetDirectory,
searchText, ignoreCase,
SearchOption.SearchAllSubDirectories, "*.txt")
```

C# 不包含与 VB 的 `FindFiles` 方法等效的方法。相反，你必须检查目标目录中的每个文件，以查看其是否包含搜索字符串。以下代码提供了如何搜索匹配项的一个示例。

```csharp
private static List<string> FindFiles(
    string targetDirectory, string searchText,
    bool ignoreCase, System.IO.SearchOption depthType,
    string fileMask = "*.*")
{
    List<string> results = new List<string>();
    bool foundMatch;
    string content;
    foreach (string oneFile
    in System.IO.Directory.GetFiles(
        targetDirectory, fileMask, depthType))
    {
        // 警告：大文件可能会填充内存。
        content = System.IO.File.ReadAllText(oneFile);
        if (ignoreCase)
            foundMatch = content.ToUpper().Contains(
                searchText.ToUpper());
        else
            foundMatch = content.Contains(searchText);
        if (foundMatch)
            results.Add(oneFile);
    }
    return results;
}
```

## Forms 对象

+   ◆ `My.Forms`

提供对当前 Windows Forms 项目中任何表的访问。

> VISUAL BASIC
' 完整语法
My.Forms.Form1.Show()

> '简化语法
Form1.Show()

用 C# 编写的 Windows Forms 应用程序不维护项目内当前活动或可用表的列表。每个表必须手动实例化，并且必须对所有活动表进行监控。

## GetAudioStream 方法

◆ `My.Computer.Clipboard.GetAudioStream`

返回来自系统剪贴板的数据对象。

```VISUAL BASIC
Dim result As System.IO.Stream =
    My.Computer.Clipboard.GetAudioStream()
```

```csharp
// --- Windows Forms 代码：
System.IO.Stream result = System.Windows.Forms.Clipboard.GetAudioStream();
```

## GetData 方法

◆ `My.Computer.Clipboard.GetData`

返回系统剪贴板中指定格式的对象。

```VISUAL BASIC
Dim result As Object = My.Computer.Clipboard.GetData("MyAppFormat")
```

```csharp
// --- Windows Forms 代码：
object result = System.Windows.Forms.Clipboard.GetData("MyAppFormat")
```

## GetDataObject 方法

◆ `My.Computer.Clipboard.GetDataObject`

返回支持`DataObject`接口的剪贴板对象。当剪贴板包含多种格式时，该接口可以访问这些格式。

```VISUAL BASIC
Dim result As System.Windows.Forms.IDataObject =
    My.Computer.Clipboard.GetDataObject()
```

```csharp
// --- Windows Forms 代码：
```

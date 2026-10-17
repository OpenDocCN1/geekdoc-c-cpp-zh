
## Log 对象
- `My.Application.Log`（用于桌面应用程序）
- `My.Log`（用于 ASP.NET 应用程序）

参见 `DefaultFileLogWriter Property`, `TraceSource Property`, `WriteEntry Method`, `WriteException Method`

## MinimumSplashScreenDisplayTime 属性
- ◆ `My.Application.MinimumSplashScreenDisplayTime`

指定启动界面显示的时间（毫秒为单位）。

```vb
' 显示至少两秒。
My.Application.MinimumSplashScreenDisplayTime = 2000
```

此属性是 Visual Basic Windows 应用程序框架的一部分，该类集未包含在 C# 项目中。`MinimumSplashScreenDisplayTime` 没有直接的 C# 等价项。相反，你必须手动管理应用程序中任何启动界面的显示。更多信息请参阅本章中的“SplashScreen Property”条目。

另请
- `SplashScreen Property`

## Mouse 对象
- ◆ `My.Computer.Mouse`

参见 `ButtonsSwapped Property`, `WheelExists Property`, `WheelScrollLines Property`

## MoveDirectory 方法
- ◆ `My.Computer.FileSystem.MoveDirectory`

将目录移动到新位置。

```vb
' 基础语法。第三个（可选）参数是覆盖标记。
My.Computer.FileSystem.MoveDirectory(source, destination, True)

' UI 调用语法。
My.Computer.FileSystem.MoveDirectory(source, destination, UIOption.OnlyErrorDialogs)
```

对于目录移动操作，`System.IO` 命名空间提供了与基本 VB 语法相当的功能。

```csharp
// Directory.Move 缺少覆盖选项。
System.IO.Directory.Move(source, destination);
```

C# 不包含调用 Windows 目录移动对话框的功能。相反，你必须直接访问 Win32 API 并调用相应的函数。在移动目录和类似的基于文件的操作中，你调用 `SHFileOperation` API。请参本章中的“CopyFile Method”条目获取调用此 API 的示例代码。

## MoveFile 方法
- `My.Computer.FileSystem.MoveFile`

将文件移动到新目录。

```vb
' 基础语法。第三个（可选）参数 覆盖标记。
My.Computer.FileSystem.MoveFile(source, destination, True)

' UI 调用语法。
My.Computer.FileSystem.MoveFile(source, destination, UIOption.OnlyErrorDialogs)
```

对于基本文件操作，`System.IO` 命名空间中的 `File.Move` 方法提供了与基本语法相当的功能。

```csharp
// File.Move 缺少覆盖选项。
System.IO.File.Move(source, destination);
```

C# 不包含调用 Windows 文件移动对话框的功能。相反，你必须直接访问 Win32 API 并调用相应的函数。在移动文件和类似的基于文件的操作中，你调用 `SHFileOperation` API。请参阅本章中的“CopyFile Method”条目获取示例示例代码。

## My 命名空间
- `My`

参见 `Application Object`, `Computer Object`, `Forms Object`, `Log Object (My)`, `Request Object`, `Response Object`, `Settings Object`, `User Object`, `WebServices Object`

## MyDocuments 属性
- `My.Computer.FileSystem.SpecialDirectories.MyDocuments`

返回当前用户的“文档”文件夹路径。

```vb
Dim result As String = My.Computer.FileSystem.SpecialDirectories.MyDocuments
```

```csharp
string result = System.Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);
```

## MyMusic 属性
- `My.Computer.FileSystem.SpecialDirectories.MyMusic`

返回当前用户的“音乐”文件夹路径。

```vb
Dim result As String = My.Computer.FileSystem.SpecialDirectories.MyMusic
```

```csharp
string result = System.Environment.GetFolderPath(Environment.SpecialFolder.MyMusic);
```

## MyPictures 属性
- `My.Computer.FileSystem.SpecialDirectories.MyPictures`

返回当前用户的“图片”文件夹路径。

```vb
Dim result As String = My.Computer.FileSystem.SpecialDirectories.MyPictures
```

```csharp
string result = System.Environment.GetFolderPath(Environment.SpecialFolder.MyPictures);
```

## Name 属性 (My.Computer)
- `My.Computer.Name`

返回本地计算机名称。

```vb
Dim result As String = My.Computer.Name
```

```csharp
string result = System.Environment.MachineName;
```

## Name 属性 (My.User)
- `My.User.Name`

返回当前用户名。

```vb
Dim result As String = My.User.Name
```

```csharp
string result = System.Threading.Thread.CurrentPrincipal.Identity.Name;
```

## Network 对象
- `My.Computer.Network`

参见 `DownloadFile`, `IsAvailable Property`, `NetworkAvailabilityChanged Event (My.Computer.Network)`, `Ping Method`, `UploadFile`

## NetworkAvailabilityChanged 事件 (My.Application)
- `My.Application.NetworkAvailabilityChanged`

此事件限于 Windows Forms 应用程序。通过 `My.Computer.Network` 类暴露的相同事件适用于所有应用程序类型。请参见该事件条目以获取 VB 的 C# 等效项。

另请
- `NetworkAvailabilityChanged Event (My.Computer.Network)`

## NetworkAvailabilityChanged 事件 (My.Computer.Network)
- `My.Computer.Network.NetworkAvailabilityChanged`

当网络可用性 way时调用事件处理程序。

```vb
' 事件处理逻辑。
Public Sub NetworkPresenceHandler(ByVal sender As Object, ByVal e As NetworkAvailableEventArgs)
' 在其他地方，将程序与事件关联。
AddHandler My.Computer.Network.NetworkAvailabilityChanged AddressOf NetworkPresenceHandler
```

```csharp
// 事件处理逻辑。
public static void NetworkPresenceHandler(object sender, System.Net.NetworkInformation.NetworkAvailabilityChangedEventArgs e) {}

// 将程序与事件关联。
System.Net.NetworkInformation.NetworkAvailabilityChanged += NetworkPresenceHandler;
```

## NumLock 属性
- * `My.Computer.Keyboard.NumLock`

指示 Num Lock 当前是否激活。

```vb
Dim result As Boolean = My.Computer.Keyboard.NumLock
```

```csharp
bool result = System.Windows.Forms.Form.IsLocked(System.Windows.Forms.Keys.NumLock);
```

```csharp
// 用于 Forms 代码：
bool result = System.Windows.Input.Keyboard.IsToggled(System.Windows.Input.Key.NumLock);
```

## OpenForms 属性
- `My.Application.OpenForms`

返回 Windows Forms 应用程序中当前打开的表集合。

```vb
Dim result As System.Windows.Forms.FormCollection = My.Application.OpenForms
```

```csharp
System.Windows.Forms.FormCollection result = System.Windows.Forms.Application.OpenForms;
```

## OpenSerialPort 方法
- `My.Computer.Ports.OpenSerialPort`

在本地工作站在串口上打开连接。

```vb
portAccess As System.IO.SerialPort = My.Computer.Ports.OpenSerialPort(portName, baudRate, parity, dataBits, stopBits)
```

```csharp
System.IO.Ports.SerialPort portAccess = new System.IO.Ports.OpenSerialPort(portName, baudRate, parity, dataBits, stopBits);
```

## OpenTextField 方法
- `My.Computer.FileSystem.OpenTextFieldParser`

C# 不包含 `OpenTextField` 方法的直接等价项，或其所使用的底层 TextField 类。可以在 C# 应用程序中对 Microsoft.VisualBasic 程序集的引用，并使用这些针对 VB 的功能。对于不需要访问所有 Visual Basic 组件的应用程序，需要从其他来源获取等效功能，或从开始开发。

要在 C# 中打开文件读取，使用相应的编码打开流。打开后，可以使用 `StreamReader` 类的 `ReadLine` 方法读取每行。

```csharp
string filePath = "C:\\temp\\FileFields.txt";
System.Text.Encoding useEncoding = System.Text.Encoding.UTF8;
bool autoDetectEncoding = true;
System.IO.StreamReader inStream new System.IO.StreamReader(filePath, useEncoding, autoDetectEncoding);
```

```csharp
filePath, useEncoding, autoDetectEncoding);
```

// 稍后，在循环中。
string lineContent = inputStream.ReadLine();
对于固定宽度字段，提取行文本的部分。

```csharp
// 行以 2 个字符的状态代码开头，后面是 30 个字符的城市名称。
string stateShort = lineContent.Substring(0, 2);
string cityName = lineContent.Substring(2, 30).Trim();
```

对于不使用单列列文本限定符的定符字段，使用字符串对象的 `Split` 方法来获取各个字段。

```csharp
// 一个制表符分隔的文件。
string[] allFields = lineContent.Split(new char[] {'\t'});
string stateShort = allFields[0];
cityName = allFields[1];
```

对于使用文本限定符的定符字段（并允许在引号字段内包含分隔符），您需要逐个处理行的字符，或者使用某些根据输入格式而变化的复杂正则表达式。以下代码表示了解析数据的一种方法，寻找带引号限定的、逗号分隔字符串。

```csharp
List<string> results = new List<string>();
int fieldPos = 0;
bool inQuote = false;
string tempField = " ";
for (int counter = 0; counter < lineContent.Length; counter++)
{
  if (lineContent[counter] == ',')
  {
    if (!inQuote)
    {
      tempField = lineContent.Substring(fieldPos, counter - fieldPos);
      if ((tempField.Length >= 2) && (tempField.Substring(0, 1) == "\\") && tempField.Substring(tempField.Length - 1, 1) == "\\")
      tempField = tempField.Substring(1, tempField.Length - 2);
      results.Add(tempField);
      fieldPos = counter + 1;
    }
  else if (lineContent[counter] == '"')
  {
    inQuote = !inQuote;
  }
}
```

此代码没有处理所有复杂情况。例如，如果引号字段被空白字符包围，引号将不会被移除。

## OpenTextFileReader 方法
- * `My.Computer.FileSystem.OpenTextFileReader`

打开一个现有文件进行文本输入。

```vb
Dim filePath As String = "C:\temp\WorkFile.txt"
Dim useEncoding As System.Text.Encoding = System.Text.UTF8
Dim result As System.IO.StreamReader = My.Computer.FileSystem.OpenTextFileReader(filePath, useEncoding)
```

```csharp
string filePath = @"C:\temp\WorkFile.txt";
System.Text.Encoding useEncoding = System.Text.UTF8;
bool autoDetectEncoding = true;
```

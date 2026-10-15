
```
<add name="FileLog" />

        </listeners>

      </source>

    </sources>

    <switches>

      <add name="DefaultSwitch" value="Information" />

    </switches>

    <sharedListeners>

      <add name="EventLog"

        type="System.Diagnostics.EventLogTraceListener"

        initializeData="EvjenEventWriter" />

      <add name="FileLog"

        type="Microsoft.VisualBasic.Logging.FileLogTraceListener,

Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral,
```

| `PROPERTY` | `DESCRIPTION` |
|---|---|
| `Network` | 此对象提供一个属性和一些方法，使您能够与运行应用程序的计算机所连接的网络进行交互。使用此对象，您可以使用 `IsAvailable` 属性首先验证计算机是否已连接到网络。如果是，则 `Network` 对象使您能够上传或下载文件，并 ping 网络。 |
| `Ports` | 此对象可以在端口可用时提供通知，并允许访问端口。 |
| `Registry` | 此对象提供对注册表和注册表设置的编程访问。使用 `Registry` 对象，您可以确定键是否存在，确定值，修改值并删除键。 |
| `Screen` | 这提供了处理可能连接到计算机的一个或多个屏幕的能力。 |

`My.Computer` 命名空间有很多内容，不可能涵盖全部或其中大部分内容。作为一个使用此命名空间的示例，我们将查看 `FileSystem` 属性。`FileSystem` 属性使您能够轻松且逻辑地访问计算机上的驱动器、目录和文件。

为了说明此属性的使用，首先创建一个 Windows 窗体，其中包含一个具有单列的 `DataGridView` 和一个按钮控件。它应如下图 4-17 所示。

![](img/d99870e80390742f93963da7be0b2e61_266_0.png)

## FIGURE 4-17

这个小应用程序将查看用户“我的音乐”文件夹并列出其中找到的所有 `.wma` 文件。列出后，应用程序用户将能够选择其中一个列出的文件；在按下播放按钮后，该文件将被启动并在 Microsoft 的 Windows Media Player 中播放。

在将控件放置在窗体上之后的第一步是引用 Windows Media Player DLL。您可以在 COM 选项卡上找到它，DLL 的位置为 `C:\WINDOWS\System32\wmp.dll`。这为您在解决方案的引用文件夹中提供了一个名为 `WMPLib` 的对象。

![](img/d99870e80390742f93963da7be0b2e61_268_0.png)

## FIGURE 4-18

要播放系统声音，请使用以下结构：

```
My.Computer.Audio.PlaySystemSound(SystemSounds.Beep)
```

`SystemSounds` 枚举中的系统声音包括 `Asterisk`、`Beep`、`Exclamation`、`Hand` 和 `Question`。

### My.Forms Namespace

`My.Forms` 命名空间提供了一种快速且逻辑的方式来访问解决方案中包含的窗体的属性和方法。例如，要访问解决方案中的第一个窗体（假设它名为 `Form1`），请使用以下命名空间结构：

```
My.Form.Form1
```

要获取其他窗体，只需更改命名空间，以便您要访问的窗体的名称跟在 `Form` 关键字之后。

### My.Resources

`My.Resources` 命名空间是访问应用程序中存储的资源的一种非常简单的方法。如果您从解决方案的 `My Project` 文件夹中打开 `MyResources.resx` 文件，您可以轻松创建任意数量的资源。例如，您可以创建一个名为 `MyResourceString` 的单个字符串资源，并为其赋值为 St. Louis Rams。

要访问您创建的资源，请使用此处所示的简单引用：

```
My.Resources.MyResourceString.ToString()
```

使用 IntelliSense，在您在 `MyResources` 字符串后输入句点后，您创建的所有资源都会出现。

### My.User

`My.User` 命名空间使您能够使用 `IPrincipal` 接口。您可以使用 `My.User` 命名空间来确定用户是否已通过身份验证、用户名等。例如，如果您的应用程序中有一个登录窗体，您可以使用类似以下的代码允许访问特定窗体：

```
If (Not My.User.IsInRole("Administrators")) Then

' Code here

End If
```

您也可以同样轻松地使用以下方法获取用户名：

`My.User.Name`

此外，您还可以检查用户是否已通过身份验证：

```
If My.User.IsAuthenticated Then

' Code here

End If
```

### My.WebServices

在使用 `My.WebServices` 命名空间时，您会以更冗长的方式访问 Web 服务引用。在任何一种情况下，第一步都是在解决方案中对某个远程 XML Web 服务进行 Web 引用。这些引用随后将出现在 Visual Studio 2010 的解决方案资源管理器中的 `Web References` 文件夹中。在引入 `My` 命名空间之前，您将以以下方式访问 Web 引用公开的值：

```
Dim ws As New ReutersStocks.GetStockDetails

Label1.Text = ws.GetLatestPrice.ToString()
```

这可行，但现在使用 `My` 命名空间，您可以使用以下结构：

```
Label1.Text = My.WebServices.GetStockDetails.GetLatestPrice.ToString()
```

### EXTENDING THE MY NAMESPACE

您并不局限于 `My` 命名空间提供的功能。就像其他命名空间一样，您可以随意扩展此命名空间以包含您自己的函数和属性。为了展示扩展 `My` 命名空间以包含您自己的函数和属性的示例，在您的 Windows 窗体应用程序中，创建一个名为 `CompanyExtensions.vb` 的新模块。

整个模块和相关类的代码如下所示：

```
Namespace My

    <HideModuleName()> _

    Module CompanyOperations

        Private _CompanyExtensions As New CompanyExtensions

        Friend Property CompanyExtensions() As CompanyExtensions

            Get

                Return _CompanyExtensions

            End Get

            Set(ByVal value As CompanyExtensions)

                _CompanyExtensions = value

            End Set

        End Property

    End Module

End Namespace

Public Class CompanyExtensions

    Public ReadOnly Property CompanyDateTime() As DateTime

        Get

            Return DateTime.Now()

        End Get

    End Property

End Class
```

Code snippet from `MusicPlayer\CompanyExtensions.vb`

从此示例可以看出，模块 `CompanyOperations` 被封装在 `My` 命名空间内。从那里，公开了一个单一属性——`CompanyExtensions`。该类 `CompanyExtensions` 是对同一文件中下方直接找到的类的引用。此类 `CompanyExtensions` 暴露了一个名为 `CompanyDateTime` 的单一 `ReadOnly` 属性。

在完成此设置后，构建你的应用程序，现在你就可以看到扩展后的 `My` 命名空间的实际效果了。从 Windows 窗体应用程序的 `Page_Load` 事件中，添加以下代码片段：

```
MessageBox.Show(My.CompanyExtensions.CompanyDateTime)
```

从 `My` 命名空间中，你现在可以在 IntelliSense 中直接找到 `CompanyExtensions` 类，如图 4-19 所示。

![](img/d99870e80390742f93963da7be0b2e61_270_0.png)

## FIGURE 4-19

模块 `CompanyOperations` 的名称也不会出现在 `My` 的列表中，因为 `<HideModuleName()>` 属性位于模块语句的开头。此属性表示你不希望将模块名称暴露给 `My` 命名空间。

前面的示例展示了如何在 `My` 命名空间内创建自己的部分，但你也可以扩展已存在的部分（例如 `Computer`、`User` 等）。扩展 `My` 命名空间只是在创建部分类并用你希望出现在整体 `My` 命名空间中的功能集对其进行扩展即可。以下代码示例展示了此类扩展：

```
Namespace My

    Partial Class MyComputer

        Public ReadOnly Property Hostname() As String

            Get

                Dim iphostentry As System.Net.IPHostEntry = _

                    System.Net.Dns.GetHostEntry(String.Empty)

                Return iphostentry.HostName.ToString()

            End Get

        End Property

    End Class

End Namespace
```

Code snippet from `MusicPlayer\CompanyExtensions.vb`

由此可以看出，这段代码只是扩展了已存在的 `MyComputer` 类：

```
Partial Class MyComputer

End Class
```

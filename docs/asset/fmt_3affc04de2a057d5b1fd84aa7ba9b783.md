
`account.Credentials`

Return `MyBase.OnStart()`

End Function

Private Sub `ConfigurationSettingPublisher`(ByVal configName As String,
                                           ByVal configSetter As Func(Of String, Boolean))

    ' We have to store these to be used in the RoleEnvironment Changed handler

    `_configName` = configName

    `_configSetter` = configSetter

    ' Provide the configSetter with the initial value

    configSetter(RoleEnvironment.GetConfigurationSettingValue(configName))

    AddHandler RoleEnvironment.Changed, AddressOf RoleEnvironmentChanged

End Sub

Private Sub `RoleEnvironmentChanging`(ByVal sender As Object,
                                    ByVal e As RoleEnvironmentChangingEventArgs)

    ' If a configuration setting is changing
    If (e.Changes.Any(Function(change) TypeOf _
                      change Is RoleEnvironmentConfigurationSettingChange)) Then

        ' Set e.Cancel to true to restart this role instance
        e.Cancel = True
    End If
End Sub

Private Sub `RoleEnvironmentChanged`(ByVal anotherSender As Object,
                                   ByVal arg As RoleEnvironmentChangedEventArgs)

    If (arg.Changes.OfType(Of RoleEnvironmentConfigurationSettingChange)().Any(_
        Function(change As RoleEnvironmentConfigurationSettingChange) _
            change.ConfigurationSettingName = _configName)) Then

        If (_configSetter(
            RoleEnvironment.GetConfigurationSettingValue(_configName))) Then

            RoleEnvironment.RequestRecycle()
        End If
    End If
End Sub

End Class

> *Code snippet from CloudToDo*

账户是从你之前创建的 `DataConnectionString` 设置中加载的。当前情况下，这将返回 `UseDevelopmentStorage=true`，但在部署应用程序后，它将包含你的应用程序密钥和账户名称。

`CreateTablesFromModel` 方法会根据你创建的类创建表。它要求你传递创建的数据上下文类的类型，以及目标 URL 和凭据给表存储服务。

此时，你可以为应用程序添加界面。在本例中，它是一个简单的 `DataGrid`，并附带几个字段用于添加新任务：

```
<%@ Page Language="vb" AutoEventWireup="false" CodeBehind="Default.aspx.vb" Inherits="ToDoWeb._Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Cloud To-Do</title>
<link href="Site.css" rel="stylesheet" type="text/css" />
</head>
<body>
<form id="form1" runat="server">
<div id="page">
<h1>Cloud To-Do</h1>
<div id="taskList">
<asp:GridView ID="TaskGrid" runat="server" AutoGenerateColumns="False" GridLines="None">
<Columns>
<asp:BoundField DataField="Name" HeaderText="Name" />
<asp:CheckBoxField DataField="IsComplete" HeaderText="Is Complete" />
</Columns>
</asp:GridView></div>
<div id="taskEntry">
<p>New task: <asp:TextBox runat="server" id="TaskField" /></p>
<p><asp:CheckBox runat="server" ID="CompleteField" Text="Is complete?" TextAlign="Left" /></p>
<p style="text-align:right"><asp:LinkButton runat="server" ID="SaveButton" Text="Insert" /></p>
</div>
<hr />
<div id="status">
<asp:Label runat="server" ID="Message" CssClass="message" /></div>
</div>
</form>
</body>
</html>
```

Code snippet from CloudToDo

`TaskGrid` 将显示当前任务列表，屏幕底部部分包含一个 `TextBox`、`CheckBox` 和 `LinkButton`，用于定义新任务。

最后，是时候添加将用户界面与应用程序功能连接起来的代码了。在解决方案资源管理器中右键单击 `Default.aspx` 页面，选择 View Code 以向类添加 Imports 语句和页面级变量：

```
Imports Microsoft.WindowsAzure.ServiceRuntime
Imports Microsoft.WindowsAzure.StorageClient
Imports Microsoft.WindowsAzure
Imports System.Data.Services.Client
Public Class _Default
```

```
Inherits System.Web.UI.Page
Dim account As CloudStorageAccount
Dim ctx As TaskContext
Dim statusMessage As String = String.Empty
End Class
```

Code snippet from CloudToDo

接下来，添加代码到 Page Load 事件处理程序以初始化 `TaskContext` 类：

```
Private Sub Page_Load(ByVal sender As Object,
    ByVal e As System.EventArgs) Handles Me.Load
    account = CloudStorageAccount.FromConfigurationSetting("DataConnectionString")
    ctx = New TaskContext(account.TableEndpoint.ToString,
        account.Credentials)
    BindGrid()
End Sub
```

Code snippet from CloudToDo

`CloudStorageAccount` 类有一个静态方法，用于读取你之前定义设置以读取有关访问 Web 和 worker 角色的信息。这提供了 `TaskContext` 类构造函数用于与表存储通信所需的所有基本凭据和 URL。在本例中，由于 `DataConnectionString` 设置为使用开发环境，`TaskContext` 将访问本地环境。

`BindGrid` 方法检索当前任务并将其绑定到 `DataGrid`：

```
Private Sub BindGrid()
    Try
        Me.TaskGrid.DataSource = ctx.Tasks
        Me.TaskGrid.DataBind()
    Catch ex As DataServiceRequestException
        statusMessage = ("Unable to connect to the table storage server." &
            ex.Message)
    End Try
    Me.Message.Text = statusMessage
End Sub
```

Code snippet from CloudToDo

这段代码相当简单，但将其放在单独的方法中以便在整个应用程序中重复使用。

保存新任务的代码如下：

```
Protected Sub SaveButton_Click(ByVal sender As Object,
    ByVal e As EventArgs) Handles SaveButton.Click
    Try
        ctx.AddTask(TaskField.Text, CompleteField.Checked)
        BindGrid()
    Catch ex As DataServiceRequestException
        statusMessage = ("Unable to connect to the table storage server." &
            ex.Message)
    End Try
    Me.Message.Text = statusMessage
End Sub
```

Code snippet from CloudToDo

上下文已经实例化，因此只需调用 `AddTask` 方法并传入两个值即可。这随后通过 Data Services 调用表存储以插入新条目。为了确认，`DataGrid` 会重新绑定以检索新添加的条目。

构建你的应用程序，网站和开发环境启动后稍作等待，你应该能够添加几个任务（见图 E-18）。注意：我添加了一些 CSS 来让它更漂亮一些（见示例项目中的 `site.css`）。

使用表存储与使用 Data Services 与其他数据库通信并没有太大不同。基本流程如下：

- 1. 定义你的实体类型。它必须继承自 `TableServiceEntity` 以获取所需的属性和属性（或者你可以自己实现）。
- 2. 创建一个数据上下文类以与表存储通信以保存该实体。此类继承自 `TableServiceContext`（它扩展了 Data Services 的标准 `DataServiceContext` 类）。
- 3. 在表存储中创建表（显然，这只需要做一次）。
- 4. 使用你的数据上下文类创建和编辑你的数据。

### 使用 Blob 存储

如果你正在使用普通的 ASP.NET 页面，你会将数据保存到 Web 服务器上的本地文件系统（或可能保存在你的数据库中）。由于 Windows Azure 应用程序不提供该选项，你将使用 blob 存储来保存文件。设置 blob 存储的步骤比你连接表存储所经历的步骤更简单。你不需要创建实体类。你只需要确保已创建 blob 容器，并为每个 blob 分配唯一的 ID。除了保存 blob 本身之外，你还可以将元数据附加到 blob。这可以提供一个存储其附加属性的位置。

创建一个新的 Windows Azure 应用程序，命名为 `CloudContacts`。此应用程序将使你能够输入一些联系人信息，以及联系人的照片。照片将保存到 blob 存储中，并将附加属性添加到照片的元数据中。包含一个 Web 角色，名为 `ContactWeb`。

与 `CloudToDo` 应用程序中的 Web 角色一样，你应该在 `CloudContacts` 项目中为 `ContactWeb` 角色添加 `DataConnectionString` 设置。在解决方案资源管理器中右键单击项目并选择 Properties 以打开项目的属性对话框；在 Settings 选项卡上，单击 Add 添加一个名为 `DataConnectionString` 的新设置。将此属性的类型设置为 `ConnectionString`，并将值设置为 `Use Development Storage=True`。此外，创建一个新的字符串设置，名为 `Container`，并将其值设置为你想要的容器名称（也许是像 `Contacts` 这样的名称）。

应用程序的用户界面由一组用于添加新联系人的控件和一个用于显示条目的 `ListView` 控件组成（见图 E-19）：

![](img/d99870e80390742f93963da7be0b2e61_1215_0.png)

FIGURE E-18

![](img/d99870e80390742f93963da7be0b2e61_1215_1.png)

FIGURE E-19

```
Imports Microsoft.WindowsAzure.StorageClient
Public Class _Default
    Inherits System.Web.UI.Page
    Private store As New BlobStore
    Protected Sub Page_Load(ByVal sender As Object,
        ByVal e As System.EventArgs) Handles Me.Load
        store.EnsureContainerExists()
        If Not IsPostBack Then
            BindGrid()
        End If
    End Sub
    Private Sub BindGrid()
        ContactList.DataSource = store.GetData()
        ContactList.DataBind()
    End Sub
    Protected Sub SubmitButton_Click(ByVal sender As Object,
        ByVal e As EventArgs) Handles SubmitButton.Click
        If PhotoFile.HasFile Then
            store.SaveContact(Guid.NewGuid().ToString(),
                NameField.Text,
                EmailField.Text,
                PhotoFile.PostedFile.ContentType,
                PhotoFile.FileBytes)
            BindGrid()
        Else
            Message.Text = "No image file"
        End If
    End Sub
End Class
```

处理 blob 存储的代码将位于 `BlobStore` 类中。如图所示，该类至少将有三个方法：

- `EnsureContainerExists` — 如果容器尚不存在则创建容器，或返回已创建的容器
- `GetData` — 返回当前存储在 blob 容器中的条目
- `SaveContact` — 在 blob 容器中添加新条目

以下是 `BlobStore` 类的代码：

```
Imports Microsoft.WindowsAzure
Imports Microsoft.WindowsAzure.StorageClient
Imports Microsoft.WindowsAzure.ServiceRuntime
Public Class BlobStore
    Public Function GetContainer() As CloudBlobContainer
        CloudStorageAccount.SetConfigurationSettingPublisher(
            Function(configName, configSetter) _



```
Select a).ToList()

For Each author In authors
    Console.WriteLine(author.Value)
Next

Console.WriteLine("Press ENTER to exit")
Console.ReadLine()
End Sub

End Module
```

虽然这种 URL 格式使查询数据库变得相对容易，但在编辑数据时帮助不大。你使用相同的 URL 语法，但使用其他一些 HTTP 动词来操作数据库（见下表）。

| VERB | DESCRIPTION |
|---|---|
| POST | 用于创建新条目。你需要在请求的主体中包含新条目，使用查询条目时收到的相同格式。 |
| PUT | 用于更新条目。更新后的条目包含在请求的主体中。 |
| DELETE | 用于删除记录 |

## WCF Data Services Client Library

使用 URL 查询 WCF Data Services 的灵活性很有吸引力，但你几乎不想构建一个每次查询或编辑数据库时都要创建 URL 的应用程序。幸运的是，WCF Data Services 还提供了使用 LINQ 操作数据的能力。DS 将 LINQ 请求转换为适当的 URL。

要使用客户端库，你需要为你的数据服务添加一个服务引用（见图 12-40）。

![](img/d99870e80390742f93963da7be0b2e61_513_0.png)

**FIGURE 12-40**

与其它 WCF 服务一样，添加服务引用会创建你服务的客户端代理。然后你可以直接查询对象，DS 会从你的 LINQ 查询创建适当的 URL。你首先实例化对服务的上下文，然后进行查询：

```
Dim context As New PubsEntities(URL)
Dim authors = From a In context.authors
    Where a.state = "CA"
    Order By a.city Select a
For Each author In authors
    'do something with the author type here
Next
```

Code snippet from SimpleDataService

无论请求使用的是 JSON、Atom 还是 HTTP，这都提供了一种更自然的查询服务的方式。

添加一个新的 Windows 窗体应用程序作为数据服务的客户端，并向项目添加服务引用。图 12-41 显示了一个可能的用户界面。在这种情况下，左侧的列表框将被填充作者。选择一个作者将允许你使用右侧的字段编辑属性，或者你可以清除字段以创建新作者（见图 12-42）。

![](img/d99870e80390742f93963da7be0b2e61_514_0.png)

# FIGURE 12-41

![](img/d99870e80390742f93963da7be0b2e61_514_1.png)

# FIGURE 12-42

```
Imports System.Data.Services.Client
Imports SimpleDataServiceClient.PubsService
```

```
Public Class MainForm

'update this to match your service
Dim ServiceUri As Uri = New Uri("http://localhost:49233/PubsService.svc")
Dim isNew As Boolean = True
Dim isDirty As Boolean = False

Dim context As PubsEntities

Private Sub MainForm_Load(ByVal sender As Object,
    ByVal e As System.EventArgs) Handles Me.Load
```

```
context = New PubsEntities(ServiceUri)

InitializeList()
End Sub

Private Sub RefreshButton_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles RefreshButton.Click
    'retrieves the list of authors
    'and updates the list
    InitializeList()
End Sub

Private Sub InitializeList()
    Me.AuthorsList.Items.Clear()

    Dim authors = From a In context.authors
                  Where a.state = "CA"
                  Order By a.city Select a
    For Each author In authors
        Me.AuthorsList.Items.Add(author)
    Next
End Sub

Private Sub ClearButton_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles ClearButton.Click
    isNew = True
    Au_fnameTextBox.Text = String.Empty
    Au_lnameTextBox.Text = String.Empty
    PhoneTextBox.Text = String.Empty
    AddressTextBox.Text = String.Empty
    CityTextBox.Text = String.Empty
    StateTextBox.Text = String.Empty
    ZipTextBox.Text = String.Empty
    ContractCheckBox.Checked = False
End Sub

Private Sub Field_TextChanged(ByVal sender As Object,
    ByVal e As System.EventArgs) _
    Handles ZipTextBox.TextChanged, _
    StateTextBox.TextChanged, _
    PhoneTextBox.TextChanged, _
    CityTextBox.TextChanged, _
    Au_lnameTextBox.TextChanged, _
    Au_fnameTextBox.TextChanged, _
    AddressTextBox.TextChanged
    isDirty = True
End Sub

Private Sub SaveButton_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles SaveButton.Click
    Dim selectedAuthor As author = Nothing

    If isNew Then
        'saving a new entity
        selectedAuthor = New author
    ElseIf isDirty Then
        'updating an existing entity
        selectedAuthor = Me.AuthorsList.SelectedItem
    End If
    'update fields
```

```
With selectedAuthor
    .au_id = Au_idTextBox.Text
    .au_fname = Au_fnameTextBox.Text
    .au_lname = Au_lnameTextBox.Text
    .phone = PhoneTextBox.Text
    .address = AddressTextBox.Text
    .city = CityTextBox.Text
    .state = StateTextBox.Text
    .zip = ZipTextBox.Text
    .contract = ContractCheckBox.Checked
End With
If isNew Then
    context.AddToauthors(selectedAuthor)
ElseIf isDirty Then
    context.UpdateObject(selectedAuthor)
End If

context.SaveChanges()

isNew = False
isDirty = False

End Sub

Private Sub AuthorsList_SelectedIndexChanged(ByVal sender As System.Object,
    ByVal e As System.EventArgs) _
    Handles AuthorsList.SelectedIndexChanged

    'fill fields
    Dim SelectedAuthor As author =
        DirectCast(Me.AuthorsList.SelectedItem, author)
    With SelectedAuthor
        Au_idTextBox.Text = .au_id
        Au_fnameTextBox.Text = .au_fname
        Au_lnameTextBox.Text = .au_lname
        PhoneTextBox.Text = .phone
        AddressTextBox.Text = .address
        CityTextBox.Text = .city
        StateTextBox.Text = .state
        ZipTextBox.Text = .zip
        ContractCheckBox.Checked = .contract
    End With
    isNew = False
    End Sub
End Class
```

Code snippet from SimpleDataService

前面大部分代码应该是不言自明的。然而，有两个例程可能需要解释。

InitializeList 例程是一个简单的 LINQ 查询，用于检索作者列表。然后将其添加到列表框中。列表框的 DisplayMember 设置为姓氏字段（au_lname），而 ValueMember 设置为键（au_id）。

SaveButton 代码分为三个逻辑部分。首先，你必须确定要保存的作者。由于这可能是现有作者或新作者，因此使用 isNew 和 isDirty 标志来确定这是插入还是更新。接下来，将字段设置为新值。最后，魔法发生了：如果执行插入操作，则使用代理方法 AddToauthors 将新作者添加到列表中，而 UpdateObject 用于标记更新。我们可以在这里进行许多更改，而上下文会跟踪这些更改。一旦调用 SaveChanges 方法，它们就会发送到服务器。

在调用 SaveChanges 时，使用 SaveChangesOptions 枚举提供了一些选项。默认情况下，每个请求单独发送。如果发生错误，保存将结束，但已发生的保存将保留在原位。如果使用 ContinueOnError 选项，DS 将继续保存项目。你可以使用 SaveChanges 方法的返回值来确定每次更新的结果。或者，SaveChangesOptions.Batch 将在单个 ChangeSet 中发送所有请求。虽然在技术上不是事务，但 ChangeSet 的行为类似：要么所有更新都会发生，要么一个都不会发生。同样，SaveChanges 方法的返回将标识错误发生的位置。

## SUMMARY

SQL Server Compact 被添加到 SQL 家族中，为你提供了一个新但熟悉的地方来存储数据。与其创建另一个 XML 文件来存储少量数据，你可以利用 SQL Server 强大的存储和查询功能。此外，当你将其与 Sync Framework 结合使用时，断开连接和部分连接的应用程序变得异常容易创建和部署。最近对 SQL Server 做的最有潜力的更改之一是能够将代码移入数据库。通过将通用语言运行时（CLR）与 SQL Server 集成，开发人员在创建数据访问代码时现在可以在 T-SQL 和 Visual Basic 之间进行选择。

虽然让数据库运行 Visual Basic 代码的想法可能有点令人不安，但你在灵活性和功能方面获得的好处可能正是某些应用程序所需要的。Visual Basic 提供了在处理 T-SQL 时通常不可用的一些工具，例如访问 .NET Framework 的类。虽然你应该只在适当时在存储过程和其他数据库结构中使用 Visual Basic，但在这些情况下，你可以显著提高数据库应用程序的可扩展性、性能和功能。

WCF Data Services 仍然是一个相对较新的技术，但它具有很大的前景：使开发人员能够轻松地为其应用程序提供 Web 风格的 API。通过利用现有标准，它有望成为跨平台、易于使用的通信工具，正如 Web 服务本应成为的那样。


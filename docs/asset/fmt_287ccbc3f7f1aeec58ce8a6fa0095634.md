
```csharp
C# <script runat="server">
    protected void Page_Load(object sender, EventArgs e)
    {
    if (!Page.IsPostBack)
        {
            foreach (System.IO.DriveInfo drive in
                System.IO.DriveInfo.GetDrives())
            {
                TreeNode node = new TreeNode();
                node.Selection = TreeNodeSelection.SelectExpand;
                node.PopulateDemand = true;
                node.Expanded = false;
                node.Value = drive.Name;

                if (drive.IsReady)
                {
                    node.Text =
                        String.Format("{0} - (free space: {1})",
                        drive.Name, drive.AvailableFreeSpace);
                }
                else
                {
                    node.Text =
                        String.Format("{0} - (not ready), {1}",
                        drive.Name);
                }
                this.TreeView.Nodes.Add(node);
            }
        }
    }

    private void LoadAllDirectories(TreeNode parent, string path)
    {
        System.IO.DirectoryInfo directory =
            new System.IO.DirectoryInfo(path);

        try
        {
            foreach (System.IO.DirectoryInfo d in
                directory.GetDirectories())
            {
                TreeNode node = new TreeNode(d.Name, d.FullName);
                node.Selection = TreeNodeSelection.SelectExpand;
                node.PopulateOnDemand = true;
                node.Expanded = false;

                parent.ChildNodes.Add(node);
            }
        } catch (System.UnauthorizedAccessException ex)
        {
            parent.Text += " (拒绝访问)";
        } catch (System.IO.IOException ex)
        {
            parent.Text +=
                String.Format("未知错误: {0}", ex.Message);
        }
    }
}
</script>
```

# 列表 24-3（续）

```c
protected void View_TreeNodePopulate(object sender,
TreeNodeEventArgs e)
{
    LoadDirectories(e.Node, e.Node.Value);
}
```

图 24-3 显示了页面在浏览器中应该有的样子。你现在应该能够像在 Windows 资源管理器中那样，通过打开和关闭 TreeView 节点来浏览目录树。

![](img/7040c21013b8e6c23c612d6da3599ff8_993_0.png)

图 24-3

注意，该示例在每次执行方法时都会持续创建 `DirectoryInfo` 类的新实例，用以枚举目录树。你可以通过将一些额外的属性作为节点文本来扩展此示例，例如 `CreationTime`（创建时间）或 `Attributes`（属性）。

使用 `GetDirectories()` 方法需要注意的一个重要点是可能会带来一些性能开销。这是因为每次调用 `GetDirectories()` 方法时，都会分配一个足够大的数组来容纳父目录的所有子目录，并用 `DirectoryInfo` 对象填充该数组。在所有工作完成之前，方法将不会返回。如果你在一个具有大量子目录的目录上执行此方法，或者你正在访问网络共享暴露的目录，这种分配和填充过程可能会很慢，在执行期间实际上会锁定你的应用程序。

在这些情况下，你可以选择使用 `EnumerateDirectories()` 方法。该方法返回一个 `IEnumerable<DirectoryInfo>` 而不是数组，因此没有数组分配或填充的性能开销。要使用 `EnumerateDirectories()` 方法，只需在列表 24-3 中替换该方法调用即可：

```
For Each d As System.IO.DirectoryInfo In directory.EnumerateDirectories
```

```
foreach (System.IO.DirectoryInfo d in directory.EnumerateDirectories())
```

要执行特定操作，如创建、读取目录属性或删除目录，你不需要创建 `DirectoryInfo` 类的实例。相反，你可以使用 `Directory` 类暴露的静态方法。与其创建一个表示特定路径的对象实例相比，`Directory` 类暴露的静态方法通常要求你将路径作为方法的参数传递。列表 24-4 显示了如何使用 `Directory` 类的静态方法来创建、读取属性并删除目录。

> 记住，从你的硬盘上删除文件夹时要非常小心。从你的系统中永久删除重要数据或更改资源的权限是可能的，并且这会导致你失去访问该资源的能力。

# 列表 24-4：使用 Directory 类的静态方法

```vb
<script runat="server">

    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)

        System.Directory.CreateDirectory(MapPath("Wrox"))

        If System.Directory.Exists(MapPath("Wrox")) Then

            Me.Label1.Text =
                System.Directory.GetCreationTime(
                MapPath("Wrox")).ToString()
            Me.Label2.Text =
                System.Directory.GetLastAccessTime(
                MapPath("Wrox")).ToString()
            Me.Label3.Text =
                System.Directory.GetWriteTime(
                MapPath("Wrox")).ToString()

            System.Directory.Delete(MapPath("Wrox"))
        End If
    End Sub
</script>
```

```html
<html xmlns="http://www.w3.org/1999/xhtml">
  <head id="Head1" runat="server">
  <title>使用静态方法</title>
</head>
<body>
  <form id="form" runat="server">
  <div>
    创建时间:
    <asp:Label ID="Label1" runat="server"
    Text="Label"></asp:Label><br />
    访问时间:
    <asp:Label ID="Label2" runat="server"
    Text="Label"></asp:Label><br />
    写入时间:
    <asp:Label ID="Label3" runat="server"
    Text="Label"></asp:Label>
  </div>
</form>
</body>
</html>
```

# 列表 24-4（续）

```csharp
<script runat="server">
    protected void Page_Load(object sender, EventArgs e)
    {
        if (System.Directory.Exists(MapPath("Wrox")))
        {
            Label1.Text = System.Directory.GetCreationTime(MapPath("Wrox")).ToString();
            Label2.Text = System.Directory.GetLastAccessTime(MapPath("Wrox")).ToString();
            Label3.Text = System.Directory.GetWriteTime(MapPath("Wrox")).ToString();

            System.Directory.Delete(MapPath("Wrox"));
        }
    }
</script>
```

运行此示例会在网站中创建一个“Wrox”目录。该示例访问了创建时间、访问时间和写入时间属性。最后，“Wrox”目录被删除了。

# 使用相对路径和设置当前目录

当 ASP.NET 页面执行时，线程有一个当前目录。如果你传递一个相对路径，它被假设是相对于当前目录的。你可以使用 `Directory` 类的 `CurrentDirectory` 属性更改工作目录。列表 24-5 显示了如何设置显示工作目录。

```vb
<script runat="server">
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
        Me.Label1.Text = System.Directory.GetCurrentDirectory()
        System.Directory.CurrentDirectory = MapPath("Wrox")
        Me.Label2.Text = System.Directory.GetCurrentDirectory()
    End Sub
</script>
```

```html
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <runat="server">
    <title>设置目录</title>
    </head>
    <body>
    <form id="form1" runat="server">
      <div>
        旧工作目录:
        <asp:Label ID="Label1" runat="server"></asp:Label><br />
        新工作目录:
        <asp:Label ID="Label2" runat="server"></asp:Label>
      </div>
    </form>
    </body>
</html>
```

# File 和 FileInfo

现在你可以显示和展示树视图，你可以通过添加当前选目录中的文件来进一步扩展此示例。显示文件最简单的方法是将 `FileInfo` 对象数组绑定到 `GridView`。你可以使用 `Directory` 类的 `GetFiles()` 方法来获取此类数组。

`FileInfo` 对象就像 `DirectoryInfo` 对象一样，代表系统中的单个元素（文件），并允许你对文件执行操作并访问文件属性。如果你只需要文件名，可以使用 `Directory` 类的 `GetFiles()` 方法，它返回一个简单的文件名数组。

列表 24-6 显示了如何使用 TreeView 的 `SelectedNodeChanged` 事件将你的 `GridView` 绑定到文件信息。

## 列表 24-6：将 GridView 绑定到目录文件

```vb
<script runat="server">
```

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    If (Not Page.IsPostBack) Then
        For Each drive As System.IO.DriveInfo In System.IO.DriveInfo.GetDrives()
            Dim node As TreeNode = New TreeNode()
            node.SelectionAction = TreeNodeSelectionAction.SelectExpand
            node.PopulateOnDemand = True
            node.Expanded = False
            node.Value = drive.Name

            If (drive.IsReady) Then
                node.Text = String.Format("{0} (可用空间: {1})", drive.Name, drive.AvailableFreeSpace)
            Else
                node.Text = String.Format("{0} (未就绪)", drive.Name)
            End If
            Me.TreeView1.Nodes.Add(node)
        Next
    End If
End Sub
```

```vb
Private Sub LoadDirectories(ByVal parent As TreeNode, ByVal path As String)
    Dim directory As System.IO.DirectoryInfo = New System.IO.DirectoryInfo(path)
    Try
        For Each d As System.IO.DirectoryInfo In directory.GetDirectories()
            Dim node As TreeNode = New TreeNode(d.Name, d.FullName)
            node.SelectionAction = TreeNodeSelectionAction.SelectExpand
            node.PopulateOnDemand = True
            node.Expanded = False
            parent.ChildNodes.Add(node)
        Next
    Catch ex As System.UnauthorizedAccessException
        parent.Text += " * (拒绝访问)"
    Catch ex As System.IO.IOException
        parent.Text += " * "
        String.Format("未知错误: {0}", ex.Message)
    End Try
End Sub
```

```vb
Protected Sub TreeView_NodePopulate(ByVal sender As Object, ByVal e As System.Web.UI.Controls.TreeViewEventArgs)
    LoadDirectories(e.Node, e.Value)
End Sub
```

## 操作驱动器、目录和文件 | 939


```vb
Protected Sub TreeView1_SelectedChanged(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim directory As System.IO.DirectoryInfo = New System.IO.DirectoryInfo(Me.TreeView1.SelectedNode.Value)
    Me.GridView1.DataSource = directory.GetFiles()
    Me.GridView1.DataBind()
End Sub
```

```html
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Header1" runat="server">
    <title>绑定 Gridview</title>
</head>
<body id="form" runat="server">
    <asp:ScriptManager id="ScriptManager1" runat="server"></asp:ScriptManager>
    <div>
        <asp:UpdatePanel id="UpdatePanel1" runat="server">
            <ContentTemplate>
                <table>
                    <td style="width:100px" valign="top">
                        <asp:TreeView Id="TreeView1" runat="server" OnSelectedNodeChanged="TreeView1_SelectedNodeChanged" PopulateTree()"></asp:TreeView>
                    </td>
                    <td valign="top">
                        <asp:GridView Id="GridView1" runat="server" AutoGenerateColumns="False" GridLines="None" CellPadding="3">
                            <Columns>
                                <asp:BoundField DataField="Name" HeaderText="名称" HeaderStyle-TextAlign=Left HeaderStyle-Font-Bold=true />
                                <asp:BoundField DataField="Length" HeaderText="大小" ItemStyle-TextAlign=Right HeaderStyle-TextAlign=Right HeaderStyle-Font-Bold=true />
                                <asp:BoundField DataField="LastWriteTime" HeaderText="修改日期" HeaderStyle-TextAlign=Left HeaderStyle-Font-Bold=true />
                            </Columns>
                        </asp:GridView>
                    </td>
                </table>
            </ContentTemplate>
        </asp:UpdatePanel>
    </div>
</body>
</html>
```

```vb
<script runat="server">
protected void Load(object sender, EventArgs e) {
  if (!Page.IsPostBack) {
    foreach (System.IO.DriveInfo drive in System.IO.DriveInfo.GetDrives()) {
      TreeNode node = new TreeNode();
      node.Selection = TreeNodeSelection.SelectExpand;
      node.PopulateOnDemand = true;
      node.Expanded = false;
      node.Value = drive.Name;

      if (drive.IsReady) {
        node.Text = String.Format("{0} - (可用空间: {1})", drive.Name, drive.AvailableFreeSpace);
      } else {
        node.Text = String.Format("{0} - (未就绪)", drive.Name);
      }
      this.TreeView.Nodes.Add(node);
    }
  }
}

private void LoadDirectories(TreeNode parent, string path) {
  System.IO.DirectoryInfo directory = new System.IO.DirectoryInfo(path);

  try {
    foreach (System.IO.DirectoryInfo d in directory.GetDirectories()) {
      TreeNode node = new TreeNode(d.Name, d.FullName);
      node.Selection = TreeNodeSelection.SelectExpand;
      node.Expanded = false;
      node.PopulateOnDemand = true;
      parent.Nodes.Add(node);
    }
  } catch (UnauthorizedAccessException ex) {
    parent.Text += " * (拒绝访问)";
  } catch (IOException ex) {
    parent.Text += String.Format("未知错误: {0}", ex.Message);
  }
}

protected void TreeView_Populate(object sender, EventArgs e) {
  LoadDirectories(e.Node, e.Value);
}
</script>
```

```vb
protected void TreeView1_SelectedChanged(object sender, EventArgs e) {
    try {
        System.IO.DirectoryInfo directory = new System.IO.DirectoryInfo(this.TreeView1.SelectedNode.Value);
        this.GridView1.DataSource = directory.GetFiles();
        this.GridView1.DataBind();
    } catch (UnauthorizedAccessException ex) {
        TreeView1.SelectedNode.Text += " (拒绝访问)";
    } catch (IOException ex) {
        TreeView1.SelectedNode.Text += string.Format("未知错误: {0}", ex.Message);
    }
}
</script>
```

图 24 显示了当您选择一个目录时，Web 页面的样子。网格已经绑定到 `FileInfo` 对象。

图 24-5

`GetDirectories()` 方法返回一个数组，这会导致性能问题。使用 `Enumerate()` 方法可以避免这种情况。`GetFiles()` 方法允许您限制结果为特定文件或匹配文件名。24-7 还显示了您可以向 `GetFiles()` 方法提供目录。

# 944 | 第 24 章 文件 I/O 与流

作为 `Path` 类的一个示例，图 24-6 所示的应用程序允许你输入路径，然后显示路径的各个组成部分，例如根路径（逻辑驱动器）、目录、文件名和扩展名。

> `GetInvalidPathChars` 和 `GetInvalidFileNameChars` 方法分别返回路径和文件名中不允许的字符数组。虽然特定的无效字符取决于其运行的平台，但这些方法返回的数组最可能包含不可打印字符、特殊 Unicode 字符或来自非拉丁字符集的字符等元素。浏览器能够渲染的字符取决于你特定的平台设置。

![](img/7040c21013b8e6c23c612d6da3599ff8_1003_0.png)

图 24-6

## 代码列表 24-8：使用 Path 类

```vb
<script runat="server">
Protected Sub Page_Load(sender As Object, e As System.EventArgs)
    If Page.IsPostBack Then
        Me.lbl1RootPath.Text =
            System.IO.Path.GetPathRoot(Me.txtPathName.Text)
        Me.lbl1DirectoryName.Text =
            System.IO.Path.GetDirectoryName(Me.txtPathName.Text)
        Me.lbl1FileName.Text =
            System.IO.Path.GetFileName(Me.txtPathName.Text)
    End If
End Sub</script>
```

# 驱动器、目录和文件 | 945

```vb
Me.lblFileNameWithoutExtension.Text = 
System.IO.Path.GetFileNameWithoutExtension(
Me.txtPathName.Text)
Me.lblExtension.Text =
System.IO.Path.GetExtension(Me.txtPathName.Text)
Me.lblTemporaryPath.Text = System.IO.Path.GetTempPath() & _
System.IO.Path.DirectorySeparatorChar.ToString()
Me.lblDirectorySeparatorChar.Text = System.IO.Path.DirectorySeparatorChar.ToString()
Me.lblAltDirectorySeparatorChar.Text = System.IO.Path.AltDirectorySeparatorChar.ToString()
Me.lblVolumeSeparatorChar.Text = System.IO.Path.VolumeSeparatorChar.ToString()
Me.lblPathSeparator.Text =
System.IO.Path.PathSeparator.ToString()
Me.lblInvalidChars.Text =
HttpUtility.HtmlEncode(
New String(System.IO.Path.GetInvalidPathChars()))
Me.lblInvalidFileName.Text =
HttpUtility.HtmlEncode(
New String(System.IO.Path.GetInvalidFileNameChars()))

End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>使用 Path 类</title>
</head>
<body>
<form id="form1" runat="server">
<div>
使用 Path 类 <br />
<br />
输入路径：
<asp:TextBox Id="txtPathName" runat="server" /> <br />
<asp:Button Id="Button1" runat="server" Text="Button" /> <br />
<br />
根路径 <br /> =
<asp:Label Id="lblRootPath" runat="server" Text="Label" />
<br />
目录 <br /> =
<asp:Label Id="lblDirectoryName" runat="server" Text="Label" />
<br />
文件名 <br /> =
<asp:Label Id="lblFileName" runat="server" Text="Label" />
<br />
文件名（不带扩展名） <br /> =
<asp:Label Id="lblFileNameWithoutExtension" runat="server" Text="Label" />
<br />
扩展名：<br /> =
<asp:Label Id="lblExtension" runat="server" Text="Label" />
<br />
<br />
临时目录 <br /> =
<asp:Label Id="lblTemporaryPath" runat="server" Text="Label" />
<br />
目录分隔符字符 <br /> =
<asp:Label Id="lblDirectorySeparatorChar" runat="server" Text="Label" />
```

## 代码列表 24-8（续）

```vb
<br />
备用分隔符字符 =
<asp:Label ID="lblAltDirectorySeparatorChar"
runat="server" Text="Label" />
<br />
卷器分隔符字符 =
<asp:Label ID="lblVolumeSeparatorChar"
runat="server" Text="Label" />
<br />
路径分隔符字符 =
<asp:Label ID="lblPathSeparator" runat="server" Text="Label" />
<br />
无效路径字符 =
<asp:Label ID="lblInvalidPathChars" runat="server" Text="Label" />
<br />
无效文件名字符 =
<asp:Label ID="lblInvalidFileNameChars"
runat="server" Text="Label" />

</div>
</form>
</body>
</html>
```

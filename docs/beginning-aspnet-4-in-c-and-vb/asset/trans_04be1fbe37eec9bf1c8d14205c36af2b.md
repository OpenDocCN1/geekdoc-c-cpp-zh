

![](img/d7d2ffa0a76feaab821930e95daace93_837_0.png)

## 图 29-2

![](img/d7d2ffa0a76feaab821930e95daace93_837_1.png)

## 图 29-3

请注意，如果愿意，你还可以使用 DirectoryInfo 属性显示文件夹的创建时间、最后访问时间和最后修改时间。为了简单起见，这里只显示所选文件的这些属性。

```csharp
{
    throw new FileNotFoundException(\"File not found: \" + fileFullName);
}
textBoxFileName.Text = theFile.Name;
textBoxCreationTime.Text = theFile.CreationTime.ToLongTimeString();
textBoxLastAccessTime.Text = theFile.LastAccessTime.ToLongDateString();
textBoxLastWriteTime.Text = theFile.LastWriteTime.ToLongDateString();
textBoxFileSize.Text = theFile.Length.ToString() + \" bytes\";
}
```

代码下载 FileProperties.sln

请注意，如果在指定位置定位文件时出现任何问题，你要采取抛出异常的预防措施。该异常本身将在调用例程（其中一个事件处理程序）中处理。最后，你定义一个方法 `DisplayFolderList()`，它会在两个列表框中显示给定文件夹的内容。该文件夹的完整路径名作为参数传递给此方法：

```csharp
protected void DisplayFolderList(string folderFullName)
{
    DirectoryInfo theFolder = new DirectoryInfo(folderFullName);

    if (!theFolder.Exists)
    {
        throw new DirectoryNotFoundException(\"Folder not found: \" + folderFullName);
    }

    ClearAllFields();
    textBoxFolder.Text = theFolder.FullName;
    currentFolderPath = theFolder.FullName;

    // list all subfolders in folder
    foreach(DirectoryInfo nextFolder in theFolder.GetDirectories())
        listBoxFolders.Items.Add(nextFolder.Name);

    // list all files in folder
    foreach(FileInfo nextFile in theFolder.GetFiles())
        listBoxFiles.Items.Add(nextFile.Name);
}
```

代码下载 FileProperties.sln

接下来，我们来检查事件处理程序。当用户单击 Display 按钮时触发的事件对应的事件处理程序是最复杂的，因为它需要处理用户在文本框中输入的文本的三种不同可能性。例如，它可能是文件夹的路径名、文件的路径名，或者两者都不是：

```csharp
protected void OnDisplayButtonClick(object sender, EventArgs e)
{
    try
    {
        string folderPath = textBoxInput.Text;
        DirectoryInfo theFolder = new DirectoryInfo(folderPath);

        if (theFolder.Exists)
        {
            DisplayFolderList(theFolder.FullName);
            return;
        }

        FileInfo theFile = new FileInfo(folderPath);
if (theFile.Exists)
{
    DisplayFolderList(theFile.Directory.FullName);
    int index = listBoxFiles.Items.IndexOf(theFile.Name);
    listBoxFiles.SetSelected(index, true);
    return;
}

throw new FileNotFoundException("There is no file or folder with "
    + "this name: " + textBoxInput.Text);
}
catch(Exception ex)
{
    MessageBox.Show(ex.Message);
}
}
```

在这段代码中，通过实例化 `DirectoryInfo` 和 `FileInfo` 对象，并检查每个对象的 `Exists` 属性，来确定提供的文本表示的是文件夹还是文件。如果两者都不存在，则抛出异常。如果是文件夹，则调用 `DisplayFolderList()` 来填充列表框。如果是文件，则需要填充列表框，并整理显示文件属性的文本框。你处理这种情况时，首先填充列表框，然后在“文件”列表框中以编程方式选择相应的文件名。这与用户选择该项具有完全相同的效果——它会引发选中项事件。然后，你可以直接退出当前事件处理程序，因为知道选中项事件处理程序将立即被调用来显示文件属性。

下面的代码是当“文件”列表框中的某个项被选中时调用的事件处理程序，无论是用户选中，还是如前所述，以编程方式选中。它只是构造所选文件的完整路径名，并将其传递给前面介绍的 `DisplayFileInfo()` 方法：

```csharp
protected void OnListBoxFilesSelected(object sender, EventArgs e)
{
    try
    {
        string selectedString = listBoxFiles.SelectedItem.ToString();
        string fullFileName = Path.Combine(currentFolderPath, selectedString);
        DisplayFileInfo(fullFileName);
    }
    catch(Exception ex)
    {
        MessageBox.Show(ex.Message);
    }
}
```

“文件夹”列表框中选中某个文件夹的事件处理程序的实现方式非常类似，只是在这种情况下，你需要调用 `DisplayFolderList()` 来更新列表框的内容：

```csharp
protected void OnListBoxFoldersSelected(object sender, EventArgs e)
{
    try
    {
        string selectedString = listBoxFolders.SelectedItem.ToString();
        string fullPathName = Path.Combine(currentFolderPath, selectedString);
        DisplayFolderList(fullPathName);
    }
    catch(Exception ex)
{
    MessageBox.Show(ex.Message);
}
}
```

最后，当单击 Up 按钮时，也必须调用 `DisplayFolderList()`，只不过这次你需要获取当前显示的文件夹的父文件夹的路径。这是通过 `FileInfo.DirectoryName` 属性完成的，该属性返回父文件夹路径：

```csharp
protected void OnUpButtonClick(object sender, EventArgs e)
{
    try
    {
        string folderPath = new FileInfo(currentFolderPath).DirectoryName;
        DisplayFolderList(folderPath);
    }
    catch(Exception ex)
    {
        MessageBox.Show(ex.Message);
    }
}
```

*代码下载 FileProperties.sln*

## 移动、复制和删除文件

如前所述，移动和删除文件或文件夹是通过 `FileInfo` 和 `DirectoryInfo` 类的 `MoveTo()` 和 `Delete()` 方法完成的。`File` 和 `Directory` 类上对应的方法是 `Move()` 和 `Delete()`。`FileInfo` 和 `File` 类还分别实现了 `CopyTo()` 和 `Copy()` 方法。但是，没有用于复制整个文件夹的方法——你需要通过复制文件夹中的每个文件来完成。

所有这些方法的使用都非常直观——你可以在 SDK 文档中找到详细说明。本节将说明在特定情况下如何调用 `File` 类上的静态 `Move()`、`Copy()` 和 `Delete()` 方法。为此，你将在前面的 FileProperties 示例的基础上进行构建，并创建其迭代版本 FilePropertiesAndMovement。这个示例将有一个额外功能：每当显示文件属性时，应用程序都会让你选择删除该文件，或者将该文件移动或复制到另一个位置。

![](img/d7d2ffa0a76feaab821930e95daace93_841_0.png)

### FilePropertiesAndMovement 示例

图 29-4 显示了新示例应用程序的用户界面。

如你所见，FilePropertiesAndMovement 在外观上与 FileProperties 类似，不同之处在于窗口底部有一组三个按钮和一个文本框。

图 29-4

这些控件只有在示例实际显示文件属性时才启用；在其他所有时候，它们都被禁用。现有控件也被压缩了一些，以免主窗体变得太大。当显示所选文件的属性时，FilePropertiesAndMovement 会自动将该文件的完整路径名放在底部文本框中供用户编辑。然后，用户可以单击任意按钮来执行相应的操作。执行时，会显示一个消息框，确认用户所执行的操作（参见图 29-5）。

当用户单击“是”按钮时，该操作将被启动。用户可以采取的一些操作会导致显示不正确。例如，如果用户移动或删除了文件，显然无法在同一位置继续显示该文件的内容。此外，如果在同一文件夹中更改了文件名，显示也会过期。在这些情况下，FilePropertiesAndMovement 会重置其控件，使其在文件操作后仅显示该文件所在的文件夹。

### 查看 FilePropertiesAndMovement 的代码

要为这个过程编写代码，你需要将相关控件及其事件处理程序添加到 FileProperties 示例的代码中。新控件的名称分别为 buttonDelete、buttonCopyTo、buttonMoveTo 和 textBoxNewPath。

首先，看一下当用户单击 Delete 按钮时调用的事件处理程序：

```csharp
protected void OnDeleteButtonClick(object sender, EventArgs e)
{
    try
    {
        string filePath = Path.Combine(currentFolderPath,
            textBoxFileName.Text);
        string query = "Really delete the file\n" + filePath + "?\n";
        if (MessageBox.Show(query,
            "Delete File?", MessageBoxButtons.YesNo) == DialogResult.Yes)
        {
            File.Delete(filePath);
            DisplayFolderList(currentFolderPath);
        }
    }
    catch(Exception ex)
    {
        MessageBox.Show("Unable to delete file. The following exception"
            + " occurred:\n" + ex.Message, "Failed");
    }
}
```

代码下载 FilePropertiesAndMovement.sln

该方法的代码包含在一个 try 块中，因为存在明显的抛出异常风险，例如你没有删除该文件的权限，或者该文件在显示之后、用户按下 Delete 按钮之前被另一个进程移动。你将从 CurrentParentPath 字段（包含父文件夹的路径）和 textBoxFileName 文本框中的文本（包含文件名）构造要删除的文件的路径。

移动和复制文件的方法在结构上非常相似：

```csharp
protected void OnMoveButtonClick(object sender, EventArgs e)
{
    try
    {
        string filePath = Path.Combine(currentFolderPath,
            textBoxFileName.Text);
        ...
    }
}
```

![](img/d7d2ffa0a76feaab821930e95daace93_842_0.png)


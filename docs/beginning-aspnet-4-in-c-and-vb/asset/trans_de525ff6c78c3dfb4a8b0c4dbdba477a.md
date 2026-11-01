
```
string query = "Really move the file\n" + filePath + "\ninto "
    + textBoxNewPath.Text + "?";
if (MessageBox.Show(query,
    "Move File?", MessageBoxButtons.YesNo) == DialogResult.Yes)
{
    File.Move(filePath, textBoxNewPath.Text);
    DisplayFolderList(currentFolderPath);
}
catch(Exception ex)
{
    MessageBox.Show("Unable to move file. The following exception"
        + " occurred:\n" + ex.Message, "Failed");
}

protected void OnCopyButtonClick(object sender, EventArgs e)
{
    try
    {
        string filePath = Path.Combine(currentFolderPath,
            textBoxFileName.Text);
        string query = "Really copy the file\n" + filePath + "\ninto "
            + textBoxNewPath.Text + "?";
        if (MessageBox.Show(query,
            "Copy File?", MessageBoxButtons.YesNo) == DialogResult.Yes)
        {
            File.Copy(filePath, textBoxNewPath.Text);
            DisplayFolderList(currentFolderPath);
        }
    }
    catch(Exception ex)
    {
        MessageBox.Show("Unable to copy file. The following exception"
            + " occurred:\n" + ex.Message, "Failed");
    }
}
```

代码下载 FilePropertiesAndMovement.sln

你还没有完全完成。你还需要确保新的按钮和文本框在适当的时候被启用和禁用。为了在显示文件内容时启用它们，你需要将以下代码添加到 `DisplayFileInfo()` 中：

```
protected void DisplayFileInfo(string fileFullName)
{
    FileInfo theFile = new FileInfo(fileFullName);

    if (!theFile.Exists)
    {
        throw new FileNotFoundException("File not found: " + fileFullName);
    }

    textBoxFileName.Text = theFile.Name;
    textBoxCreationTime.Text = theFile.CreationTime.ToLongTimeString();
    textBoxLastAccessTime.Text = theFile.LastAccessTime.ToLongDateString();
    textBoxLastWriteTime.Text = theFile.LastWriteTime.ToLongDateString();
    textBoxFileSize.Text = theFile.Length.ToString() + " bytes";

    // enable move, copy, delete buttons
    textBoxNewPath.Text = theFile.FullName;
    textBoxNewPath.Enabled = true;
    buttonCopyTo.Enabled = true;
    buttonDelete.Enabled = true;
    buttonMoveTo.Enabled = true;
}
```

代码下载 FilePropertiesAndMovement.sln

你还需要对 `DisplayFolderList` 做一处修改：

```
protected void DisplayFolderList(string folderFullName)
{
    DirectoryInfo theFolder = new DirectoryInfo(folderFullName);
    if (!theFolder.Exists)
    {
        throw new DirectoryNotFoundException("Folder not found: " + folderFullName);
    }
    ClearAllFields();
    DisableMoveFeatures();
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

代码下载 FilePropertiesAndMovement.sln

`DisableMoveFeatures` 是一个禁用新控件的小型实用函数：

```
void DisableMoveFeatures()
{
    textBoxNewPath.Text = "";
    textBoxNewPath.Enabled = false;
    buttonCopyTo.Enabled = false;
    buttonDelete.Enabled = false;
    buttonMoveTo.Enabled = false;
}
```

代码下载 FilePropertiesAndMovement.sln

你还需要向 `ClearAllFields()` 中添加额外代码，以清除额外的文本框：

```
protected void ClearAllFields()
{
    listBoxFolders.Items.Clear();
    listBoxFiles.Items.Clear();
    textBoxFolder.Text = "";
    textBoxFileName.Text = "";
    textBoxCreationTime.Text = "";
    textBoxLastAccessTime.Text = "";
    textBoxLastWriteTime.Text = "";
    textBoxFileSize.Text = "";
    textBoxNewPath.Text = "";
}
```

代码下载 FilePropertiesAndMovement.sln

下一节将介绍文件的读取和写入。

```
InitializeComponent();

private void button1_Click(object sender, EventArgs e)
{
    textBox2.Text = File.ReadAllText(textBox1.Text);
}
```

代码下载 ReadingFiles.sln

在构建此示例时，第一步是添加 `using` 语句以引入 `System.IO` 命名空间。然后，只需使用窗体上“发送”按钮的 `button1_Click` 事件，用文件返回的内容填充文本框。现在，你可以通过 `File.ReadAllText()` 方法访问文件内容。如你所见，一条语句即可读取文件。`ReadAllText()` 方法会打开指定文件，读取内容，然后关闭文件。`ReadAllText()` 方法的返回值是一个字符串，包含所指定文件的全部内容。结果将与图 29-7 中显示的内容类似。

![](img/d7d2ffa0a76feaab821930e95daace93_846_0.png)

## 图 29-7

前面示例中显示的 `File.ReadAllText()` 签名具有以下构造：

```
File.ReadAllText(FilePath);
```

另一个选项是指定所读取文件的编码：

```
File.ReadAllText(FilePath, Encoding);
```

使用此签名，你可以指定打开和读取文件内容时要使用的编码。因此，这意味着你可以执行类似以下操作：

```
File.ReadAllText(textBox1.Text, Encoding.ASCII);
```

其他打开和处理文件的选项包括使用 `ReadAllBytes()` 和 `ReadAllLines()` 方法。`ReadAllBytes()` 方法允许你打开二进制文件并将内容读取到字节数组中。前面展示的 `ReadAllText()` 方法将指定文件的全部内容以单个字符串实例返回。你可能对此不感兴趣，而是希望逐行处理文件返回的内容。在这种情况下，应使用 `ReadAllLines()` 方法，因为它支持这种功能，并会返回一个字符串数组供你处理。

## 写入文件

除了让文件读取在 .NET Framework 下变得极为简单之外，基类库也让文件写入变得同样简单。正如基类库（BCL）提供 `ReadAllText()`、`ReadAllLines()` 和 `ReadAllBytes()` 方法以不同方式读取文件一样，它也提供了 `WriteAllText()`、`WriteAllBytes()` 和 `WriteAllLines()` 方法来写入文件。

为了演示如何写入文件，请使用同一个 Windows Forms 应用程序，但使用窗体中的多行文本框将数据输入到文件中。`button1_Click` 事件处理程序的代码应如下所示：

```
private void button1_Click(object sender, EventArgs e)
{
    File.WriteAllText(textBox1.Text, textBox2.Text);
}
```

生成并启动窗体后，在第一个文本框中键入 `C:\Testing.txt`，在第二个文本框中键入一些随机内容，然后点击按钮。虽然在视觉上不会发生任何事情，但如果你查看 C: 盘根目录，就会看到 `Testing.txt` 文件以及你指定的内容。

`WriteAllText()` 方法会转到指定位置，创建新的文本文件，并在保存和关闭文件之前将指定内容写入文件。仅用一行代码就能实现，相当不错！

如果再次运行该应用程序，并指定相同的文件（`Testing.txt`）但包含一些新内容，再次点击按钮将导致应用程序执行相同的任务。不过，这次新内容不会添加到之前指定的内容上，而是会完全覆盖之前的内容。实际上，`WriteAllText()`、`WriteAllBytes()` 和 `WriteAllLines()` 都会覆盖任何先前存在的文件，因此使用这些方法时必须小心。

前面示例中的 `WriteAllText()` 方法使用以下签名：

```
File.WriteAllText(FilePath, Contents)
```

你还可以指定新文件的编码：

```
File.WriteAllText(FilePath, Contents, Encoding)
```

`WriteAllBytes()` 方法允许你使用字节数组将内容写入文件，而 `WriteAllLines()` 方法允许你将字符串数组写入文件。以下事件处理程序演示了这一点：

```
private void button1_Click(object sender, EventArgs e)
{
    string[] movies =
    {
        "Grease",
        "Close Encounters of the Third Kind",
        "The Day After Tomorrow"
    };
    File.WriteAllLines(@"C:\Testing.txt", movies);
}
```

现在，点击此类应用程序的按钮，你将得到一个 `Testing.txt` 文件，其内容如下：


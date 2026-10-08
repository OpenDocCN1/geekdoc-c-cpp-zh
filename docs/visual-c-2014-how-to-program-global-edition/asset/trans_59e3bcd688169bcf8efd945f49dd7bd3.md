

## 15.9 TreeView 控件

```cs
// 检查是否存在子目录
if (directoryArray.Length != 0)
{
    // 对于每个子目录，创建一个新的 TreeNode，
    // 将其作为当前节点的子节点，并递归地
    // 使用子目录填充子节点
    foreach (string directory in directoryArray)
    {
        // 通过调用 Path 类的 GetFileNameWithoutExtension 方法
        // 从完整路径中获取最后部分
        string subDirectory = Path.GetFileNameWithoutExtension(directory);

        // 为当前目录创建 TreeNode
        TreeNode node = new TreeNode(subDirectory);

        // 将当前目录节点添加到父节点
        parentNode.Nodes.Add(node);

        // 递归填充每个子目录
        PopulateTreeView(directory, node);
    }
}
catch (UnauthorizedAccessException)
{
    parentNode.Nodes.Add("Access denied");
}

// 处理 enterButtonClick 事件
private void enterButtonClick_Click(object sender, EventArgs e)
{
    // 清除所有节点
    directoryTreeView.Nodes.Clear();

    // 检查用户输入的目录是否存在
    // 如果存在，则填充 TreeView；
    // 如果不存在，显示错误 MessageBox
    if (Directory.Exists(inputTextBox.Text))
    {
        // 将完整路径名添加到TreeView
        directoryTreeView.Nodes.Add(inputTextBox.Text);
    }
    else
    {
        // 插入子文件夹
        PopulateTreeView(inputTextBox.Text, directoryTreeView.Nodes[0]);
    }
    // 如果未找到目录，则显示错误 MessageBox
}
```

图 15.28 | 使用 TreeView 显示目录结构。（3 部分中的第 2 部分。）

| 行 | 代码 |
|---|---|
| 83 | MessageBox.Show(inputTextBox.Text + " could not be found.", |
| 84 | "Directory Not Found", MessageBoxButtons.OK, |
| 85 | |
| 86 | } |
| 87 | MessageBoxIcon.Error); |
| 88 | } |
| 89 | |

- *a) 用户输入目录路径后的 GUI*

![](img/57baed2319be0bb1b5f98674846f2711_672_0.png)

图 15.28 | 使用 TreeNode 显示目录结构。（3 部分中的第 3 部分）

当用户点击 Enter 按钮时，`directoryTreeView` 中的所有节点都会清除（第 66 行）。如果目录存在（第 71 行），则使用 TextBox 中输入的路径来创建根节点。第 74 行将目录作为根节点添加到 TreeView 中，第 77–78 行调用 `PopulateTreeView`（第 21–60 行），该方法接收一个目录（字符串）和一个父节点。然后 `PopulateTreeView` 创建与接收到的参数的子目录对应的子节点。

`PopulateTreeView` 方法（第 21–60 行）使用第 25–26 行中 `Directory` 类（namespace.IO）的 `GetDirectories` 获取子目录列表。`GetDirectories` 方法接收一个字符串（当前目录）并返回字符串数组（子目录）。由于安全原因无法访问目录，将抛出 `UnauthorizedAccessException`。第 56–59 行可以捕获此异常，并添加节点“Access denied”而不是显示子目录。

如果有子目录，第 42–43 行使用 `Path` 类的 `GetFileNameWithoutExtension` 通过将完整路径名缩短为目录名来提高可读性。接下来，`directoryArray` 中的每个字符串都被用于创建一个新的子节点（第 46 行）。我们使用 `Add`（第 49 行）将每个子节点添加到父节点。然后对每个子目录递归调用 `PopulateTreeView` 方法（第 52 行），最终为 Tree 填充整个目录结构。我们的递归算法在程序加载大型目录时可能会导致延迟。然而，一旦文件夹名称被添加到相应的 `Nodes` 集合，就可以无延迟地展开和折叠它们。在下一节中，我们将介绍一种解决此问题的替代算法。

## 15.10 ListView 控件

`ListView` 与 `ListBox` 类似，两者都可以显示列表，且用户可以选择一个或多个项目（可以在 15.31 中找到 ListView 的示例）。`ListView` 更通用，可以以不同的格式显示项目。`ListView` 可以在列表项旁边显示项目（由其 `SmallImageList`、`LargeImage-ImageList` 控制），并在列中显示项目的详细信息。属性 `MultiSelect`（一个 bool）决定是否允许选择多个项目。通过将属性 `CheckBoxes`（一个 bool）设置为 `true`，可以包含复选框，使 `ListView` 的外观类似于 `CheckListBox`。属性 `Activation` 决定用户选择列表的方法。这些属性以及 `Click` 和 `ItemActivate` 事件的细节将在 15.29 中进行解释。

| ListView 属性和事件 | 描述 |
|---|---|
| 通用属性 Activation | 决定用户如何激活项目。此属性接受 `ItemActivation` 枚举中的值。可能的值有 `OneClick`（单击激活）、`TwoClick`（双击激活，鼠标悬过项目时项目颜色会变化）和 `Standard`（默认值；双击激活，项目颜色不变化）。 |
| CheckBoxes | 表明项目是否带有复选框出现。`true` 显示复选框。默认值为 `false`。 |
| LargeImageList Items | 指定包含显示大图标的 `ImageList`。返回控件中 `ListViewItems` 集合。 |
| MultiSelect | 决定是否允许多选。如果是 `true`，则启用多选。 |
| SelectedItems | 返回被选中项目的 `ListView.SelectedItemsCollection`。 |
| SmallImageList View | 指定包含显示小图标的 `ImageList`。决定 `ListViewItems` 的外观。可能的值有 `LargeIcon`（默认；显示大图标，可以是多列）、`SmallIcon`（显示小图标，可以是多列）、`List`（小图标显示在单列）、`Details`（每个项目可以显示多列信息）和 `Tile`（显示大图标，右提供提供）。 |
| 通用事件 Click Activate | 项目被点击时触发。这是默认事件。当 ListView 中的项目被激活（点击或双击）时触发。它不包含激活项目的具体信息——可以使用 `SelectedItems` 或 `SelectedIndices` 来确定这一点。 |

图 15.29 | ListView 属性和事件。



*(注：上述代码部分的 `switch` 逻辑由于用户提供的原始文本在 `switch` 处截断，翻译部分已严格遵循提供的原文范围进行)*

## 15.9 TreeView 控件

应用程序根据所选项的索引绘制形状（第 35–61 行）。图形方法 `DrawEllipse`（第 38 行）接受一个 `Pen`，以及左上角的 x 和 y 坐标，以及显示椭圆的边界框（即矩形区域）的宽度和高度。坐标系的原点是表单（`Form`）的左上角；x 坐标向右增加，y 坐标向下增加。圆是椭圆的一种特殊情况（宽度和高度相等）。第 38 行绘制了一个圆。第 44 行绘制了一个宽度和高度不同的椭圆。

`Graphics` 类 `DrawRectangle`（第 41 行）接受一个 `Pen`、左上角的 x 和 y 坐标以及要绘制的矩形的宽度和高度。`DrawPie`（第 47 行）绘制椭圆的扇形。椭圆由矩形限定。`DrawPie` 接受一个 `Pen`、矩形左上角的 x 和 y 坐标、其宽度和高度、扇形的起始角度（角度）和扫掠角度（角度）。角度顺时针增加。`FillEllipse`（第 50 和 56 行）、`FillRectangle`（第 53–54 行）和 `FillPie`（第 60–61 行）方法与它们的未填充版本相似，不同在于它们接受一个 `Brush`（例如 `SolidBrush`）而不是 `Pen`。部分绘制的形状在图 15.23 的截图中所示。

`TreeView` 控件在树中以分级方式显示节点。传统上，节点是包含值并可以引用其他对象的实例。父节点包含子节点，而子节点可以是其他节点的父节点。两个具有相同父节点的节点被视为兄弟节点。树是节点的集合，通常以分级方式组织。一个节点的第一个父节点是根节点（`TreeView` 可以有多个根节点）。例如，计算机的文件系统可以表示为树树。顶层目录（可能是 `C:`）将是根节点，`C` 的每个子文件夹都是子节点，每个子文件夹都可以有自己的子节点。`TreeView` 控件用于显示分级信息，例如我们刚刚提到的文件结构。我们将在第 19 章“自定义链接数据结构”中更详细地介绍节点和树。图 15.24 显示了表单上的示例 `TreeView`。

![](img/57baed2319be0bb1b5f98674846f2711_667_0.png)

图 15.24 | 显示示例树的 `TreeView`。

### 第 15 章 使用 Windows Forms 构建图形用户界面：第二部分

可以通过点击左侧的加号框或减号框展开或折叠父节点。没有子节点没有这些框。

树中的节点是 `TreeNode` 类的实例。每个 `TreeNode` 都有一个 `Nodes` 集合（类型为 `TreeNodeCollection`），它包含其他 `TreeNode` 列表——即其子节点。`Parent` 属性返回父节点的引用（如果节点是根节点，则返回 null）。图 15.25 和 15.26 列出了 `TreeView` 的常用属性、`TreeNode` 方法以及一个常用的 `TreeView` 事件。

| 常用属性 | 说明 |
| --- | --- |
| CheckBoxes | 表示节点旁边是否出现复选框。值为 `true` 时显示复选框。默认值为 `false`。 |
| ImageList | 指定一个包含节点的 `ImageList` 对象。`ImageList` 对象是一个包含 `Image` 对象的集合。 |
| Nodes | 以 `TreeNodeCollection` 形式返回控件中的 `Nodes` 集合。它包含方法 `Add`（添加 `TreeNode` 对象）、`Clear`（删除整个集合）和 `Remove`（删除特定节点）。删除父节点会删除所有子节点。 |
| SelectedNode | 被选中的节点。 |
| 常用事件 (event arguments EventArgs) | 在所选节点发生变化后生成。这是在设计器中双击控件时的默认事件。 |

**图 15.25** | `TreeView` 属性和事件。

| 常用属性 | 说明 |
| --- | --- |
| Checked | 表示 `TreeNode` 是否被勾选（在父节点 `TreeNode` 中 `CheckBoxes` 属性必须设置为 `true`）。 |
| FirstNode | 指定 `Nodes` 集合中的第一个节点（即树中的第一个子节点）。 |
| FullPath | 表示节点的路径，从树的根节点开始。 |
| ImageIndex | 指定节点未被选中时显示的图像在 `TreeNode` 的 `ImageList` 中的索引。 |
| LastNode | 指定 `Nodes` 集合中的最后一个节点（即树中的最后一个子节点）。 |
| NextNode | 下一个兄弟节点。 |
| Nodes | 当前节点中的 `Nodes` 集合（即当前节点的所有子节点）。它包含方法 `Add`（添加 `TreeNode` 对象）、`Clear`（删除整个集合）和 `Remove`（删除特定节点）。删除父节点会删除所有子节点。 |

**图 15.26** | `TreeNode` 属性和方法。（部分内容，共 2 部分）。

| TreeNode 属性和方法 |get |
| ---|---|
| PrevNode | 上一个兄弟节点。 |
| SelectedImageIndex | 指定节点被选中时使用的图像在 `TreeView` 的 `Image` 中的索引。 |
| Text | 指定 `TreeNode` 的文本。 |
| 常用方法 | |
| Collapse | 折叠节点。 |
| Expand | 展开节点。 |
| ExpandAll | 展开节点的所有子节点。 |
| GetNodeCount | 返回子节点的数量。 |

图 15.26 | `TreeNode` 属性和方法。（部分内容，共 2 部分）。

要可视化地向 `TreeView` 添加节点，请点击属性窗口中 `Nodes` 属性旁边的省略号。这会打开 `TreeNode` 编辑器（图 15.27），它显示了一个表示 `TreeView` 的空树。有按钮可以创建根节点以及在当前节点右侧添加或删除节点。在这里你可以重命名节点。

![](img/57baed2319be0bb1b5f98674846f2711_669_0.png)

图 15.27 | `TreeNode` 编辑器。

要通过程序向 `TreeView` 添加节点，首先创建一个根节点。创建一个新的 `TreeNode` 对象并传递一个要显示的字符串。然后调用 `Add` 方法将此 `TreeNode` 添加到 `TreeView`。

```csharp
myTreeView.Nodes.Add(new TreeNode(rootNode));
```

其中 `myTreeView` 是我们正在添加节点的 `TreeView`，`rootLabel` 是要显示的文本。要向根节点添加子节点，通过我们向 `myTreeView` 添加节点的相同方式。

```csharp
myTreeView.Nodes[index]
```

其中 `index` 是根节点在 `TreeView` 集合中的索引。要向根节点添加子节点，编写：

```csharp
myTreeView.Nodes[index].Nodes.Add(new TreeNode(childLabel));
```

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

图 15.28 | 使用 `TreeView` 显示目录结构。（3 部分中的第 2 部分。）

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

图 15.28 | 使用 `TreeNode` 显示目录结构。（3 部分中的第 3 部分）

当用户点击 Enter 按钮时，`directoryTreeView` 中的所有节点都会清除（第 66 行）。如果目录存在（第 71 行），则使用 `TextBox` 中输入的路径来创建根节点。第 74 行将目录作为根节点添加到 `TreeView` 中，第 77–78 行调用 `PopulateTreeView`（第 21–60 行），该方法接收一个目录（字符串）和一个父节点。然后 `PopulateTreeView` 创建与接收到的参数的子目录对应的子节点。

`PopulateTreeView` 方法（第 21–60 行）使用第 25–26 行中 `Directory` 类（namespace.IO）的 `GetDirectories` 获取子目录列表。`GetDirectories` 方法接收一个字符串（当前目录）并返回字符串数组（子目录）。由于安全原因无法访问目录，将抛出 `UnauthorizedAccessException`。第 56–59 行可以捕获此异常，并添加节点“Access denied”而不是显示子目录。

如果有子目录，第 42–43 行使用 `Path` 类的 `GetFileNameWithoutExtension` 通过将完整路径名缩短为目录名来提高可读性。接下来，`directoryArray` 中的每个字符串都被用于创建一个新的子节点（第 46 行）。我们使用 `Add`（第 49 行）将每个子节点添加到父节点。然后对每个子目录递归调用 `PopulateTreeView` 方法（第 52 行），最终为 Tree 填充整个目录结构。我们的递归算法在程序加载大型目录时可能会导致延迟。然而，一旦文件夹名称被添加到相应的 `Nodes` 集合，就可以无延迟地展开和折叠它们。在下一节中，我们将介绍一种解决此问题的替代算法。

## 15.10 ListView 控件

`ListView` 与 `ListBox` 类似，两者都可以显示列表，且用户可以选择一个或多个项目（可以在 15.31 中找到 `ListView` 的示例）。`ListView` 更通用，可以以不同的格式显示项目。`ListView` 可以在列表项旁边显示项目（由其 `SmallImageList`、`LargeImage-ImageList` 控制），并在列中显示项目的详细信息。属性 `MultiSelect`（一个 bool）决定是否允许选择多个项目。通过将属性 `CheckBoxes`（一个 bool）设置为 `true`，可以包含复选框，使 `ListView` 的外观类似于 `CheckListBox`。属性 `Activation` 决定用户选择列表的方法。这些属性以及 `Click` 和 `ItemActivate` 事件的细节将在 15.29 中进行解释。

| ListView 属性和事件 | 描述 |
|---|---|
| 通用属性 Activation | 决定用户如何激活项目。此属性接受 `ItemActivation` 枚举中的值。可能的值有 `OneClick`（单击激活）、`TwoClick`（双击激活，鼠标悬过项目时项目颜色会变化）和 `Standard`（默认值；双击激活，项目颜色不变化）。 |
| CheckBoxes | 表明项目是否带有复选框出现。`true` 显示复选框。默认值为 `false`。 |
| LargeImageList Items | 指定包含显示大图标的 `ImageList`。返回控件中 `ListViewItems` 集合。 |
| MultiSelect | 决定是否允许多选。如果是 `true`，则启用多选。 |
| SelectedItems | 返回被选中项目的 `ListView.SelectedItemsCollection`。 |
| SmallImageList View | 指定包含显示小图标的 `ImageList`。决定 `ListViewItems` 的外观。可能的值有 `LargeIcon`（默认；显示大图标，可以是多列）、`SmallIcon`（显示小图标，可以是多列）、`List`（小图标显示在单列）、`Details`（每个项目可以显示多列信息）和 `Tile`（显示大图标，右提供提供）。 |
| 通用事件 Click Activate | 项目被点击时触发。这是默认事件。当 `ListView` 中的项目被激活（点击或双击）时触发。它不包含激活项目的具体信息——可以使用 `SelectedItems` 或 `SelectedIndices` 来确定这一点。 |

图 15.29 | `ListView` 属性和事件。

# 15.10 ListView 675

```cpp
// 表单包含一个 ListView，用于显示
// 目录中的文件夹和文件
public partial class ListViewTestForm : Form
{
    // 存储当前目录
    string currentDirectory = Directory.GetCurrentDirectory();
    // 构造函数
    public ListViewTestForm()
    {
        InitializeComponent();
    }
    // 点击浏览器列表框 或向上跳一级
    private void browserListView_Click(object sender, EventArgs e)
    {
        // 确保至少选择了一个项
        if (listView.SelectedItems.Count == 0)
        {
            // 如果选中了第一个项，则向上跳一级
            if (listView.Items[0].Selected)
            {
                //为目录创建 DirectoryInfo 对象
                DirectoryInfo directoryObject =
                    new DirectoryInfo(currentDirectory);
                // 如果目录有父目录，则加载它
                if (directoryObject.Parent != null)
                {
                    LoadFilesDirectory(directoryObject.Parent.FullName);
                }
            }
            // 选中的目录或文件
            else
            {
                // 选择了目录或文件
                string chosen = browserListView.SelectedItems[0].Text;
                // 如果选中的项是目录，则加载选定的目录

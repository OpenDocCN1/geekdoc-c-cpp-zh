
| TreeNode 属性和方法 | 描述 |
|---|---|
| PrevNode | 前一个兄弟节点。 |
| SelectedImageIndex | 指定在节点被选中时使用的图像在 TreeView 的 ImageList 中的索引。 |
| Text | 指定 TreeNode 的文本。 |
| *通用方法* | |
| Collapse | 折叠一个节点。 |
| Expand | 展开一个节点。 |
| ExpandAll | 展开一个节点的所有子节点。 |
| GetNodeCount | 返回子节点的数量。 |

图 15.26 | TreeNode 属性和方法。 (第 2 部分，共 2 部分。)

要可视化地向 TreeView 添加节点，请在属性窗口中单击 Nodes 属性旁边的省略号。这将打开 TreeNode 编辑器 (图 15.27)，它显示代表 TreeView 的空树。 有按钮可用于创建根节点以及添加或删除节点。 右侧是当前节点的属性。 在这里您可以重命名节点。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_505_0.png)

图 15.27 | TreeNode 编辑器。

要以编程方式添加节点，首先创建根节点。 创建一个新的 TreeNode 对象并传递要显示的字符串。 然后调用方法 Add 将此新的 TreeNode 添加到 TreeView 的 Nodes 集合中。 因此，要向 TreeView myTreeView 添加根节点，请编写

```
myTreeView.Nodes.Add(new TreeNode(rootLabel));
```

其中 myTreeView 是我们要添加节点的 TreeView，rootLabel 是要在 myTreeView 中显示的文本。 要向根节点添加子节点，请向其 Nodes 集合添加新的 TreeNodes。 我们通过编写以下内容从 TreeView 中选择适当的根节点

```
myTreeView.Nodes[myIndex]
```

其中 myIndex 是 myTreeView 的 Nodes 集合中根节点的索引。 我们通过与将根节点添加到 myTreeView 相同的过程将节点添加到子节点。 要向索引为 myIndex 的根节点添加子节点，请编写

```
myTreeView.Nodes[myIndex].Nodes.Add(new TreeNode(ChildLabel));
```

类 TreeViewDirectoryStructureForm (图 15.28) 使用 TreeView 显示用户选择的目录的内容。 使用 TextBox 和 Button 指定目录。 首先，输入要显示的目录的完整路径。 然后单击 Button 将指定的目录设置为 TreeView 中的根节点。 此目录的每个子目录都成为一个子节点。 这种布局与 Windows Explorer 中使用的布局相似。 可以通过单击其左侧出现的加号或减号框来展开或折叠文件夹。

```csharp
1  // Fig. 15.28: TreeViewDirectoryStructureForm.cs
2  // Using TreeView to display directory structure.
3  using System;
4  using System.Windows.Forms;
5
6  using System.IO;
7
8  namespace TreeViewDirectoryStructure
9  {
10     // Form uses TreeView to display directory structure
11     public partial class TreeViewDirectoryStructureForm : Form
12     {
13         string substringDirectory; // store last part of full path name
14
15         // constructor
16         public TreeViewDirectoryStructureForm()
17         {
18             InitializeComponent();
19         }
20
21         // populate current node with subdirectories
22         public void PopulateTreeView(
23             string directoryValue, TreeNode parentNode)
24         {
25             // array stores all subdirectories in the directory
26             string[] directoryArray =
27                 Directory.GetDirectories(directoryValue);
28
29             // populate current node with subdirectories
30             try
31             // check to see if any subdirectories are present
32             if (directoryArray.Length != 0)
33             {
34                 // for every subdirectory, create new TreeNode,
35                 // add as a child of current node and recursively
36                 // populate child nodes with subdirectories
37                 foreach (string directory in directoryArray)
38                 {
39                     // obtain last part of path name from the full path
40                     // name by calling the GetFileNameWithoutExtension
41                     // method of class Path
42                     substringDirectory =
43                         Path.GetFileNameWithoutExtension(directory);
44
45                     // create TreeNode for current directory
46                     TreeNode myNode = new TreeNode(substringDirectory);
47
48                     // add current directory node to parent node
49                     parentNode.Nodes.Add(myNode);
50
51                     // recursively populate every subdirectory
52                     PopulateTreeView(directory, myNode);
53                 }
54             }
55             catch (UnauthorizedAccessException)
56             {
57                 parentNode.Nodes.Add("Access denied");
58             }
59         }
60
61         // handles enterButton click event
62         private void enterButton_Click(object sender, EventArgs e)
63         {
64             // clear all nodes
65             directoryTreeView.Nodes.Clear();
66
67             // check if the directory entered by user exists
68             // if it does, then fill in the TreeView,
69             // if not, display error MessageBox
70             if (Directory.Exists(inputTextBox.Text))
71             {
72                 // add full path name to directoryTreeView
73                 directoryTreeView.Nodes.Add(inputTextBox.Text);
74
75                 // insert subfolders
76                 PopulateTreeView(
77                     inputTextBox.Text, directoryTreeView.Nodes[0]);
78             }
79             // display error MessageBox if directory not found
80             else
81             {
82                 MessageBox.Show(inputTextBox.Text + "  could not be found.",
83                     "Directory Not Found", MessageBoxButtons.OK,
84                     MessageBoxIcon.Error);
85             }
86         }
87     }
88 }
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_508_0.png)

**图 15.28** | 使用 TreeView 显示目录结构。 (第 3 部分，共 3 部分。)

当用户单击 enterButton 时，directoryTreeView 中的所有节点将被清除 (第 66 行)。 然后，如果目录存在 (第 71 行)，则在 inputTextBox 中输入的路径用于创建根节点。 第 74 行将目录添加到 directoryTreeView 作为根节点，第 77–78 行调用方法 PopulateTreeView (第 21–60 行)，该方法接受一个目录 (字符串) 和一个父节点。 方法 PopulateTreeView 然后创建与它作为参数接收的目录的子目录相对应的子节点。

方法 PopulateTreeView (第 21–60 行) 使用类 Directory (命名空间 System.IO) 的方法 GetDirectories 在第 25–26 行获取子目录列表。 方法 GetDirectories 接受一个字符串 (当前目录) 并返回一个字符串数组 (子目录)。 如果由于安全原因目录无法访问，则会抛出 UnauthorizedAccessException。 第 56–59 行捕获此异常并添加包含 "Access denied" 的节点，而不是显示子目录。

如果存在可访问的子目录，则第 42–43 行使用类 Path 的方法 GetFileNameWithoutExtension 通过将完整路径名缩短为仅目录名来提高可读性。 Path 类提供用于处理文件或目录路径字符串的功能。 接下来，directoryArray 中的每个字符串都用于创建新的子节点 (第 46 行)。 我们使用方法 Add (第 49 行) 将每个子节点添加到父节点。 然后方法 PopulateTreeView 在每个子目录上递归调用 (第 52 行)，最终用整个目录结构填充 TreeView。 我们的递归算法在程序加载大目录时可能会导致延迟。 然而，一旦文件夹名称被添加到适当的 Nodes 集合中，它们就可以在没有延迟的情况下展开和折叠。 在下一节中，我们将介绍一种替代算法来解决此问题。

## 15.10 ListView 控件

ListView 控件与 ListBox 相似，因为两者都显示用户可以从中选择一个或多个项目的列表 (ListView 的示例可在图 15.31 中找到)。 ListView 更通用，可以以不同的格式显示项目。 例如，ListView 可以在列表项旁边显示图标 (由其 SmallImageList、LargeImageList 或 StateImageList 属性控制) 并以列的形式显示项目的详细信息。 属性 MultiSelect (布尔值) 确定是否允许选择多个项目。 可以通过将属性 CheckBoxes (布尔值) 设置为 true 来包含 CheckBoxes，使 ListView 的外观类似于 CheckedListBox。 View 属性指定 ListBox 的布局。 属性 Activation 确定用户选择列表项的方法。 这些属性和 Click 以及 ItemActivate 事件的详细信息在图 15.29 中解释。

| ListView 属性和事件 | 描述 |
| --- | --- |
| *通用属性* | |
| Activation | 确定用户如何激活项目。 此属性采用 ItemActivation 枚举中的值。 可能的值为 OneClick (单击激活)、TwoClick (双击激活，鼠标移过项目时项目颜色发生变化) 和 Standard (默认值；双击激活，项目颜色不发生变化)。 |
| CheckBoxes | 指示项目是否带有 CheckBoxes 显示。 true 显示 CheckBoxes。 默认值为 false。 |
| LargeImageList | 指定用于显示的大图标的 ImageList。 |
| Items | 返回控件中的 ListViewItems 集合。 |
| MultiSelect | 确定是否允许多选。 默认值为 true，这启用多选。 |
| SelectedItems | 以 ListView.SelectedListViewItemCollection 的形式返回所选项目的集合。 |
| SmallImageList | 指定用于显示的小图标的 ImageList。 |
| View | 确定 ListViewItems 的外观。 可能的值为 LargeIcon (默认值；显示大图标，项目可以位于多列中)、SmallIcon (显示小图标，项目可以位于多列中)、List (显示小图标，项目出现在单列中)、Details (类似于 List，但每个项目可以显示多列信息) 和 Tile (显示大图标，信息提供在图标右侧)。 |
| *通用事件* | |
| Click | 在单击项目时生成。 这是默认事件。 |
| ItemActivate | 在 ListView 中的项目被激活时生成 (单击或双击)。 不包含激活的是哪个项目的具体信息——您可以使用 SelectedItems 或 SelectedIndices 来确定这一点。 |

**图 15.29** | ListView 属性和事件。

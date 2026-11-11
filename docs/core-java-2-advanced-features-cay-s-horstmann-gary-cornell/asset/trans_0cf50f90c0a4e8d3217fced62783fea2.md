

> **警告：** `DefaultTreeModel` 类有一个 `reload` 方法，用于重新加载整个模型。但是，不要仅仅为了在做了少量更改后更新树而调用 `reload`。当树被重新生成时，根节点的子节点之外的所有节点都会再次折叠。如果用户每次更改后都必须不断展开树，那将会让他们感到非常困扰。

当视图收到节点结构发生变化的通知时，它会更新显示，但不会自动展开节点来显示新添加的子节点。特别是，如果示例程序中的用户向一个当前子节点已折叠的节点添加新的子节点，这个新节点会被静默地添加到折叠的子树中。这使用户得不到任何命令已经实际执行的反馈。在这种情况下，你应该特意展开所有父节点，使新添加的节点变为可见。为此，可以使用 `JTree` 类的 `makeVisible` 方法。`makeVisible` 方法需要一个指向应变得可见节点的树路径。

因此，你需要构造一条从根节点到新插入节点的树路径。要获得树路径，首先调用 `DefaultTreeModel` 类的 `getPathToRoot` 方法。它会返回一个 `TreeNode[]` 数组，其中包含从某个节点到根节点的所有节点。将该数组传递给 `TreePath` 构造函数。

例如，下面演示如何使新节点可见：

```java
TreeNode[] nodes = model.getPathToRoot(newNode);
TreePath path = new TreePath(nodes);
tree.makeVisible(path);
```

> **注意：** 有趣的是，`DefaultTreeModel` 类几乎完全无视 `TreePath` 类，尽管它的工作就是与 `JTree` 进行通信。`JTree` 类大量使用树路径，而从不使用节点对象数组。

但现在假设你的树位于滚动窗格中。在树节点展开之后，新节点可能仍然不可见，因为它位于视口之外。要解决这个问题，调用

```java
tree.scrollPathToVisible(path);
```

而不是调用 `makeVisible`。这个调用会展开沿路径的所有节点，并告诉周围的滚动窗格将路径末尾的节点滚动到视图中（参见图10.29）。

![](img/7dd923a566750151a3aab0dacd0cdaa5_674_0.png)

**图10.29** 滚动窗格滚动以显示新节点

默认情况下，树节点不可编辑。但是，如果你调用

```java
tree.setEditable(true);
```

用户只需双击、编辑字符串并按下回车键即可编辑节点。双击会调用*默认单元格编辑器*，它由 `DefaultCellEditor` 类实现（参见图10.30）。也可以使用我们在讨论表格单元格编辑器时看到的相同过程来安装其他单元格编辑器。

![](img/7dd923a566750151a3aab0dacd0cdaa5_674_1.png)

**图10.30** 默认单元格编辑器

清单10.13展示了树编辑程序的完整源代码。运行该程序，添加几个节点，然后通过双击来编辑它们。观察折叠的节点如何展开以显示添加的子节点，以及滚动窗格如何将添加的节点保持在视口内。

## 清单10.13 TreeEdit/TreeEditFrame.java

```java
1 package treeEdit;
2
3 import java.awt.*;
4
5 import javax.swing.*;
6 import javax.swing.tree.*;
7
8 /**
9  * A frame with a tree and buttons to edit the tree.
10 */
11 public class TreeEditFrame extends JFrame
12 {
13    private static final int DEFAULT_WIDTH = 400;
14    private static final int DEFAULT_HEIGHT = 200;
15
16    private DefaultTreeModel model;
17    private JTree tree;
18
19    public TreeEditFrame()
20    {
21       setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
22
23       // construct tree
24
25       TreeNode root = makeSampleTree();
26       model = new DefaultTreeModel(root);
27       tree = new JTree(model);
28       tree.setEditable(true);
29
30       // add scroll pane with tree
31
32       JScrollPane scrollPane = new JScrollPane(tree);
33       add(scrollPane, BorderLayout.CENTER);
34
35       makeButtons();
36    }
37
38    public TreeNode makeSampleTree()
39    {
40       DefaultMutableTreeNode root = new DefaultMutableTreeNode("World");
41       DefaultMutableTreeNode country = new DefaultMutableTreeNode("USA");
42       root.add(country);
43       DefaultMutableTreeNode state = new DefaultMutableTreeNode("California");
44       country.add(state);
45       DefaultMutableTreeNode city = new DefaultMutableTreeNode("San Jose");
46       state.add(city);
47      city = new DefaultMutableTreeNode("San Diego");
48      state.add(city);
49      state = new DefaultMutableTreeNode("Michigan");
50      country.add(state);
51      city = new DefaultMutableTreeNode("Ann Arbor");
52      state.add(city);
53      country = new DefaultMutableTreeNode("Germany");
54      root.add(country);
55      state = new DefaultMutableTreeNode("Schleswig-Holstein");
56      country.add(state);
57      city = new DefaultMutableTreeNode("Kiel");
58      state.add(city);
59      return root;
60  }
61
62  /**
63   * Makes the buttons to add a sibling, add a child, and delete a node.
64   */
65  public void makeButtons()
66  {
67      JPanel panel = new JPanel();
68      JButton addSiblingButton = new JButton("Add Sibling");
69      addSiblingButton.addActionListener(event ->
70          {
71              DefaultMutableTreeNode selectedNode = (DefaultMutableTreeNode) tree
72                  .getLastSelectedPathComponent();
73
74              if (selectedNode == null) return;
75
76              DefaultMutableTreeNode parent = (DefaultMutableTreeNode) selectedNode.getParent();
77
78              if (parent == null) return;
79
80              DefaultMutableTreeNode newNode = new DefaultMutableTreeNode("New");
81
82              int selectedIndex = parent.getIndex(selectedNode);
83              model.insertNodeInto(newNode, parent, selectedIndex + 1);
84
85              // now display new node
86
87              TreeNode[] nodes = model.getPathToRoot(newNode);
88              TreePath path = new TreePath(nodes);
89              tree.scrollPathToVisible(path);
90          });
91      panel.add(addSiblingButton);
92
93      JButton addChildButton = new JButton("Add Child");
addChildButton.addActionListener(event ->
{
    DefaultMutableTreeNode selectedNode = (DefaultMutableTreeNode) tree
        .getLastSelectedPathComponent();

    if (selectedNode == null) return;

    DefaultMutableTreeNode newNode = new DefaultMutableTreeNode("New");
    model.insertNodeInto(newNode, selectedNode, selectedNode.getChildCount());

    // now display new node

    TreeNode[] nodes = model.getPathToRoot(newNode);
    TreePath path = new TreePath(nodes);
    tree.scrollPathToVisible(path);
});
panel.add(addChildButton);

JButton deleteButton = new JButton("Delete");
deleteButton.addActionListener(event ->
{
    DefaultMutableTreeNode selectedNode = (DefaultMutableTreeNode) tree
        .getLastSelectedPathComponent();

    if (selectedNode != null && selectedNode.getParent() != null) model
        .removeNodeFromParent(selectedNode);
});
panel.add(deleteButton);
add(panel, BorderLayout.SOUTH);
}
```

- **javax.swing.JTree 1.2**
  - `TreePath getSelectionPath()`  
    获取当前选中节点的路径，如果选中了多个节点，则获取第一个选中节点的路径。如果没有选中节点，则返回 `null`。
  - `Object getLastSelectedPathComponent()`  
    获取表示当前选中节点的节点对象，如果选中了多个节点，则获取第一个选中的节点。如果没有选中节点，则返回 `null`。
  - `void makeVisible(TreePath path)`  
    展开沿路径的所有节点。
  - `void scrollPathToVisible(TreePath path)`  
    展开沿路径的所有节点，如果树包含在滚动窗格中，则滚动以确保路径上的最后一个节点可见。


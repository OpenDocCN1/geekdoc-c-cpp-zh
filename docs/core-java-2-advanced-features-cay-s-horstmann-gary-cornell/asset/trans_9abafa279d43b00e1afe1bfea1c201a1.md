

![](img/7dd923a566750151a3aab0dacd0cdaa5_666_0.png)

图 10.22 没有连接线的树

相反，要确保显示这些线，请使用

```java
tree.putClientProperty("JTree.lineStyle", "Angled");
```

另一种线样式“Horizontal”如图 10.23 所示。该树显示为仅用水平线分隔根节点的子节点。我们不太确定它有什么用处。

![](img/7dd923a566750151a3aab0dacd0cdaa5_666_1.png)

图 10.23 使用水平线样式的树

默认情况下，没有用于折叠树根的控制柄。如果愿意，可以通过以下调用添加一个

```java
tree.setShowsRootHandles(true);
```

图 10.24 显示了结果。现在可以将整棵树折叠到根节点中。

![](img/7dd923a566750151a3aab0dacd0cdaa5_668_0.png)

**图 10.26** 叶子和文件夹图标

显示树时，每个节点都用一个图标绘制。实际上有三种图标：叶子图标、打开的非叶子图标和关闭的非叶子图标。为简单起见，我们将后两种称为文件夹图标。

节点渲染器需要知道每个节点使用哪个图标。默认情况下，判定过程如下：如果节点的 `isLeaf` 方法返回 true，则使用叶子图标；否则使用文件夹图标。

`DefaultMutableTreeNode` 类的 `isLeaf` 方法在节点没有子节点时返回 true。因此，有子节点的节点获得文件夹图标，没有子节点的节点获得叶子图标。

有时，这种行为并不合适。假设我们向示例树中添加了一个节点“Montana”，但不知道该添加哪些城市。我们不希望州节点获得叶子图标，因为从概念上讲，只有城市才是叶子。

`JTree` 类并不知道哪些节点应该是叶子。它会询问树模型。如果无子节点的节点并不自动成为概念上的叶子，可以要求树模型使用不同的叶子判定标准——即查询节点的“allows children”属性。

对于那些不应有子节点的节点，请调用

```java
node.setAllowsChildren(false);
```

然后，告诉树模型查询“allows children”属性的值，以确定是否应将节点显示为叶子图标。使用 `DefaultTreeModel` 类的 `setAsksAllowsChildren` 方法设置此行为。

```java
model.setAsksAllowsChildren(true);
```

使用此判定标准时，允许有子节点的节点获得文件夹图标，不允许有子节点的节点获得叶子图标。

或者，如果从根节点构造树，请在构造函数中提供“asks allows children”属性的设置。

```java
JTree tree = new JTree(root, true); // nodes that don't allow children get leaf icons
```

**javax.swing.JTree 1.2**

- `JTree(TreeModel model)`  
  从树模型构造一棵树。
- `JTree(TreeNode root)`
- `JTree(TreeNode root, boolean asksAllowsChildren)`  
  使用显示根节点及其子节点的默认树模型构造一棵树。

  **参数：**
  - `root` — 根节点
  - `asksAllowsChildren` — 为 true 时使用“allows children”节点属性来确定节点是否为叶子
- `void setShowsRootHandles(boolean b)`  
  如果 b 为 true，则根节点具有用于折叠或展开其子节点的控制柄。
- `void setRootVisible(boolean b)`  
  如果 b 为 true，则显示根节点。否则，隐藏根节点。

**javax.swing.tree.TreeNode 1.2**

- `boolean isLeaf()`  
  如果此节点在概念上是叶子，则返回 true。
- `boolean getAllowsChildren()`  
  如果此节点可以有子节点，则返回 true。

**javax.swing.tree.MutableTreeNode 1.2**

- `void setUserObject(Object userObject)`  
  设置树节点用于渲染的“用户对象”。

**javax.swing.tree.TreeModel 1.2**

- `boolean isLeaf(Object node)`  
  如果 node 应显示为叶子节点，则返回 true。

| `javax.swing.tree.DefaultTreeModel` 1.2 |
| --- |
| - `void setAsksAllowsChildren(boolean b)`<br>如果 b 为 true，则当节点的 `getAllowsChildren` 方法返回 false 时，节点显示为叶子。否则，当节点的 `isLeaf` 方法返回 true 时，它们显示为叶子。 |

| `javax.swing.tree.DefaultMutableTreeNode` 1.2 |
| --- |
| - `DefaultMutableTreeNode(Object userObject)`<br>使用给定的用户对象构造一个可变树节点。<br>- `void add(MutableTreeNode child)`<br>将一个节点添加为此节点的最后一个子节点。<br>- `void setAllowsChildren(boolean b)`<br>如果 b 为 true，则可以向此节点添加子节点。 |

| `javax.swing.JComponent` 1.2 |
| --- |
| - `void putClientProperty(Object key, Object value)`<br>向每个组件管理的一个小表中添加一个键/值对。这是一种“逃生舱口”机制，一些 Swing 组件用它来存储特定于外观风格的属性。 |

### 10.3.2 编辑树和树路径

在下一个示例程序中，你将看到如何编辑树。图 10.27 显示了用户界面。如果单击“Add Sibling”或“Add Child”按钮，程序会向树中添加一个新节点（标题为 New）。如果单击“Delete”按钮，程序会删除当前选中的节点。

要实现此行为，需要找出当前选中的是哪个树节点。JTree 类识别树中节点的方式令人意外。它不处理树节点，而是处理*对象路径*，称为*树路径*。树路径从根开始，由一系列子节点组成（见图 10.28）。

你可能想知道，JTree 类为什么需要整个路径。它难道不能直接获取一个 TreeModel 并不断调用 getParent 方法吗？实际上，JTree 类对 TreeNode 接口一无所知。JTree 类从不使用该接口；它只由 DefaultTreeModel 实现使用。你也可以使用其他树模型，其中的节点根本不实现 TreeNode 接口。如果使用管理其他类型对象的树模型，那些对象可能没有 getParent 和 getChild 方法。它们当然需要通过某种其他方式相互连接。将节点链接在一起是树模型的职责。JTree 类本身完全不了解它们之间链接的性质。因此，JTree 类始终需要使用完整路径。

![](img/7dd923a566750151a3aab0dacd0cdaa5_671_0.png)

![](img/7dd923a566750151a3aab0dacd0cdaa5_671_1.png)

TreePath 类管理一系列 Object（不是 TreeNode！）引用。许多 JTree 方法返回 TreePath 对象。当拥有树路径时，通常只需知道终端节点，可以通过 getLastPathComponent 方法获取。例如，要找出树中当前选中的节点，请使用 JTree 类的 getSelectionPath 方法。你将得到一个 TreePath 对象，从中可以获取实际节点。

```java
TreePath selectionPath = tree.getSelectionPath();
DefaultMutableTreeNode selectedNode
    = (DefaultMutableTreeNode) selectionPath.getLastPathComponent();
```

实际上，由于这种查询非常常见，因此有一个便捷方法可以直接给出选中的节点：

```java
DefaultMutableTreeNode selectedNode
    = (DefaultMutableTreeNode) tree.getLastSelectedPathComponent();
```

此方法不叫 `getSelectedNode`，因为树并不知道自己包含节点——它的树模型只处理对象路径。

> **注意：** 树路径是 `JTree` 类描述节点的两种方式之一。不少 `JTree` 方法接受或返回一个整数索引——*行位置*。行位置就是节点在树显示中的行号（从 0 开始）。只有可见节点才有行号，并且如果节点之前的其他节点被展开、折叠或修改，该节点的行号会发生变化。因此，应避免使用行位置。所有使用行的 `JTree` 方法都有使用树路径的等价方法。

一旦获得选中的节点，就可以编辑它。但是，不要只是向树节点添加子节点：

```java
selectedNode.add(newNode); // No!
```

如果更改节点的结构，就会更改模型，但关联的视图不会收到通知。你可以自己发出通知，但如果使用 `DefaultTreeModel` 类的 `insertNodeInto` 方法，模型类会处理这件事。例如，以下调用会将一个新节点追加为选中节点的最后一个子节点，并通知树视图：

```java
model.insertNodeInto(newNode, selectedNode, selectedNode.getChildCount());
```

对 `removeNodeFromParent` 的类似调用会移除一个节点并通知视图：

```java
model.removeNodeFromParent(selectedNode);
```

如果保持节点结构不变但更改用户对象，则应调用以下方法：

```java
model.nodeChanged(changedNode);
```

自动通知是使用 `DefaultTreeModel` 的一个主要优势。如果提供自己的树模型，则必须手动实现自动通知。（详情请参阅 Kim Topley 的 *Core Swing*。）


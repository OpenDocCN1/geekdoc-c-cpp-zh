
| 成员/方法 | 说明 |
|---|---|
| `javax.swing.CellEditor` | 版本 `1.2` |
| `boolean isCellEditable(EventObject event)` | 如果该事件适合启动此单元格的编辑过程，则返回 true。 |
| `boolean shouldSelectCell(EventObject anEvent)` | 启动编辑过程。如果应选中被编辑的单元格，则返回 true。通常希望返回 true，但如果不希望编辑过程改变单元格选择，可以返回 false。 |
| `void cancelCellEditing()` | 取消编辑过程。可以放弃部分编辑。 |
| `boolean stopCellEditing()` | 停止编辑过程，意图使用编辑结果。如果编辑后的值处于可检索的正确状态，则返回 true。 |
| `Object getCellEditorValue()` | 返回编辑后的结果。 |
| `void addCellEditorListener(CellEditorListener l)` | 添加必需的单元格编辑器监听器。 |
| `void removeCellEditorListener(CellEditorListener l)` | 移除必需的单元格编辑器监听器。 |

## 11.2 树

每位使用过分层文件系统的计算机用户都见过树形显示。当然，目录和文件只是众多树状组织示例之一。许多树结构出现在日常生活中，例如图 11.11 所示的国家、州和城市的层级结构。

作为程序员，我们经常需要显示树结构。幸运的是，Swing 库为此提供了 `JTree` 类。`JTree` 类（及其辅助类）负责布置树，并处理用户展开和折叠节点的请求。在本节中，你将学习如何使用 `JTree` 类。

与其他复杂的 Swing 组件一样，我们必须关注常见且有用的情形，无法涵盖每个细节。如果你想实现某些不寻常的功能，我们建议查阅 David M. Geary 所著的 *Graphic Java™, 第三版* 或 Kim Topley 所著的 *Core Swing*。

在继续之前，我们先确定一些术语（见图 11.12）。树由节点组成。每个节点要么是叶节点，要么有子节点。除根节点外，每个节点恰好有一个父节点。一棵树恰好有一个根节点。有时你会有一组树，每棵树都有自己的根节点。这样的集合称为*森林*。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_675_0.png)

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_675_1.png)

### 11.2.1 简单的树

在第一个示例程序中，我们将简单地显示一棵包含几个节点的树（见图 11.14）。与许多其他 Swing 组件一样，你需要提供数据模型，组件会为你显示它。要构造 JTree，请在构造函数中提供树模型：

```
TreeModel model = . . . ;
var tree = new JTree(model);
```

> **注意：** 还有一些构造函数可以从元素集合构造树：
>
> ```java
> JTree(Object[] nodes)
> JTree(Vector<?> nodes)
> JTree(Hashtable<?, ?> nodes) // the values become the nodes
> ```
>
> 这些构造函数不太有用。它们只是构建一个由树组成的森林，每棵树只有一个节点。第三个构造函数似乎尤其无用，因为节点似乎以由键的哈希码决定的随机顺序出现。

如何获得树模型？你可以通过创建一个实现 TreeModel 接口的类来构造自己的模型。本章后面你将看到如何做到这一点。目前，我们将沿用 Swing 库提供的 DefaultTreeModel。

要构造默认树模型，必须提供根节点。

```
TreeNode root = . . . ;
var model = new DefaultTreeModel(root);
```

TreeNode 是另一个接口。用任何实现该接口的类的对象填充默认树模型。目前，我们将使用 Swing 提供的具体节点类——即 DefaultMutableTreeNode。该类实现 MutableTreeNode 接口，而该接口是 TreeNode 的子接口（见图 11.13）。

默认可变树节点包含一个对象——用户对象。树会为所有节点渲染用户对象。除非指定渲染器，否则树显示 toString 方法的结果字符串。

在第一个示例中，我们使用字符串作为用户对象。实践中，你通常会用更具表现力的用户对象填充树。例如，显示目录树时，为节点使用文件对象是合理的。

你可以在构造函数中指定用户对象，也可以稍后使用 setUserObject 方法设置它。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_677_0.png)

**图 11.13** 树类

```
var node = new DefaultMutableTreeNode("Texas");
. . .
node.setUserObject("California");
```

接下来，需要建立节点之间的父/子关系。从根节点开始，使用 add 方法添加子节点：

```
var root = new DefaultMutableTreeNode("World");
var country = new DefaultMutableTreeNode("USA");
root.add(country);
var state = new DefaultMutableTreeNode("California");
country.add(state);
```

图 11.14 展示了树的外观。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_678_0.png)

**图 11.14** 一棵简单的树

按这种方式连接所有节点。然后，用根节点构造 DefaultTreeModel。最后，用树模型构造 JTree。

```
var treeModel = new DefaultTreeModel(root);
var tree = new JTree(treeModel);
```

或者，作为一种快捷方式，你可以直接将根节点传给 JTree 构造函数。这样树会自动构造默认树模型：

```
var tree = new JTree(root);
```

清单 11.8 包含完整代码。

**清单 11.8** `tree/SimpleTreeFrame.java`

```java
package tree;

import javax.swing.*;
import javax.swing.tree.*;

/**
 * This frame contains a simple tree that displays a manually constructed tree model.
 */
public class SimpleTreeFrame extends JFrame
{
    private static final int DEFAULT_WIDTH = 300;
    private static final int DEFAULT_HEIGHT = 200;

    public SimpleTreeFrame()
    {
        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

        // set up tree model data

        var root = new DefaultMutableTreeNode("World");
        var country = new DefaultMutableTreeNode("USA");
        root.add(country);
        var state = new DefaultMutableTreeNode("California");
        country.add(state);
        var city = new DefaultMutableTreeNode("San Jose");
        state.add(city);
        city = new DefaultMutableTreeNode("Cupertino");
        state.add(city);
        state = new DefaultMutableTreeNode("Michigan");
        country.add(state);
        city = new DefaultMutableTreeNode("Ann Arbor");
        state.add(city);
        country = new DefaultMutableTreeNode("Germany");
        root.add(country);
        state = new DefaultMutableTreeNode("Schleswig-Holstein");
        country.add(state);
        city = new DefaultMutableTreeNode("Kiel");
        state.add(city);

        // construct tree and put it in a scroll pane

        var tree = new JTree(root);
        add(new JScrollPane(tree));
    }
}
```

运行程序时，树最初如图 11.15 所示。只有根节点及其子节点可见。单击圆形图标（即*控制柄*）以展开子树。当子树折叠时，从控制柄图标伸出的线指向右；当子树展开时，该线指向下（见图 11.16）。我们不知道 Metal 外观风格的设计者当时是怎么想的，但我们把这个图标看作门把手。向下按把手即可打开子树。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_679_0.png)

**图 11.15** 初始树显示

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_680_0.png)

**图 11.16** 折叠和展开的子树

> **注意：** 当然，树的显示取决于所选的外观风格。我们刚才描述的是 Metal 外观风格。在 Windows 外观风格中，控制柄具有更熟悉的外观——方框中的“−”或“+”（见图 11.17）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_680_1.png)

**图 11.17** 采用 Windows 外观风格的树

你可以使用以下神奇咒语关闭连接父节点和子节点的线（见图 11.18）：

```java
tree.putClientProperty("JTree.lineStyle", "None");
```

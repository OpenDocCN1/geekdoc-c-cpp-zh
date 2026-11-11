

```java
    // tell caller is ok to use color value
    return true;
}

public Object getCellEditorValue()
{
    return colorChooser.getColor();
}
```

## javax.swing.JTable 1.2

- `TableCellRenderer getDefaultRenderer(Class<?> type)`  
  获取给定类型的默认渲染器。
- `TableCellEditor getDefaultEditor(Class<?> type)`  
  获取给定类型的默认编辑器。

## javax.swing.table.TableCellRenderer 1.2

- `Component getTableCellRendererComponent(JTable table, Object value, boolean selected, boolean hasFocus, int row, int column)`  
  返回一个组件，该组件的 `paint` 方法被调用以渲染表格单元格。

  **参数：**

  | 参数 | 说明 |
  |---|---|
  | `table` | 包含要渲染单元格的表格 |
  | `value` | 要渲染的单元格 |
  | `selected` | 如果该单元格当前被选中，则为 `true` |
  | `hasFocus` | 如果该单元格当前获得焦点，则为 `true` |
  | `row, column` | 单元格的行和列 |

## javax.swing.table.TableColumn 1.2

- `void setCellEditor(TableCellEditor editor)`
- `void setCellRenderer(TableCellRenderer renderer)`  
  设置此列中所有单元格的单元格编辑器或渲染器。
- `void setHeaderRenderer(TableCellRenderer renderer)`  
  设置此列中表头单元格的单元格渲染器。
- `void setHeaderValue(Object value)`  
  设置此列表头要显示的值。

## javax.swing.DefaultCellEditor 1.2

- `DefaultCellEditor(JComboBox comboBox)`  
  构造一个单元格编辑器，显示用于选择单元格值的组合框。

## javax.swing.table.TableCellEditor 1.2

- `Component getTableCellEditorComponent(JTable table, Object value, boolean selected, int row, int column)`  
  返回一个组件，其 `paint` 方法渲染一个表格单元格。

  **参数：**

  | 参数 | 说明 |
  |---|---|
  | `table` | 包含要渲染单元格的表格 |
  | `value` | 要渲染的单元格 |
  | `selected` | 如果该单元格当前被选中，则为 `true` |
  | `row, column` | 单元格的行和列 |

## javax.swing.CellEditor 1.2

- `boolean isCellEditable(EventObject event)`  
  如果该事件适合为此单元格启动编辑过程，则返回 `true`。
- `boolean shouldSelectCell(EventObject anEvent)`  
  启动编辑过程。如果应选中正在编辑的单元格，则返回 `true`。通常应返回 `true`；但如果不想让编辑过程更改单元格选择，则可以返回 `false`。
- `void cancelCellEditing()`  
  取消编辑过程。可以放弃部分编辑内容。
- `boolean stopCellEditing()`  
  停止编辑过程，目的是使用编辑结果。如果编辑后的值处于可检索的正确状态，则返回 `true`。
- `Object getCellEditorValue()`  
  返回编辑后的结果。
- `void addCellEditorListener(CellEditorListener l)`
- `void removeCellEditorListener(CellEditorListener l)`  
  添加或移除必需的单元格编辑器监听器。

![](img/7dd923a566750151a3aab0dacd0cdaa5_660_0.png)

**图 10.16** 树的术语

### 10.3.1 简单树

在我们的第一个示例程序中，我们将简单地显示一棵带有几个节点的树（参见第 642 页的图 10.18）。与许多其他 Swing 组件一样，你需要提供数据的模型，然后组件会为你显示它。要构造一个 `JTree`，请在构造函数中提供树模型：

```java
TreeNode model = ...;
JTree tree = new JTree(model);
```

> **注意：** 还有一些构造函数可以从元素集合构造树：

```java
JTree(Object[] nodes)
JTree(Vector<?> nodes)
JTree(Hashtable<?, ?> nodes) // the values become the nodes
```

这些构造函数不太有用。它们只是构建一片树的森林，每棵树只有一个节点。第三个构造函数看起来尤其无用，因为节点的顺序由键的哈希码决定，看起来是随机的。

如何获得树模型？你可以通过创建一个实现 `TreeModel` 接口的类来构造自己的模型。本章后面你将看到如何做到这一点。现在，我们只使用 Swing 库提供的 `DefaultTreeModel`。

要构造默认的树模型，你必须提供一个根节点。

```java
TreeNode root = ...;
DefaultTreeModel model = new DefaultTreeModel(root);
```

`TreeModel` 是另一个接口。用任何实现该接口的类的对象来填充默认的树模型。现在，我们使用 Swing 提供的具体节点类——即 `DefaultMutableTreeNode`。这个类实现了 `MutableTreeNode` 接口，它是 `TreeNode` 的子接口（参见图 10.17）。

![](img/7dd923a566750151a3aab0dacd0cdaa5_661_0.png)

**图 10.17** 树类

一个默认的可变树节点持有一个对象——即 *用户对象*。树会渲染所有节点的用户对象。除非你指定了渲染器，否则树会显示由 `toString` 方法产生的字符串。

在我们的第一个示例中，我们使用字符串作为用户对象。在实际应用中，你通常会使用更有表现力的用户对象来填充树。例如，在显示目录树时，为节点使用 *文件对象* 是合理的。

你可以在构造函数中指定用户对象，也可以稍后用 `setUserObject` 方法设置它。

```java
DefaultMutableTreeNode node = new DefaultMutableTreeNode("Texas");
. . .
node.setUserObject("California");
```

接下来，你需要在节点之间建立父子关系。从根节点开始，使用 `add` 方法添加子节点：

```java
DefaultMutableTreeNode root = new DefaultMutableTreeNode("World");
DefaultMutableTreeNode country = new DefaultMutableTreeNode("USA");
root.add(country);
DefaultMutableTreeNode state = new DefaultMutableTreeNode("California");
country.add(state);
```

图 10.18 展示了这棵树的外观。

![](img/7dd923a566750151a3aab0dacd0cdaa5_662_0.png)

**图 10.18** 一个简单树

以这种方式连接所有节点。然后，用根节点构造一个 `DefaultTreeModel`。最后，用该树模型构造一个 `JTree`。

```java
DefaultTreeModel treeModel = new DefaultTreeModel(root);
JTree tree = new JTree(treeModel);
```

或者，作为一种快捷方式，你可以直接将根节点传给 `JTree` 构造函数。然后树会自动构造一个默认的树模型：

```java
JTree tree = new JTree(root);
```

清单 10.12 包含了完整代码。

### **清单 10.12** `tree/SimpleTreeFrame.java`

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

        DefaultMutableTreeNode root = new DefaultMutableTreeNode("World");
        DefaultMutableTreeNode country = new DefaultMutableTreeNode("USA");
        root.add(country);
        DefaultMutableTreeNode state = new DefaultMutableTreeNode("California");
        country.add(state);
        DefaultMutableTreeNode city = new DefaultMutableTreeNode("San Jose");
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

        JTree tree = new JTree(root);
        add(new JScrollPane(tree));
    }
}
```

运行该程序时，树最初如图 10.19 所示。只有根节点及其子节点可见。点击圆形图标（即 *手柄*）可以展开子树。当子树折叠时，手柄图标伸出的线指向右侧；当子树展开时，该线指向下方（参见图 10.20）。我们不知道 Metal 外观的设计者当时是怎么想的，但我们把这个图标看作一个门把手。向下推手柄即可打开子树。

![](img/7dd923a566750151a3aab0dacd0cdaa5_664_0.png)



**javax.swing.tree.TreePath 1.2**

- `Object getLastPathComponent()`
  获取此路径上的最后一个对象——即该路径所表示的节点对象。

**javax.swing.tree.TreeNode 1.2**

- `TreeNode getParent()`
  返回此节点的父节点。
- `TreeNode getChildAt(int index)`
  查找给定索引处的子节点。索引必须介于 `0` 和 `getChildCount() - 1` 之间。
- `int getChildCount()`
  返回此节点的子节点数量。
- `Enumeration children()`
  返回一个枚举对象，用于遍历此节点的所有子节点。

**javax.swing.tree.DefaultTreeModel 1.2**

- `void insertNodeInto(MutableTreeNode newChild, MutableTreeNode parent, int index)`
  将 `newChild` 作为 `parent` 的新子节点插入到给定索引处，并通知树模型监听器。
- `void removeNodeFromParent(MutableTreeNode node)`
  从此模型中移除 `node`，并通知树模型监听器。
- `void nodeChanged(TreeNode node)`
  通知树模型监听器 `node` 已更改。
- `void nodeChanged(TreeNode parent, int[] changedChildIndexes)`
  通知树模型监听器：`parent` 中具有给定索引的所有子节点都已更改。
- `void reload()`
  将所有节点重新加载到模型中。这是一项剧烈操作，仅当节点因某些外部影响而完全改变时才应使用。

```
    Enumeration breadthFirst = node.breadthFirstEnumeration();
    while (breadthFirst.hasMoreElements())
        do something with breadthFirst.nextElement();
```

最后，还有一个相关方法 `pathFromAncestorEnumeration`，它查找从某个祖先到给定节点的一条路径，并枚举沿该路径的节点。这没什么大不了的——它只是不断调用 `getParent`，直到找到该祖先，然后按相反顺序呈现该路径。

在下一个示例程序中，我们将节点枚举投入使用。该程序显示类的继承树。在框架底部的文本字段中输入类名。该类及其所有超类都会被添加到树中（参见图 10.32）。

![](img/7dd923a566750151a3aab0dacd0cdaa5_680_0.png)

**图 10.32** 继承树

在此示例中，我们利用了树节点的用户对象可以是任意类型对象这一事实。由于我们的节点描述类，因此我们在节点中存储 `Class` 对象。

我们不希望同一个类对象被添加两次，因此需要检查某个类是否已存在于树中。以下方法会在树中查找具有给定用户对象的节点（如果存在）。

```java
public DefaultMutableTreeNode findUserObject(Object obj)
{
   Enumeration e = root.breadthFirstEnumeration();
   while (e.hasMoreElements())
   {
      DefaultMutableTreeNode node = (DefaultMutableTreeNode) e.nextElement();
      if (node.getUserObject().equals(obj))
         return node;
   }
   return null;
}
```

## 10.3.4 渲染节点

在应用程序中，你经常需要改变树组件绘制节点的方式。最常见的变化当然是为节点和叶节点选择不同的图标。其他变化可能包括更改节点标签的字体，或在节点处绘制图像。所有这些变化都可以通过向树中安装新的树单元格渲染器来实现。默认情况下，`JTree` 类使用 `DefaultTreeCellRenderer` 对象绘制每个节点。`DefaultTreeCellRenderer` 类扩展了 `JLabel` 类。标签包含节点图标和节点标签。

> **注意：** 单元格渲染器不会绘制用于展开和折叠子树的“手柄”。这些手柄属于外观风格的一部分，建议不要更改它们。

你可以通过三种方式自定义显示。

- 你可以更改 `DefaultTreeCellRenderer` 所使用的图标、字体和背景色。这些设置会用于树中的所有节点。
- 你可以安装一个扩展 `DefaultTreeCellRenderer` 类的渲染器，并为每个节点设置不同的图标、字体和背景色。
- 你可以安装一个实现 `TreeCellRenderer` 接口的渲染器，为每个节点绘制自定义图像。

让我们逐一查看这些可能性。最简单的自定义方式是构造一个 `DefaultTreeCellRenderer` 对象，更改图标，然后将其安装到树中：

```java
DefaultTreeCellRenderer renderer = new DefaultTreeCellRenderer();
renderer.setLeafIcon(new ImageIcon("blue-ball.gif")); // used for leaf nodes
renderer.setClosedIcon(new ImageIcon("red-ball.gif")); // used for collapsed nodes
renderer.setOpenIcon(new ImageIcon("yellow-ball.gif")); // used for expanded nodes
tree.setCellRenderer(renderer);
```

你可以在图 10.32 中看到效果。我们只是使用“球”图标作为占位符——想必你的用户界面设计师会为你提供适合应用程序使用的图标。

我们不建议你更改整棵树的字体或背景色——那实际上是外观风格的职责。

不过，更改树中某些节点的字体以突出显示它们可能很有用。如果仔细观察图 10.32，你会注意到*抽象*类以斜体显示。

要更改单个节点的外观，请安装树单元格渲染器。树单元格渲染器与本章前面讨论的列表单元格渲染器非常相似。`TreeCellRenderer` 接口只有一个方法：

```java
Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected,
                                      boolean expanded, boolean leaf, int row, boolean hasFocus)
```

`DefaultTreeCellRenderer` 类的 `getTreeCellRendererComponent` 方法返回 `this`——换句话说，返回一个标签。（`DefaultTreeCellRenderer` 类扩展了 `JLabel` 类。）要自定义组件，请扩展 `DefaultTreeCellRenderer` 类。按如下方式重写 `getTreeCellRendererComponent` 方法：调用超类方法，以便它准备标签数据、自定义标签属性，最后返回 `this`。

```java
class MyTreeCellRenderer extends DefaultTreeCellRenderer
{
   public Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected,
                                                 boolean expanded, boolean leaf, int row, boolean hasFocus)
   {
      Component comp = super.getTreeCellRendererComponent(tree, value, selected,
                                                          expanded, leaf, row, hasFocus);
      DefaultMutableTreeNode node = (DefaultMutableTreeNode) value;
      look at node.getUserObject();
      Font font = appropriate font;
      comp.setFont(font);
      return comp;
   }
}
```

**警告：** `getTreeCellRendererComponent` 方法的 `value` 参数是*节点*对象，而不是*用户对象*！回想一下，用户对象是 `DefaultMutableTreeNode` 的一个特性，并且 `JTree` 可以包含任意类型的节点。如果你的树使用 `DefaultMutableTreeNode` 节点，则必须像前面的代码示例那样，在第二步中获取用户对象。

**警告：** `DefaultTreeCellRenderer` 为所有节点使用*同一个*标签对象，只是为每个节点更改标签文本。如果为某个特定节点更改了字体，那么当方法再次被调用时，必须将其恢复为默认值。否则，所有后续节点都将以更改后的字体绘制！查看代码清单 10.14 中的代码，了解如何将字体恢复为默认值。

我们不展示绘制任意图形的树单元格渲染器示例。如果需要此能力，你可以改编代码清单 10.4 中的列表单元格渲染器；该技术完全类似。

代码清单 10.14 中的 `ClassNameTreeCellRenderer` 根据 `Class` 对象的 `ABSTRACT` 修饰符，以正常字体或斜体字体设置类名。我们不想设置某个特定字体，因为不想改变外观风格通常用于标签的字体。因此，我们使用来自 `label` 的字体，并从中派生出一个斜体字体。回想一下，所有调用只返回一个共享的 `JLabel` 对象。我们需要保留原始字体，并在下一次调用 `getTreeCellRendererComponent` 方法时恢复它。

另外，请注意我们如何在 `ClassTreeFrame` 构造函数中更改节点图标。

| **javax.swing.tree.DefaultMutableTreeNode 1.2** | |
|---|---|
| - `Enumeration breadthFirstEnumeration()`<br>- `Enumeration depthFirstEnumeration()`<br>- `Enumeration preOrderEnumeration()`<br>- `Enumeration postOrderEnumeration()` | 返回用于按特定顺序访问树模型所有节点的枚举对象。在广度优先遍历中，更靠近根的节点会先于较远的节点被访问。在深度优先遍历中，一个节点的所有子节点会在访问其兄弟节点之前被完整枚举。`postOrderEnumeration` 方法是 `depthFirstEnumeration` 的同义词。先序遍历与后序遍历相同，只是父节点会在其子节点之前被枚举。 |

| **javax.swing.tree.TreeCellRenderer 1.2** | |
|---|---|
| **方法** | `Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected, boolean expanded, boolean leaf, int row, boolean hasFocus)` |
| | 返回一个组件，其绘制方法会被调用以渲染树单元格。 |
| **参数：** | |
| `tree` | 包含要渲染节点的树 |
| `value` | 要渲染的节点 |
| `selected` | 如果节点当前被选中，则为 `true` |
| `expanded` | 如果节点的子节点可见，则为 `true` |
| `leaf` | 如果节点需要显示为叶节点，则为 `true` |
| `row` | 包含该节点的显示行 |
| `hasFocus` | 如果节点当前拥有输入焦点，则为 `true` |


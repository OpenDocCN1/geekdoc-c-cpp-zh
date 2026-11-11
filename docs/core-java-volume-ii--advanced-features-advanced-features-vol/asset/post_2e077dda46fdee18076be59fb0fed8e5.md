
![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_681_0.png)

**Figure 11.10** A tree with no connecting lines

Conversely, to make sure that the lines are shown, use

```java
tree.putClientProperty("JTree.lineStyle", "Angled");
```

Another line style, "Horizontal", is shown in Figure 11.19. The tree is displayed with horizontal lines separating only the children of the root. We aren't quite sure what it is good for.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_681_1.png)

**Figure 11.19** A tree with the horizontal line style

By default, there is no handle for collapsing the root of the tree. If you like, you can add one with the call

```java
tree.setShowsRootHandles(true);
```

Figure 11.20 shows the result. Now you can collapse the entire tree into the root node.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_682_0.png)

**Figure 11.20** A tree with a root handle

Conversely, you can hide the root altogether. You will thus display a *forest*—a set of trees, each with its own root. You still must join all trees in the forest to a common root; then, hide the root with the instruction

```java
tree.setRootVisible(false);
```

Look at Figure 11.21. There appear to be two roots, labeled “USA” and “Germany.” The actual root that joins the two is made invisible.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_682_1.png)

**Figure 11.21** A forest

Let’s turn from the root to the leaves of the tree. Note that the leaves have an icon different from the other nodes (see Figure 11.22).

## 한순간의 선택

우리는 살아가면서 수많은 선택의 순간을 마주한다. 어떤 선택은 크고 중요한 것이며, 어떤 선택은 사소하고 가벼운 것이다. 그러나 모든 선택은 우리의 삶을 조금씩 변화시킨다.

한순간의 선택이 때로는 인생의 방향을 바꾸기도 한다. 우리가 내린 결정은 과거로 되돌릴 수 없기에 더욱 신중해야 한다. 그러나 너무 두려워할 필요는 없다. 완벽한 선택은 없기 때문이다.

중요한 것은 선택 그 자체보다도, 선택 후에 어떻게 행동하느냐이다. 최선의 선택을 했다면 그 결과에 책임을 지고, 만약 결과가 좋지 않다면 그것을 교훈삼아 더 나은 방향으로 나아가면 된다.

> 모든 선택에는 의미가 있고, 모든 순간에는 가치가 있다.

삶은 선택의 연속이다. 우리는 그 선택들을 통해 성장하고, 배우며, 더 나은 자신을 만들어간다. 오늘의 작은 선택이 내일의 큰 변화를 만든다는 것을 잊지 말아야 한다.

**javax.swing.tree.TreeModel** *1.2*

- `boolean isLeaf(Object node)`
  returns true if node should be displayed as a leaf node.

**javax.swing.tree.DefaultTreeModel** *1.2*

- `void setAsksAllowsChildren(boolean b)`
  if b is true, nodes are displayed as leaves when their `getAllowsChildren` method returns false. Otherwise, they are displayed as leaves when their `isLeaf` method returns true.

**javax.swing.tree.DefaultMutableTreeNode** *1.2*

- `DefaultMutableTreeNode(Object userObject)`
  constructs a mutable tree node with the given user object.
- `void add(MutableTreeNode child)`
  adds one as the last child of this node.
- `void setAllowsChildren(boolean b)`
  if b is true, children can be added to this node.

**javax.swing.JComponent** *1.2*

- `void putClientProperty(Object key, Object value)`
  adds a key/value pair to a small table that each component manages. This is an “escape hatch” mechanism that some Swing components use for storing properties specific to a look-and-feel.

### 11.2.1 Editing Trees and Tree Paths

In the next example program, you will see how to edit a tree. Figure 11.23 shows the user interface. If you click the Add Sibling or Add Child button, the program adds a new node (with title New) to the tree. If you click the Delete button, the program deletes the currently selected node.

To implement this behavior, you need to find out which tree node is currently selected. The JTree class has a surprising way of identifying nodes in a tree. It does not deal with tree nodes but with *paths of objects*, called tree paths. A

The automatic notification is a major advantage of using the `DefaultTreeModel`. If you supply your own tree model, you have to implement automatic notification by hand. (See *Core Swing* by Kim Topley for details.)

> **CAUTION:** The `DefaultTreeModel` class has a reload method that reloads the entire model. However, don’t call reload simply to update the tree after making a few changes. When the tree is regenerated, all nodes beyond the root’s children are collapsed again. It will be quite disconcerting to your users if they have to keep expanding the tree after every change.

When the view is notified of a change in the node structure, it updates the display but does not automatically expand a node to show newly added children. In particular, if a user in our sample program adds a new child node to a node for which children are currently collapsed, the new node is silently added to the collapsed subtree. This gives the user no feedback that the command was actually carried out. In such a case, you should make a special effort to expand all parent nodes so that the newly added node becomes visible. Use the `makeVisible` method of the `JTree` class for this purpose. The `makeVisible` method expects a tree path leading to the node that should become visible.

Thus, you need to construct a tree path from the root to the newly inserted node. To get a tree path, first call the `getPathToRoot` method of the `DefaultTreeModel` class. It returns a `TreeNode[]` array of all nodes from a node to the root node. Pass that array to a `TreePath` constructor.

For example, here is how you make the new node visible:

```java
TreeNode[] nodes = model.getPathToRoot(newNode);
var path = new TreePath(nodes);
tree.makeVisible(path);
```

> **NOTE:** It is curious that the `DefaultTreeModel` class feigns almost complete ignorance of the `TreePath` class, even though its job is to communicate with a `JTree`. The `JTree` class uses tree paths a lot, and it never uses arrays of node objects.

Now, suppose your tree is contained inside a scroll pane. After the tree node expansion, the new node might still not be visible because it falls outside the viewport. To overcome that problem, call

```java
tree.scrollPathToVisible(path);
```

instead of calling `makeVisible`. This call expands all nodes along the path and tells the ambient scroll pane to scroll the node at the end of the path into view (see Figure 11.25).

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_689_0.png)

**Figure 11.25** The scroll pane scrolls to display a new node.

By default, tree nodes cannot be edited. However, if you call

```java
tree.setEditable(true);
```

the user can edit a node simply by double-clicking, editing the string, and pressing the Enter key. Double-clicking invokes the *default cell editor*, which is implemented by the `DefaultCellEditor` class (see Figure 11.26). It is possible to install other cell editors, using the same process that you have seen in our discussion of table cell editors.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_689_1.png)

**Figure 11.26** The default cell editor

Listing 11.9 shows the complete source code of the tree editing program. Run the program, add a few nodes, and edit them by double-clicking. Observe how collapsed nodes expand to show added children and how the scroll pane keeps added nodes in the viewport.

### Listing 11.9 treeEdit/TreeEditFrame.java

```java
package treeEdit;

import java.awt.*;
import javax.swing.*;
import javax.swing.tree.*;

/**
 * A frame with a tree and buttons to edit the tree.
 */
public class TreeEditFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 400;
   private static final int DEFAULT_HEIGHT = 200;

   private DefaultTreeModel model;
   private JTree tree;

   public TreeEditFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      // construct tree

      TreeNode root = makeSampleTree();
      model = new DefaultTreeModel(root);
      tree = new JTree(model);
      tree.setEditable(true);

      // add scroll pane with tree

      var scrollPane = new JScrollPane(tree);
      add(scrollPane, BorderLayout.CENTER);

      makeButtons();
   }

   public TreeNode makeSampleTree()
   {
      var root = new DefaultMutableTreeNode("World");
      var country = new DefaultMutableTreeNode("USA");
      root.add(country);
      var state = new DefaultMutableTreeNode("California");
```

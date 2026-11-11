Listing 11.9 shows the complete source code of the tree editing program. Run the program, add a few nodes, and edit them by double-clicking. Observe how collapsed nodes expand to show added children and how the scroll pane keeps added nodes in the viewport.

# Listing 11.9  treeEdit/TreeEditFrame.java

```
~~~java
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
~~~
```
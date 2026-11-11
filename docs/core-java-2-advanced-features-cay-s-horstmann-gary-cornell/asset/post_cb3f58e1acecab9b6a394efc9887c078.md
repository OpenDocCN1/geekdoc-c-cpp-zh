
- `javax.swing.tree.DefaultTreeCellRenderer` 1.2
  - `void setLeafIcon(Icon icon)`
  - `void setOpenIcon(Icon icon)`
  - `void setClosedIcon(Icon icon)`

sets the icon to show for a leaf node, an expanded node, and a collapsed node.

## 10.3.5 Listening to Tree Events

Most commonly, a tree component is paired with some other component. When the user selects tree nodes, some information shows up in another window. See Figure 10.33 for an example. When the user selects a class, the instance and static variables of that class are displayed in the text area to the right.

![](img/7dd923a566750151a3aab0dacd0cdaa5_684_0.png)

**Figure 10.33** A class browser

To obtain this behavior, you need to install a *tree selection listener*. The listener must implement the `TreeSelectionListener` interface—an interface with a single method:

```
void valueChanged(TreeSelectionEvent event)
```

That method is called whenever the user selects or deselects tree nodes.

Add the listener to the tree in the normal way:

```
tree.addTreeSelectionListener(listener);
```

You can specify whether the user is allowed to select a single node, a contiguous range of nodes, or an arbitrary, potentially discontinuous, set of nodes. The `JTree` class uses a `TreeSelectionModel` to manage node selection. You need to retrieve the model to set the selection state to one of `SINGLE_TREE_SELECTION`, `CONTIGUOUS_TREE_SELECTION`, or `DISCONTIGUOUS_TREE_SELECTION`. (Discontiguous selection mode is the default.) For example, in our class browser, we want to allow selection of only a single class:

```
int mode = TreeSelectionModel.SINGLE_TREE_SELECTION;
tree.getSelectionModel().setSelectionMode(mode);
```

Apart from setting the selection mode, you need not worry about the tree selection model.

> **NOTE:** How the user selects multiple items depends on the look-and-feel. In the Metal look-and-feel, hold down the Ctrl key while clicking an item to add it to the selection, or to remove it if it is currently selected. Hold down the Shift key while clicking an item to select a range of items, extending from the previously selected item to the new item.

To find out the current selection, query the tree with the `getSelectionPaths` method:

```
TreePath[] selectedPaths = tree.getSelectionPaths();
```

If you restricted the user to single-item selection, you can use the convenience method `getSelectionPath` which returns the first selected path or null if no path was selected.

> **CAUTION:** The `TreeSelectionEvent` class has a `getPaths` method that returns an array of `TreePath` objects, but that array describes selection changes, not the current selection.

Listing 10.14 shows the frame class for the class tree program. The program displays inheritance hierarchies and customizes the display to show abstract classes in italics. (See Listing 10.15 for the cell renderer.) You can type the name of any class into the text field at the bottom of the frame. Press the Enter key or click the Add button to add the class and its superclasses to the tree. You must enter the full package name, such as `java.util.ArrayList`.

This program is a bit tricky because it uses reflection to construct the class tree. This work is done inside the `addClass` method. (The details are not that important; we use the class tree in this example because inheritance provides a nice supply of trees without laborious coding. When you display trees in your applications, you will have your own source of hierarchical data.) The method uses the breadth-first search algorithm to find whether the current class is already in the tree by calling the `findUserObject` method that we implemented in the preceding section. If the class is not already in the tree, we add the superclasses to the tree, then make the new class node a child and make that node visible.

When you select a tree node, the text area to the right is filled with the fields of the selected class. In the frame constructor, we restrict the user to single-item selection and add a tree selection listener. When the `valueChanged` method is called, we ignore its event parameter and simply ask the tree for the current selection path. As always, we need to get the last node of the path and look up its user object. We then call the `getFieldDescription` method which uses reflection to assemble a string with all fields of the selected class.

### Listing 10.14 `treeRender/ClassTreeFrame.java`

```java
package treeRender;

import java.awt.*;
import java.awt.event.*;
import java.lang.reflect.*;
import java.util.*;

import javax.swing.*;
import javax.swing.tree.*;

/**
 * This frame displays the class tree, a text field, and an "Add" button to add more classes
 * into the tree.
 */
public class ClassTreeFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 400;
   private static final int DEFAULT_HEIGHT = 300;

   private DefaultMutableTreeNode root;
   private DefaultTreeModel model;
   private JTree tree;
   private JTextField textField;
   private JTextArea textArea;

   public ClassTreeFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      // the root of the class tree is Object
      root = new DefaultMutableTreeNode(java.lang.Object.class);
      model = new DefaultTreeModel(root);
      tree = new JTree(model);

      // add this class to populate the tree with some data
      addClass(getClass());

      // set up node icons
      ClassNameTreeCellRenderer renderer = new ClassNameTreeCellRenderer();
      renderer.setClosedIcon(new ImageIcon(getClass().getResource("red-ball.gif")));
      renderer.setOpenIcon(new ImageIcon(getClass().getResource("yellow-ball.gif")));
      renderer.setLeafIcon(new ImageIcon(getClass().getResource("blue-ball.gif")));
      tree.setCellRenderer(renderer);

      // set up selection mode
      tree.addTreeSelectionListener(event ->
      {
          // the user selected a different node--update description
          TreePath path = tree.getSelectionPath();
          if (path == null) return;
          DefaultMutableTreeNode selectedNode = (DefaultMutableTreeNode) path
              .getLastPathComponent();
          Class<?> c = (Class<?>) selectedNode.getUserObject();
          String description = getFieldDescription(c);
          textArea.setText(description);
      });
      int mode = TreeSelectionModel.SINGLE_TREE_SELECTION;
      tree.getSelectionModel().setSelectionMode(mode);

      // this text area holds the class description
      textArea = new JTextArea();

      // add tree and text area
      JPanel panel = new JPanel();
      panel.setLayout(new GridLayout(1, 2));
      panel.add(new JScrollPane(tree));
      panel.add(new JScrollPane(textArea));

      add(panel, BorderLayout.CENTER);

      addTextField();
   }

   /**
    * Add the text field and "Add" button to add a new class.
    */
   public void addTextField()
   {
       JPanel panel = new JPanel();

       ActionListener addListener = event ->

public DefaultMutableTreeNode addClass(Class<?> c)
{
    // add a new class to the tree

    // skip non-class types
    if (c.isInterface() || c.isPrimitive()) return null;

    // if the class is already in the tree, return its node
    DefaultMutableTreeNode node = findUserObject(c);
    if (node != null) return node;

    // class isn't present--first add class parent recursively

    Class<?> s = c.getSuperclass();

    DefaultMutableTreeNode parent;
    if (s == null) parent = root;
    else parent = addClass(s);

    // add the class as a child to the parent
    DefaultMutableTreeNode newNode = new DefaultMutableTreeNode(c);
    model.insertNodeInto(newNode, parent, parent.getChildCount());

    // make node visible
    TreePath path = new TreePath(model.getPathToRoot(newNode));
    tree.makeVisible(path);

    return newNode;
}

/**
 * Returns a description of the fields of a class.
 * @param c the class to be described
 * @return a string containing all field types and names
 */
public static String getFieldDescription(Class<?> c)
{
    // use reflection to find types and names of fields
    StringBuilder r = new StringBuilder();
    Field[] fields = c.getDeclaredFields();
    for (int i = 0; i < fields.length; i++)
    {
        Field f = fields[i];
        if ((f.getModifiers() & Modifier.STATIC) != 0) r.append("static ");
        r.append(f.getType().getName());
        r.append(" ");
        r.append(f.getName());
        r.append("\n");
```

_(Continues)_

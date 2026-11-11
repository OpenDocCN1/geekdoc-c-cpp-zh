
To change the appearance of individual nodes, install a tree cell renderer. Tree cell renderers are very similar to the list cell renderers we discussed earlier in this chapter. The TreeCellRenderer interface has a single method:

```java
Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected,
    boolean expanded, boolean leaf, int row, boolean hasFocus)
```

The getTreeCellRendererComponent method of the DefaultTreeCellRenderer class returns this—in other words, a label. (The DefaultTreeCellRenderer class extends the JLabel class.) To customize the component, extend the DefaultTreeCellRenderer class. Override the getTreeCellRendererComponent method as follows: Call the superclass method so it can prepare the label data, customize the label properties, and finally return this.

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

> **CAUTION:** The value parameter of the getTreeCellRendererComponent method is the node object, not the user object! Recall that the user object is a feature of the DefaultMutableTreeNode, and that a JTree can contain nodes of an arbitrary type. If your tree uses DefaultMutableTreeNode nodes, you must retrieve the user object in a second step, as we did in the preceding code sample.

> **CAUTION:** The DefaultTreeCellRenderer uses the *same* label object for all nodes, only changing the label text for each node. If you change the font for a particular node, you must set it back to its default value when the method is called again. Otherwise, all subsequent nodes will be drawn in the changed font! Look at the code in Listing 11.10 to see how to restore the font to the default.

The ClassNameTreeCellRenderer in Listing 11.10 sets the class name in either the normal or italic font, depending on the ABSTRACT modifier of the Class object. We don’t want to set a particular font because we don’t want to change whatever font the look-and-feel normally uses for labels. For that reason, we use the font from the label and *derive* an italic font from it. Recall that only a single shared `JLabel` object is returned by all calls. We need to hang on to the original font and restore it in the next call to the `getTreeCellRendererComponent` method.

Also, note how we change the node icons in the `ClassTreeFrame` constructor.

## `javax.swing.tree.DefaultMutableTreeNode` 1.2

- `Enumeration breadthFirstEnumeration()`
- `Enumeration depthFirstEnumeration()`
- `Enumeration preOrderEnumeration()`
- `Enumeration postOrderEnumeration()`

returns enumeration objects for visiting all nodes of the tree model in a particular order. In breadth-first traversal, children that are closer to the root are visited before those that are farther away. In depth-first traversal, all children of a node are completely enumerated before its siblings are visited. The postOrderEnumeration method is a synonym for depthFirstEnumeration. The preorder traversal is identical to the postorder traversal except that parents are enumerated before their children.

## `javax.swing.tree.TreeCellRenderer` 1.2

- `Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected, boolean expanded, boolean leaf, int row, boolean hasFocus)`

returns a component whose paint method is invoked to render a tree cell.

**Parameters:**

| Parameter | Description |
| --- | --- |
| tree | The tree containing the node to be rendered |
| value | The node to be rendered |
| selected | true if the node is currently selected |
| expanded | true if the children of the node are visible |
| leaf | true if the node needs to be displayed as a leaf |
| row | The display row containing the node |
| hasFocus | true if the node currently has input focus |

## `javax.swing.tree.DefaultTreeCellRenderer` 1.2

- `void setLeafIcon(Icon icon)`
- `void setOpenIcon(Icon icon)`
- `void setClosedIcon(Icon icon)`

sets the icon to show for a leaf node, an expanded node, and a collapsed node.

### 11.2.4 Listening to Tree Events

Most commonly, a tree component is paired with some other component. When the user selects tree nodes, some information shows up in another window. See Figure 11.29 for an example. When the user selects a class, the instance and static variables of that class are displayed in the text area to the right.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_699_0.png)

**Figure 11.29** A class browser

To obtain this behavior, you need to install a *tree selection listener*. The listener must implement the `TreeSelectionListener` interface—an interface with a single method:

```java
void valueChanged(TreeSelectionEvent event)
```

That method is called whenever the user selects or deselects tree nodes.

Add the listener to the tree in the normal way:

```java
tree.addTreeSelectionListener(listener);
```

You can specify whether the user is allowed to select a single node, a contiguous range of nodes, or an arbitrary, potentially discontiguous, set of nodes. The `JTree` class uses a `TreeSelectionModel` to manage node selection. You need to retrieve the model to set the selection state to one of `SINGLE_TREE_SELECTION`, `CONTIGUOUS_TREE_SELECTION`, or `DISCONTIGUOUS_TREE_SELECTION`. (Discontiguous selection mode is the default.) For example, in our class browser, we want to allow selection of only a single class:

When you select a tree node, the text area to the right is filled with the fields of the selected class. In the frame constructor, we restrict the user to single-item selection and add a tree selection listener. When the valueChanged method is called, we ignore its event parameter and simply ask the tree for the current selection path. As always, we need to get the last node of the path and look up its user object. We then call the getFieldDescription method which uses reflection to assemble a string with all fields of the selected class.

## Listing 11.10 `treeRender/ClassTreeFrame.java`

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
    }
}
```

(Continues)

## Listing 11.10 (Continued)

```java
38  // set up node icons
39  var renderer = new ClassNameTreeCellRenderer();
40  renderer.setClosedIcon(new ImageIcon(getClass().getResource("red-ball.gif")));
41  renderer.setOpenIcon(new ImageIcon(getClass().getResource("yellow-ball.gif")));
42  renderer.setLeafIcon(new ImageIcon(getClass().getResource("blue-ball.gif")));
43  tree.setCellRenderer(renderer);
44
45  // set up selection mode
46  tree.addTreeSelectionListener(event ->
47  {
48      // the user selected a different node--update description
49      TreePath path = tree.getSelectionPath();
50      if (path == null) return;
51      var selectedNode = (DefaultMutableTreeNode) path.getLastPathComponent();
52      Class<?> c = (Class<?>) selectedNode.getUserObject();
53      String description = getFieldDescription(c);
54      textArea.setText(description);
55  });
56  int mode = TreeSelectionModel.SINGLE_TREE_SELECTION;
57  tree.getSelectionModel().setSelectionMode(mode);
58
59  // this text area holds the class description
60  textArea = new JTextArea();
61
62  // add tree and text area
63  var panel = new JPanel();
64  panel.setLayout(new GridLayout(1, 2));
65  panel.add(new JScrollPane(tree));
66  panel.add(new JScrollPane(textArea));
67
68  add(panel, BorderLayout.CENTER);
69
70  addTextField();
71  }
72
73  /**
74   * Add the text field and "Add" button to add a new class.
75   */
76  public void addTextField()
77  {
78      var panel = new JPanel();
79
80      ActionListener addListener = event ->
81      {
82          // add the class whose name is in the text field
83          try
84          {
```

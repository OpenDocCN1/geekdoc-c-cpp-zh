How do you obtain a tree model? You can construct your own model by creating a class that implements the TreeModel interface. You will see later in this chapter how to do that. For now, we will stick with the DefaultTreeModel that the Swing library supplies.

To construct a default tree model, you must supply a root node.

```
    TreeModel root = ...;
    DefaultTreeModel model = new DefaultTreeModel(root);
```

TreeModel is another interface. Populate the default tree model with objects of any class that implements the interface. For now, we will use the concrete node class that Swing supplies—namely, DefaultMutableTreeNode. This class implements the MutableTreeNode interface, a subinterface of TreeNode (see Figure 10.17).

![](bbox=[0.186, 0.362, 0.714, 0.777])

Figure 10.17 Tree classes
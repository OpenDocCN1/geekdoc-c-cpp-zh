# Listing 10.13 (Continued)

```
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
```
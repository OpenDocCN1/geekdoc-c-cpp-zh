# THE TREEVIEW

The TreeView, which displays hierarchical data, is the only common control that descends directly from ItemsControl. (Most descend by way of the Selector class.) Like many of the items controls, the TreeView re-defines the Items collection to be a collection of a specific type, in this case TreeViewItem, which is itself an items control, by way of HeaderedItemsControl.

![](bbox=[0.1, 0.28, 0.9, 0.75])

The TreeViewItem is itself an items control, which allows it to contain a collection of children.
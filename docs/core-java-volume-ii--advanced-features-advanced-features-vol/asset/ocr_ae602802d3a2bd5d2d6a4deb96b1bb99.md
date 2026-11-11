instead of calling `makeVisible`. This call expands all nodes along the path and tells the ambient scroll pane to scroll the node at the end of the path into view (see Figure 11.25).

![](bbox=[0.2, 0.215, 0.71, 0.415])

Figure 11.25 The scroll pane scrolls to display a new node.

By default, tree nodes cannot be edited. However, if you call

```
```
tree.setEditable(true);
```
```

the user can edit a node simply by double-clicking, editing the string, and pressing the Enter key. Double-clicking invokes the *default cell editor*, which is implemented by the `DefaultCellEditor` class (see Figure 11.26). It is possible to install other cell editors, using the same process that you have seen in our discussion of table cell editors.

![](bbox=[0.2, 0.596, 0.71, 0.796])

Figure 11.26 The default cell editor
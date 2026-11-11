![](bbox=[0.286, 0.141, 0.801, 0.339])

**Figure 10.29** The scroll pane scrolls to display a new node.

By default, tree nodes cannot be edited. However, if you call

```
tree.setEditable(true);
```

the user can edit a node simply by double-clicking, editing the string, and pressing the Enter key. Double-clicking invokes the *default cell editor*, which is implemented by the `DefaultCellEditor` class (see Figure 10.30). It is possible to install other cell editors, using the same process that you have seen in our discussion of table cell editors.

![](bbox=[0.286, 0.564, 0.801, 0.763])

**Figure 10.30** The default cell editor

Listing 10.13 shows the complete source code of the tree editing program. Run the program, add a few nodes, and edit them by double-clicking them. Observe how collapsed nodes expand to show added children and how the scroll pane keeps added nodes in the viewport.
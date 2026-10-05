# 64 Chapter 3 Linked Lists

top_sentinel

![](bbox=[0.137, 0.118, 0.693, 0.233])

Algorithms for manipulating doubly linked lists are similar to those that work with singly linked lists, except they must do some extra work to manage the second set of links. For example, the following pseudocode an algorithm for inserting a cell at a given cell:

```
InsertCell(Cell: after_me, Cell: new_cell)
// Update Next links.
new_cell.Next = after_me.Next
after_me.Next = new_cell
// Update Prev links.
new_cell.Next.Prev = new_cell
new_cell.Prev = after_me
End InsertCell
```

The only really tricky part of these algorithms is keeping track of which links have been updated at any point in time. For example, in the preceding algorithm, the second-to-last statement sets the Prev link that should point to the new cell. You might be tempted to do this by using the following statement:

after_me.Next.Prev = new_cell

However, when this statement executes, after_me.Next has already been updated to point to the new cell, so this won't work. The algorithm needs to use new_cell.Next instead.

Figure 3-7 shows the algorithm graphically.
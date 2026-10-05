# Chapter 3 = Linked Lists

This algorithm sets the new cell's Next pointer so that it points to the first cell in the list after the sentinel. It then sets the sentinel's Next pointer to point to the new cell. It places the new cell after the sentinel so that it becomes the first cell in the linked list.

Figure 3-2 shows a linked list before and after a new cell is added at the top of the list. The list's sentinel is shaded.

![](bbox=[0.137, 0.223, 0.599, 0.443])

**Figure 3-2**: To add an item at the top of a linked list, make the new cell's link point to the old top of the list, and make the sentinel's link point to the new cell.

This algorithm performs only two steps, its run time is O(1) no matter how many cells the list contains.

# Adding Cells at the End

Adding a cell at the end of the list is a bit more difficult than adding it at the beginning, because the algorithm must first traverse the list to find the last cell. The following pseudocode shows an algorithm for adding a new cell at the end of a list:

```
AddAtEnd(Cell: top, Cell: new_cell)
  // Find the last cell.
  While (top.Next != null)
    top = top.Next
  End While

  // Add the new cell at the end.
  top.Next = new_cell
  new_cell.Next = null
End AddAtEnd
```
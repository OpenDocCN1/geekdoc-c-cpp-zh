# 500 Appendix B Solutions to Exercises

```
top = top.Next
End While

// Update Next links.
new_cell.Next = top.Next
top.Next = new_cell
```

```
// Update Prev links.
new_cell.Next.Prev = new_cell
new_cell.Prev = top
End InsertCell
```

This algorithm is similar to the one used for a singly linked list except for the two lines that update the Prev links.

+   9. The following pseudocode determines whether a list is sorted:
Boolean: IsSorted(Cell: sentinel)
// If the list has 0 or 1 items, it's sorted.
If (sentinel.Next == null) Then Return true
If (sentinel.Next.Next == null) Then Return true

// Compare the other items.
sentinel = sentinel.Next;
While (sentinel.Next != null)
// Compare this item with the next one.
If (sentinel.Value > sentinel.Next.Value) Then Return false

// Move to the next item.
sentinel = sentinel.Next
End While

// If we get here, the list is sorted.
Return true
End IsSorted

+   10. Insertion takes the first item from the input list and then finds the place in the growing sorted list where it belongs. Depending on its value, sometimes the item will belong near the beginning of the list, and sometimes it will belong near the end. The algorithm will always search the whole list, unless the new item is larger than all the items already on the sorted list.
In contrast, selection searches the unsorted input list to find the largest, it must search the whole list. Unlike insertion, it can never stop the search early.

+   11. The PlanetList example program, which is available for download on the book's website, shows one solution.

+   12. The BreakLoopTortoiseAndHare program, which is available for download on the book's website, shows a C# solution.
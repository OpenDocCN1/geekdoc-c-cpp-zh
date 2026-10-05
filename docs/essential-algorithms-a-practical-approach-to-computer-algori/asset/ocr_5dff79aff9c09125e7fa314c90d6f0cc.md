# Chapter 3 ■ Linked Lists 73

```
Boolean: Has_loopMarking(Cell: sentinel)
// Assume there is no loop.
Boolean: has_loop = false

// Loop through the list.
cell = sentinel
While (cell.Next != null)
// See if we already visited the next cell.
If (cell.Next.Visited)
// This is the start of a loop.
// Break the loop.
cell.Next = null
has_loop = true
<Break out of the While loop>
End If

// Move to the next cell.
cell = cell.Next

// Mark the cell as visited.
cell.Visited = true
End While

// Traverse the list again to clear the Visited flags.
cell = sentinel
While (cell.Next != null)
cell.Visited = false
cell = cell.Next
End While

// Return the result.
Return has_loop
End HasLoopMarking
```

The BreakLoopMarking sample program, which is available for download on the book's website, demonstrates this algorithm.
This algorithm must traverse the list twice—once to set the cells' Visited flags to true, and again to reset them to false. If the list contains N cells, this algorithm takes 2 × N steps and runs in O(N) time.
This also requires that each cell have an added Visited field, so it requires O(N) space. The list already takes O(N) space to hold the cells and links so this shouldn't be a problem but it's worth acknowledging that the algorithm has some memory requirements.

> NOTE Marking cells is a simple technique that is also useful for other data structures, particularly networks. Some of the algorithms described in Chapters 13 and 14 use marking techniques.
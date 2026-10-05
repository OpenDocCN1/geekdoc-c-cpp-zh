# Chapter 3 = Linked Lists

The algorithm enters a While loop that executes as long as top is null. Inside the loop, the algorithm compares the top cell's value to the target value. If the values matches, the algorithm returns top. If the values do not match, the algorithm moves top to point to the next cell in the list.

If top runs all the way through the list, the target value is not in the list, so the algorithm returns null. (Alternatively, the algorithm could throw an exception or raise some kind of error, depending on your programming language.)

As you'll see in some of the following sections, it's easiest to work with a linked list if you have a pointer to the cell before that cell. The following algorithm finds the cell that contains a target cell:

```
Cell FindBefore(Cell: top, Value: target)
  // If the list is empty, the target value isn't present.
  If (top == null) Return null

  // Search for the target value.
  While (top.Next != null)
    If (top.Next == target) Then Return top
    top = top.Next
  End

  // If we get this far, the target is not in the list.
  Return null
FindCellBefore
```

This code is similar to the previous version—with two exceptions. It must first check that top is not null before it starts so it can look at top.Next safely. If top is null, top.Next is undefined, and a program that implemented the algorithm would crash.

If top is not null, the algorithm enters a While loop as before, but this time it looks at top.Next.Value instead of top.Value. When it finds it, top points to the cell before the one that holds the target value, and the algorithm returns top.

# Sentinels

If you study the preceding algorithm closely, you may find one where it fails. If the linked list contains the target value, there is no cell before that one, so the algorithm cannot return it. The first value that the algorithm examines is in list's second cell, and it never looks back.

One way to handle this situation is to add special-purpose code that explicitly looks for the target value in the first cell and then handles that case specially. The program would probably need to handle this situation as a special case, and it could get messy.

Another approach is to create a sentinel at the beginning of the list. A sentinel is a cell that is part of the linked list but doesn't contain any meaningful
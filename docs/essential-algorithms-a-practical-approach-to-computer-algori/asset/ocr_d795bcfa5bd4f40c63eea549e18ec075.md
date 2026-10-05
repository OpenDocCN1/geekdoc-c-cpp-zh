# Chapter 9 Recursion

```
DrawRelative(gr, dy, dx)
section = section + 1
If (depth > 0) Then
    sections.Push(section)
    depths.Push(depth)
    dxs.Push(dx)
    dys.Push(dy)
    // Hilbert - 1, gr, dx, dy
    depth = depth - 1
    section = 1
End If
Else If (section == 4) Then
    DrawRelative(gr, -dx, -dy)
    section = section + 1
    If (depth > 0) Then
        sections.Push(section)
        depths.Push(depth)
        dxs.Push(dx)
        dys.Push(dy)
        // Hilbert - 1, gr, -dy, -dx
        depth = depth - 1
        float temp = dx
        dx = -dy
        dy = -temp
        section = 1
    End If
Else If (section == 5) Then
    // Return from a recursion.
    // If there's nothing to pop, we're at the top.
    If (sections.Count == 0) Then section = -1
    Else
        // Pop the previous parameters.
        section = sections.Pop()
        depth = depths.Pop()
        dx = dxs.Pop()
        dy = dys.Pop()
    End If
End While
End Hilbert
```

This version is a bit longer, because it contains several copies of code to push values onto stacks, update parameters, and pop values back off stacks.

# Summary

Recursion is a powerful technique. Some problems are naturally recursive, and when they are, a recursive algorithm is sometimes much easier to design than a nonrecursive version. For example, recursion makes the Tower of Hanoi puzzle
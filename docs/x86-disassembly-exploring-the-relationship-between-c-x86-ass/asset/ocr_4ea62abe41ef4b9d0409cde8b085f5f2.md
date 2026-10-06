# 10.2 Example: Standard Entry Sequences

This code example uses MASM Syntax

Does the following function follow the Standard Entry and Exit Sequences? if not, where does it differ?

```
_Question2:
call _SubQuestion2
mul 2
ret
```

The function does not follow the standard entry sequence, because it doesn't set up a proper stack frame with ebp and esp. The function basically performs the following C instructions:

```
int Question2()
{
    return SubQuestion2() * 2;
}
```

Although an optimizing compiler has chosen to take a few shortcuts.
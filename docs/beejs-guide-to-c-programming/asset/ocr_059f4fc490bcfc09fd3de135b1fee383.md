# Chapter 23

# Pointers III: Pointers to Pointers andnMore

Here's where we cover some intermediate and advanced pointer usage. If you don't have pointers down well, review the previous chapters on pointers and pointer arithmetic before starting on this stuff.

# 23.1 Pointers to Pointers

If you can have a pointer to a variable, and a variable can be a pointer, can you have a pointer to a variablenthat itself is a pointer?

Yes! This is a pointer to a pointer, and it's held in variable of type pointer-pointer.

Before we tear into that, I want to try for a *feel* for how pointers to pointers work.
Remember that a pointer is just a number. It's a number that represents an index in computer memory,
typically one that holds a value we're interested in for some reason.

That pointer, which is a number, it has to be stored somewhere. And that place is memory, just like everything
else.

But because it has an index it's stored at, right? The pointer must have an index
in memory where it is stored. And that index is a number. It's the address of the pointer. A pointer to the
pointer.

Let's start with a regular pointer to int, back from the earlier chapters:

```
#include <stdio.h>

int main(void)
{
    int x = 3490; // Type: int
    int *p = &x; // Type: pointer to an int

    printf("%d\n", p); // 3490
}
```

> There's some detail in the values that are stored in registers only, but we can safely ignore that for our purposes here. Also the C spec makes no stance on "register" things beyond the register keyword, the description for which doesn't mention registers.
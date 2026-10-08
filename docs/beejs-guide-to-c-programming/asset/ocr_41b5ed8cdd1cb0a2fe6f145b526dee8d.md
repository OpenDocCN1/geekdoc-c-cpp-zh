# Chapter 6. Arrays

Lastly, you can also have C compute the size of the array from the initializer, just by leaving the size off:

```
int a[3] = {22, 37, 3490};
```

```
// is the same as:
```

```
int a[] = {22, 37, 3490};  // Left the size off!
```

# 6.4 Out of Bounds!

C doesn't stop you from accessing arrays out of bounds. It might not even warn you.

Let's steal the example from above and keeping off the end of the array. It only has 5 elements, but let's try to print 10 and see what happens:

```
#include <stdio.h>

int main(void)
{
  int i;
  int a[5] = {22, 37, 3490, 18, 95};

  for (i = 0; i < 10; i++) { // BAD NEWS: printing too many elements
    printf("%d\n", a[i]);
  }
}
```

Running it on my computer prints:

22
37
3490
18
32765
1847652632
1788534144
-56487472
21896

Yikes! What's that? Turning out the end of an array results in what C developers call undefined behavior. We'll talk more about this beast later, but for now, "You’ve done something bad, and anything could go wrong during your program."

And by anything, I mean things like finding zeros, finding garbage numbers, or crashing. The real C specs says in this circumstance the compiler is allowed to emit code that does nothing⁵.

Short version: don't do that causes undefined behavior. Ever⁶.

> ⁵In the old-DOS days before memory protection was a thing, I was writing some C code that actively engaged in kinds of undefined behavior. But I knew what I was doing, and things were working pretty well. Until I made a mistake that caused a lock and, as I found upon reboot, nuked all my BIOS settings. That was for to @man for those times.

> ⁶There are a lot of things that cause undefined behavior, not just out-of-bounds array accesses. This is what makes the C language so exciting.
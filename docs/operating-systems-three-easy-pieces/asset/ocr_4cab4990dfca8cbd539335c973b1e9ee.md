# INTERLUDE: MEMORY API

It is this need for long-lived memory that gets us to the second type
memory, called heap memory, where all allocations and deallocations
areis explicitly handled by you, the programmer. A heavy responsibility,
doubt! And certainly the cause of many bugs. But if you are careful
of pay attention, you will use such interfaces correctly and without
touch trouble. It is an example of how one might allocate an integer
on the heap:

```
void func() {
    int *x = (int *) malloc(sizeof(int));
...
}
```

A couple of notes about this small code snippet. First, you might no-
tice that both stack and heap allocation occur on this time: first the com-
piler makes room for a pointer to an integer when it sees your
declaring of said pointer (int *x); subsequently, when the program
calls malloc(), it requests for space on the heap; the routine
returns the address of such an integer (upon success, or NULL on failure),
which is then stored on the stack for the program.

Because of its explicit nature, and because of its varied usage,
heap memory presents more challenges to both users and systems. Thus,
it is the focus of the remainder of our discussion.

# 14.2 The malloc() Call

The malloc() is quite simple: you pass a size asking for some\upon the heap, and it either succeeds and gives you back a pointer to
tnewly-allocated space, or fails and returns NULL².

The manual page shows what you need to do to use malloc; type man
malloc at the command line and you will see:

```
...
#include <stdlib.h>
void *malloc(size_t size);
```

From this information, you can see that all you need is to include
theader file stdlib.h to use. In fact, you don't really need to
do this, as the C library, which all C programs link with by default,
as the code for malloc() inside it; adding the header lets the
compiler check whether you are calling malloc() correctly (e.g., passing
the number of arguments to it, of the right type).

The single parameter malloc() takes of type size_t which sim-
plcribes how many bytes you need. However, most programmers
d not type in a number here directly (as 10); indeed, it would be
poor performance to do so. Instead, various routines and macros are

> ²Note that NULL in C isn't anything special at all, just a macro for the zero value.

OPERATING
SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG
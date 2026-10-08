Better still, use a header file:

```
```c
/* in file x.h: */
extern int x;        /* a declaration, not a definition */

/* in file x.c: */
#include "x.h"
int x = 0;            /* the definition */

/* in file y.c: */
#include "x.h"
/* the declaration of x is in the header */
```
```

Better still, avoid the global variable.

# ## 27.3.4 C-style casts

In C (and C++), you can explicitly convert a value `v` to a type `T` by this minimal notation:

```
```c
(T)v
```
```

This “C-style cast” or “old-style cast” is beloved by poor typists and sloppy thinkers because it’s minimal and you don’t have to know what it takes to make a **T** from **v**. On the other hand, this style of cast is rightfully feared by maintenance programmers because it is just about invisible and leaves no clue about the writer’s intent. The C++ casts (*named casts* or *template-style casts*; see §A.5.7) were introduced to make explicit type conversion easy to spot (ugly) and specific. In C, you have no choice:

```
```c
int* p = (int*)7;     /* reinterpret bit pattern: reinterpret_cast<int*>(7) */
int x = (int)7.5;     /* truncate double: static_cast<int>(7.5) */



typedef struct S1 { /* . . . */ } S1;
typedef struct S2 { /* . . . */ } S2;
S2 a;
const S2 b;           /* uninitialized consts are allowed in C */



S1* p = (S1*)&a;     /* reinterpret bit pattern: reinterpret_cast<S1*>(&a) */
S2* q = (S2*)&b;     /* cast away const: const_cast<S2*>(&b) */
S1* r = (S1*)&b;     /* remove const and change type; probably a bug */
```
```
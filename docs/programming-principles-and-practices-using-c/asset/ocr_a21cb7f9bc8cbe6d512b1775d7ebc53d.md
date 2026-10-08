To implement our **List** functions, we first **#include** some standard library headers:

```
```c
#include<stdio.h>
#include<stdlib.h>
#include<assert.h>
```
```

C doesn't have namespaces, so we need not worry about **using** declarations or **using** directives. On the other hand, we should probably worry that we have grabbed some very common short names (*Link*, *insert*, *init*, etc.), so this set of functions cannot be used “as is” outside a toy program.

Initializing is trivial, but note the use of **assert()**:

```
```c
void init(struct List* lst)     /* initialize *lst to the empty list */
{
    assert(lst);
    lst->first = lst->last = 0;
}
```
```

We decided not to deal with error handling for bad pointers to lists at run time. By using **assert()**, we simply give a (run-time) system error if a list pointer is null. The “system error” will give the file name and line number of the failed **assert()**; **assert()** is a macro defined in `<assert.h>` and the checking is enabled only during debugging. In the absence of exceptions, it is not easy to know what to do with bad pointers.

The **create()** function simply makes a **List** on the free store. It is a sort of combination of a constructor (*init()* initializes) and **new** (*malloc()* allocates):

```
```c
struct List* create()           /* make a new empty list */
{
    struct List* lst = (struct List*)malloc(sizeof(struct List));
    init(lst);
    return lst;
}
```
```

The **clear()** function assumes that all **Links** are created on the free store and **free()** s them:

```
```c
void clear(struct List* lst)    /* free all elements of lst */
{
    assert(lst);
    {
```
```
# ### 17.4.1 Free-store allocation

We request memory to be *allocated* on the *free store* by the **new** operator:

+   - The **new** operator returns a pointer to the allocated memory.
- A pointer value is the address of the first byte of the memory.
- A pointer points to an object of a specified type.
- A pointer does *not* know how many elements it points to.

The **new** operator can allocate individual elements or sequences (arrays) of elements. For example:

```
int* pi = new int;                // allocate one int
int* qi = new int[4];             // allocate 4 ints (an array of 4 ints)

double* pd = new double;          // allocate one double
double* qd = new double[n];       // allocate n doubles (an array of n doubles)
```

Note that the number of objects allocated can be a variable. That’s important because that allows us to select how many objects we allocate at run time. If **n** is **2**, we get

![](bbox=[0.25, 0.48, 0.85, 0.7])

Pointers to objects of different types are different types. For example:

```
pi = pd;     // error: can’t assign a double* to an int*
pd = pi;     // error: can’t assign an int* to a double*
```

Why not? After all, we can assign an **int** to a **double** and a **double** to an **int**. The reason is the `[ ]` operator. It relies on the *size* of the element type to figure out where to find an element. For example, **qi[2]** is two **int** sizes further on in memory than **qi[0]**, and **qd[2]** is two **double** sizes further on in memory than **qd[0]**. If the size of an **int** is different from the size of **double**, as it is on many computers, we
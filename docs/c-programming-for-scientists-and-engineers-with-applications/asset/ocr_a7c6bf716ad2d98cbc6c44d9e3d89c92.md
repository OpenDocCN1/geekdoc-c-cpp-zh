# One-Level Indirection

| 10000 | 15000 |
|---|---|
| 68745 | 10000 |

```
int value;
int *ptrvalue;

ptrvalue = &value;
*ptrvalue = 68745;
```

Notice that the integer number 68745 may be assigned by dereferencing the pointer ptrvalue. The pointer ptrvalue is a one-level pointer.

Multilevel Indirection A pointer variable may point to any value constant. A pointer variable may even point to another pointer. This means that a pointer variable may point directly to an ordinary variable.

```
ptra -> ptrx -> x;
```

This is called multilevel indirection. The storage of a variable may be accessed by using multilevel pointers. The following code shows the declaration of multilevel pointers and storage access using multilevel pointers.

```
int value;
int *ptrvalue1, **ptrvalue2, ***ptrvalue3;
```

Here ptrvalue1 can only point to a variable of type int, ptrvalue2 can only point to a variable of type int *, and ptrvalue3 can only point to a variable of type int **. The following example shows the organization of multilevel pointers.

```
ptrvalue1 = &value;
ptrvalue2 = &ptrvalue1;
ptrvalue3 = &ptrvalue2;
```

Notice that the addresses of the variables must be assigned to the pointer variables before a value may be accessed through the pointer variables ptrvalue1, ptrvalue2, and ptrvalue3.

| ptrvalue1 | ptrvalue2 | ptrvalue3 |
|---|---|---||
| 5234 | 10000 | 20000 | 30000 |
| | 20000 | 30000 | 40000 |
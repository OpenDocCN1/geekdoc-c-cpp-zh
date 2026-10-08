One- and two-dimensional arrays may be accessed by using the array names in address arithmetic. For example the third element of array stress[10] may be accessed at the location stress + 2 since the array name stress is the address of the array.

One- and two-dimensional arrays may be allocated dynamic storage using the calloc() function from the stdlib.h header file. Input/output and manipulation of one- and two-dimensional arrays may be accomplished using array pointers to the block of dynamic storage. For example, for one-dimensional arrays a dynamic pointer is declared, a block of storage is allocated for an array, and the address of such storage is assigned to the pointer. The following code shows such a declaration and storage allocation for an array of integers.

```
int *aprtr;
```

```
aprtr = (int *) calloc(n, sizeof(int));
```

Now aprtr will contain the address of a block of memory allocated by the calloc() function. Notice that the first argument is n, which means it allocates n cells of storage for the array. Each cell has enough bytes to store an integer. Dynamic storage allocation should be used when the amount of space needed is not known in advance.

Similarly for two dimensional arrays, dynamic storage is allocated using the calloc() function. The following code shows such an allocation:

```
float *aprtr;
```

```
aprtr = ( float *) calloc(imax jmax, sizeof(float));
```

A block of memory containing imax jmax cells is allocated. This storage can hold a two-dimensional array of size [imax][jmax]. In this case each cell contains four bytes of storage because the type of data stored in these cells is float.

Character strings may be stored in string variables by declaring pointers. The following code shows the declaration of a pointer to a character string.

```
char *strname;
```

In this case strname is a character string pointer that will be assigned the address of storage where the string is stored. In this declaration, storage is set up to store an address in strname.

A character string pointer can point to a character string variable in static storage or to dynamically allocated storage.
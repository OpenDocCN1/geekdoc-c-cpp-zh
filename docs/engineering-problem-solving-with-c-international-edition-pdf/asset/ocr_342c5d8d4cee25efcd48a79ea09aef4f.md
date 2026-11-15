# One-Dimensional Arrays

Consider the following declaration that defines and initializes a one-dimensional array with floating-point values:

```
double x[6]={1.5, 2.2, 4.3, 7.5, 9.1, 10.5};
```

The memory snapshot after this statement is executed is the following:

| double x[0] | 1.5 |
|---|---|
| double x[1] | 2.2 |
| double x[2] | 4.3 |
| double x[3] | 7.5 |
| double x[4] | 9.1 |
| double x[5] | 10.5 |

In referencing the array x using standard array notation, reference x[0] refers to the first element in the array, reference x[1] refers to the second element in the array, and reference x[k] refers to the (k+1)th element in the array. Similar references to an array can be generated with pointers. Assume that a pointer ptr has been defined to be a pointer to double and is then initialized with the statement

```
ptr = &x[0];
```

The address of the first element in the array is then stored in the pointer ptr. Thus, reference *ptr refers to x[0], reference *(ptr+1) refers to x[1], and reference *(ptr+k) refers to x[k]. The value of k in reference *(ptr+k) is the offset from the first element in the array.

The following statements compute the sum of the values in the array x using array notation and a for loop:

```
// Declare and initialize objects.
double x[6], sum=0.0;
...
// Sum the values in the array x.
for (int k=0; k<5; ++k)
   sum += x[k];
}
```

An equivalent set of statements that uses pointers instead of array notation is the following:

```
// Declare and initialize objects.
double x[6], sum=0.0; *ptr=&x[0];
...
// Sum the values in the array x.
for (int k=0; k<5; ++k)
{
   sum += *(ptr+k);
}
```
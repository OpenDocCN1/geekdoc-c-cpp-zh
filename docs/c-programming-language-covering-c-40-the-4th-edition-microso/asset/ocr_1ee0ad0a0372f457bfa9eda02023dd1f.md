The new operator permits the initial values of the array elements to be specified using an *array initializer*, which is a list of expressions written between the delimiters { and }. The following example allocates and initializes an int[] with three elements.

```
int[] a = new int[] { 1, 2, 3 };
```

Note that the length of the array is inferred from the number of expressions between { and }. Local variable and field declarations can be shortened further such that the array type does not have to be restated.

```
int[] a = { 1, 2, 3 };
```

Both of the previous examples are equivalent to the following:

```
int[] t = new int[3];
t[0] = 1;
t[1] = 2;
t[2] = 3;
int[] a = t;
```

> **ERIC LIPPERT**  In a number of places thus far, the specification notes that a particular local initialization is equivalent to “assign something to a temporary variable, do something to the temporary variable, declare a local variable, and assign the temporary to the local variable.” You may be wondering why the specification calls out this seemingly unnecessary indirection. Why not simply say that this initialization is equivalent to this:
> 
>     int[] a = new int[3];
>     a[0] = 1; a[1] = 2; a[2] = 3;
> 
> In fact, this practice is necessary because of definite assignment analysis. We would like to ensure that all local variables are definitely assigned before they are used. In particular, we would like an expression such as object[] arr = {arr}; to be illegal because it appears to use arr before it is definitely assigned. If this were equivalent to
> 
>     object[] arr = new object[1];
>     arr[0] = arr;
> 
> then that would be legal. But by saying that this expression is equivalent to
> 
>     object[] temp = new object[1];
>     temp[0] = arr;
>     object[] arr = temp;
> 
> then it becomes clear that arr is being used before it is assigned.
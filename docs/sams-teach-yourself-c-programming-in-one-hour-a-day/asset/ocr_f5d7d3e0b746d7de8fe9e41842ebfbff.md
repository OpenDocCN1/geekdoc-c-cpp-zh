# Analysis

The precise values might be different on your system, but the relationships are the same. Incrementing multi by one increases its value by 16 and makes it point to the next element of the array, multi[1].

In this example, you've seen that multi is a pointer to multi[0]. You've also seen that multi[0] is itself a pointer (to multi[0] [0]). Therefore, multi is a pointer to a pointer. To use the expression multi to access array data, you must use double indirection. To print the stored value in multi[0] [0], you could use any of the following statements:

```
printf("%d", multi[0]);
printf("%d", **multi[0]);
printf("%d", **multi);
```

These concepts apply equally to arrays with three or more dimensions. Thus, a three-dimensional array is an array with elements that are each two-dimensional arrays; each of these elements is itself an array of one-dimensional arrays.

This material on multidimensional arrays and pointers might seem a bit confusing. When you work with multidimensional arrays, keep this point in mind: An array with n dimensions has elements that are arrays of n-1 dimensions. When n becomes 1, array's elements are variables of the data type specified at the beginning of the array declaration line.

So far, you've been using array names that are pointer constants and can't be changed. How would you declare a pointer variable that points to an element of a multidimensional array? Look at the previous example, which declared a two-dimensional array as follows:

```
int multi[2][4];
```

To declare a pointer variable ptr that can point to an element of multi (that is, can point to a four-element integer array), you write

```
int (*ptr)[4];
```

You then make ptr point to the first element of multi by writing

```
ptr = multi;
```

You might wonder why the parentheses are necessary in the pointer declaration. Brackets ([]) have a higher precedence than *. If you wrote

```
int *ptr[4];
```
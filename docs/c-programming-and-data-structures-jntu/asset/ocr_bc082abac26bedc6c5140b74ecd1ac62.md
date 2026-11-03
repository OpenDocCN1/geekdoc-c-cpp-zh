# Variable-Length Arrays

In C89, array dimensions must be declared using integer constant expressions, and the size of an array is fixed at compile time. C99 changes this for certain circumstances. In C99, you can declare an array whose dimensions are specified by any valid integer expression, including those whose value is known only at run time. This is called a variable-length array (VLA). However, only local arrays (that is, those with block scope or prototype scope) can be of variable length.

Here is an example of a variable-length array:

```
void f(int dim1, int dim2)
{
    int matrix[dim1][dim2]; /* a variable-length, 2-D array */
    /* . . . */
}
```

Here, the size of matrix is determined by the values passed to f() in dim1 and dim2. Thus, each call to f() can result in matrix being created with different dimensions.

It is important to understand that variable-length arrays do not change their dimensions during their lifetime. (That is, they are not dynamic arrays.) Rather, a variable-length array can be created with a different size each time its declaration is encountered.

You can specify a variable-length array of an unspecified size by using * as the size.

The inclusion of variable-length arrays causes a small change in the sizeof operator. In general, sizeof * is a compile-time operator. That is, it is normally translated into an integer constant whose value is equal to the size of the type or object when a program is compiled. However, when it is applied to a variable-length array, sizeof * is evaluated at run time. This change is necessary because the size of a variable-length array may not be known until run time.

One of the major reasons for the addition of variable-length arrays to C99 is to support numeric processing. Of course, it is a feature that has widespread applicability. But remember, variable-length arrays are not supported by C89 (or by C++).

# Use of Type Qualifiers in an Array Declaration

In C99 you can use the keyword static inside the brackets of an array declaration when that declaration is for a function parameter. It tells the compiler that the array pointed to by the parameter will always contain at least the specified number of elements. Here is an example:

```
int f(char str[static 80])
{
    // here, str is always a pointer to an 80-element array
    /* . . . */
}
```

In this example, str is guaranteed to point to the start of an array of chars that contains at least 80 elements.

You also can use the keywords restrict, volatile, and const inside the brackets, but only for function parameters. Using restrict specifies that the pointer is the sole initial means of access to the object.
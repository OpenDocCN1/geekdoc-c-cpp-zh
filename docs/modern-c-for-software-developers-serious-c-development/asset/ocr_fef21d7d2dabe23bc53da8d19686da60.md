```
int array[5] = {1, 2, 3, 4, 5};
```

We can have fewer initializers than the length of the array, in which case, the remaining array elements will be initialized to the ‘zero’ of the type of the array.

# Passing Single-Dimension Arrays to Functions

In C and C++, we cannot pass an entire array as an argument to a function. We can, however, pass a pointer to the array by specifying the array's name without an index.

```
int main(void)
{
    int sample[10];
    func(sample);
}
```

An array name (without an index) is a pointer to the first element of the array.

The formal parameter of a function that receives an array can be declared as a pointer to the array's data type or as a sized or unsized array. For example:

```
func (int *p)
func (int m[10]);
func(int m[])
```

All of the above are equivalent. The array size can be any value; for example, func(int m[100000]) is also valid. An array parameter in a function parameter list is syntactic sugar only a pointer to an array is received by the function. The programmer is responsible to ensure that a buffer overrun does not occur.

# Multi-Dimensional Arrays

A multi-dimensional array can be specified with the following syntax:

```
int m[6][8];              // two dimensional array of integers
char s[7][3][5];      // three dimensional array of chars
```
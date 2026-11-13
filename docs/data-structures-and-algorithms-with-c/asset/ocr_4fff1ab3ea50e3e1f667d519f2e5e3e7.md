```
int a[10];
```

there is no element a [10]; the end element is a [9].

Arrays are not limited to type int; you can have arrays of char or float or double or any other type.

# Example:

```
char name [30];
float x[10];
double d[100];
```

There are some important points about arrays. These are as follows:

+   - Arrays are always stored in consecutive memory locations.
+   - An array can store multiple values that can be referenced by a single name.
+   - An array name is actually an address of the first element of the array.
+   - An array can be either an integer, character or floating-point data type can be initialized only during declaration.
+   - In C, array index starts from zero.
+   - There is no bound checking concept for arrays in C.

# Size of One-Dimensional Array

The one-dimensional array can be declared as:

```
data_type array_name[size];
```

The total size of the array in bytes can be calculated by using the following expression:

```
sizeof (data_type) * size
```

where data_type is the data type of the array and size specifies the total number of elements of the array.

Another way to calculate the total size of the array in bytes is simpler; that uses the following expression

```
sizeof(array_name)
```

where array_name is the name of the array.

# Initialization of One-Dimensional Array

Although it is not possible to assign values to all elements of an array at once using an assignment expression, it is possible to initialize some or all elements of an array when the array is defined.

The syntax looks like this:

```
int a[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
```

The list of values, enclosed in braces {}, separated by commas, provides the initial values for successive elements of the array. The individual array elements are as follows:

```
a[0] = 0
a[1] = 1
a[2] = 2
a[3] = 3
a[4] = 4
a[5] = 5
a[6] = 6
a[7] = 7
```
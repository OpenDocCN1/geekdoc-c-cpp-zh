# ARRAY AND STRING

> "Computers make it easier to do a lot of things, but most of the things they make it easier to do don't need to be done." -Andy Rooney

Many applications require the processing of multiple data items, that have common characteristics. For example, let us say we have to find the average marks obtained in a class. In this case, we have a couple of choices. Either we can store all the values in different variables or we can create an array that will hold all these values in contiguous memory location. If they are stored in different variables and the number of such variables is quite large then it is quite unmanageable as these variables are scattered throughout the memory. In such situations, it is often convenient to place the data items into an array, where they will all share the same name.

+   ## KEY FEATURES
+   - One dimensional array
+   - Processing an array
+   - Two-dimensional array
+   - Representation of 2D array
+   - Sparse Matrix
+   - String

# ARRAY

Definition: An array is a collection of the same type of data items, which are stored in consecutive memory locations under a common name.

An array variable must be followed by square bracket enclosing size specification of the array. The size signifies the number of elements of the array. That number should be a positive integer number (greater than 0).

# One-dimensional Array

A one-dimensional array is one in which only one subscript is needed to specify a particular element of the array.

# Declaration of One-Dimensional Array

The one-dimensional array can be declared as follows:

```
data_type array_name [size];
```

where array_name is the name of an array and size is the number of elements of data type data_type and size must be an integer constant specified within a pair of square brackets.

# Example:

```
int a[10];
```

The above declaration states an array, named “a”, consisting of ten elements, each of type int. Simply speaking, an array is a variable that can hold more than one value. (Arrays in programming are similar to vectors or matrices in mathematics.) We represent the array in above with a picture like this:
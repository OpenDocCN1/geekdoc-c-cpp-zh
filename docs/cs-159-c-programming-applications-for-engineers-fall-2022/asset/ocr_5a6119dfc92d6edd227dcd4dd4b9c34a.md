# # Multidimensional Arrays

The arrays we have seen so far are single dimension arrays. Each single dimension array is one row of indexed column values. Mastery of logic with single dimension arrays is necessary before considering multidimensional structures that may increase memory usage significantly.

With multidimensional arrays we can add a second dimension (multiple rows each with its own columns), a third dimension (planes, rows, and columns), and further as necessary. Your only limitation may be memory, but rarely does a problem call for an array with more than three dimensions.

Regardless of the number of dimensions in an array the name selected for the array will continue to represent the location where in memory its allocated space begins. We will see how this requires additional information to be communicated with functions that have a multidimensional array as a parameter.

# # Declaration and Defining Multidimensional Arrays

Multidimensional arrays, like single dimension arrays, must be declared and defined before being used. Declaration and definition tell the compiler the name, data type, and size, or extent, of each dimension of the array.

| Data Type | Identifier | Dimension Extents |
| :--- | :--- | :--- |
| int | table | [4][4] ; |

# ## Two-dimensional array:

+   - Each dimension is zero-based.
+   - The intersection of every row and column represents the capacity to store a value of the defined type.
+   - Total capacity is the product of the extent of each dimension.
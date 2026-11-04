# ### 8.9.2 Jagged Arrays

A jagged array is a one-dimensional array in which each element refers to a one-dimensional array. This makes them quite flexible, because the lengths of the rows in the array need *not* be the same. For example, jagged arrays could be used to store a single student’s exam grades across multiple courses, where the number of exams may vary from course to course.

# #### Array Initializer for a Two-Dimensional Jagged Array

We can access the elements in a jagged array by an array-access expression of the form *arrayName[row][column]*—similar to the array-access expression for rectangular arrays, but with a separate set of square brackets for each dimension. A jagged array with three rows of different lengths could be declared and initialized as follows:

```
int[][] jagged = {new int[] {1, 2},
                  new int[] {3},
                  new int[] {4, 5, 6}};
```

where 1 and 2 initialize jagged[0][0] and jagged[0][1], respectively; 3 initializes jagged[1][0]; and 4, 5 and 6 initialize jagged[2][0], jagged[2][1] and jagged[2][2], respectively. So array jagged is actually composed of four separate one-dimensional arrays—one for the rows, one per row. Thus, array jagged itself is an array of three elements, each a reference to a one-dimensional array of int values.

# #### Diagram of a Two-Dimensional Jagged Array in Memory

Observe the differences between the array-creation expressions for rectangular arrays and for jagged arrays. Two sets of square brackets follow the type of jagged, indicating that this is an array of int arrays. Furthermore, in the array initializer, C# requires the keyword *new* to create an array object for each row. Figure 8.18 illustrates the array reference jagged after it’s been declared and initialized.

![](bbox=[0.121, 0.668, 0.921, 0.783])

# #### Creating Two-Dimensional Arrays with Array-Creation Expressions

A rectangular array can be created with an array-creation expression. For example, the following lines declare variable b and assign it a reference to a three-by-four rectangular array:

```
int[,] b;
b = new int[3, 4];
```

In this case, we use the literal values 3 and 4 to specify the number of rows and number of columns, respectively, but this is *not* required—apps also can use variables and expressions to specify array dimensions. As with one-dimensional arrays, the elements of a rectangular array are initialized when the array object is created.
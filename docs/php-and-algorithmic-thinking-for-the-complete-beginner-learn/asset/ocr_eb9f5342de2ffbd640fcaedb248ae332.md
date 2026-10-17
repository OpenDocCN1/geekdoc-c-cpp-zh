# # Chapter 32 Introduction to Arrays

64 71 74 63 61 64 57

Maria George John Tom Andrew Helen

57 58 65 71 75 68 56 64 71 74 63 61 64 57 66 61 71 62 74 64 78 73 60 67 54 59 62 64

Each item in an array is called an element. In memory, array elements are located in consecutive memory locations. Each element in an array is assigned a unique number known as its index position, or simply an index.

> **Notice:** Arrays in computer science resemble the matrices used in mathematics. A mathematical matrix is a collection of numbers or other mathematical objects, arranged in rows and columns.

There are one-dimensional and multidimensional arrays. A multidimensional array can be two-dimensional, three-dimensional, four-dimensional, and so on.

# ## One-Dimensional Arrays

The following example presents a one-dimensional array that holds the grades of six students. The name of the array is Grades. For your convenience, the corresponding index is written above each element. By default, in PHP, index numbering always starts at zero.

![](bbox=[0.018, 0.565, 0.981, 0.769])

> **Remember!** Since index numbering starts at zero, the index of the last element of an array is 1 less than the total number of elements in the array.

You can think of an array as if it were six individual variables—Grades0, Grades1, Grades2, ... Grades5—with each variable holding the grade of one student. The advantage of the array, however, is that it can hold multiple values under one common name.
# Arrays

The variables we used so far can store only one value at a time. So, if you want to store 30 test scores in memory and do computations with them simultaneously, you would have to declare 30 different variables.

A single array allows you to store multiple data items of the same type. For example, a single one-dimensional array can store all 30 scores at the same time. Because one-dimensional (1-D) arrays are the simplest type of arrays, we will discuss them first.

# Topics

| 7.1 | Introduction to One-Dimensional Arrays | 7.4 | Accessing Elements of an Array Using foreach Loop |
| 7.2 | Assigning a Value to an Element of an Array | 7.5 | Copying an Array |
| 7.3 | Accessing Elements of an Array Using the Index | 7.6 | Looking Up Values in an Array |

# 7.1 Introduction to One-Dimensional Arrays

An array can be thought of as a container of data with multiple storage locations or slots, one location for each data item. An array called testScore that stores 10 test scores may be represented as follows:

testScore
| 85 | 92 | 87 | 67 | 83 | 91 | 73 | 98 | 83 | 84 |
Element number: (subscript or index) 0 1 2 3 4 5 6 7 8 9

Each storage location of the array is called an element. The elements are numbered consecutively, starting with zero. An individual element of an array is accessed using the array name, followed by the element number (subscript or index) in brackets. The subscript must be an integer. For example, testScore[0] refers to the first element of the array, that is, the number 85, testScore[1] refers to the second element of the array—that is, the number 92, and testScore[9] refers to the tenth element of the array, the number 84.

Different arrays can hold data items of different types, including numbers, strings, arrays and objects. However, within an array, all elements must be of the same type. Thus, an array is a collection of data items of the same type.

An array, like testScore, which can store one set of data, is called a one-dimensional (1-D) array. A two-dimensional (2-D) array, discussed later in Chapter 8, can store multiple sets of data, all of the same type.
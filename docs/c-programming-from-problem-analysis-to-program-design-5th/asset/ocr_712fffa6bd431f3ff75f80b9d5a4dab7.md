if the index is out of bounds, the program must terminate with an appropriate error message. Consider the following statements:

```
```
myArray<int> list(5);              //Line 1
myArray<int> myList(2, 13);        //Line 2
myArray<int> yourList(-5, 9);      //Line 3
```
```

The statement in Line 1 declares list to be an array of 5 components, the component type is int, and the components are: list[0], list[1], . . . , list[4]; the statement in Line 2 declares myList to be an array of 11 components, the component type is int, and the components are: myList[2], myList[3], . . . , myList[12]; the statement in Line 3 declares yourList to be an array of 14 components, the component type is int, and the components are: yourList[-5], yourList[-4], . . . , yourList[0], . . . , yourList[8]. Write a program to test the class myArray.

+   11. Programming Exercise 10 processes only int arrays. Redesign the class myArray using class templates so that the class can be used in any application that requires arrays to process data.

+   12. Design a class to perform various matrix operations. A matrix is a set of numbers arranged in rows and columns. Therefore, every element of a matrix has a row position and a column position. If A is a matrix of five rows and six columns, we say that the matrix A is of the size 5 × 6 and sometimes denote it as A_{5×6}. Clearly, a convenient place to store a matrix is in a two-dimensional array. Two matrices can be added and subtracted if they have the same size. Suppose A = [a_{ij}] and B = [b_{ij}] are two matrices of the size m × n, in which a_{ij} denotes the element of A in the ith row and the jth column, and so on. The sum and difference of A and B are given by:
+   
+   A + B = [a_{ij} + b_{ij}]
+   
+   A - B = [a_{ij} - b_{ij}]
+   
+   The multiplication of A and B (A * B) is defined only if the number of columns of A is the same as the number of rows of B. If A is of the size m × n and B is of the size n × t, then A * B = [c_{ik}] is of the size m × t and the element c_{ik} is given by the formula:
+   
+   c_{ik} = a_{i1}b_{1k} + a_{i2}b_{2k} + · · · + a_{in}b_{nk}
+   
+   Design and implement a class matrixType that can store a matrix of any size. Overload the operators +, -, and * to perform the addition, subtraction, and multiplication operations, respectively, and overload the operator << to output a matrix. Also, write a test program to test various operations on the matrices.

+   13. a. In Programming Exercise 1 in Chapter 12, we defined a class romanType to implement Roman numbers in a program. In that exercise, we also implemented a function, romanToDecimal, to con-
# MATRIX AND VECTOR CLASSES

```
g(m1);
Matrix m2;
m2 = m1;
cout << "A copy of the matrix obtained with =" << endl;
m2.printMatrix();

cout << "The sum of the last 2 matrices is" << endl;
(m1 + m2).printMatrix();
cout << "The product of the first matrix and its transpose is" << endl;
(m1*m1.trans()).printMatrix();
cout << "The first matrix left multiplied by 2 is" << endl;
(2*m1).printMatrix();
cout << "The (1, 1) element of the first matrix is " <<
m1[1][1] << endl;
return 0;
```

The output produced by this program

+   A matrix initialized from a pointer-to-pointer
1 3
2 5
The function g was called
A copy of the matrix obtained with =
1 3
2 5
The sum of the last 2 matrices is
2 6
4 10
The product of the first matrix and its transpose is
10 17
29
The first matrix left multiplied by 2 is
2 6
4 10
The (1, 1) element of the first matrix is 5

Class Matrix represents our attempt at creating a framework for manipulating two-dimensional arrays. The developments in this section are just the beginning and this topic will arise in Chapter 7. Our final version of the class is summarized in Appendix D.
A two-dimensional array with one column is a vector which means that the Matrix class encompasses the vector case in a section code. The code developed from this approach (e.g., the use of Ai[0] for working with a two-dimensional representation of a vector) can be cumbersome. There are also certain entities like the scalar product of two vectors that are vector-specific and do not translate particularly to a two-dimensional environment. Obstacles can be overcome by creating methods that are specialized for the case of ncols being 1. The fact that specialization is needed suggests that vector objects should have their own identity rather than being encapsulated in the Matrix class. Accordingly, in the remainder of this section we will provide a sketch of how a class Vector can be developed. The task of providing the class with more functionality is the subject of Exercise 32.

Listing 3.16 represents the header file for our first attempt at creating a class Vector.
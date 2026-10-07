# 42

# A SKETCH OF C++

```
cout << endl;
return 0;
}
```

produces the output

```
$ g++ -Wall breakEx.cpp -o breakEx
./breakEx
0 1 0 1 0 1
```

# 3.5 Using arrays and pointers

To this point we have primarily dealt with primitive data types. These include arrays and classes. are the building blocks for compound data types that are either primitive or defined. Arrays will be treated in this section while these are the topic of Section 3.7.

An important part of most programming languages is the use of arrays for data storage and manipulation. A one-dimensional array is a vector that, in C++, may contain objects of any one data type, either.

Arrays are declared in C++ code using square brackets []. There is nothing special about the one-dimensional case. The declaration is

```
int nRows[nCols];
```

will reserve the memory space for a two-dimensional integer array or matrix with nRows rows and nCols columns. The (i, j)th array is accessed using x[i][j]. Note that in C/C++ 0-offset indexing, which means the first element of a one-dimensional array is x[0] rather than x[1]. Similarly, the first component of a two-dimensional array is x[0].

```
double a[3] = {1, 2, 3};
int a[7] = {1, 2};
float a[2][3] = {1, 3, 5}, {2, 4, 6}};
```

The first statement initializes a three-element array of doubles with a[0] = 1, a[1] = 2 and a[2] = 3. The second statement initializes only the two elements in the integer array a[2] = a[6]. The uninitialized elements are set to 0 by default; Finally, a is a 2x3 array with row a[0][0] = 1, a[0][1] = 3, a[0][2] = 5 and second row a[1][1] = 4, a[1][2] = 6.

Another way to work with arrays is through the use of pointers. The value of an object type pointer is a memory location. Pointers may have indices beyond their connection to arrays that make an essential ingredient of any C++ programmer's repertoire.

Whenever we execute a program it is loaded into the computer's memory. One may think of memory being sequentially arranged, one-byte blocks that are numbered from zero and going up to an integer that represents the total amount of available memory, although this may not be strictly in reality. Each part of the program occupies one or more of these memory blocks. The address of a program component can be accessed in C/C++ using the address operator &. An illustration of this is the following simple program.
+   g) The ______ operator dynamically allocates memory for an object of a specified type and returns a(n) ______ to that type.
+   
+   11.2  Explain the multiple meanings of the operators << and >>.
+   
+   11.3  In what context might the name operator() be used?
+   
+   11.4  (True/False) Only existing operators can be overloaded.
+   
+   11.5  How does the precedence of an overloaded operator compare with the precedence of the original operator?

# Answers to Self-Review Exercises

+   11.1  a) operator overloading.  b) operator.  c) assignment (=), address (&), comma (,).
+    d) precedence, associativity, “arity.”  e) ?, :, ::, *, and ::  f) delete.  g) new, pointer.
+   
+   11.2  Operator >> is both the right-shift operator and the stream extraction operator, depending on its context. Operator << is both the left-shift operator and the stream insertion operator, depending on its context.
+   
+   11.3  For operator overloading: It would be the name of a function that would provide an overloaded version of the / operator for a specific class.
+   
+   11.4  True.
+   
+   11.5  The precedence is identical.

# Exercises

+   11.6  *(Memory Allocation and Deallocation Operators)* Compare and contrast dynamic memory allocation and deallocation operators new, new [ ], delete and delete [ ].
+   
+   11.7  *(Overloading the Parentheses Operator)* One nice example of overloading the function call operator () is to allow another form of double-array subscripting popular in some programming languages. Instead of saying

```
chessBoard[ row ][ column ]
```

for an array of objects, overload the function call operator to allow the alternate form

```
chessBoard( row, column )
```

Create a class DoubleSubscriptedArray that has similar features to class Array in Figs. 11.10–11.11. At construction time, the class should be able to create an array of any number of rows and any number of columns. The class should support operator() to perform double-subscripting operations. For example, in a 3-by-5 DoubleSubscriptedArray called a, the user could write a(1, 3) to access the element at row 1 and column 3. Remember that operator() can receive any number of arguments. The underlying representation of the double-subscripted array should be a single-subscripted array of integers with rows * columns number of elements. Function operator() should perform the proper pointer arithmetic to access each element of the array. There should be two versions of operator()—one that returns int & (so that an element of a DoubleSubscriptedArray can be used as an lvalue) and one that returns const int &. The class should also provide the following operators: =, !=, =, << (for outputting the array in row and column format) and >> (for inputting the entire array contents).

+   11.8  *(Complex Class)* Consider class Complex shown in Figs. 11.14–11.16. The class enables operations on so-called complex numbers. These are numbers of the form realPart + imaginaryPart * i, where i has the value

√−1
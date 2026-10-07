# ISO/IEC 9899:2011 (E)

argument-expression-list:
ignment-expression
argument-expression-list , assignment-expression

# 6.5.2.1 Array subscribing

Constraints

+   One of the expressions shall have type "pointer to complete object type", the other expression shall have integer type, and the result has type "type".

Semantics

+   A postfix expression followed by square brackets [] is a subscribed designation of an array object. The definition of the subscript operator [] is that E1[E2] is identical to (* ((E1)+(E2))). Because of the conversion it applied to the binary +, if E1 is an array object (equivalently, a pointer to the initial element of an array object) and E2 is an integer, E1[E2] designates the E element of E1 (counting from zero).

+   Successive subscript operators denote the element of a multidimensional array object. If E is an n-dimensional array (n ≥ 2) with dimensions ix×...×k, then E (used as other than an lvalue) is converted to a pointer to an (n−1)-dimensional array with dimensions j×...×k. If the unary * operator is applied explicitly, or implicitly as a result of subscribing, the result is the referenced (n−1)-dimensional array, which itself is converted into a pointer if other than an lvalue. It follows that these arrays are stored in row-major order (last subscript varies fastest).

+   EXAMPLE Consider the array object defined by the
int *x[3] [5];

Here x is a 3×5 array of ints; more precisely, x is an array of three elements, each of which is an array of five ints. In the expression x[i], which is equivalent to (* ((x)+(i))), is first converted to a pointer to the initial array and is then adjusted according to the type of x, which conceptually entails multiplying i by the size of the object to which the pointer points, namely an array of int objects. The results are added and applied to yield an array of five ints. When used in the expression x[i][j], which in turn is converted to a pointer to the first of the, so x[i][j] yields an int.

Forward references: additive operators (6.5.6), address and indirection operators (6.5.3.2), array declarators (6.7.6.2).
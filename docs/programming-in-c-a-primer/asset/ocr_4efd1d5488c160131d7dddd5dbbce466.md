+   - In the case of unary operators, the argument must be the same type as that of the enclosing class or struct.
+   - In the case of binary operators, the first argument must be of the same type as that of the enclosing class or struct and the second may be of any type.

Examples of overloaded operators are:

```
// vector addition
public static Vector operator + (Vector a, Vector b)
// unary minus
public static Vector operator - (Vector a)
// comparison
public static bool operator == (Vector a, Vector b)
```

Vector is a data type of class and may represent both magnitude and direction (as in physics and engineering) or a series of points called elements (as in mathematics). The process of overloading involves the following steps:

+   - Create a class (or struct) that defines the data type that is to be used in the overloading operation.
+   - Declare the operator method operator op() using public and static modifiers.
+   - Define the body of the operator method to implement the required operation.

# 15.5 OVERLOADING UNARY OPERATORS

Let us consider the unary minus operator. A minus operator, when used as unary, takes just one argument. We know that this operator changes the sign of an operand when applied to a basic data item. We shall see here how to overload this operator so that it can be applied to an object in much the same way as is applied to an int or float variable. The unary minus when applied to an object should change the sign of each of its data items. Program 15.1 shows how the unary minus operator is overloaded.

The method operator - () takes one argument of type Space and changes the sign of data members of the object s. Since it is a member method of the same class, it can directly access the members of the object which activated it. Remember, a statement like
s2 = -s1;
will not work, because the operator method does not return any value. It can work if the method is modified to return an object.

# Program 15.1 OVERLOADING UNARY MINUS

```
using System;
class Space
{
    int x, y, z;
    public Space ( int a, int b, int c )
    {
        x = a;
        y = b;
```
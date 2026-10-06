A pointer in C++ is a variable that stores the memory address of an object (instead of storing the object directly). Java and C# have a similar concept, that of "reference", but the syntax is different. We will start by studying a contrived example of pointers in action:

```
1 include "point2d.h"

2 int main()
3 {
4 Point2D alpha;
5 Point2D beta;
6 Point2D *ptr;

7 ptr = &alpha;
8 ptr->setX(1.0);
9 ptr->setY(2.5);

10 ptr = &beta;
11 ptr->setX(4.0);
12 ptr->setY(4.5);

13 ptr = 0;

14 return 0;
15 }
```

The example relies on the Point2D class from the previous subsection. Lines 4 and 5 define two objects of type Point2D. These objects are initialized to (0, 0) by the default Point2D constructor.

Line 6 defines a pointer to a Point2D object. The syntax for pointers uses an asterisk in the variable name. Since we did not initialize the pointer, it contains a random memory address. This is solved on line 7 by assigning alpha's address to the pointer. The unary & operator returns the memory address of an object. An address is typically a 32-bit or a 64-bit integer value specifying the offset of an object in memory.

On lines 8 and 9, we access the alpha object through the ptr pointer. Because ptr is a pointer and not an object, we must use the -> (arrow) operator instead of the (dot) operator.

On line 10, we assign beta's address to the pointer. Then from on, any operation we perform through the pointer will affect the object.

Line 13 sets the pointer to a null pointer. C++ has no keyword for representing
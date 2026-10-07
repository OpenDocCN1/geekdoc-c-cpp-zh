# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

value is given by the initializer list.¹99)

+   4 If the type name specifies an array of unknown size, the size is determined by the initializer list as specified in 6.7.9, and the type of the compound literal is that of the completed array type. Otherwise (when the type name specifies an object type), the type of the compound literal is specified by the type name. In either case, the result is an lvalue.

+   5 The value of the compound literal is that of an unnamed object initialized by the initializer list. If the compound literal occurs outside the body of a function, the object has static storage duration; otherwise, it has automatic storage associated with the enclosing block.

+   6 All the semantic rules for initializer lists in 6.7.9 apply to compound literals.¹⁰⁰⁰)

+   7 String literals, and compound literals with const-qualified types, need not designate distinct objects.¹⁰⁰¹)

+   8 EXAMPLE 1 The file scope definition
```c
int *p = (int[]){2, 4);
```
pializes p to point to the first element of an array of two, the first having the value two and the second, four. The expressions in this compound literal are required to be constant. The unnamed object has static storage duration.

+   9 EXAMPLE 2 In contrast, in
```c
void f(void)
{
    int *p;
    /*...*/
    p = (int [2]){*p};
}
```
p is assigned to the first element of an array of two, the value previously pointed to by p and the second. The expressions in this compound literal need not be constant. The unnamed object has automatic storage duration.

+   10 EXAMPLE 3 Initializers with definitions can be combined with compound literals. Structure objects created using compound literals can be passed to functions depending on order of member:
```c
drawline(struct point){.x=1, .y=1,
       struct point){.x=3, .y=4});
```

> 99) Note that this differs from a cast expression. For example, a cast specifies a conversion to scalar types or void, and the result of a cast expression is not an lvalue.

> 100) For example, subjects without explicit initializers are initialized to zero.

> 101) This allows implementations to share storage for string literals and constant compound literals with the same or overlapping representations.

86

Language

$6.5.2.5
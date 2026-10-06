The prototype of a friend function should be declared in the class if the operator is overloaded as a friend function:

```
friend function type operator operandname (argument list);
```

The function type is the type of return value of the overloaded operator, i.e., the type of the result of the operation. The term operator is the key in defining overload. operandname is the name of the operator to be overloaded. It must refer to an operator that can be overloaded, such as "+", the add sign. The argument list lists the arguments and the types needed for operand. If the operator is overloaded as a friend function, then the key word friend should be declared in the function in the class. The function is implemented outside the class.

If the operator overloaded as a member function, the number of arguments is one less than the number of operands (not applicable to "+" or "-"). If the operator is overloaded as a friend function, then the two numbers are same. The reason is that the operator overloaded as a member function and an object uses the overloaded member function, then the data of the object can be accessed directly, so there is no need to pass it by argument list. The missing operand is the object itself. But when the operator is overloaded as a friend function, and the friend operates on the data of an object, it must work through the object name. The number of operands does not change.

The main advantage of operator overloading is that we can change the operations of existing operators so they can operate on a user-defined class.

# 8.2.2 Operator Overloaded as Member Function

Operator overload is essentially function overload. When an operator is overloaded as a member function, it can freely access data members in the class. We always use an object of the class to access overloaded operators. If it is a binary operator, an operand is the object's data, pointed by this pointer, and the other operand is passed by an argument list of the overloaded function. If the operator is unary, the operand is pointed by this pointer of the object, so it does not require any argument. These two cases are illustrated below.

For binary operator B, if it is overloaded as a member function in order to indicate the expression oprnd1 B oprnd2, where oprnd1 is an object of class A, then B should be overloaded as a member function of A and the class has one formal argument, where type is that of oprnd2. After overloading, expression oprnd1 B oprnd2 is equivalent to calling function oprnd1.operator B oprnd2.

For a prefix operator U, such as "-" (minus sign), if it is to be overloaded as a member function in order to indicate expression U oprnd, where oprnd is an object of class A, then operator U should be overloaded as a member of class A, which has no argument
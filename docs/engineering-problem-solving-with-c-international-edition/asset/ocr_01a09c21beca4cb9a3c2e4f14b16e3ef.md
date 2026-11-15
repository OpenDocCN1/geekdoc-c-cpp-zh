Constructor functions are programmer-defined functions. Here are the constructor functions that should be added to the class implementation file:

```
//--------------------------------------------------------------
// This constructor function initializes x and y to zero.
xy_coordinate::xy_coordinate()
{
    x = 0;
    y = 0;
}
//--------------------------------------------------------------
// This constructor function initializes x and y to parameters.
xy_coordinate::xy_coordinate(double a, double b)
{
    x = a;
    y = b;
}
//--------------------------------------------------------------
```

# Class Operators

The assignment operator is defined for objects of the same class type. If pt1 and pt2 are both xy_coordinate objects, then this statement is a valid statement:

```
pt1 = pt2;
```

Each data member of the object pt1 is assigned the value of the corresponding data member of the object pt2. However, the C++ arithmetic operators and relational operators cannot automatically be used with a programmer-defined class type. This comparison is not valid:

```
if (pt1 == pt2) (invalid comparison)
```

A class definition can include a set of operators to be used with objects of the class.

# Overload

The ability to overload operators is a powerful feature in C++. Overloading operators allows a programmer-defined data type to be used as easily as any predefined data type. As an example, consider the arithmetic operators defined in C++. These operators are defined to operate on all predefined data types. However, they are not defined for objects of programmer-defined data types. When designing a class data type, a set of arithmetic operators that work on objects of the class may be included. Operators are included in a class definition in the same way as member functions, except that the keyword operator is used. It is followed by the name of the function, where the name of the function is one of the predefined C++ operators. Only predefined operators may be overloaded. You may not, for example, define a new operator ** to perform exponentiation since this operator is not one of the predefined operators in C++. In the next section, we illustrate the use of overloaded operators in the definition of a complex number class that includes the arithmetic operators (i.e., +, -, *, /).
# Introduction to Classes

# Point of Information

Accessor Functions

An accessor function is any non-constructor member function that accesses a class's private data members. For example, the showDate() function in the Date class is an accessor function. These functions are extremely important because they provide a means of displaying private data members' stored values.

When you construct a class, make sure to provide a complete set of accessor functions, each function should return a data member's exact value, but it should return a useful representation of the value. For example, the date 12/25/2006 is stored as a long integer variable in the form 20062512. Although an accessor function could display this value, a more useful representation is 12/25/06 or December 25, 2006.

The keyword inline isn't required in this declaration because member functions defined in the class declaration are inline by default.
Generally, only inline functions that can be coded on a single line are good candidates for inline functions. This guideline reinforces the convention that inline functions should be small. Therefore, the first constructor is more conventionally written with:

```
Date(int mm = 7, int dd = 4, int yyyy = 2005)
{ month = mm; day = dd; year = yyyy; }
```

The second constructor, which extends over three lines, should be written as an inline function.

# Destructors

The counterpart to constructor functions are destructor functions. Destructors are functions with the same name as constructors but are preceded by a tilde (~). Therefore, for the Date class, the destructor is ~Date(). Like constructors, the C++ compiler provides a default-nothing destructor in the absence of an explicit destructor. Unlike constructors, there can be only one destructor per class because destructors take no parameters and return nothing.

Destructors are called automatically when an object gets out of existence and are meant to 'clean up' any undesirable effects the object might leave. Generally, these effects occur only when an object contains a pointer member.

![](bbox=[0.105, 0.773, 0.175, 0.833])

# EXERCISES 10.2

+   1. (For Review) Determine whether the following statements are true or false:

+   a. A constructor must have the same name as its class.

+   b. A class can have only one constructor function.
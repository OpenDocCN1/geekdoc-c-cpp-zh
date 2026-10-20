GetArea() and Display(), can also access those variables directly without the use of any instance of the class. Display(), the member function has also been declared public. This allows it to be accessed as well from Main() with the instance r of the Rectangle class

# Private Access Specifier

With this specifier, a class can hide the member functions and member variables from the other objects and functions. Only the functions belonging to the same class can access the private members. It is not even possible for an instance of class to access the private members.

The example given below illustrates the concept of private access specifiers.

```
using System;

namespace RectangleApplication
{

class Rectangle
{

//member variables

private double length;

private double width;
```
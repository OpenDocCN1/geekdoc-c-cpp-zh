# Friend Functions

If your class has a full set of accessor functions, you can use the accessor functions to define a function to test for equality or to do any other kind of computing that depends on the private member variables. However, although this may give you access to the private member variables, it may not give you efficient access to them. Look again at the definition of the function equal given in Display 11.1. To read the month, it must make a call to the accessor function getMonth. To read the day, it must make a call to the accessor function getDay. This works, but the code would be simpler and more efficient if we could just access the member variables.

A simpler and more efficient definition of the function equal given in Display 11.1 would be as follows:

```
bool equal(DayOfYear date1, DayOfYear date2)
{
    return (date1.month == date2.month &&
            date1.day == date2.day);
}
```

There is just one problem with this definition: It’s illegal! It’s illegal because the member variables month and day are private members of the class DayOfYear. Private member variables (and private member functions) cannot normally be referenced in the body of a function unless the function is a member function, and equal is not a member function of the class DayOfYear. But there is a way to give a nonmember function the same access privileges as a member function. If we make the function equal a friend of the class DayOfYear, then the previous definition of equal will be legal.

A friend function of a class is not a member function of the class, but a friend function has access to the private members of that class just as a member function does. A friend function can directly read the value of a member variable and can even directly change the value of a member variable, for example, with an assignment statement that has a private member variable on one side of the assignment operator. To make a function a friend function, you must name it as a friend in the class definition. For example, in Display 11.2 we have rewritten the definition of the class DayOfYear so that the function equal is a friend of the class. You make a function a friend of a class by listing the function declaration in the definition of the class and placing the keyword friend in front of the function declaration.

A friend function is added to a class definition by listing its function declaration, just as you would list the declaration of a member function, except that you precede the function declaration by the keyword friend. However, a friend is not a member function; rather, it really is an ordinary function with extraordinary access to the data members of the class. The friend is defined and called exactly like the ordinary function it is. In

![](bbox=[0.071, 0.593, 0.194, 0.625])

![](bbox=[0.071, 0.814, 0.194, 0.847])
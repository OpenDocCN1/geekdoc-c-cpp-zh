# Classes, Pointers, and Dynamic Arrays

The copy constructor defines what it means to plug in the argument sample for the call-by-value parameter named parameter, so that now the picture is as follows:

![](bbox=[0.347, 0.153, 0.652, 0.238])

Thus, any change that is made to parameter.a has no effect on the argument sample, and there are no problems with the destructor. If the destructor is called and then called for sample, each call to the destructor defines a different dynamic array.

When a function returns a value of class type, the copy constructor is called automatically to copy the value specified by the return statement. If there is no copy constructor, problems similar to what we described for call-by-value parameters will occur.

If a class definition involves pointers and dynamically allocates memory using the new operator, you must include a copy constructor. Classes that do not involve pointers or dynamically allocated memory do not need to define a copy constructor.

Contrary to what you might expect, the copy constructor is not called when you set one object to another using the assignment operator. However, if you do not like what the default assignment operator does, you can redefine the assignment operator as we have done in Displays 10.10 and 10.11.

> Copy Constructor
A copy constructor is a constructor that has one call-by-reference parameter that is of the same type as the class. The one parameter must be a call-by-reference parameter; normally, the parameter is also a constant parameter—that, it is preceded by the const parameter modifier. The copy constructor for a class is called automatically whenever a function returns a value of the class type. The copy constructor is also called whenever an argument is plugged in for a call-by-value parameter of the class type. A copy constructor can also be used in the same ways as other constructors.
Any class that uses pointers and the new operator should have a copy constructor.

⁶C++ makes a distinction between initialization (the three cases where the copy constructor is called) and assignment. Initialization uses the copy constructor to create a new object; the assignment operator takes an existing object and modifies it so that it is an identical copy (in all location) of the right-hand side of the assignment.
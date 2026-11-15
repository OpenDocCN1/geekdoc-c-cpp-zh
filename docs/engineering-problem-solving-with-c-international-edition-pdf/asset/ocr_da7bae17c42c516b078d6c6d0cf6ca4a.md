The constructors and overloaded operators declared in the Point class declaration are methods or member functions of the Point class. Recall from Chapter 2 that methods define the operations that can be performed on a class object. The current definition of our Point class has a very limited set of operations. An application can declare and initialize Point objects using either of the two constructor methods, but an application does not have access to the attributes of Point objects. Thus, once a Point object is initialized, its value cannot be modified, and the value of the private attributes cannot be accessed by the application. In this section, we will define a set of accessor methods and a set of mutator methods to provide a better public interface for our user-defined data type, Point.

# Public Interface

The public interface of a well-designed data type provides a complete, yet minimal, set of public methods and hides the implementation of the data type through encapsulation. Encapsulation requires that direct access to the class attributes be restricted to the member functions defined within the class and friend functions. The keyword friend will be discussed in Chapter 10. Encapsulation and a good public interface allow for efficient maintenance and expansion of a data type. We have used the keyword private in the Point class declaration to restrict access to the attributes. Thus, with the current public interface, an application cannot access or modify the value of a Point object. Consider the test program shown below:

```
#include <iostream>
#include " Point.h"
using namespace std;
int main()
{
    Point p1;
    cout << p1.xCoord << endl;
    return 0;
}
```

This program attempts to print the value of the private data member, xCoord, of the Point object p1. The syntax p1.xCoord is correct, but the compiler will generate an error message in this case because xCoord is a private attribute. The error message generated when this program was compiled using the g++ compiler on a MacBook Pro is shown below.

![](bbox=[0.14, 0.71, 0.2, 0.77])

```
Ingers-MacBook-Pro:Programs jaingber$ g++ main.cpp Point.cpp
Point.h: In function 'int main()':
Point.h:9: error: 'double Point::xCoord' is private
main.cpp:7: error: within this context
```

A good public interface requires a complete set of public methods to support the private attributes of the class. Since our Point class has two private attributes, we will add four additional methods to our public interface: two accessor methods and two mutator methods. The expanded class declaration is given below.
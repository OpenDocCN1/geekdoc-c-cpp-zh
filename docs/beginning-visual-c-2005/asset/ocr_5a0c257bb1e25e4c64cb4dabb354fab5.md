With this definition for the function, the program would be exactly the same as the original. This enables you to put the member function definitions outside of the class definition, if you so choose, and still retain the execution performance benefits of inlining.

You can apply the keyword `inline` to ordinary functions in your program that have nothing to do with classes and get the same effect. Remember, however, that it’s best used for short, simple functions.

You now need to understand a little more about what happens when you declare an object of a class.

# Class Constructors

In the previous program example, you declared the CBox objects, box1 and box2, and then laboriously worked through each of the data members for each object in order to assign an initial value to it. This is unsatisfactory from several points of view. First of all, it would be easy to overlook initializing a data member, particularly with a class which had many more data members than our CBox class. Initializing the data members of several objects of a complex class could involve pages of assignment statements. The final constraint on this approach arises when you get to defining data members of a class that don’t have the attribute public — you won’t be able to access them from outside the class anyway. There has to be a better way, and of course there is — it’s known as the class constructor.

# What Is a Constructor?

A class constructor is a special function in a class which is called when a new object of the class is created. It therefore provides the opportunity to initialize objects as they are created and to ensure that data members only contain valid values. A class may have several constructors enabling you to create objects in various ways.

You have no leeway in naming the constructors in a class — they always have the same name as the class in which they are defined. The function CBox(), for example, is a constructor for our class CBox. It also has no return type. It’s wrong to specify a return type for a constructor; you must not even write it as void. The primary purpose of a class constructor is to assign initial values to the data elements of the class, and no return type for a constructor is necessary or permitted.

# Try It Out Adding a Constructor to the CBox class

Let’s extend our CBox class to incorporate a constructor.

```
// Ex7_04.cpp
// Using a constructor
#include <iostream>
using std::cout;
using std::endl;

class CBox        // Class definition at global scope
{
    public:
        double m_Length;        // Length of a box in inches
        double m_Width;         // Width of a box in inches
        double m_Height;        // Height of a box in inches
```
You then have a statement that calculates the volume of box1 as the product of its three data members, and this value is output to the screen. Next, you output the sum of the data members of box2 by writing the expression for the sum of the data members directly in the output statement. The final action in the program is to output the number of bytes occupied by box1, which is produced by the operator sizeof.

If you run this program, you should get this output:

```
Volume of box1 = 33696
box2 has sides which total 66.5 inches.
A CBox object occupies 24 bytes.
```

The last line shows that the object box1 occupies 24 bytes of memory, which is a result of having 3 data members of 8 bytes each. The statement that produced the last line of output could equally well have been written like this:

```
cout << endl                 // Display the size of a box in memory
    << "A CBox object occupies "
    << sizeof (CBox) << " bytes.";
```

Here, I have used the type name between parentheses, rather than a specific object name as the operand for the sizeof operator. You’ll remember that this is standard syntax for the sizeof operator, as you saw in Chapter 4.

This example has demonstrated the mechanism for accessing the public data members of a class. It also shows that they can be used in exactly the same way as ordinary variables. You are now ready to break new ground by taking a look at member functions of a class.

# Member Functions of a Class

A member function of a class is a function that has its definition or its prototype within the class definition. It operates on any object of the class of which it is a member, and has access to all the members of a class for that object.

# Try It Out   Adding a Member Function to CBox

To see how you access the members of the class from within a function member, create an example extending the CBox class to include a member function that calculates the volume of the CBox object.

```
// Ex7_03.cpp
// Calculating the volume of a box with a member function
#include <iostream>
using std::cout;
using std::endl;

class CBox                         // Class definition at global scope
{
public:
    double m_Length;               // Length of a box in inches
    double m_Width;                // Width of a box in inches
    double m_Height;               // Height of a box in inches
```
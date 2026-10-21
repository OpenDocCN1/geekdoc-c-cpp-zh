
## Class Inheritance and Virtual Functions

```cpp
cout << endl << "CBox copy constructor called";
m_Length = initB.m_Length;
m_Width = initB.m_Width;
m_Height = initB.m_Height;
}
```

```cpp
// CBox destructor - just to track calls
~CBox()
{ cout << "CBox destructor called" << endl; }

protected:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

Also recall that the copy constructor must have its parameter specified as a reference to avoid an infinite number of calls to itself, which would otherwise result from the need to copy an argument that is transferred by value. When the copy constructor in our example is invoked, it outputs a message to the screen, so you’ll be able to see from the output when this is happening.

We will use the version of CCandyBox class from Ex9_04.cpp, shown again here:

```cpp
// CandyBox.h in Ex9_05
#pragma once
#include "Box.h"
#include <iostream>
using std::cout;
using std::endl;

class CCandyBox: public CBox
{
public:
    char* m_Contents;

    // Derived class function to calculate volume
    double Volume() const
    { return m_Length*m_Width*m_Height; }

    // Constructor to set dimensions and contents
    // with explicit call of CBox constructor
    CCandyBox(double lv, double wv, double hv, char* str = "Candy")
        :CBox(lv, wv, hv)  // Constructor
    {
        cout << endl <<"CCandyBox constructor2 called";
        m_Contents = new char[ strlen(str) + 1 ];
        strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    // Constructor to set contents
    // calls default CBox constructor automatically
    CCandyBox(char* str = "Candy")           // Constructor
    {
        cout << endl << "CCandyBox constructor1 called";
        m_Contents = new char[ strlen(str) + 1 ];
        strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    ~CCandyBox()                         // Destructor
    {
        cout << "CCandyBox destructor called" << endl;
        delete[] m_Contents;
    };
};
```

This doesn’t have a copy constructor added yet, so you’ll be relying on the compiler-generated version.

### Try It Out    The Copy Constructor in Derived Classes

You can exercise the copy constructor that you have just defined with the following example:

```cpp
// Ex9_05.cpp
// Using a derived class copy constructor
#include <iostream>                // For stream I/O
#include <cstring>                 // For strlen() and strcpy()
#include "CCandyBox.h"             // For CBox and CCandyBox
using std::cout;
using std::endl;

int main()
{
    CCandyBox chocBox(2.0, 3.0, 4.0, "Chockies");  // Declare and initialize
    CCandyBox chocolateBox(chocBox);               // Use copy constructor

    cout << endl
         << "Volume of chocBox is " << chocBox.Volume()
         << endl
         << "Volume of chocolateBox is " << chocolateBox.Volume()
         << endl;

    return 0;
}
```

### How It Works (or Why It Doesn’t)

When you run the Debug version of this example, in addition to the expected output, you’ll see the dialog shown in Figure 9-4 displayed.

Click Abort to clear the dialog box and you’ll see the output in the console window that you might expect. The output shows that the compiler-generated copy constructor for the derived class automatically called the copy constructor for the base class.

![](img/2359b0c604600c58fba3539c738a356e_534_0.png)

Figure 9-4

However, as you’ve probably realized, all is not as it should be. In this particular case, the compiler-generated copy constructor causes problems because the memory pointed to by the m_Contents member of the derived class in the second object declared points to the same memory as the one in the first object. When one object is destroyed (when it goes out of scope at the end of main()), it releases the memory occupied by the text. When the second object is destroyed, the destructor attempts to release some memory that has already been freed by the destructor call for the previous object—and that’s the reason for the error message in the dialog box.

The way to fix this is to supply a copy constructor for the derived class that allocates some additional memory for the new object.

### Try It Out   Fixing the Copy Constructor Problem

You can do this by adding the following code for the copy constructor to the public section of the derived CCandyBox class in Ex9_05:

```cpp
// Derived class copy constructor
CCandyBox(const CCandyBox& initCB)
{
    cout << endl << "CCandyBox copy constructor called";

    // Get new memory
    m_Contents = new char[ strlen(initCB.m_Contents) + 1 ];

    // Copy string
    strcpy_s(m_Contents, strlen(initCB.m_Contents) + 1, initCB.m_Contents);
}
```

You can now run this new version of the last example with the same function main() to see how the new copy constructor works.

### How It Works

Now when you run the example, it behaves better and produces the following output:

```text
CBox constructor called
CCandyBox constructor2 called
CBox constructor called
CCandyBox copy constructor called
Volume of chocBox is 24
Volume of chocolateBox is 1
CCandyBox destructor called
CBox destructor called
CCandyBox destructor called
CBox destructor called
```

However, there is still something wrong. The third line of output shows that the default constructor for the CBox part of the object chocolateBox is called, rather than the copy constructor. As a consequence, the object has the default dimensions rather than the dimensions of the initializing object, so the volume is incorrect. The reason for this is that when you write a constructor for an object of a derived class, you are responsible for ensuring that the members of the derived class object are properly initialized. This includes the inherited members.

The fix for this is to call the copy constructor for the base part of the class in the initialization list for the copy constructor for the CCandyBox class. The copy constructor then becomes:

```cpp
// Derived class copy constructor
CCandyBox(const CCandyBox& initCB): CBox(initCB)
{
    cout << endl << "CCandyBox copy constructor called";

    // Get new memory
    m_Contents = new char[ strlen(initCB.m_Contents) + 1 ];

    // Copy string
    strcpy_s(m_Contents, strlen(initCB.m_Contents) + 1, initCB.m_Contents);
}
```

Now the CBox class copy constructor is called with the initCB object. Only the base part of the object is passed to it, so everything works out. If you modify the last example by adding the base copy constructor call, the output is as follows:

```text
CBox constructor called
CCandyBox constructor2 called
CBox copy constructor called
CCandyBox copy constructor called
Volume of chocBox is 24
Volume of chocolateBox is 24
CCandyBox destructor called
CBox destructor called
CCandyBox destructor called
CBox destructor called
```

The output shows that all the constructors and destructors are called in the correct sequence and the copy constructor for the CBox part of chocolateBox is called before the CCandyBox copy constructor. The volume of the object chocolateBox of the derived class is now the same as that of its initializing object, which is as it should be.

You have, therefore, another golden rule to remember:

> If you write any kind of constructor for a derived class, you are responsible for the initialization of all members of the derived class object, including all its inherited members.

## Class Members as Friends

You saw in Chapter 7 how a function can be declared as a friend of a class. This gives the friend function the privilege of free access to any of the class members. Of course, there is no reason why a friend function cannot be a member of another class.

Suppose you define a CBottle class to represent a bottle:

```cpp
class CBottle
{
public:
    CBottle(double height, double diameter)
    {
        m_Height = height;
        m_Diameter = diameter;
    }

private:
    double m_Height;            // Bottle height
    double m_Diameter;          // Bottle diameter
};
```

You now need a class to represent the packaging for a dozen bottles that automatically has custom dimensions to accommodate a particular kind of bottle. You could define this as:

```cpp
class CCarton
{
public:
    CCarton(const CBottle& aBottle)
    {
        m_Height = aBottle.m_Height;        // Bottle height
        m_Length = 4.0*aBottle.m_Diameter;  // Four rows of ...
        m_Width = 3.0*aBottle.m_Diameter;   // ...three bottles
    }

private:
    double m_Length;    // Carton length
    double m_Width;     // Carton width
    double m_Height;    // Carton height
};
```

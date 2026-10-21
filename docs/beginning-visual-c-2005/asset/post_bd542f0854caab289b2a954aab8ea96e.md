
## Class Inheritance and Virtual Functions

```cpp
// Calling the base class constructor
CCandyBox(double lv, double wv, double hv, char* str = "Candy"):
CBox(lv, wv, hv)
{
    ...
}
```

This is perfectly consistent with what you are doing here because you are essentially initializing a CBox sub-object of the derived class object. In the first case, you are explicitly calling the default constructor for the double members m_Length, m_Width and m_Height in the initialization list. In the second instance, you are calling the constructor for CBox. This causes the specific CBox constructor you have chosen to be called before the CCandyBox constructor is executed.

If you build and run this example, it produces the output shown as follows:

```
CBox constructor called
CBox constructor called
CBox constructor1 called
CBox constructor called
CBox constructor2 called
myBox occupies 24 bytes
myCandyBox occupies 32 bytes
myMintBox occupies 32 bytes
myMintBox volume is 6
```

| Screen output | Object being constructed |
|---------------|-------------------------|
| CBox constructor called | MyBox |
| CBox constructor called | MyCandyBox |
| CBox constructor1 called | MyCandyBox |
| CBox constructor called | MyMintBox |
| CBox constructor2 called | MyMintBox |

The first line of output is due to the CBox class constructor call, originating from the declaration of the CBox object, myBox. The second line of output arises from the automatic call of the base class constructor caused by the declaration of the CCandyBox object myCandyBox.

> *Notice how the base class constructor is always called before the derived class constructor.*

The following line is due to your version of the default derived class constructor being called for the myCandyBox object. This constructor is invoked because the object is not initialized. The fourth line of output arises from the explicit identification of the CBox class constructor to be called in our new constructor for CCandyBox objects. The argument values specified for the dimensions of the CCandyBox object are passed to the base class constructor. Next comes the output from the new derived class constructor itself, so constructors are again called for the base class first, followed by the derived class.

It should be clear from what you have seen up to now that when a derived class constructor is executed, a base class constructor is always called to construct the base part of the derived class object. If you don’t specify the base class constructor to be used, the compiler arranges for the default base class constructor to be called.

The last line in the table shows that the initialization of the base part of the myMintBox object is working as it should be, with the private members having been initialized by the CBox class constructor.

Having the private members of a base class only accessible to function members of the base class isn’t always convenient. There will be many instances where you want to have private members of a base class that can be accessed from within the derived class. As you surely have anticipated by now, C++ provides a way to do this.

## Declaring Class Members to be Protected

In addition to the public and private access specifiers for members of a class, you can also declare members of a class as protected. Within the class, the protected keyword has the same effect as the private keyword: members of a class that are protected can only be accessed by member functions of the class, and by friend functions of the class (also by member functions of a class that is declared as a friend of the class — you will learn about friend classes later in this chapter). Using the protected keyword, you could redefine the CBox class as follows:

```
// Box.h in Ex9_04
#pragma once
#include <iostream>
using std::cout;
using std::endl;

class CBox
{
public:
    // Base class constructor
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0):
        m_Length(lv), m_Width(wv), m_Height(hv)
    { cout << endl << "CBox constructor called"; }
```

```
// CBox destructor - just to track calls
~CBox()
{ cout << "CBox destructor called" << endl; }
```

```
protected:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

Now the data members are still effectively private, in that they can’t be accessed by ordinary global functions, but they’ll still be accessible to member functions of a derived class.

## Try It Out    Using Protected Members

You can demonstrate the use of protected data members by using this version of the class CBox to derive a new version of the class CCandyBox, which accesses the members of the base class through its own member function, Volume():

```
// CandyBox.h in Ex9_04
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
    CCandyBox(char* str = "Candy")                 // Constructor
    {
        cout << endl << "CCandyBox constructor1 called";
        m_Contents = new char[ strlen(str) + 1 ];
        strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    ~CCandyBox()                                 // Destructor
    {
        cout << "CCandyBox destructor called" << endl;
        delete[] m_Contents;
    }
};
```

The code for main() in Ex9_04.cpp is:

```
// Ex9_04.cpp
// Using the protected access specifier
#include <iostream>                 // For stream I/O
```

```
error C2248: 'm_Length' : cannot access protected member declared in class 'CBox'
```

which indicates quite clearly that the member m_Length is inaccessible.

## The Access Level of Inherited Class Members

You know that if you have no access specifier for the base class in the definition of a derived class, the default specification is private. This has the effect of causing the inherited public and protected members of the base class to become private in the derived class. The private members of the base class remain private to the base and therefore inaccessible to member functions of the derived class. In fact, they remain private to the base class regardless of how the base class is specified in the derived class definition.

You have also used public as the specifier for a base class. This leaves the members of the base class with the same access level in the derived class as they had in the base, so public members remain public and protected members remain protected.

The last possibility is that you declare a base class as protected. This has the effect of making the inherited public members of the base protected in the derived class. The protected (and private) inherited members retain their original access level in the derived class. This is summarized in Figure 9-3.

![](img/2359b0c604600c58fba3539c738a356e_530_0.png)

Figure 9-3

This may look a little complicated, but you can reduce it to the following three points about the inherited members of a derived class:

- Members of a base class that are declared as `private` are never accessible in a derived class
- Defining a base class as `public` doesn’t change the access level of its members in the derived class
- Defining a base class as `protected` changes its `public` members to `protected` in the derived class

Being able to change the access level of inherited members in a derived class gives you a degree of flexibility, but don’t forget that you cannot relax the level specified in the base class; you can only make the access level more stringent. This suggests that your base classes need to have `public` members if you want to be able to vary the access level in derived classes. This may seem to run contrary to the idea of encapsulating data in a class in order to protect it from unauthorized access, but, as you’ll see, it is often the case that you define base classes in such a manner that their only purpose is to act as a base for other classes, and they aren’t intended to be used for instantiating objects in their own right.

## The Copy Constructor in a Derived Class

Remember that the copy constructor is called automatically when you declare an object that is initialized with an object of the same class. Look at these statements:

```
CBox myBox(2.0, 3.0, 4.0);          // Calls constructor
CBox copyBox(myBox);                // Calls copy constructor
```

The first statement calls the constructor that accepts three arguments of type `double`, and the second calls the copy constructor. If you don’t supply your own copy constructor, the compiler supplies one that copies the initializing object member by member to the corresponding members of the new object. So that you can see what is going on during execution, you can add your own version of a copy constructor to the class CBox. You can then use this class as a base for defining the CCandyBox class.

```
// Box.h in Ex9_05
#pragma once
#include <iostream>
using std::cout;
using std::endl;

class CBox                         // Base class definition
{
public:
    // Base class constructor
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0):
        m_Length(lv), m_Width(wv), m_Height(hv)
    { cout << endl << "CBox constructor called"; }

    // Copy constructor
    CBox(const CBox& initB)
    {
```

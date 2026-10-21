
// Version of the classes that will not compile
class CBox
{
public:
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0):
        m_Length(lv), m_Width(wv), m_Height(hv) {}

private:
    double m_Length;
    double m_Width;
    double m_Height;
};

class CCandyBox: public CBox
{
public:
    char* m_Contents;

    // Function to calculate the volume of a CCandyBox object
    double Volume() const        // Error - members not accessible
    { return m_Length*m_Width*m_Height; }

    CCandyBox(char* str = "Candy")    // Constructor
    {
        m_Contents = new char[ strlen(str) + 1 ];
        strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    ~CCandyBox()                // Destructor
    { delete[] m_Contents; }
};

A program using these classes does not compile. The function Volume() in the class CCandyBox attempts to access the private members of the base class, which is not legal.

## Try It Out    Accessing Private Members of the Base Class

It is, however, legal to use the Volume() function in the base class, so if you move the definition of the function Volume() to the public section of the base class, CBox, not only will the program compile but you can use the function to obtain the volume of a CCandyBox object. Create a new WIN32 project, Ex9_02, with the Box.h contents as the following:

```
// Box.h in Ex9_02
#pragma once

class CBox
{
public:
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0):
```

## Class Inheritance and Virtual Functions

```
m_Length(lv), m_Width(wv), m_Height(hv) {

    //Function to calculate the volume of a CBox object
    double Volume() const
    { return m_Length*m_Width*m_Height; }

    private:
        double m_Length;
        double m_Width;
        double m_Height;
};
```

The CandyBox.h header in the project contains:

```
// Header file CandyBox.h in project Ex9_02
#pragma once
#include "Box.h"
class CCandyBox: public CBox
{
public:
    char* m_Contents;

    CCandyBox(char* str = "Candy")                 // Constructor
    {
        m_Contents = new char[ strlen(str) + 1 ];
        strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    ~CCandyBox()                                    // Destructor
    { delete[] m_Contents; };
};
```

The Ex9_02.cpp file in the project contains:

```
// Ex9_02.cpp
// Using a function inherited from a base class
#include <iostream>                         // For stream I/O
#include <cstring>                          // For strlen() and strcpy()
#include "CandyBox.h"                       // For CBox and CCandyBox
using std::cout;
using std::endl;

int main()
{
    CBox myBox(4.0,3.0,2.0);                     // Create CBox object
    CCandyBox myCandyBox;                       // Create CCandyBox object
    CCandyBox myMintBox("Wafer Thin Mints");   // Create CCandyBox object

    cout << endl
         << "myBox occupies " << sizeof myBox     // Show how much memory
         << " bytes" << endl                     // the objects require
         << "myCandyBox occupies " << sizeof myCandyBox

    << " bytes" << endl
    << "myMintBox occupies " << sizeof myMintBox
    << " bytes";
    cout << endl
        << "myMintBox volume is " << myMintBox.Volume(); // Get volume of a
        // CCandyBox object
    cout << endl;
    return 0;
}
```

This example produces the following output:

```
myBox occupies 24 bytes
myCandyBox occupies 32 bytes
myMintBox occupies 32 bytes
    myMintBox volume is 1
```

## How It Works

The interesting additional output is the last line. This shows the value produced by the function Volume(), which is now in the public section of the base class. Within the derived class, it operates on the members of the derived class that are inherited from the base. It is a full member of the derived class, so it can be used freely with objects of the derived class.

The value for the volume of the derived class object is 1 because, in creating the CCandyBox object, the CBox() default constructor was called first to create the base class part of the object, and this sets default CBox dimensions to 1.

## Constructor Operation in a Derived Class

Although I said the base class constructors are not inherited in a derived class, they still exist in the base class and are used for creating the base part of a derived class object. This is because creating the base class part of a derived class object is really the business of a base class constructor, not the derived class constructor. After all, you have seen that private members of a base class are inaccessible in a derived class object, even though they are inherited, so responsibility for these has to lie with the base class constructors.

The default base class constructor was called automatically in the last example to create the base part of the derived class object, but this doesn’t have to be the case. You can arrange to call a particular base class constructor from the derived class constructor. This enables you to initialize the base class data members with a constructor other than the default, or indeed to choose to call a particular class constructor, depending on the data supplied to the derived class constructor.

## Try It Out  Calling Constructors

You can see this in action through a modified version of the previous example. To make the class usable, you really need to provide a constructor for the derived class that allows you to specify the dimensions of the object. You can add an additional constructor in the derived class to do this, and call the base class constructor explicitly to set the values of the data members that are inherited from the base class.

In the Ex9_03 project, Box.h contains:

```
// Box.h in Ex9_03
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

    //Function to calculate the volume of a CBox object
    double Volume() const
    { return m_Length*m_Width*m_Height; }

private:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

The CandyBox.h header file should contain:

```
// CandyBox.h in Ex9_03
#pragma once
#include <iostream>
#include "Box.h"
using std::cout;
using std::endl;

class CCandyBox: public CBox
{
public:
    char* m_Contents;

    // Constructor to set dimensions and contents
    // with explicit call of CBox constructor
    CCandyBox(double lv, double wv, double hv, char* str = "Candy")
        :CBox(lv, wv, hv)
    {
    cout << endl <<"CCandyBox constructor2 called";
    m_Contents = new char[ strlen(str) + 1 ];
    strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    // Constructor to set contents
    // calls default CBox constructor automatically
    CCandyBox(char* str = "Candy")
    {

## Chapter 9

```
cout << endl << "CCandyBox constructor1 called";
    m_Contents = new char[ strlen(str) + 1 ];
    strcpy_s(m_Contents, strlen(str) + 1, str);
}
```

```
~CCandyBox()
    // Destructor
{ delete[] m_Contents; }
};
```

The #include directive for the <iostream> header and the two using declarations are not strictly necessary here because Box.h contains the same code, but it does no harm to put them in. On the contrary, putting these statements in here also means that if you were to remove this code from Box.h because it was no longer required there, CandyBox.h still compiles.

The contents of Ex9_03.cpp is:

```
// Ex9_03.cpp
// Calling a base constructor from a derived class constructor
#include <iostream>                // For stream I/O
#include <cstring>                 // For strlen() and strcpy()
#include "CandyBox.h"              // For CBox and CCandyBox
using std::cout;
using std::endl;

int main()
{
    CBox myBox(4.0, 3.0, 2.0);
    CCandyBox myCandyBox;
    CCandyBox myMintBox(1.0, 2.0, 3.0, "Wafer Thin Mints");

    cout << endl
        << "myBox occupies " << sizeof myBox      // Show how much memory
        << " bytes" << endl                     // the objects require
        << "myCandyBox occupies " << sizeof myCandyBox
        << " bytes" << endl
        << "myMintBox occupies " << sizeof myMintBox
        << " bytes";
    cout << endl
        << "myMintBox volume is "               // Get volume of a
        << myMintBox.Volume();                 // CCandyBox object
    cout << endl;
    return 0;
}
```

## How It Works

As well as adding the additional constructor in the derived class, you have added an output statement in each constructor so you know when either gets called. The explicit call of the constructor for the CBox class appears after a colon in the function header of the derived class constructor. You have perhaps noticed that the notation is exactly the same as what you have been using for initializing members in a constructor anyway:


# Chapter 9

The constructor here sets the height to be the same as that of the bottle it is to accommodate, and the length and width are set based on the diameter of the bottle so that twelve fit in the box.

As you know by now, this won’t work. The data members of the CBottle class are private, so the CCarton constructor cannot access them. As you also know, a friend declaration in the CBottle class fixes it:

```
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

    // Let the carton constructor in
    friend CCarton::CCarton(const CBottle& aBottle);
};
```

The only difference between the friend declaration here and what you saw in Chapter 7 is that you must put the class name and the scope resolution operator with the friend function name to identify it. For this to compile correctly, the compiler needs to have information about the CCarton class constructor, so you would need to put an #include statement for the header file containing the CCarton class definition before the definition of the CBottle class.

## Friend Classes

You can also allow all the function members of one class to have access to all the data members of another by declaring it as a friend class. You could define the CCarton class as a friend of the CBottle class by adding a friend declaration within the CBottle class definition:

```
friend CCarton;
```

With this declaration in the CBottle class, all function members of the CCarton class now have free access to all the data members of the CBottle class.

## Limitations on Class Friendship

Class friendship is not reciprocated. Making the CCarton class a friend of the CBottle class does not mean that the CBottle class is a friend of the CCarton class. If you want this to be so, you must add a friend declaration for the CBottle class to the CCarton class.

Class friendship is also not inherited. If you define another class with CBottle as a base, members of the CCarton class will not have access to its data members, not even those inherited from CBottle.

## Virtual Functions

Look more closely at the behavior of inherited member functions and their relationship with derived class member functions. You could add a function to the CBox class to output the volume of a CBox object. The simplified class then becomes:

```
// Box.h in Ex9_06
#pragma once
#include <iostream>
using std::cout;
using std::endl;

class CBox  // Base class
{
public:
    // Function to show the volume of an object
    void ShowVolume() const
    {
        cout << endl << "CBox usable volume is " << Volume();
    }

    // Function to calculate the volume of a CBox object
    double Volume() const
    {
        return m_Length*m_Width*m_Height;
    }

    // Constructor
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0)
    :m_Length(lv), m_Width(wv), m_Height(hv) {}

protected:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

Now you can output the usable volume of a CBox object just by calling the ShowVolume() function for any object for which you require it. The constructor sets the data member values in the initialization list, so no statements are necessary in the body of the function. The data members are as before and are specified as protected, so they are accessible to the member functions of any derived class.

Suppose you want to derive a class for a different kind of box called CGlassBox, to hold glassware. The contents are fragile, and because packing material is added to protect them, the capacity of the box is less than the capacity of a basic CBox object. You therefore need a different Volume() function to account for this, so you add it to the derived class:

```
// GlassBox.h in Ex9_06
#pragma once
#include "Box.h"

class CGlassBox: public CBox  // Derived class
{
public:
    // Constructor
    CGlassBox(double lv = 1.0, double wv = 1.0, double hv = 1.0)
    : CBox(lv, wv, hv) {}

    // Function to calculate the volume of a CGlassBox object
    double Volume() const
    {
        return 0.8 * CBox::Volume();
    }
};
```

# Chapter 9

```
// Function to calculate volume of a CGlassBox
// allowing 15% for packing
double Volume() const
{ return 0.85*m_Length*m_Width*m_Height; }

// Constructor
CGlassBox(double lv, double wv, double hv): CBox(lv, wv, hv){}
};
```

There could conceivably be other additional members of the derived class, but we’ll keep it simple and concentrate on how the inherited functions work for the moment. The constructor for the derived class objects just calls the base class constructor in its initialization list to set the data member values. No statements are necessary in its body. You have included a new version of the Volume() function to replace the version from the base class, the idea being that you can get the inherited function ShowVolume() to call the derived class version of the member function Volume() when you call it for an object of the class CGlassBox.

## Try It Out Using an Inherited Function

Now see how your derived class works in practice. You can try this out very simply by creating an object of the base class and an object of the derived class with the same dimensions and then verifying that the correct volumes are being calculated. The main() function to do this is as follows:

```
// Ex9_06.cpp
// Behavior of inherited functions in a derived class
#include <iostream>
#include "GlassBox.h"                // For CBox and CGlassBox
using std::cout;
using std::endl;

int main()
{
    CBox myBox(2.0, 3.0, 4.0);           // Declare a base box
    CGlassBox myGlassBox(2.0, 3.0, 4.0); // Declare derived box - same size

    myBox.ShowVolume();                 // Display volume of base box
    myGlassBox.ShowVolume();            // Display volume of derived box

    cout << endl;
    return 0;
}
```

## How It Works

If you run this example, it produces the following output:

```
CBox usable volume is 24
CBox usable volume is 24
```

This isn’t only dull and repetitive, it’s also disastrous. It isn’t working the way you want at all, and the only interesting thing about it is why. Evidently, the fact that the second call is for an object of the

derived class CGlassBox is not being taken into account. You can see this from the incorrect result for the volume in the output. The volume of a CGlassBox object should definitely be less than that of a basic CBox with the same dimensions.

The reason for the incorrect output is that the call of the Volume() function in the function ShowVolume() is being set once and for all by the compiler as the version defined in the base class. ShowVolume() is a base class function and when CBox is compiled the call to Volume() is resolved at that time to the base class Volume() function; the compiler has no knowledge of any other Volume() function. This is called static resolution of the function call since the function call is fixed before the program is executed. This is also sometimes called early binding because the particular Volume() function chosen is bound to the call from the function ShowVolume() during the compilation of the program.

What we were hoping for in this example was that the question of which Volume() function call to use in any given instance would be resolved when the program was executed. This sort of operation is referred to as dynamic linkage, or late binding. We want the actual version of the function Volume() called by ShowVolume() to be determined by the kind of object being processed, and not arbitrarily fixed by the compiler before the program is executed.

No doubt you’ll be less than astonished that C++ does, in fact, provide you with a way to do this, because this whole discussion would have been futile otherwise! You need to use something called a virtual function.

## What Is a Virtual Function?

A virtual function is a function in a base class that is declared using the keyword virtual. If you specify a function in a base class as virtual and there is another definition of the function in a derived class, it signals to the compiler that you don’t want static linkage for this function. What you do want is the selection of the function to be called at any given point in the program to be based on the kind of object for which it is called.

## Try It Out   Fixing the CGlassBox

To make this example work as originally hoped, you just need to add the keyword virtual to the definitions of the Volume() function in the two classes. You can try this in a new project, Ex9_07. Here’s how the definition of CBox should be:

```
// Box.h in Ex9_07
#pragma once
#include <iostream>
using std::cout;
using std::endl;

class CBox
                        // Base class
{
public:
    // Function to show the volume of an object
    void ShowVolume() const
    {
        cout << endl
            << "CBox usable volume is " << Volume();
```

an object, and you want it initialized before any object is created. The answer is to write the initialization of the static data member outside of the class definition with this statement:

```
int CBox::objectCount = 0;    // Initialize static member of class CBox
```

> Notice that the static keyword is not included here; however, you do need to qualify the member name by using the class name and the scope resolution operator so that the compiler understands that you are referring to a static member of the class. Otherwise, you would simply create a global variable that was nothing to do with the class.

# Try It Out Counting Instances

Let's add the static data member and the object counting capability to the last example.

```
// Ex7_12.cpp
// Using a static data member in a class
#include <iostream>
using std::cout;
using std::endl;

class CBox                 // Class definition at global scope
{
public:
    static int objectCount;           // Count of objects in existence

    // Constructor definition
    CBox(double lv, double bv = 1.0, double hv = 1.0)
    {
        cout << endl << "Constructor called.";
        m_Length = lv;                 // Set values of
        m_Width = bv;                  // data members
        m_Height = hv;
        objectCount++;
    }

    CBox()                         // Default constructor
    {
        cout << endl
             << "Default constructor called.";
        m_Length = m_Width = m_Height = 1.0;
        objectCount++;
    }

    // Function to calculate the volume of a box
    double Volume() const
    {
        return m_Length*m_Width*m_Height;
    }

private:
    double m_Length;                // Length of a box in inches
    double m_Width;                 // Width of a box in inches
    double m_Height;                // Height of a box in inches
```
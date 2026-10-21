```
// Divide one box into another
int CBox::operator/(const CBox& aBox) const
{
    // Temporary for number in horizontal plane this way
    int tc1 = 0;
    // Temporary for number in a plane that way
    int tc2 = 0;

    tc1 = static_cast<int>((m_Length/aBox.m_Length)) *
        static_cast<int>((m_Width/aBox.m_Width));    // to fit this way

    tc2 = static_cast<int>((m_Length/aBox.m_Width)) *
        static_cast<int>((m_Width/aBox.m_Length));    // and that way

    //Return best fit
    return static_cast<int>((m_Height/aBox.m_Height))*(tc1>tc2 ? tc1 : tc2);
}
```

The shaded lines are those that you should have modified or added manually.

The very short functions, particularly those that just return the value of a data member, have their definitions within the class definition so that they are inline. If you take a look at Class View by clicking the tab and then click the + beside the CBox class name, you'll see that all the members of the class are shown in the lower pane.

This completes the CBox class, but you still need to define the global functions that implement operators to compare the volume of a CBox object with a numerical value.

# Adding Global Functions

You need to create a .cpp file that will contain the definitions for the global functions supporting operations on CBox objects. The file also needs to be part of the project. Click the Solution Explorer tab to display it (you currently will have the Class View tab displayed) and right-click the Source Files folder. Select Add > New Item from the context menu to display the dialog box. Choose the category as Code and the template as C++ File (.cpp) in the right pane of the dialog box and enter the file name as BoxOperators.

You can now enter the following code in the Editor pane:

```
// BoxOperators.cpp
// CBox object operations that don't need to access private members
#include "Box.h"

// Function for testing if a constant is > a CBox object
bool operator>(const double& value, const CBox& aBox)
{ return value > aBox.Volume(); }

// Function for testing if a constant is < CBox object
bool operator<(const double& value, const CBox& aBox)
{ return value < aBox.Volume(); }

// Function for testing if CBox object is > a constant
```
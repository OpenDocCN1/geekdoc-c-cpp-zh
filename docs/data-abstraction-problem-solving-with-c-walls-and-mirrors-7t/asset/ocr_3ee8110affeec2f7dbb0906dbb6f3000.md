not normally contain executable code. For example, here is the header file for the C++ version of the previous Python class:

```
/* @ file PlainBox.h */
#include <string> // Needed because we use string objects.
using namespace std; // Strings are part of the system std library.
class PlainBox // This is a class declaration for PlainBox.
{
private: // Items defined below have private access.
string item; // Items defined below have public access.
public: // Prototypes for constructors and methods:
PlainBox();
PlainBox(string theItem);
void setItem(string theItem);
string getItem();
}; // end PlainBox - Note semi-colon after declaration.
```

Notice that each data member and method does not need to have an access modifier. Private data members and methods are grouped together, and public methods are grouped with each other. A colon follows each access modifier. It is possible to have more than one private, protected, or public section, but it is not common. The class declaration must end with a semi-colon after the closing brace, as shown above.

The implementation file, or source file, for the class typically has the same name as the header file, but ends in .cpp to indicate that it is a C++ file. The implementation file contains the definition for the methods declared in the accompanying header file. Here is the implementation file for the C++ class PlainBox:

```
/* @ file PlainBox.cpp */
#include "PlainBox.h" // We need to tell the compiler about our data
// fields and methods.
PlainBox::PlainBox()
{ // end default constructor
PlainBox::PlainBox(string theItem)
{ // end constructor
void PlainBox::setItem(string theItem)
{ // end setItem
string PlainBox::getItem()
{ return item;
} // end getItem
```

This implementation file begins by including the header file, so that the compiler has the class declaration and knows the data fields and methods of this class. We then define each method. In the implementation file there is no “master” set of braces enclosing all of the methods. Each method is individually defined. To let the compiler know that a method belongs to the PlainBox class, we add
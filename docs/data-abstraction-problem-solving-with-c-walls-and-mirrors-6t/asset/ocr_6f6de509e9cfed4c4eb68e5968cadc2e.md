virtual methods—methods that use the keyword virtual to indicate that they can be overridden.
In the example in Section C2.2, PlainBox is the base class, which we defined in Listing C1-3 of
C++ Interlude 1. The code that we wrote then did not behave as we desired. To correct that problem, we
must declare as virtual the methods of PlainBox that we want other classes to override, as Listing C2-4
shows. Notice that only the header file of the base class (PlainBox) needs to be revised. Declaring
the methods setItem and getItem as virtual makes it possible for the method code to be bound
late.

# LISTING C2-4 Revised header file for the class PlainBox

```
```cpp
/** @file PlainBox.h */
#ifndef _PLAIN_BOX
#define _PLAIN_BOX

template<class ItemType>; // Indicates this is a template

// Declaration for the class PlainBox
class PlainBox
{
private:
   // Data field
   ItemType item;
public:
   // Default constructor
   PlainBox();
   // Parameterized constructor
   PlainBox(const ItemType& theItem);
   // Mutator method that can change the value of the data field
   virtual void setItem(const ItemType& theItem);
   // Accessor method to get the value of the data field
   virtual ItemType getItem() const;
}; // End PlainBox

#include "PlainBox.cpp" // Include the implementation file
#endif
```
```

To fully implement late binding, we must create the variables in the free store and use pointers to
reference them. Thus, we must also change the code from our first example of early binding in
Section C2.2 to

```
```cpp
string specialItem = "Riches beyond compare!";
string otherItem = "Hammer";

PlainBox<string>* myMagicBoxPtr = new PlainBox<string>();
placeInBox(myPlainBoxPtr, specialItem);

MagicBox<string>* myMagicBoxPtr = new MagicBox<string>();
placeInBox(myMagicBoxPtr, otherItem);
placeInBox(myMagicBoxPtr, specialItem);

cout << myMagicBoxPtr->getItem() << endl;
```
```

An example of late binding
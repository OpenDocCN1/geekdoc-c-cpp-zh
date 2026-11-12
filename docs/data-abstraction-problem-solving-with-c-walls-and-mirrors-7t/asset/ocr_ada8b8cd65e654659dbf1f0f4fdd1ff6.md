setItem is the first item we are asked to store. If firstItemStored is true, we know this is not the first item, and we simply do nothing.

Here is the UML notation for our MagicBox methods:

```
+setItem(ItemType theItem)
+getItem(): ItemType
```

These methods are like those in the class PlainBox, but we need a different implementation of setItem to meet the special requirements of this box. Therefore, we need to override the PlainBox implementation of setItem. Listing C1-7 gives the header file for our class MagicBox. It has the private data field firstItemStored, a default constructor, a parameterized constructor, and the special version of setItem that we need.

```
LISTING C1-7 Header file for the class MagicBox

/** @file MagicBox.h */
#ifndef _MAGIC_BOX
#define _MAGIC_BOX
#include "PlainBox.h"

template<class ItemType>
class MagicBox : public PlainBox<ItemType>
{
private:
   bool firstItemStored;
public:
   MagicBox();
   MagicBox(const ItemType& theItem);
   void setItem(const ItemType& theItem);
}; // end MagicBox

#include "MagicBox.cpp"
#endif
```

The implementation of the default constructor must call the base-class constructor and then initialize the data field firstItemStored to true to indicate that the first item has not been stored yet. The method setItem must check this data field and, if no item has been stored, call the base-class method setItem to store the parameter in the data field item. You can see these implementations in Listing C1-8.

```
LISTING C1-8 Implementation file for the class MagicBox

/** @file MagicBox.cpp */
template<class ItemType>
MagicBox<ItemType>::MagicBox()
{
   PlainBox<ItemType>();
}
(continues)
```
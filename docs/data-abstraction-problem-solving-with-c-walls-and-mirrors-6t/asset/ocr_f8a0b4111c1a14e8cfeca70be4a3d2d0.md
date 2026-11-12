# FIGURE 12-4 SortedListHasA is composed of an instance of the class LinkedList

![](bbox=[0.5, 0.14, 0.65, 0.28])

type of containment called composition and illustrates the *has-a* relationship between the class of sorted lists and the class of lists. If we name our new class SortedListHasA and use an instance of LinkedList, as given in Listing 9.2 of Chapter 9, Figure 12-4 illustrates the relationship between these two classes using UML notation.

The header file. Listing 12-3 declares the class SortedListHasA so that it *has a* private data member that is an instance of LinkedList containing the items in the sorted list. Our class will derive from the interface SortedListInterface, as given earlier in Listing 12-1.

```
LISTING 12-3 The header file for the class SortedListHasA

/** ADT sorted list using the ADT list. */
#ifndef SORTED_LIST_H_A /*
 #ifndef _SORTED_LIST_H_A
 #define _SORTED_LIST_H_A

#include "SortedListInterface.h"
#include "ListInterface.h"
#include "Node.h"
#include "PrecondViolatedExcep.h"

template<class ItemType>
class SortedListHasA : public SortedListInterface<ItemType>
{
private:
   ListInterface<ItemType>* listPtr;

public:
   SortedListHasA();
   SortedListHasA(const SortedListHasA<ItemType>& sList);
   virtual ~SortedListHasA();

   void insertSorted(const ItemType& newEntry);
   bool removeSorted(const ItemType& anEntry);
   int getPosition(const ItemType& newEntry) const;

   // The following methods have the same specifications
   // as given in ListInterface in Chapter 8:
```
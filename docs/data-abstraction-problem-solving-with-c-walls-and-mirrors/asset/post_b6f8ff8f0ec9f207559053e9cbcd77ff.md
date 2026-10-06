
```cpp
template <class ItemType>
LinkedIterator<ItemType> LinkedList<this>::end()
{
    return LinkedIterator<ItemType>(this, nullptr);
} // end
```

In begin, we send the iterators to the object and the first node in the chain that contains the list items. Giving the iterator direct access to LinkedList's data member violates the wall of abstraction and must be done with care. Well-designed iterators only traverse the collection and access the items stored; they should not change the structure of a collection.

## C6.1.3 Implementing an Iterator

Listing C6-1 is the header file for the class, LinkedIterator, of input iterators designed to work with our LinkedList class. It is a distinct class separate from LinkedList. The constructor has two parameters, else traversed by the iterator and an initial node for the iterator. The second parameter is used by the LinkedList class methods begin and initialize the iterator's position.

LISTING C6-1 The header file for the class LinkedIterator
```cpp
#ifndef _LINKED_ITERATOR
#define _LINKED_ITERATOR

#include <iterator>
#include "Node.h"

template<class ItemType>
class LinkedList;

template<class ItemType>
class LinkedIterator : public iterator<input_iterator_tag, int>
{
private:
    // AD associated with iterator
    const LinkedList<ItemType>* containerPtr;
    // Current location in collection
    Node<ItemType>* currentItemPtr;
public:
    LinkedIterator(const LinkedList<ItemType>* someList,
                   Node<ItemType>* nodePtr);

    /* Dereferencing operator overload.
     * @return The item at the position referenced by iterator. */
    const ItemType operator*() const;

    /* Prefix increment operator overload.
     * @return The iterator referencing the next position in
     * the list */
    LinkedIterator<ItemType>& operator++();

    /* Equality operator overload.
     * @param other The iterator for comparison.
     * @return True if this iterator references the same list and
     * the same position as rightHandSide, false otherwise. */
    bool operator=(const LinkedIterator<ItemType>& rightHandSide) const;

    /** Inequality operator overload.
     * @param other The iterator for comparison.
     * @return True if this iterator does not reference the same
     * list and the same position as rightHandSide,
     * False otherwise. */
    bool operator!=(const LinkedIterator<ItemType>& rightHandSide) const;
}; // end LinkedIterator
#include "LinkedIterator.cpp"
#endif
```

In the base class specification and class constructor, there are two other lines in this header file that differ from previous headers. Before the LinkedIterator class is declared, the following two lines provide a forward declaration of the class LinkedList:

```cpp
template<class ItemType>
class LinkedList;
```

These lines are necessary because LinkedList must instantiate an object of the class LinkedIterator<ItemType> in the begin and end methods, but the LinkedIterator class must have a complete declaration of LinkedList<ItemType> to instantiate it. To resolve these circular references, we include this forward declaration. When the compiler begins to compile the LinkedIterator class, it will read these statements and know that LinkedList<ItemType> is also a class. The compiler can then use placeholders for the details of LinkedList.

The implementation of LinkedIterator is shown in Listing C6-2.

LISTING C6-2 The implementation file for the class LinkedIterator
```cpp
#include "LinkedIterator.h"
template <class ItemType>
LinkedIterator<ItemType>::
LinkedIterator(const LinkedList<ItemType>* someList,
Node<ItemType>* nodePtr):
containerPtr(someList), currentItemPtr(nodePtr)
{
}
// end constructor

template <class ItemType>
const ItemType& LinkedIterator<ItemType>::operator*()
{
    return currentItemPtr->get();
}
// end operator*

template <class ItemType>
LinkedIterator<ItemType>::operator++()
{
    currentItemPtr = currentItemPtr->next();
    return *this;
} // prefix operator++

template <class ItemType>
bool LinkedIterator<ItemType>::operator===(const
const LinkedIterator<ItemType>& rightHandSide)
{
    return ((containerPtr == rightHandSide.containerPtr) &&
        currentItemPtr == rightHandSide.currentItemPtr);
} // end operator==

template <class ItemType>
bool LinkedIterator<ItemType>::operator!=(const
const LinkedIterator<ItemType>& rightHandSide)
{
    return ((containerPtr != rightHandSide.containerPtr) ||
        currentItemPtr != rightHandSide.currentItemPtr);
} // end operator!=
```

The implementations of the iterator methods use the methods of the Node class. For example, the dereferencing operator* returns the result of calling getItem on the current node, and the ++ operator uses next to advance the iterator to the next position. Note that the ++ operator returns the object to the caller. This is part of the C++ standard for ++ operator, but clients seldom return the value.

An alternative is to use only iterators that have access to public methods of your data structure, but then you lose the efficiencies by directly accessing the structure. The best approach is to design an iterator for your class at the time you design your ADT, so that you can coordinate the features and ensure that the iterator does not break the class's structure.

## C6.2 Advanced Iterator Functionality

Deriving our iterator from the standard library allows us to use many of the powerful algorithms. The best approach is to design an iterator for your class at the time you design your ADT, so that you can coordinate the features and ensure that the iterator does not break the class's structure.

The implementation of the iterator methods use the methods of the Node class. For example, the dereferencing operator* returns the result of calling getItem on the current node, and the ++ operator uses next to advance the iterator to the next position. Note that the ++ operator returns the object to the caller. This is part of the C++ standard for ++ operator, but clients seldom return the value.

The function find. To search a collection for a target entry, you use the collection find. This function returns an iterator to the target if it exists in the collection, collection between the starting iterator and ending iterator.

The function advance. To move an iterator forward a specific number of positions, you can use the advance function.

The function distance. To determine how many entries remain to be processed, we can determine the distance from the current position to the end of the collection.

The function equal. To determine whether the elements in two lists are same, either for the entire list or for a subray within the lists, you can use the equal function.


```cpp
template <class ItemType>
LinkedIterator<ItemType> LinkedList<ItemType>::end()
{
    return LinkedIterator<ItemType>(this, nullptr);
} // end end
```

In the begin method, we send the iterator references to the list object and the first node in the chain that contains the list items. Giving the iterator direct access to LinkedList’s data member violates the wall of abstraction and must be done with care. Well-designed iterators only traverse the collection and access the items stored in the collection; they should not change the structure of a collection.

## C6.1.3 Implementing an Iterator

Listing C6-1 is the header file for the class LinkedIterator, of input iterators designed to work with our LinkedList class. It is a distinct class separate from LinkedList. The constructor has two parameters, the list traversed by the iterator and an initial node for the iterator to reference. The second parameter is used by the LinkedList class methods begin and end to initialize the iterator’s position.

```cpp
LISTING C6-1 The header file for the class LinkedIterator

#ifndef _LINKED_ITERATOR
#define _LINKED_ITERATOR

#include <iterator>
#include "Node.h"

template <class ItemType>
class LinkedList;

template <class ItemType>
class LinkedIterator : public iterator<input_iterator_tag, int>
{
private:
    // ADT associated with iterator
    const LinkedList<ItemType>* containerPtr;

    // Current location in collection
    Node<ItemType>* currentItemPtr;

public:
    LinkedIterator(const LinkedList<ItemType>* someList,
                   Node<ItemType>* nodePtr);
    // Dereferencing operator overload.
    // @return The item at the position referenced by iterator.
    const ItemType operator*();

    // Prefix increment operator overload.
    // @return The iterator referencing the next position in
    //         the list.
    LinkedIterator<ItemType> operator++();

    // Equality operator overload.
    // @param LinkedList The iterator for comparison.
    // @return True if this iterator references the same list and
    //         the same position as rightHandSide, false otherwise.
    bool operator==(const LinkedIterator<ItemType>& rightHandSide) const;
    /* Inequality operator overload.
    @param rightHandSide The iterator for comparison.
    @return True if this iterator does not reference the same
    list and the same position as rightHandSide,
    false otherwise. */
    bool operator!=(const LinkedIterator<ItemType>& rightHandSide) const;
}; // end LinkedIterator
#include "LinkedIterator.cpp"
#endif
```

In addition to the base class specification and class constructor, there are two other lines in this header file that differ from previous header files. Before the LinkedIterator class is declared, the following two lines provide a forward declaration of the class LinkedList:

```cpp
template<class ItemType>
class LinkedList;
```

These lines are necessary because LinkedList must instantiate an object of the class LinkedIterator<ItemType> in the begin and end methods, but the LinkedIterator class must have a complete declaration of LinkedList<ItemType> to instantiate itself. To resolve these circular references, we include this forward declaration. When the compiler begins to compile the LinkedIterator class, it will read these statements and know that LinkedList<ItemType> is also a class. The compiler can then use placeholders for the details of LinkedList.

The implementation of LinkedIterator is shown in Listing C6-2.

```cpp
LISTING C6-2 The implementation file for the class LinkedIterator
#include "LinkedIterator.h"
template <class ItemType>
LinkedIterator<ItemType>::LinkedIterator(const LinkedList<ItemType>* someList,
                                         Node<ItemType>* nodePtr)
    : containerPtr(someList), currentItemPtr(nodePtr)
{ } // end constructor
template <class ItemType>
const ItemType LinkedIterator<ItemType>::operator*()
{
    return currentItemPtr->getItem();
} // end operator*
template <class ItemType>
LinkedIterator<ItemType> LinkedIterator<ItemType>::operator++()
{
    currentItemPtr = currentItemPtr->getNext();
    return *this;
} // end prefix operator++
template <class ItemType>
bool LinkedIterator<ItemType>::operator==(const
LinkedIterator<ItemType>& rightHandSide) const
{
    return ((containerPtr == rightHandSide.containerPtr) &&
    (currentItemPtr == rightHandSide.currentItemPtr));
} // end operator==
template <class ItemType>
bool LinkedIterator<ItemType>::operator!=(const
LinkedIterator<ItemType>& rightHandSide) const
{
    return ((containerPtr != rightHandSide.containerPtr) ||
    (currentItemPtr != rightHandSide.currentItemPtr));
} // end operator!=
```

The implementations of the iterator methods use the methods of the node class. For example, the dereferencing * operator returns the result of calling getItem on the current node, and the ++ operator uses getNext to advance the iterator to the next position. Notice that the ++ operator returns the current object to the caller. This is part of the C++ standard for the ++ operator, but clients seldom use the return value.

An alternative is to use only iterators that have access to public methods of your data structure, but then you lose the efficiencies gained by directly accessing the structure. The best approach is to design an iterator for your class at the same time that you design your ADT, so that you can coordinate the features and ensure that the iterator does not change the class's structure.

## C6.2 Advanced Iterator Functionality

Deriving our iterator from the C++ template class iterator enables the iterator to be used in a number of standard functions provided by C++ that simplify the processing of many common algorithms, such as displaying the items in a collection, searching a collection, and counting the number of occurrences of an item in the collection.

The function for_each. Earlier in this interlude, we presented a while loop that used iterators to access and display each item in a list of strings. C++ provides a function for_each that can accomplish this in a simpler manner. The syntax of the for_each function is:

```cpp
for_each(start_iterator, end_iterator, function_to_perform);
```

where start_iterator and end_iterator are iterators to the first and last position that should be processed in the collection, and function_to_perform is a function with a single parameter of the same type as the entries stored in the collection. This is similar to the visit function discussed with respect to ADT binary tree traversals in Chapter 15. This function is applied to each of the items in the collection from start_iterator to end_iterator.

To use the for_each function, we must create a function to be applied to each of the items in the collection. In this case, the items are strings, and we want to display each one:

```cpp
void displayOneItem(string itemToDisplay)
{
    cout << itemToDisplay << endl;
} // end displayOneItem
```

We can then call the `for_each` function to display all items in the collection as follows:

```cpp
for_each(myList.begin(), myList.end(), displayOneItem);
```

With this one statement, C++ takes care of all the details. The compiler will insert code that begins at the first position of `myList` and sends each item to the function `displayOneItem` to be displayed until all items have been processed.

> Note: The syntax used to call most of the special functions that use iterators to process collections follows the form
>
> `function_name(start_iterator, end_iterator, special_parameters);`
>
> where `special_parameters` represents one or more parameters that the function needs to perform its task.

### The function find.

To search a collection for a specified target entry, you use the function find. This function returns an iterator to the target if it exists in the collection. If the target is not in the collection, find returns an iterator to the last position:

```cpp
// Find the entry "Ace" in the collection myList
ListIterator<string> myCard = find(myList.begin(), myList.end(), "Ace");
```

### The function count.

Another useful function is count. This function returns an integer that represents the number of times a specified value occurs in the collection between the starting iterator and ending iterator:

```cpp
// Count the number of occurrences of "Ace" in collection myList
int aceCount = count(myList.begin(), myList.end(), "Ace");
```

### The function advance.

To move an iterator forward a specific number of positions, you can use the advance function. It has a slightly different form:

```cpp
advance(someIterator, distanceToAdvance);
```

For example, if we needed an iterator to the fifth element of myList, we would use the following statements:

```cpp
// Iterator to first position in myList
ListIterator<string> myIterator = myList.begin();
// Advance from first position to fifth (4 positions ahead)
advance(myIterator, 4);
```

### The function distance.

To determine how many entries remain to be processed, we can determine the distance from our current position to the end of the collection, using the distance function:

```cpp
int numberRemaining = distance(myIterator, myList.end());
```

### The function equal.

If you want to determine whether the elements in two lists are the same, either for the entire list or for a subrange within the lists, you can use the equal function. Suppose myList and yourList are two instances of LinkedList<string>. To determine if all entries in myList are equal to the first entries in yourList, you would write:

```cpp
bool same = equal(myList.begin(), myList.end(), yourList.begin());
```

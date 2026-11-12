```
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

The implementations of the iterator methods use the methods of the Node class. For example, the dereferencing * operator returns the result of calling getItem on the current node, and the ++ operator uses getNext to advance the iterator to the next position. Notice that the ++ operator returns the current object to the caller. This is part of the C++ standard for the ++ operator, but clients seldom use the return value.

An alternative is to use only iterators that have access to public methods of your data structure, but then you lose the efficiencies gained by directly accessing the structure. The best approach is to design an iterator for your class at the same time that you design your ADT, so that you can coordinate the features and ensure that the iterator does not change the class’s structure.

# C6.2 Advanced Iterator Functionality

Deriving our iterator from the C++ template class iterator enables the iterator to be used in a number of standard functions provided by C++ that simplify the processing of many common algorithms, such as displaying the items in a collection, searching a collection, and counting the number of occurrences of an item in the collection.

The function for_each. Earlier in this interlude, we presented a while loop that used iterators to access and display each item in a list of strings. C++ provides a function for_each that can accomplish this in a simpler manner. The syntax of the for_each function is:

```
for_each(start_iterator, end_iterator, function_to_perform);
```

where start_iterator and end_iterator are iterators to the first and last position that should be processed in the collection, and function_to_perform is a function with a single parameter of the same type as the entries stored in the collection. This is similar to the visit function discussed with respect to ADT binary tree traversals in Chapter 15. This function is applied to each of the items in the collection from start_iterator to end_iterator.

To use the for_each function, we must create a function to be applied to each of the items in the collection. In this case, the items are strings, and we want to display each one:

```
void displayOneItem(string itemToDisplay)
{
    cout << itemToDisplay << endl;
} // end displayOneItem
```
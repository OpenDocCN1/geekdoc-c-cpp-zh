# Advanced Iterator Functionality 499

```
currentItemPtr = currentItemPtr->next();
return *this;
 // prefix operator++ntemplate <class ItemType>
bool LinkedIterator<ItemType>::operator===(const
LinkedIterator<ItemType>& rightHandSide)
{
    return ((containerPtr == rightHandSide.containerPtr) &&
        currentItemPtr == rightHandSide.currentItemPtr));
} // end operator==ntemplate <class ItemType>
bool LinkedIterator<ItemType>::operator!=(const
LinkedIterator<ItemType>& rightHandSide)
{
    return ((containerPtr != rightHandSide.containerPtr) ||
        currentItemPtr != rightHandSide.currentItemPtr));
} // end operator!=
```

The implementations of the iterator methods use the methods of the Node class. For example, the dereferencing *operator returns the result of calling getItem on the current node, and the ++ operator uses next to advance the iterator to the next position. Note that the ++ operator returns the object to the caller. This is part of the C++ standard for ++ operator, but clients seldom return the value.
an alternative is to use only iterators that have access to public methods of your data structure, but then you lose the efficiencies by directly accessing the structure. The best approach is to design an iterator for your class at the time you design your ADT, so that you can coordinate the features and ensure that the iterator does not break the class's structure.

# C6.2 Advanced Iterator Functionality

Deriving our iterator from the C++ template class enables the iterator to be used in a number of standard functions provided by C++ that simplify the processing of many common algorithms, such as displaying the items in a collection, searching a collection, and counting the number of occurrences of an item in the collection.
The for_each function. Earlier in this, we presented a while loop that used iterators to access and display each item in a list of strings. C++ provides a function for_each that can accomplish this in a much simpler manner. The syntax of the for_each function is:

```
for_each(start_iterator, end_iterator, function_to_perform);
```

where start_iterator and end_iterator are iterators to the first and last position that should be processed in the collection, and function_to_perform is a function with a single parameter of the same type as the entries stored in the collection. This is similar to the visit function discussed with respect to ADT binary tree traversals in Chapter 15. This is applied to each of the items in the collection from start_iterator to end_iterator.
to use the for_each function, we must create a function to be applied to each of the items in the collection. In this case the items are strings, and we want to display each one:

```
void displayOneItem(string itemToDisplay)
{
    cout << itemToDisplay << endl;
} // end displayOneItem
```
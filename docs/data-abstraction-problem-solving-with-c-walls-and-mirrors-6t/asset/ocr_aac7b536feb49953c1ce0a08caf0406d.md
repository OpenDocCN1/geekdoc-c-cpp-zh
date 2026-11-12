explicitly in the header file for SortedListIsA, if you were to call them without the qualifier LinkedList<ItemType>::, the C++ compiler would assume that they were client functions instead of class methods. You could get a syntax error.

An alternate way of calling these methods is to precede their calls by this-> instead of LinkedList<ItemType>::. For example, you could write

```
if (this->isEmpty())
```

instead of

```
if (LinkedList<ItemType>::isEmpty())
```

**Overridden methods.** Recall that we have inherited two methods—insert and setEntry—from LinkedList that we do not want as public methods of the ADT sorted list. Although we called insert in our definition of insertSorted, we do not want clients to be able to destroy the sorted order of our entries by inserting an item at any specific position within a sorted list. To this end, we override insert so that it always returns false:

```
template<class ItemType>
bool SortedListIsA<ItemType>::insert(const ItemType& newEntry)
{
   return false;
} // end insert
```

Overriding insert prevents insertions into a sorted list by position

This approach ensures that a client of SortedListIsA can never use insert to add items by position to an object of SortedListIsA. We override setEntry in a similar manner.

> **Note:** Recall that public inheritance enables you to use a derived-class object anywhere that you can use a base-class object. But you cannot use a sorted list in the same way that you can use a list and expect to maintain the values stored in the sorted list in sorted order. Moreover, the value-oriented nature of a sorted list does not support all of a list’s operations. Therefore, a sorted list is not really a list, and hence public inheritance is not appropriate.

A sorted list is not a list; do not use public inheritance

> **Programming Tip:** You should use public inheritance only when two classes have an is-a relationship.

> **Question 15** What would have happened if you preceded the call to insert in the method insertSorted by this-> instead of LinkedList<ItemType>::? Explain.

**Efficiency issues.** If you compare the implementation of SortedListIsA with the one for SortedListHasA, you will notice slight differences in the syntax, but the basic logic of the methods is the same. Both classes use methods of the ADT list to define their operations. The performance of corresponding methods is virtually the same.
# Implementations That Use the ADT

explicitly LinkedList<Item>::, if you were to call them without the qualifier LinkedList<Item>::, the C++ compiler would assume that they were client functions instead of class methods. You would get a syntax error.

An alternate way of calling these methods is to precede their calls with this-> instead of LinkedList<Item>::. For example, you could write

```
if (this->isEmpty())
```

instead of

```
if (LinkedList<Item>::isEmpty())
```

Overridden methods. Recall that we have inherited two methods—insert and setEntry—from LinkedList that we do not publish as public methods of the ADT sorted list. Although in our definition of insertSorted, we do not want clients to be able to destroy the sorted order of entries by inserting them at any specific position within a sorted list. To this end, we override sort so that it returns false;

```
template<class ItemType>
bool SortedListA<ItemType>::
insert(int newPosition, const ItemType& newEntry) {
  return false;
} // end insert
```

> Overriding insert prevents insertions into a sorted list by position

This approach ensures that a client of SortedListA can never insert to add items by position to an object of SortedListA. We override setEntry in a similar manner.

> Note: Recall that public inheritance enables you to use a derived-class object where you can use a base-class object. But you cannot use a sorted list in the same way that you can use a list and expect to maintain the values stored in the sorted list in order. The value-oriented nature of class does not support all of a list's operations. Therefore, a sorted list is not really a list, and hence public inheritance is not appropriate.

> A sorted list is not a list; do not use public inheritance

> Programming Tip: You should use public inheritance only when two classes have an-is-a relationship.

> Question 15 What would have happened if you preceded the call to insert in the method insertSorted by this-> instead of LinkedList<ItemType>::? Explain.

Efficiency issues. If you compare the implementation of SortedListA with the one for SortedAS, you will notice slight differences in the syntax, but the basic logic of the methods is the same. Both classes use methods of the ADT to define their operations. The performance of corresponding methods is virtually the same.
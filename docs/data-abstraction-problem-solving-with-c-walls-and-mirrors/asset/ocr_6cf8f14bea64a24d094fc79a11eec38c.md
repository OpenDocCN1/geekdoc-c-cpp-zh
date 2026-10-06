# 352 CHAPTER 12 Sorted Lists And Their Implementations

```
nameListPtr->insertSorted("Sarah");
nameListPtr->insertSorted("Tom");
nameListPtr->insertSorted("Carlos");
```

The sorted list now contains the following entries:

+   - Brenda
- Carlos
- Jamie
- Sarah
- Tom

Assuming the list just given, here are some examples of the operations on the sorted list:

```
nameListPtr->getPosition("Jamie") returns 3, the position of Jamie in the list
nameListPtr->getPosition("Jill") returns -4, because Jill belongs at position 4 in the list
nameListPtr->getEntity(2) returns Carlos, because he is at position 2 in the list
```

Remove Tom and the first name in the list by using

```
nameList.remove("Tom");
nameList.remove(1);
```

The list now contains

+   - Carlos
- Jamie
- Sarah

Removing the last entry, Tom, did not change the positions of the other entries in the list, removing the first entry did. Carlos is now at position 1, instead of 2.

> Note: The ADT list can add, remove, or locate an entry, given the entry as an argument. The sorted list has several operations that are the same as ADT list operations, getEntry(by position), removeSorted(by position), clear, length, and isEmpty. However, a sorted list will not let you add or replace an entry by position.

Question 3 Suppose that wordListPtr points to an unordered list of words. Using the operations of the ADT list and the ADT sorted list, create a sorted list of these words.

Question 4 Assuming that the sorted list you created in the previous question is not empty, write C++ statements

+   a. Display the entry in the sorted list.
b. Add the sorted list's first entry to the sorted list again.

# 12.2 A Link-Based Implementation

As with ADTs, you have a choice of several ways to implement the sorted list. You could store a sorted list's entries in, for example, an array, a chain of linked nodes, an instance of a vector, or an instance of an ADT list. We will first consider a chain of linked nodes and then an instance of an ADT list. Finally, we will use inheritance to develop a completely different implementation.
Drew and Ellen will be at positions 4 and 5, respectively. Thus, aList.getEntry(4) would return Drew.

Finally, suppose that we want to replace a name in this list. We cannot replace a name with just any name and expect that the list will remain in alphabetical order. Replacing Bob with Ben by writing

```
aList.setEntry(3, "Ben");
```

would maintain alphabetical order, but replacing Bob with Nancy would not. The list's alphabetical order resulted from our original decisions about where to place names on the list. The order did not come about automatically as a result of list operations. That is, the client, not the list, maintains the order. We could, however, design an ADT that maintains its data in alphabetical order. You will see an example of such an ADT in Chapter 12.

![](bbox=[0.06, 0.3, 0.1, 0.35])

Question 3 Write a pseudocode function swap(aList, i, j) that interchanges the items currently in positions i and j of a list. Define the function in terms of the ADT list operations, so that it is independent of any particular implementation of the list. Assume that the list, in fact, has items at positions i and j. What impact does this assumption have on your solution? (See Exercise 2 at the end of this chapter.)

Question 4 What grocery list results from the following sequence of ADT list operations?

```
aList = a new empty list
aList.insert(1, "butter")
aList.insert(1, "eggs")
aList.insert(1, "milk")
```

Question 5 Suppose that myList is a list that contains the five objects a b c d e.

+   a. What does myList contain after executing myList.insert(5, w)?
+   b. Starting with the original five entries, what does myList contain after executing myList.insert(6, w)?
+   c. Which of the operations in parts a and b of this question require entries in the array to shift?

# 8.3 An Interface Template for the ADT List

We now will formalize our specification of the ADT list by writing a C++ interface, which is given in Listing 8-1.

# LISTING 8-1 A C++ interface for lists

```
/** Interface for the ADT list
@file List_Interface.h */
#ifndef _LIST_INTERFACE
#define _LIST_INTERFACE
template<class ItemType>
class ListInterface
```
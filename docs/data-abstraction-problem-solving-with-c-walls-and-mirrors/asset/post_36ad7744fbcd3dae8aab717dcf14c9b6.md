
# FIGURE 12-2 Places to insert strings into a sorted chain of linked nodes

![](img/d0cb86b2f18b2db569968ad7c743510e_381_0.png)

**The method insertSorted.** Adding an entry to a sorted list requires that you find where in the list the new entry belongs. Since the entries are sorted, you compare the new entry with the entries in the sorted list until you reach an entry that is not smaller than the new entry. Figure 12-2 depicts a chain of linked nodes, each containing a string alphabetically sorted. The figure shows where the additional strings "Ally","Cathy","Luke," and "Tom" would be inserted into the chain and the comparisons that would have to occur at those locations.

You can see from the figure that, in simple comparison, Ally is less than Bob, and so it would be inserted at the beginning of the chain. To Sue, you would find that Luke is greater than Bob and Jill but less than Mike. Thus, Luke belongs before Mike. On the other hand, Sue is one of the nodes. You would find Sue is greater than Bob, Jill, and Mike but not greater than Sue. So you would insert the new entry just before the existing entry. Finally, Tom is greater than all the names in the list, so you would add it to the end of the chain.

> Note: Given a sorted list with entries in ascending order, you insert a new entry before the first entry that is not smaller than the new entry.

Recall from earlier chapters that you add a new node to the beginning of a chain differently than at other points in the chain. Adding to the beginning is easy, since headPtr references the first node in the chain. To add anywhere else, you need a pointer to the node that will ultimately occur before the new node. Thus, while you traverse the chain of linked nodes to discover where the new entry belongs, you must retain a reference to the node prior to the one under consideration.

The following high-level algorithm describes our strategy:

```
// Adds a new entry to the sorted list.
add(newEntry)
Allocate a new node containing newEntry
Search the chain until you find a node containing newEntry or you pass
the point where it should be
prevPtr point to the node before the insertion point
(head is empty or the new node belongs at the beginning of the chain)
    Add the new node to the beginning of the chain
\else
    Insert the new node after the node referenced by prevPtr
Increment the length of the sorted list
```

# 356 CHAPTER 12 Sorted Lists and Their Implementations

Assuming the private method getNodeBefore that we specified in the header file, we can use the previous algorithm to define the insertSorted method, as follows:

```cpp
template<class ItemType>
void SortedList<ItemType>::insertSorted(const ItemType& newEntry)
{
    Node<ItemType>* newNodePtr = new Node<ItemType>(newEntry);
    Node<ItemType>* prevPtr = getNodeBefore(newEntry);

    if (isEmpty() || (prevPtr == nullptr)) // Add at beginning
    {
        newNodePtr->setNext(headPtr);
        headPtr = newNodePtr;
    }
    else // Add after node
    {
        Node<ItemType>* aftPtr = prevPtr->getNext();
        newNodePtr->setNext(aftPtr);
        prevPtr->setNext(newNodePtr);
    }
    itemCount++;
}
```

**The private method getNodeBefore** We still need to implement the private method getNodeBefore to locate the node that is before or should contain the given entry. We will need two pointers as we traverse the list. Clearly, we need a pointer to the current node so we can compare its entry to the desired entry. We must also retain a pointer to the previous node, because it is this pointer that the method returns. In the following implementation, these pointers are curPtr and prevPtr.

```cpp
template<class ItemType>
Node<ItemType>* SortedList<ItemType>::getNodeBefore(const ItemType& anEntry) const
{
    Node<ItemType>* curPtr = headPtr;
    Node<ItemType>* prevPtr = nullptr;
    while ((curPtr != nullptr) && (anEntry != curPtr->getItem()))
    {
        prevPtr = curPtr;
        curPtr = curPtr->getNext();
    }
    return prevPtr;
}
```

The programming problems at the end of this chapter allow you to complete the implementation of the sorted list.

> Note: Since the ADTs sorted list and list share many of the same operations, portions of their implementations are identical.

- **Question 5** In the while statement of the method getNodeBefore, how important is the order of the two boolean expressions that the operator && joins? Explain.

- **Question 6** What does getNodeBefore return if the sorted list is empty? How can you use this fact to simplify the implementation of the method insertSorted given previously?

- **Question 7** Suppose that you use the previous method insertSorted to add an entry to a sorted list. If the entry is already in the list, in list will the method insert it? Before the first occurrence of the entry, after the first occurrence of the entry, after the last occurrence of the entry, or somewhere else?

- **Question 8** What would be the answer to the previous question if you changed to >= in the while statement of the method getNodeBefore?

# 2.2.3 The Efficiency of the Link-Based Implementation

The performance of insertSorted depends on the efficiency of the method getNodeBefore. The later method locates the insertion point by traversing the chain of nodes. This traversal is O(n), making the addition to a sorted O(n) operation. With except isEmpty and length, which are O(1) operations, the sorted-list methods are O(n). We leave these observations for you to show as Exercise 11.

# 2.3 Implementations That Use The ADT List

As noted earlier in this chapter, the link-based implementation of the ADT sorted list repeats much of the corresponding implementation of the ADT list. We can avoid this duplication of effort and reuse portions of the list's implementation? The answer to this question is yes, you will soon see.
You can certainly use the ADT to create and maintain an alphabetical list of strings. It is natural, then, to consider using the ADT list when implementing the ADT sorted list. Basically, you can do this using one of three techniques:

- Containment
- Public inheritance
- Private inheritance

In most cases, one or more of these approaches will not be applicable to a particular problem; usually, one of the approaches will be best. However, we will use the sorted list to demonstrate all three techniques.

# 2.3.1 Containment

A sorted list can maintain its entries within a list, as Figure 12-3 illustrates. You use a list as a data field within the class that implements the sorted list. As noted in C++ Interlude 4, this approach uses a type of containment called composition and illustrates the has-a relationship between the class of sorted lists and the class of lists.

> FIGURE 12-3 An instance of a sorted list that contains a list of its entries

![](img/d0cb86b2f18b2db569968ad7c743510e_383_0.png)

![](img/d0cb86b2f18b2db569968ad7c743510e_383_1.png)

# 358 CHAPTER 12 Sorted Lists and Their Implementations

FIGURE 12-4 SortedListHasA is composed of an instance of the class LinkedList

![](img/d0cb86b2f18b2db569968ad7c743510e_384_0.png)

composition and illustrates the has-a relationship between the class of sorted lists and the class of lists. If we name our new class SortedListHasA and an instance of LinkedList, as given in Listing 9-2 of Chapter 9, illustrates the relationship between these two classes using UML notation.

The header file. Listing 12-3 declares the class SortedListHasA so that it has a private member that is an instance of LinkedList containing the items in the sorted list. Our class will derive from the interface SortedListInterface, as earlier in Listing 12-1.

LISTING 12-3 The header file for the class SortedListHasA
/** ADT sorted list using the ADT list.
 * @file SortedListHasA.h */
#ifndef SORTED_LIST_HAS_A
#define SORTED_LIST_HAS_A

#include "SortedListInterface.h"
#include "LinkedList.h"
#include "Node.h"
#include "PrecondViolatedExcep.h"

template<class ItemType>
class SortedListHasA : public SortedListInterface<ItemType>
{
private:
    LinkedList<ItemType>* ListPtr;

public:
    SortedListHasA();
    SortedListHasA(const SortedListHasA<ItemType>& sList);
    virtual ~SortedListHasA();

    void insertSorted(const ItemType& newEntry);
    bool removeSorted(const ItemType& anEntry);
    int getPosition(const ItemType& newEntry) const;

// The following methods have the same specifications
// as given in ListInterface in Chapter 8:


**FIGURE 12-2** Places to insert strings into a sorted chain of linked nodes

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_381_0.png)

The method insertSorted. Adding an entry to a sorted list requires that you find where in the list the new entry belongs. Since the entries are sorted, you compare the new entry with the entries in the sorted list until you reach an entry that is not smaller than the new entry. Figure 12-2 depicts a chain of linked nodes, each containing a string that is sorted alphabetically. The figure shows where the additional strings “Ally,” “Cathy,” “Luke,” “Sue,” and “Tom” would be inserted into the chain and the comparisons that would have to occur to arrive at those locations.

You can see from the figure that, in a string comparison, Ally is less than Bob, and so it would be inserted at the beginning of the chain. To see where to insert Luke, you would find that Luke is greater than both Bob and Jill but less than Mike. Thus, Luke belongs before Mike in the chain. Sue, on the other hand, is already in one of the nodes. You would discover that Sue is greater than Bob, Jill, and Mike but not greater than Sue. So you would insert the new entry Sue just before the existing entry Sue. Finally, Tom is greater than all the current names in the list, so you would add it to the end of the chain.

> Note: Given a sorted list with entries in ascending order, you insert a new entry just before the first entry that is not smaller than the new entry.

Recall from earlier chapters that you add a new node to the beginning of a chain differently than at other points in the chain. Adding to the beginning is easy, since headPtr references the first node in the chain. To add anywhere else, you need a pointer to the node that will ultimately occur before the new node. Thus, while you traverse the chain of linked nodes to discover where the new entry belongs, you must retain a reference to the node prior to the one under consideration.

The following high-level algorithm describes our strategy:

```
// Adds a new entry to the sorted list
add(newEntry)
Allocate a new node containing newEntry
Search the chain until either you find a node containing newEntry or you pass
the point where it should be
Let prevPtr point to the node before the insertion point
if (the chain is empty or the new node belongs at the beginning of the chain)
    Add the new node to the beginning of the chain
else
    Insert the new node after the node referenced by prevPtr
Increment the length of the sorted list
```

Assuming the private method getNodeBefore that we specified in the header file, we can use the previous algorithm to define the insertSorted method, as follows:

```cpp
template<class ItemType>
void LinkedSortedList<ItemType>::insertSorted(const ItemType& newEntry)
{
   Node<ItemType>* newNodePtr = new Node<ItemType>(newEntry);
   Node<ItemType>* prevPtr = getNodeBefore(newEntry);

   if (isEmpty() || (prevPtr == nullptr)) // Add at beginning
   {
      newNodePtr->setNext(headPtr);
      headPtr = newNodePtr;
   }
   else // Add after node before
   {
      Node<ItemType>* aftPtr = prevPtr->getNext();
      newNodePtr->setNext(aftPtr);
      prevPtr->setNext(newNodePtr);
   } // end if

   itemCount++;
} // end insertSorted
```

The private method getNodeBefore. We still need to implement the private method getNodeBefore to locate the node that is before the node that should or does contain the given entry. We will need two pointers as we traverse the list. Clearly, we need a pointer to the current node so we can compare its entry to the desired entry. But we also must retain a pointer to the previous node, because it is this pointer that the method returns. In the following implementation, these pointers are curPtr and prevPtr.

```cpp
template<class ItemType>
Node<ItemType>* LinkedSortedList<ItemType>::getNodeBefore(const ItemType& anEntry) const
{
   Node<ItemType>* curPtr = headPtr;
   Node<ItemType>* prevPtr = nullptr;
   while ((curPtr != nullptr) && (anEntry > curPtr->getItem()))
   {
      prevPtr = curPtr;
      curPtr = curPtr->getNext();
   } // end while

   return prevPtr;
} // end getNodeBefore
```

The programming problems at the end of this chapter ask you to complete this implementation of the sorted list.

> Note: Since the ADTs sorted list and list share many of the same operations, portions of their implementations are identical.

Question 5 In the while statement of the method getNodeBefore, how important is the order of the two boolean expressions that the operator && joins? Explain.

Question 6 What does getNodeBefore return if the sorted list is empty? How can you use this fact to simplify the implementation of the method insertSorted given previously?

**Question 7** Suppose that you use the previous method `insertSorted` to add an entry to a sorted list. If the entry is already in the list, where in the list will the method insert it? Before the first occurrence of the entry, after the first occurrence of the entry, after the last occurrence of the entry, or somewhere else?

**Question 8** What would be the answer to the previous question if you changed `>` to `>=` in the while statement of the method `getNodeBefore`?

## 12.2.3 The Efficiency of the Link-Based Implementation

The performance of `insertSorted` depends on the efficiency of the method `getNodeBefore`. The latter method locates the insertion point by traversing the chain of nodes. This traversal is $O(n)$, making the addition to a sorted list an $O(n)$ operation. With the exception of `isEmpty` and `getLength`, which are $O(1)$ operations, the sorted-list methods are $O(n)$. We leave these observations for you to show as Exercise 11.

## 12.3 Implementations That Use the ADT List

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_383_0.png)

As we noted earlier in this chapter, the link-based implementation of the ADT sorted list repeats much of the corresponding implementation of the ADT list. Can we avoid this duplication of effort and reuse portions of the list's implementation? The answer to this question is yes, as you will soon see.

You can certainly use the ADT list to create and maintain an alphabetical list of strings. It is natural, then, to consider using the ADT list when implementing the ADT sorted list. Basically, you can do this using one of three techniques:

- Containment
- Private inheritance
- Private inheritance

In most cases, one or more of these three approaches will not be applicable to a particular problem; usually, one of the approaches will be best. However, we will use the sorted list to demonstrate all three techniques.

### 12.3.1 Containment

A sorted list can maintain its entries within a list, as Figure 12-3 illustrates. You use a list as a data field within the class that implements the sorted list. As noted in C++ Interlude 4, this approach uses a

**FIGURE 12-3** An instance of a sorted list that contains a list of its entries

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_383_1.png)

**FIGURE 12-4** SortedListHasA is composed of an instance of the class LinkedList

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_384_0.png)

type of containment called composition and illustrates the *has-a* relationship between the class of sorted lists and the class of lists. If we name our new class SortedListHasA and use an instance of LinkedList, as given in Listing 9.2 of Chapter 9, Figure 12-4 illustrates the relationship between these two classes using UML notation.

The header file. Listing 12-3 declares the class SortedListHasA so that it *has a* private data member that is an instance of LinkedList containing the items in the sorted list. Our class will derive from the interface SortedListInterface, as given earlier in Listing 12-1.

LISTING 12-3 The header file for the class SortedListHasA

```cpp
/** ADT sorted list using the ADT list. */
#ifndef SORTED_LIST_H_A
#define SORTED_LIST_H_A

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

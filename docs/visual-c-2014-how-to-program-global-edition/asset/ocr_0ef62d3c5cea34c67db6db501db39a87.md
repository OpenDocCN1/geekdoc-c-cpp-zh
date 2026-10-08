# 19.4 Linked Lists

# Linked-List Implementation

Figures 19.4–15 use an object of our List class to manipulate a list of miscellaneous objects. ClassTest's Main method (Fig. 19.5) creates of objects, inserts objects at the beginning of the list using List method InsertFront, inserts at the end of the list using List method InsertBack, deletes objects from the front of the list using List method RemoveFront. After each insert and delete operation, the program invokes List method Display to output the list contents. If an attempt is made to remove an item from the list, an EmptyListException occurs. A detailed discussion of the program follows.

# Performance Tip 19.4

Insertion and deletion in a sorted array can be consuming—all the elements inserted or deleted element must be shifted appropriately.

The program consists of four classes—Node (Fig. 19.4, lines 8–27), List (lines 30–161), EmptyListException (lines 164–170) and ListTest (Fig. 19.5). The classes in Fig. 19.4 create a linked-list library (in namespace LinkedLibrary) that can be reused throughout this chapter. You should place the code of Fig. 19.4 in its own class project, as we describe in Section 15.13.

```
// Fig. 19.4: LinkedList.cs
// Node, List and EmptyAccessException class declarations.
using System;
namespace LinkedListLibrary
{
    // class to represent one node in a list
    class Node
    {
        // automatic read-only property Data
        public object Data { get; private set; }
        // automatic property Next
        public Node Next { get; set; }
        // constructor to create Node that refers to dataValue
        // and is last node in list
        public Node(object dataValue) : this(dataValue, null) {}
        // constructor to create Node that refers to dataValue
        // and refers to last Node in List
        public Node(object dataValue, Node nextNode)
        {
            Data = dataValue;
            Next = nextNode;
        }
    }
```

> Fig. 19.4 | Node, List and EmptyAccessException class declarations. (Part I of 4).
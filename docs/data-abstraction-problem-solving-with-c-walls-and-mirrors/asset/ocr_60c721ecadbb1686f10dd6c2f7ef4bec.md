```
{
  if (isEmpty())
    throw PreconditionViolatedException("peekFront() called with empty queue.");

  // Queue is not empty; return front
  return listPtr->getEntry(1);
} // end peekFront
// end of implementation file
```

Particular note in the implementation file are the definitions of the constructor, copy constructor, and destructor. The constructor creates a new instance of a list. Omitting this is an easy oversight, leading to incorrect execution of a syntax error. The copy constructor uses an initializer, list1Ptr(queue, listPtr) to invoke the list's copy constructor. Finally, even though the destructor has an empty body, its destructor will be invoked.
Exercise 8 at the end of this chapter asks you to consider the efficiency of this implementation.

# 14.1.2 A Link-Based Implementation

A link-based implementation of a queue uses a chain of linked nodes, like the other link-based implementations you have seen. However, the queue presents a challenge, since we must be able not only remove entries from its front but also add to its back. Removing a node from the beginning of a linked chain is easy, but to add a new node to the chain's end, we need a pointer to the chain's last node. One way to accomplish this is to begin at the front and traverse the chain until we reach the last one. A much more efficient approach uses a tail pointer to reference the end of the chain—just as the head pointer references the beginning of the chain. Figure 14-2 illustrates a chain of linked nodes that has both head and tail pointers. Like the head pointer frontPtr, backPtr is external to the chain.

FIGURE 14-2 A chain of linked nodes with head and tail pointers

![](bbox=[0.355, 0.626, 0.816, 0.751])

A linear linked chain or a circular linked chain can represent a queue

Figure 14-3 shows that you can actually get by with one external pointer—to the back—if you make the last node point to the first one. This data structure is a circular chain of linked nodes. Notice that the nodes in a circular chain have next pointers that never contain null. We will refer to a chain like the one in Figure 14-2 as a linear chain, regardless of how many external pointers it has. Such a chain has no end.
P Problem 1 at the end of the chapter asks you to consider the details of the circular chain implementation. Here we will develop an implementation of the ADT queue using a chain that has both head and tail pointers, as illustrated in Figure 14-2.
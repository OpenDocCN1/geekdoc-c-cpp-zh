# Data Structures 299

```
void main()
/*
    Create a fresh node and assign its address to a pointer.
*/
SingleLinkedListNode * temp = new SingleLinkedListNode();
/*
    Delete the memory occupied by the new node.
*/
delete temp;
}
/*
End of NodeDestructor.cpp
```

Two things happen as a result of the last statement in the above program. One, the destructor is called for the object at which temp points. Second, the memory block occupied by the object at which temp points gets deallocated (returned to the system for use). Since the destructor has a blank definition, no code gets executed.

Let us now study the linked list class. Let us start by looking at the header file of the linked list class (Listing 9.9).

# Listing 9.9 Header file declaration of single linked list class

```
/*
    Beginning of SingleLinkedList.h
*/
#ifndef SINGLE_LINKED_LIST_H
#define SINGLE_LINKED_LIST_H

#include "SingleLinkedListNode.h"

/*
    The linked list class.
    Each instance of this class will represent a linked list.
*/
class SingleLinkedList {
private:
/*
    The head pointer. It will point at the first node of the list.
    It will be NULL when the list id empty.
*/
    SingleLinkedListNode * head;
    public:
/*
    The constructor of the single linked list class.
    will nullify the head pointer.
*/
    SingleLinkedList();
/*
    Function to add a node at the bottom of the list.
*/
```
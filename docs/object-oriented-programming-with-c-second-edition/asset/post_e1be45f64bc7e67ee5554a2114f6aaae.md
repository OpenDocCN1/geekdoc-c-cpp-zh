
Data Structures 307

245

| NULL | head |
| list1 | |

**Figure 9.16** Effects of the list class constructor

list1 is an object of the SingleLinkedList class. The box depicts the memory block occupied by list1. It is evident from the definition of the SingleLinkedList class that an object of the class will have only one data member. The name of this data member is head. The constructor of the class will fire at the time the object is created. It will set the value of the head pointer to NULL.

Let us look at the next function appendNode().

```cpp
/*
Function to add a node at the bottom of the list.
*/
void SingleLinkedList::appendNode(int pVal)
{
    /*
    Create a temporary node that we will append to the
    list.
    The constructor of SingleLinkedListNode class will
    nullify the next pointer of this node.
    */
    SingleLinkedNode * temp = new SingleLinkedListNode();
    /*
    Copy the parameter value passed to the function, to the
    new node.
    */
    temp->set(pVal);
    /* If the head pointer is NULL (list is empty) ...
    */
    if(head == NULL)
    {
        /* make the head pointer point at the temporary node
        */
        head = temp;
    }
    /* otherwise ...
    else
    {
        /* make a temporary pointer, ...
        */
        SingleLinkedNode * iter;
        /*
        make it point at the first node, traverse to the
        end of the list and ...
        */
        for(iter = head->getNext(); iter != NULL;
        iter = iter->getNext());
```

# 308 Object-Oriented Programming with C++

```cpp
/*
... make the next pointer of the last node point at
the temporary node.
*/
iter->setNext(temp);
```The above function is designed to add a node to the linked list. Let us first understand what we will like the function to do. Then, by studying the definition of the function (Listing 9.12), we will decide whether it actually does what we want to do or not.

# Listing 9.12 Executing the appendNode() function

```cpp
/*
Beginning of AppendNode01.cpp
*/
#include "SingleLinkedList.h"
void main() {
    /*
    Create a list
    */
    SingleLinkedList list1;
    /*
    Call the appendNode() function on the list1 object.
    */
    list1.appendNode(5287);
}
/*
End of AppendNode01.cpp
*/
```After the first statement in the above program, because of the constructor of the SingleLinkedList class, the value of the head pointer inside the object will be set to NULL. This can be depicted by Figure 9.17.

| 245 | |
| NULL | head |
| list1 | |

**Figure 9.17** Effects of the list constructor

The above box depicts the object named list1 (labelled at the bottom of the box). Since it is an object of the SingleLinkedList class, it has only one data member—head(labelled on the right of the box). Let us look at the call to the appendNode() function on the list1 object.

```cpp
list1.appendNode(5287);
```

If the function has been defined correctly, then at the end of its execution, the linked list should look like Figure 9.18.

# Data Structures 309

| | 245 | 320 |
|---|---|---|
| head | 320 | 5287 | val |
| | list1 | NULL | next |

**Figure 9.18** Expected effect of the appendNode() function

Let us see whether the function performs as expected or not. Before the function executes, the value of the head pointer is NULL. When the function starts executing, the value of the function’s parameter pVal gets to 5287 because that is the value that has been passed to the function. After this, a temporary node gets created by the new operator and the temporary pointer temp is made to point at it (Figure 9.19).

| | 695 | 320 |
|---|---|---|
| | 320 | 0 | val |
| temp | NULL | next |

**Figure 9.19** The creation of a temporary node that will be added to the list by the appendNode() function

The next statement is:
temp->setVal(pVal);

This will copy the value of pVal, which is 5287, to the val data member of the node. After this, the if statement will check whether the value of the head pointer is NULL or not. This test will return true at this time the list is empty. The if block will execute and the value of temp will be copied to head. This will cause the head pointer to point at the temporary node that has been created earlier. Figure 9.20 illustrates this.

| | 695 | 320 |
|---|---|---|
| | 320 | 5287 | val |
| temp | NULL | next |
| 245 | | |
| | 320 | |
| head | | |

**Figure 9.20** Value of the temp pointer copied to the head pointer

The else block will not execute and the function will come to an end. Since temp is a local variable, it goes out of scope.

# 310 Object-Oriented Programming with C++

# Data Structures 311

**Figure 9.21** Observed effect of the appendNode() function

**Figure 9.22** Effects of the appendNode() function

**Figure 9.23** The temporary node and the iterator over the list

**Figure 9.24**

**Figure 9.25**

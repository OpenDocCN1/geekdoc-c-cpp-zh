
![](img/5bfa77b13fdaa376725789bb8c00ee79_299_0.png)

Figure 9.3 Addition of a node to a linked list

![](img/5bfa77b13fdaa376725789bb8c00ee79_299_1.png)

Figure 9.4 An empty linked list

Figure 9.5 A node added to an empty list

members and member functions of the class. Thereafter, we will look at the implementation file that contains the definitions of the member functions of the node class.

We will next look at a header file that contains the declaration of the linked list class. Like the other class declarations, this declaration will also include the declarations of the data members and member functions of the class. Thereafter, we will look at the implementation file that contains the definitions of the member functions of the single linked list class.

You will find a lot of comments in the program lists. Please ensure that you read them. Reading these comments will make it much easier to understand the code.

Let us start with studying the header file that contains a declaration of the node class (Listing 9.1).

# Listing 9.1 Header file containing declaration of single linked list node class

```cpp
/*
Beginning SingleLinkedListNode.
*/
#ifndef SINGLE_LINKED_LIST_NODE_H
#define SINGLE_LINKED_LIST_NODE_H
/*
The node class.
Each instance of this class will be a node in the single linked list.
*/
class SingleLinkedListNode{
    private:
    /*
    The data part of the nodes.
    */
    int val;
    /*
    The next pointer will exist in each node and will point at the next node (or be NULL)
    */
    SingleLinkedListNode * next;
public:
    /*
    The constructor of the node class. It will nullify the next pointer by default.
    */
    SingleLinkedListNode();
    /*
    This function sets the value of the data part.
    */
    void setValue(int);
    /*
    This function returns the data part.
    */
    int getVal();
    /*
    This function sets the value of the next pointer.
    */
    void setNext(SingleLinkedListNode *);
    /*
    This function returns the value of the next pointer.
    */
    SingleLinkedListNode * getNext();
    /*
The destructor of the class.
*/
```

# 288 Object-Oriented Programming with C++

```cpp
~SingleLinkedListNode();
};
#endif
```

> /*
End of SingleLinkedListNode.h
*/

The header file begins with a comment that specifies the name of the header file and also announces the beginning of the file. This is followed by pre-processor directives that prevent multiple inclusion of the header file in other source codes (you must have studied this in your C language course). This is followed by the declaration of the node class. The last line of the header file contains the declaration of the pre-process block and the last line that marks the end of the header file.

Each object of the SingleLinkedList class will be a node in the linked list. This class has an integer data member, val, which is supposed to contain the value of the node. In this example, each node has this integer-type variable as the data member. However, the data part can be of any type, including class objects.

The other member of the node class is a pointer. It is obvious from its definition that next is supposed to point at another node, i.e., another object of the same class. In our program, it will either be made to point to the next node in the linked list or will be assigned the NULL value (to indicate that the current node is the linked list).

Let us look at the implementation file (Listing 9.2) which contains the definitions of the member functions of the node class. It is important to clearly understand these functions because they serve as the building blocks for the functions of the single linked list class.

## 9.2 Implementation file of the linked list node class

```cpp
/*
Beginning of SingleLinkedList.cpp
*/
#include "SingleLinkedListNode.h"
```

```cpp
/*
The constructor of the node class. It will nullify the
next pointer by default.
*/
```

```cpp
SingleLinkedListNode::SingleLinkedListNode()
{
    /* Set the data part to zero. */
    val = 0;
    /* Set the next pointer to NULL. */
    next = NULL;
}
```

```cpp
/*
This function sets the value of the data part.
*/
```

```cpp
void SingleLinkedList::setVal(int pVal)
{
    /*
    Set the value of the data part to the value of the
    passed parameter.
    */
    val = pVal;
}
```

```cpp
/*
 * This function returns the data part.
 */
int SingleLinkedList::getVal() {
    /*
     * Return the value of the data part.
     */
    return val;
}

/*
 * This function sets the value of the next pointer.
 */
void SingleLinkedList::setNext(SingleLinkedListNode *pNext) {
    /*
     * Set the value of the next pointer to the value of the
     passed parameter.
     */
    next = pNext;
}

/*
 * This function returns the value of the next pointer.
 */
SingleLinkedListNode* SingleLinkedList::getNext() {
    /*
     * Return the value of the next pointer.
     */
    return next;
}

/*
 * The destructor of the class.
 */
SingleLinkedList::~SingleLinkedList() {
    /*
     * Now the destructor has empty definition.
     But we may like to insert some statements here later.
     */
}

// End of SingleLinkedListNode.cpp
```

The implementation file begins with a comment that specifies the implementation file and also announces the beginning of the file. This is followed by an include directive that includes the header file, which contains the declaration of the node class. This is followed by the definitions of the member functions of the node class. The last line contains a comment that marks the end of the implementation file.

To understand the implementation, let us start with the constructor of the node class.

```cpp
/*
 * The constructor of the node class. It will nullify the
 * next pointer by default.
 */
```

```cpp
SingleLinkedListNode::SingleLinkedListNode()
/*
 * Set the data part to zero.
 */
val = 0;
/*
 * Set the next pointer to NULL.
 */
next = NULL;
```

As a result of the constructor, the SingleLinkedList class is created, its val member will be zero and its next pointer will be NULL. It is very important to note that the new operator was used in the statement to create the object, the created object will occupy memory in the heap. This block of memory will continue to be allocated after the block of code ends. Let us understand the rest of the functions with the help of Listing 9.3.

## 9.3 Executing the constructor of the linked list class

```cpp
/*
Beginning of SingleLinkedList.cpp
*/
#include <iostream>
#include "SingleLinkedListNode.h"
void main()
{
    SingleLinkedListNode* temp = new SingleLinkedListNode();
}
/*
End of SingleLinkedList.cpp
*/
```

A diagrammatic representation of the effects of the above statement is shown in Figure 9.6.

| 245 | | val |
|---|---|---|
| temp | 0 | next |
| | NULL |

Figure 9.6 box on the right represents the newly created object. Its members—val and next—have been labelled. As we can see, their values are 0 and NULL respectively. They have been separated by a line in the box. Let us assume that the address of this node is 245. The value of the temp pointer will therefore be 245. Let us now look at the set() function.

```cpp
/*
* This function sets the value of the data part.
 */
void SingleLinkedListNode::setVal(int pVal)
{
    /*
    Set the value of the data part to the value of the
    passed parameter.
    */
    val = pVal;
}
```

This is a very simple function. It assigns the value of the parameter that is passed to it the val data member. Continuing with our previous example, suppose we call it as follows (Listing 9.4).

# Listing 9.4 Executing the setVal() function of the single linked node class

```cpp
/*
Beginning of SetVal.cpp
 */
#include <iostream>
#include "SingleLinkedListNode.h"
void main()
{
    SingleLinkedListNode* temp = new SingleLinkedListNode();
    temp->setVal(10);
}
/*
End of SetVal.cpp
*/
```

A diagrammatic representation of the effects of the above statement is shown in Figure 9.7.

| 245 | 10 | val |
|---|---|---|
| temp | NULL | next |

Figure 9.7 Effect of setVal() function

The next function we need to look at is the getVal() function (Listing 9.5).

```cpp
/*
 This function returns the data part.
 */
int SingleLinkedListNode::getVal()
{
    /*
     Return the value of the data part.
     */
    return val;
}
```

Again, this is a simple function. It simply returns the value of the val data member. Still continuing with our previous example, suppose we call it as follows.

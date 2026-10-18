
## DISPLAY 13.22 Program Using the Queue Class (part 2 of 2)

### Sample Dialogue

```
Enter a word: straw
You entered: straw
Again?(y/n): y
Enter a word: C++
You entered: C++
Again?(y/n): n
```

### Implementation

As shown in Displays 13.21 and 13.23, our queue class is implemented as a linked list in which the head of the list serves as the front of the queue. The member variable front is a pointer that points to the head of the linked list. Nodes are removed at the head of the linked list. The member variable back is a pointer that points to the node at the other end of the linked list. Nodes are added at this end of the linked list.

An empty queue is just an empty linked list, so an empty queue is implemented by setting the pointers front and back equal to NULL. The rest of the details of the implementation are similar to things we have seen before.

## DISPLAY 13.23 Implementation of the Queue Class (part 1 of 3)

```
//This is the implementation file queue.cpp.
//This is the implementation of the class Queue.
//The interface for the class Queue is in the header file queue.h.
#include <iostream>
#include <cstdlib>
#include <cstddef>
#include "queue.h"
using namespace std;

namespace queuesavitch
{
    //Uses cstddef:
    Queue::Queue() : front(NULL), back(NULL)
    {
        //Intentionally empty.
    }

    Queue::Queue(const Queue& aQueue)
        <The definition of the copy constructor is Self-Test Exercise 12.>

```

## DISPLAY 13.23 Implementation of the Queue Class (part 2 of 3)

```
20

   Queue::~Queue()
       <The definition of the destructor is Self-Test Exercise 13.>

   //Uses cstddef:
   bool Queue::empty() const
   {
       return (back == NULL); //front == NULL would also work
   }

   //Uses cstddef:
   void Queue::add(char item)
   {
       if (empty())
       {
           front = new QueueNode;
           front->data = item;
           front->link = NULL;
           back = front;
       }

       else
       {
           QueueNodePtr tempPtr;
           tempPtr = new QueueNode;
           tempPtr->data = item;
           tempPtr->link = NULL;
           back->link = tempPtr;
           back = tempPtr;
       }
   }

   //Uses cstdlib and iostream:
   char Queue::remove()
   {
       if (empty())
       {
           cout << "Error: Removing an item from an empty queue.\n";
           exit(1);
       }

       char result = front->data;

       QueueNodePtr discard;
       discard = front;
       front = front->link;
```

## DISPLAY 13.23 Implementation of the Queue Class (part 3 of 3)

```
    if (front == NULL) //if you removed the last node
        back = NULL;

    delete discard;

    return result;
    }
}//queuesavitch
```

### SELF-TEST EXERCISES

- 12. Give the definition of the copy constructor for the class Queue described in Display 13.21.
- 13. Give the definition of the destructor for the class Queue described in Display 13.21.

### CHAPTER SUMMARY

- - A node is a struct or class object that has one or more member variables that are pointer variables. These nodes can be connected by their member pointer variables to produce data structures that can grow and shrink in size while your program is running.
- - A linked list is a list of nodes in which each node contains a pointer to the next node in the list.
- - The end of a linked list (or other linked data structure) is indicated by setting the pointer member variable equal to NULL or nullptr.
- - A stack is a first-in/last-out data structure. A stack can be implemented using a linked list.
- - A queue is a first-in/first-out data structure. A queue can be implemented using a linked list.

### Answers to Self-Test Exercises

- 1. Sally
  Sally
  18
  18

Note that (*head).name and head->name mean the same thing. Similarly, (*head).number and head->number mean the same thing

2. The best answer is

```
head->next = NULL;
```

However, the following is also correct:

```
(*head).next = NULL;
```

3. delete head;

4. head->item = "Wilbur's brother Orville";

```
struct NodeType
{
    char data;
    NodeType *link;
};
typedef NodeType* PointerType;
```

6. The pointer value NULL is used to indicate an empty list.

```
p1 = p1-> next;
```

7. p1 = p1-> next;

8. Pointer discard;

```
discard = p2->next;
//discard now points to the node to be deleted.
p2->next = discard->next;
```

This is sufficient to delete the node from the linked list. However, if you are not using this node for something else, you should destroy the node with a call to delete as follows:

```
delete discard;
```

9. a. Inserting a new item at a known location into a large linked list is more efficient than inserting into a large array. If you are inserting into a list, you have about five operations, most of which are pointer assignments, regardless of the list size. If you insert into an array, on the average you have to move about half the array entries to insert a data item.

For small lists, the answer is (c), about the same.

```
//Uses cstddef:
void Stack::push(char theSymbol)
{
    StackFramePtr tempPtr;
    tempPtr = new StackFrame;
```

```
```cpp
tempPtr->data = theSymbol;
tempPtr->link = top;
top = tempPtr;
}
```
```

```
```cpp
11. //Uses cstddef:
Stack::Stack(const Stack& aStack)
{
    if (aStack.top == NULL)
        top = NULL;
    else
    {
        StackFramePtr temp = aStack.top; //temp moves
            //through the nodes from top to bottom of
            //aStack.
        StackFramePtr end; //Points to end of the new stack.

        end = new StackFrame;
        end->data = temp->data;
        top = end;
        //First node created and filled with data.
        //New nodes are now added AFTER this first node.

        temp = temp->link;
        while (temp != NULL)
        {
            end->link = new StackFrame;
            end = end->link;
            end->data = temp->data;
            temp = temp->link;
        }
        end->link = NULL;
    }
}
```
```

```
```cpp
12. //Uses cstddef:
Queue::Queue(const Queue& aQueue)
{
    if (aQueue.empty())
        front = back = NULL;
    else
    {
        QueueNodePtr tempPtrOld = aQueue.front;
        //tempPtrOld moves through the nodes
        //from front to back of aQueue.
        QueueNodePtr tempPtrNew;
        //tempPtrNew is used to create new nodes.

        back = new QueueNode;
        back->data = tempPtrOld->data;
```

```
listPtr = new Node;
listPtr->name = "Emily";

tempPtr = new Node;
tempPtr->name = "James";
listPtr->link = tempPtr;

tempPtr->link = new Node;
tempPtr = tempPtr->link;
tempPtr->name = "Joules";
tempPtr->link = NULL;

return 0;
}
```

Add code to the main function that:

- a. Outputs in order all names in the list.
- b. Inserts the name "Joshua" in the list after "James" then outputs the modified list.
- c. Deletes the node with "Joules" then outputs the modified list.
- d. Deletes all nodes in the list.

2. Displays 13.13, 13.14 and 13.15 demonstrate a Node represented by a class structure. At the end of the main method in Display 13.15, all the dynamic memory is deleted through a loop outside the class. Without this loop, the program would leak memory. Modify the class definition such that the Node class is able to destroy the objects it points to through a destructor rather than the main method.

### PROGRAMMING PROJECTS

Programming Projects require more problem-solving than Practice Programs and can usually be solved many different ways. Visit www.myprogramminglab.com to complete many of these Programming Projects online and get instant feedback.

- 1. Write a void function that takes a linked list of integers and reverses the order of its nodes. The function will have one call-by-reference parameter that is a pointer to the head of the list. After the function is called, this pointer will point to the head of a linked list that has the same nodes as the original list, but in the reverse of the order they had in the original list. Note that your function will neither create nor destroy any nodes. It will simply rearrange nodes. Place your function in a suitable test program.
- 2. Write a function called mergeLists that takes two call-by-reference arguments that are pointer variables that point to the heads of linked lists of values of type int. The two linked lists are assumed to be sorted so that the number at the head is the smallest number, the number in the next node is the next smallest, and so forth. The function returns a pointer to

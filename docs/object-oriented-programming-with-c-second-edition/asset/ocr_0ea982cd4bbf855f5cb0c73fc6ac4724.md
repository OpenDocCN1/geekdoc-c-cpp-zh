Data Structures 341

The queue class.
Each instance of this class will represent a queue.

```
/*
class Queue : private SingleLinkedList
public:
    /*
    Function to push a value to the end of the queue.
    */
    void push(int);
    /*
    Function to display the values in the nodes of the queue.
    */
    void display();
    /*
    Function to pop a value from the top of the queue.
    */
    void pop();
};
#endif
/*
End of Queue.h*/
```

The above header file contains the definition of the linked queue class. As we can see, the Queue class does private inheritance from the SingleLinkedList class. We already know the reason for inheriting from the SingleLinkedList class. We also know the reason for inheriting privately.
Let have a look at the implementation of the Queue class (Listing 9.27).

# Listing 9.27 Implementation file of the Queue class

```
/*
Beginning of Queue.cpp
*/
#include "Queue.h"
/*
Function to push a value to the end of the queue.
*/
void Queue::push(int pVal)
{
    /*
    Call the base class function.
    */
    appendNode(pVal);
}
/*
Function to display the values in the nodes of the queue.
*/
void Queue::display()
{
    /*
    Call the base class function.
    */
```
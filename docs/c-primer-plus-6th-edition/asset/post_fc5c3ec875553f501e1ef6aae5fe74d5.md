
```cpp
public:
    Customer() { arrive = processstime = 0; }
    void set(long when);
    long when() const { return arrive; }
    int ptime() const { return processstime; }
};
void Customer::set(long when) {
    processstime = std::rand() % 3 + 1;
    arrive = when;
}
```

The default constructor creates a customer. The set() member function sets the arrival time to its argument and randomly picks a value from 1 through 3 for the processing time.

Listing 12.10 gathers together the Queue and Customer class declarations, and Listing 12.11 provides the methods.

# Listing 12.10 queue.h

```cpp
// queue.h -- interface for a queue
#ifndef QUEUE_H_
#define QUEUE_H_
// This queue will contain Customer items
class Customer {
private:
    long arrive; // arrival time for customer
    int processstime; // processing time for customer
public:
    Customer() { arrive = processstime = 0; }
    void set(long when);
    long when() const { return arrive; }
    int ptime() const { return processstime; }
};
```

```cpp
class Queue {
private:
    // class scope definitions
    // Node is a nested structure definition local to this class
    struct Node { Item item; struct Node * next; };
    enum {Q_SIZE = 10};
    // private class members
    Node * front; // pointer to front of Queue
    Node * rear; // pointer to rear of Queue
    int items; // current number of items in Queue
    const int qsize; // maximum number of items in Queue
    // preemptive definition to prevent public copying
    Queue(const Queue & q) : qsize(0) {}
    Queue &operator=(const Queue & q) { return *this; }
public:
    Queue(int qs = Q_SIZE); // create queue with a qs limit
    ~Queue();
    bool empty() const;
    bool isfull() const;
    int queuecount() const;
    bool enqueue(const Item&item); // add item to end
    bool dequeue(Item&item); // remove item from front
};
#endif
```

# Listing 12.11 queue.cpp

```cpp
// queue.cpp -- Queue and Customer methods
#include "queue.h"
#include <cstdlib> // (or stdlib.h) for rand())

// Queue methods
Queue::Queue(int qs) : qsize(qs)
{
    front = nullptr; // or nullptr
    items = 0;
}

Queue::~Queue()
{
    Node * temp;
    while (front != NULL) // while queue is not yet empty
    {
        temp = front; // save address of front item
        front = front->next; // reset pointer to next item
        delete temp; // delete former front
    }
}

bool Queue::isEmpty() const
{
    return items == 0;
}

bool Queue::isfull() const
{
    return items == qsize;
}

int Queue::queuecount() const
{
    return items;
}

// Add item to queue

bool Queue::enqueue(const Item &item)
{
    if (isfull())
        return false;
    Node *add = new Node; // create node
    // on failure, new std::bad_alloc exception
    add->item = item; // set node pointers
    add->next = NULL; // or nullptr;
    items++;
    if (front == NULL) // if queue is empty,
        front = add; // place item at front
    else
        rear->next = add; // else place at rear
    rear = add; // have rear point to new node
    return true;
}

// Place item into item variable and remove from queue

bool Queue::dequeue(Item &item)
{
    if (front == NULL)
        return false;
    item = front->item; // set item to first item in queue
    items--;
    Node *temp = front; // save location of first item
    front = front->next; // reset front to next item
    delete temp;
    if (front == NULL)
        rear = nullptr;
    return true;
}
```

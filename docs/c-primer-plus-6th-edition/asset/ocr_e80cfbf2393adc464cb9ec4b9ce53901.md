shows how this conversion can be made. As is common for class templates, the header file includes the class template, along with method function templates.

# Listing 15.5 queuetp.h

```
// queuetp.h -- queue template with a nested class
#ifndef QUEUETP_H_
#define QUEUETP_H_

template <class Item>
class QueueTP
{
private:
    enum {Q_SIZE = 10};
    // Node is a nested class definition
class Node
{
public:
    Item item;
    Node * next;
    Node(const Item &i):item(i), next(0) {}
};
Node * front; // pointer to front of Queue
Node * rear; // pointer to rear of Queue
int items; // current number of items in Queue
const int qsize; // maximum number of items in Queue
QueueTP(const QueueTP & q) : qsize(0) {}
QueueTP & operator=(const QueueTP & q) { return *this; }
public:
    QueueTP(int qs = Q_SIZE);
    ~QueueTP();
    bool isEmpty() const {
        return items == 0;
    }
    bool isFull() const {
        return items == qsize;
    }
    int queuecount() const
{
}const {
        return items;
    }
    bool enqueue(const Item &item); // add item to end
    bool dequeue(Item &item); // remove item from front
};
```
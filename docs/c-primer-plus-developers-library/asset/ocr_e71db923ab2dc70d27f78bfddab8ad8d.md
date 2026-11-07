```
```cpp
public:
    Customer() { arrive = processtime = 0; }
    void set(long when);
    long when() const { return arrive; }
    int ptime() const { return processtime; }
};
void Customer::set(long when)
{
    processtime = std::rand() % 3 + 1;
    arrive = when;
}
```
```

The default constructor creates a null customer. The set() member function sets the arrival time to its argument and randomly picks a value from 1 through 3 for the processing time.

Listing 12.10 gathers together the Queue and Customer class declarations, and Listing 12.11 provides the methods.

# Listing 12.10  `queue.h`

```
```cpp
// queue.h -- interface for a queue
#ifndef QUEUE_H_
#define QUEUE_H_
// This queue will contain Customer items
class Customer
{
private:
    long arrive;        // arrival time for customer
    int processtime;     // processing time for customer
public:
    Customer() { arrive = processtime = 0; }
    void set(long when);
    long when() const { return arrive; }
    int ptime() const { return processtime; }
};

typedef Customer Item;

class Queue
{
private:
    // class scope definitions
        // Node is a nested structure definition local to this class
        struct Node { Item item; struct Node * next;};
        enum {Q_SIZE = 10};
    // private class members
        Node * front;        // pointer to front of Queue
```
```
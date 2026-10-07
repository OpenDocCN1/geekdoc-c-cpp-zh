# Chapter 12 Classes and Dynamic Memory Allocation

```
class Queue
{
    enum (Q_SIZE = 10);
    private:
        // private representation to be developed later
    public:
        Queue(int gs = Q_SIZE); // create queue with a qs limit
        -Queue();
        bool isEmpty() const;
        bool isFull() const;
        int queuecount() const;
        bool enqueue(Item &item); // add item to end
        bool dequeue(Item &item); // remove item from front
};
```

The constructor creates an empty queue. By default, the queue can hold up to 10 items, but that can be overridden with an explicit initialization argument:

```
Queue line1; // queue with 10-item limit
Queue line2(20); // queue with 20-item limit
```

When using the queue, you can use a typedef to define Item. (In Chapter 14, "Reusing Code in C++", you’ll learn how to use templates instead.

# The Queue Class Implementation

After you determine the interface, you can implement it. First, you have to decide how to represent the queue data. One approach is to use new to dynamically allocate an array with the required number of elements. However, arrays are not a good match for queue operations. For example, removing an from the front of the array should be followed by shifting every element one closer to the front. Otherwise, you need to do something more elaborate, such as treat the array as circular. Using a linked list, however, is a reasonable fit to the requirements of a queue. A linked list consists of a sequence of nodes. Each node contains the information to be held in the list, plus a pointer to the next node in the list. For the queue in this example, each data part is a type Item value, and you can use a structure to represent a node:

```
struct Node
{
    Item item; // data stored in the node
    struct Node *next; // pointer to next node
};
```

Figure 12.8 illustrates a linked list.
The example in Figure 12.8 is called a singly linked list because each node has a single link, or pointer, to another node. If you have the address of the first node, you can follow the pointers to each subsequent node in the list. Commonly, the pointer in the last node in the list is set to NULL (or, equivalently, to O) to indicate that there are no further nodes. With C++11, you should use the new nullptr keyword. To keep track of a linked
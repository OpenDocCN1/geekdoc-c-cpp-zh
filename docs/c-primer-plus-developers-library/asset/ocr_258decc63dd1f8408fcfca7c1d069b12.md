```
```cpp
//...
};
```
```

This is equivalent to using a member initialization list in the constructors:

```
```cpp
Classy::Classy() : mem1(10), mem2(20) {...}
```
```

The members mem1 and mem2 get initialized to 10 and 20, respectively, unless a constructor using a member initialization list is called. Then the actual list overrides these default initializations:

```
```cpp
Classy::Classy(int n) : mem1(n) {...}
```
```

In this case, the constructor would use the value of n to initialize mem1, and mem2 still would be set to 20.

The code for isempty(), isfull(), and dequeue() is simple. If items is 0, the queue is empty. If items is qsize, the queue is full. Returning the value of items answers the question of how many items are in the queue. You’ll see the code later this chapter in Listing 12.11.

Adding an item to the rear of the queue (enqueuing) is more involved. Here is one approach:

```
```cpp
bool Queue::enqueue(const Item & item)
{
    if (isfull())
        return false;
    Node * add = new Node;  // create node
    // on failure, new throws std::bad_alloc exception
        add->item = item;       // set node pointers
        add->next = NULL;       // or nullptr;
        items++;
        if (front == NULL)      // if queue is empty,
            front = add;        // place item at front
        else
        {
            rear->next = add;   // else place at rear
            rear = add;          // have rear point to new node
        }
        return true;
}
```
```

In brief, the method goes through the following phases (see Figure 12.10):

+   1. Terminate if the queue is already full. (For this implementation, the maximum size is selected by the user via the constructor.)
+   
+   2. Create a new node. If new can’t do so, it throws an exception, which is a topic taken up in Chapter 15, “Friends, Exceptions, and More.” The practical upshot is that unless one provides additional programming to handle the exception, the program terminates.
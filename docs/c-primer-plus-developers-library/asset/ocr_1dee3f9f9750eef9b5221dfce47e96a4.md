Because a structure is a class whose members are public by default, Node really is a nested class. However, this definition doesn’t take advantage of class abilities. In particular, it lacks an explicit constructor. Let’s remedy that now.

First, you need to find where Node objects are created in the Queue example. Examining the class declaration (see Listing 12.10) and the methods definitions (see Listing 12.11) reveals that the only place in which Node objects are created is in the enqueue() method:

```
```cpp
bool Queue::enqueue(const Item & item)
{
    if (isfull())
        return false;
    Node * add = new Node;  // create node
    // on failure, new throws std::bad_alloc exception
    add->item = item;       // set node pointers
    add->next = NULL;
    ...
}
```
```

This code explicitly assigns values to the Node members after creating a Node. This is the sort of work that is more properly done by a constructor.

Knowing now where and how a constructor should be used, you can provide an appropriate constructor definition:

```
```cpp
class Queue
{
    // class scope definitions
        // Node is a nested class definition local to this class
        class Node
        {
        public:
            Item item;
            Node * next;
            Node(const Item & i) : item(i), next(0) { }
        };
        ...
};
```
```

This constructor initializes the node’s item member to i and sets the next pointer to 0, which is one way of writing the null pointer in C++. (Using NULL would require including a header file that defines NULL. Users of a C++11-compliant compiler can use nullptr.) Because all nodes created by the Queue class have next initially set to the null pointer, this is the only constructor the class needs.

Next, you need to rewrite enqueue() by using the constructor

```
```cpp
bool Queue::enqueue(const Item & item)
{
    if (isfull())
        return false;
```
```
+   - A queue can be implemented as a linked list.
+   - When implementing a stack, you need only keep track of one end of the list of entries, but when implementing a queue, you need to keep track of both ends of the list.
+   - A deque (or “double-ended queue”) allows quick removal and insertion of elements from both ends. It can be implemented with a circular array, a doubly linked list or more complex structures of pointers.

# FIGURE 8.14 Reference Return Values from STL Member Functions

# For the stack<Item> Template Class

```
stack<Item> b;
const stack<Item>& c;
// For these declarations, the return value of b.top() is Item& (a reference to an
// Item), so that b.top() can be used to change the top item (such as the
// assignment statement: b.top() = 42;
// But the return value of c.top() is const Item& (a reference to a constant
// Item), which cannot be used to change the item in the stack.
```

# For the queue<Item> Template Class

```
queue<Item> b;
const queue<Item>& c;
// For these declarations, the return value of b.front() is Item& (a reference to an
// Item), so that b.front() can be used to change the front item (such as the
// assignment statement: b.front() = 42;
// But the return value of c.front() is const Item& (a reference to a constant
// Item), which cannot be used to change the item in the queue.
```

# For the priority_queue<Item> and deque<Item> Template Classes

```
priority_queue<Item> b;
const priority_queue<Item>& c;
deque<Item> b;
deque<Item>& c;
// The back(), front(), and top() member functions all return const references,
// which cannot be used to change the item.
```
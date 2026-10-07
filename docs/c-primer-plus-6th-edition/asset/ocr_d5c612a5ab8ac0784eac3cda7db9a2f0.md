The sort(), merge(), unique() methods also each have a version that accepts an additional argument to specify an alternative function be used for comparing elements. Similarly, the remove() method has a version with an additional argument that specifies a function used to determine whether an element is removed. These arguments are examples of predicate functions, to which we will return later.

# forward_list (C++11)

C++11 adds forward_list as a container class. This class implements a singly linked list. In this kind of list, each item is linked to the next item, but not to the preceding item. Therefore, the class requires a forward iterator, not a bidirectional one.Thus, unlike vector and list, forward_list isn't a reversible container. Compared to list, forward_list is simpler, more compact, but with better features

# queue

The queue template (declared in the queue header file) is an adapter class. Recall that theostream template is an adapter that allows output stream to use the iterator interface. Similarly, the queue template allows an underlying class (deque, by default) to exhibit the typical queue interface.

The queue template is more restrictive than the deque. Not only does it permit access to elements of a queue, the queue doesn't allow you to iterate through a queue. Instead, it limits you to the basic operations that define a queue.You can add an element to the rear of a queue, remove an element from the front of a queue, view the values of the front and rear elements, check the number of elements, and test to see if a queue is empty.Table.10 lists these operations.

Note that pop() is a data removal method, not a data retrieval method. If you want to use a value from a queue, you first use front() to retrieve the value and then use pop() to remove it from the queue.

# Table 16.10 queue Operations

| Method | Description |
| --- | --- |
| bool empty() const | Returns true if the queue is empty and false otherwise. |
| size_type size() const | Returns the number of elements in the queue. |
| T& front() | Returns a reference to the element at the front of the queue. |
| T& back() | Returns a reference to the element at the back of the queue. |
| void push(const T& x) | Inserts x at the back of the queue. |
| void pop() | Removes the element at the front of the queue. |

# priority_queue

The priority_queue template class (declared in the queue header file) is another adapter class. It supports the same operations as queue.The main difference between the two is that with priority_queue, the largest item gets to the front of the queue. (Life is
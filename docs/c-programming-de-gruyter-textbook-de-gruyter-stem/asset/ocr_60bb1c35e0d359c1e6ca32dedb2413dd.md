# 408 10 Generic Programming and the Standard Template Library

These three ways are standard ways to add elements into a sequential container.
Calling push_front() or push_back(), using insert(), and using the assignment operator are the three standard ways to add elements to a sequential container.

# b) Removing Elements

There are also a number of ways to remove elements in a container. We should notice to remove elements rather than the container's destructor. The first method is to call pop_front() or pop_back(). They remove the element at the head and the element at the tail of the container, respectively.

The second way is to call the erase() method. erase(L1, L2) removes all elements at location L between locations L1 and L2.

The third way is to call the clear() method, which removes all elements in the container.
Removing elements will also invalidate iterators. erase() and clear() will invalidate the iterators to the deleted elements in list container. The effect of removing elements from the head or the tail of the double queue is the same as the one in list, but removing an element from the middle of a double queue will invalidate all iterators. Removing elements in vectors also invalidate all iterators.

# c) Traversing the Sequential Container

The iterator is the object-oriented approach to traverse a container. It overloads the dereference operator "*" to return the reference of the element it points to, just as a normal pointer.

# d) Other Ways to Access Elements in a Sequential Container

Programmer can use methods front() and back() to access the element at the head or at the tail of the container respectively. subscript operator "[]" can also be used to directly access elements in the container, which is only available in vectors and double queues. For example, in a double queue A that holds 15 elements, A[7] points to the seventh element in the queue, and A[N] points to the N-th element in A. Table 10.3 demonstrates these methods.

# 2. Vectors

The vector is a variable length linear collection designed to provide rapid access for objects. It is very similar to the static array, but vectors can change their storage size on demand at runtime.

Vectors are powerful containers. They can be used to implement queues, stacks, lists, or other complicated data structures.
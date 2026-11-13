# CHAPTER SUMMARY

+   - A linked list consists of nodes; each node contains some data and a pointer to the next node in the list. The pointer field of the final node contains the null pointer.
+   - Typically, a linked list is accessed through a head pointer that points to the head node (i.e., the first node). Sometimes a linked list is accessed elsewhere, such as through the tail pointer that points to the last node.
+   - You should be familiar with our functions to manipulate a linked list. These functions follow basic patterns that every programmer uses. Such functions are not node member functions (so that they can handle empty lists with no nodes).
+   - Linked lists can be used to implement a class. Such a class has one or more private member variables that are pointers to nodes in a linked list. The member functions of the class use the linked-list functions to manipulate the linked list, which is accessed through private member variables.
+   - You have seen two classes implemented with the linked-list toolkit: a bag and a list. You will see more in the chapters that follow.
+   - A doubly linked list has nodes with two pointers: one to the next node and one to the previous node. Doubly linked lists are a good choice for supporting a cursor that moves forward and backward.
+   - Classes can often be implemented in many different ways, such as by using a dynamic array or using a linked list. In general, arrays are better at random access; linked lists are better at insertions/removals at a cursor. In the STL, the vector uses a dynamic array and the list uses a linked list. A third choice, the STL deque, uses a mechanism that we’ll see later.

# Solutions to Self-Test Exercises

+   1. See the class definition on page 226.
+   2. The null pointer is a special value that can be used for any pointer that does not point anywhere. The `cstddef` library should be included to use NULL, but because NULL is not part of the std namespace, it can be written without preceding `std::`.
+   3. The null pointer is used for the link field of the final node of a linked list; it is also used for the head and tail pointers of a list that doesn't yet have any nodes.
+   4. Numbers are given a default value of 0, and bools are given a default value of false.
+   5. `head_ptr` is a pointer to a node. On the other hand, `*head_ptr` is a node, and the type of `head_ptr->data()` is `node::value_type`.
+   6. `if (head_ptr->data() == 0)
+       cout << "zero";`
+   7. The operation of accessing a data member has higher precedence than the dereferencing asterisk. Therefore, `*head_ptr.data()` will cause a syntax error because the call to `data()` is attempted before dereferencing `head_ptr`. The alternative syntax is `head_ptr->data();`
+   8. `cout << b_ptr->size();`
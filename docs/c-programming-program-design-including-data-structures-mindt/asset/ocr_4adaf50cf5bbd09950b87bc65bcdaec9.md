Use the linked list created by this code to answer the following questions. (These questions are independent of each other.) Declare additional pointers if you need them.

+   a. Which pointer points to the first node of the linked list?
+   
+   b. Determine the order of the nodes of the linked list.
+   
+   c. Write a C++ code that creates and inserts a node with `info 45` after the node with `info 16`.
+   
+   d. Write a C++ code that creates and inserts a node with `info 58` before the node with `info 25`. Does this require you to change the value of the pointer that was pointing to the first node of the linked list?
+   
+   e. Write a C++ code that deletes the node with `info 25`. Does this require you to change the value of the pointer that was pointing to the first node of the linked list?

+   19. a. What does the function begin of the `class linkedListType` do? (5, 6)
+   
+   b. What does the function end of the `class linkedListType` do? (5, 6)

20. How does the function `insertFirst` of the class `unorderedLinkedList` differ from the function `insertFirst` of the class `orderedLinkedList`. (7, 8)

21. Consider the following C++ statements. (The class `unorderedLinkedList` is as defined in this chapter.) (6, 8)

```
unorderedLinkedList<int> list;

list.insertFirst(36);
list.insertLast(10);
list.insertFirst(65);
list.insertLast(30);
list.insertFirst(44);
list.deleteNode(10);
list.insertLast(27);
list.insertFirst(15);
list.insertFirst(5);
list.deleteNode(44);
list.deleteNode(87);

linkedListIterator<int> it;

for (it = list.begin(); it != list.end(); ++it)
    cout << *it << " ";
cout << endl;
```

What is the output of this program segment?
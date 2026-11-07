+   3. Extend the `class linkedListType` by adding the following operations:
+      a. Write a function that returns the info of the kth element of the linked list. If no such element exists, terminate the program.
+      b. Write a function that deletes the kth element of the linked list. If no such element exists, terminate the program.
+      Provide the definitions of these functions in the `class linkedListType`. Also, write a program to test these functions. (Use either the `class unorderedLinkedList` or the `class orderedLinkedList` to test your function.)

+   4. **(Printing a single linked list backward)** Include the functions `reversePrint` and `recursiveReversePrint`, as discussed in this chapter, in the `class linkedListType`. Also, write a program function to print a (single) linked list backward. (Use either the `class unorderedLinkedList` or the `class orderedLinkedList` to test your function.)

+   5. **(Dividing a linked list into two sublists of almost equal sizes)**
+      a. Add the operation `divideMid` to the `class linkedListType` as follows:

```
```cpp
void divideMid(linkedListType<Type> &subList);
    //This operation divides the given list into two sublists
    //of (almost) equal sizes.
    //Postcondition: first points to the first node and last
    //               points to the last node of the first
    //               sublist.
    //               subList.first points to the first node
    //               and subList.last points to the last node
    //               of the second sublist.
```
```

Consider the following statements:

```
```cpp
unorderedLinkedList<int> myList;
unorderedLinkedList<int> subList;
```
```

Suppose `myList` points to the list with elements 34 65 27 89 12 (in this order). The statement:

```
```cpp
myList.divideMid(subList);
```
```

divides `myList` into two sublists: `myList` points to the list with the elements 34 65 27, and `subList` points to the sublist with the elements 89 12.

+   b. Write the definition of the function template to implement the operation `divideMid`. Also, write a program to test your function.

+   6. **(Splitting a linked list, at a given node, into two sublists)**
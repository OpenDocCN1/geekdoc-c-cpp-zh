b. Find and delete all occurrences of a given info from the list. (Traverse the list only once.)

Add these as abstract functions in the `class linkedListType` and provide the definitions of these functions in the `class unorderedLinkedList`. Also, write a program to test these functions.

# 3. Extend the `class linkedListType` by adding the following operations:

+   a. Write a function that returns the info of the *k*th element of the linked list. If no such element exists, terminate the program.
+   
+   b. Write a function that deletes the *k*th element of the linked list. If no such element exists, terminate the program.
+   
+   Provide the definitions of these functions in the `class linkedListType`. Also, write a program to test these functions. (Use either the `class unorderedLinkedList` or the `class orderedLinkedList` to test your function.)

# 4. (Printing a single linked list backward)

Include the functions `reversePrint` and `recursiveReversePrint`, as discussed in this chapter, in the `class linkedListType`. Also, write a program function to print a (single) linked list backward. (Use either the `class unorderedLinkedList` or the `class orderedLinkedList` to test your function.)

# 5. (Dividing a linked list into two sublists of almost equal sizes)

+   a. Add the operation `divideMid` to the `class linkedListType` as follows:

```
void divideMid(linkedListType<Type> &sublist);
//This operation divides the given list into two sublists
//of (almost) equal sizes.
//Postcondition: first points to the first node and last
//              points to the last node of the first
//              sublist.
//              sublist.first points to the first node
//              and sublist.last points to the last node
//              of the second sublist.
```

Consider the following statements:

`unorderedLinkedList<int> myList;`
`unorderedLinkedList<int> subList;`

Suppose myList points to the list with elements 34 65 27 89 12 (in this order). The statement:

`myList.divideMid(subList);`

divides myList into two sublists: myList points to the list with the elements 34 65 27, and subList points to the sublist with the elements 89 12.

+   b. Write the definition of the function template to implement the operation `divideMid`. Also, write a program to test your function.
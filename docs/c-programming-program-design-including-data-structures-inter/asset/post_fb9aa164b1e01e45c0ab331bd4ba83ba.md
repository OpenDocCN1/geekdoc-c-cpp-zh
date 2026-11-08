
## QUICK REVIEW

- 1. A linked list is a list of items, called nodes, in which the order of the nodes is determined by the address, called a link, stored in each node.
- 2. The pointer to a linked list—that is, the pointer to the first node in the list—is stored in a separate location called the head or first.
- 3. A linked list is a dynamic data structure.
- 4. The length of a linked list is the number of nodes in the list.
- 5. Item insertion and deletion from a linked list do not require data movement; only the pointers are adjusted.
- 6. A (single) linked list is traversed in only one direction.
- 7. The search on a linked list is sequential.
- 8. The first (or head) pointer of a linked list is always fixed, pointing to the first node in the list.
- 9. To traverse a linked list, the program must use a pointer different than the head pointer of the list, initialized to the first node in the list.
- 10. In a doubly linked list, every node has two links: one points to the next node and one points to the previous node.
- 11. A doubly linked list can be traversed in either direction.
- 12. In a doubly linked list, item insertion and deletion require the adjustment of two pointers in a node.
- 13. A linked list in which the last node points to the first node is called a circular linked list.

## EXERCISES

- 1. Mark the following statements as true or false.
  - a. In a linked list, the order of the elements is determined by the order in which the nodes were created to store the elements.
  - b. In a linked list, memory allocated for the nodes is sequential.
  - c. A single linked list can be traversed in either direction.
  - d. In a linked list, nodes are always inserted either at the beginning or the end because a linked list is not a random-access data structure.
- 2. Describe the two typical components of a single linked list node.
- 3. What is stored in the link field of the last node of a nonempty single linked list?
- 4. Suppose that first is a pointer to a linked list. What is stored in first?
- 5. Suppose that the fourth node of a linked list is to be deleted, and a pointer points to the fourth node? Why do you need a pointer to the third node of the linked list?

Consider the linked list shown in Figure 16-50. Assume that the nodes are in the usual info-link form. Use this list to answer Exercises 6 through 14. If necessary, declare additional variables. (Assume that list, current, temp, trail, and last are pointers of type nodeType.)

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1156_0.png)

**FIGURE 16-50** Linked list for exercises 6 through 14

- 6. What is the output, if any, of each of the following C++ statements?
  - a. `cout << current->info;`
  - b.
    ```cpp
    current = current->link;
    cout << current->info;
    ```
  - c. `cout << temp->link->link->info;`
  - d.
    ```cpp
    trail->link = NULL;
    cout << trail->info;
    ```
  - e. `cout << last->link->info;`
- 7. What is the value of each of the following relational expressions?
  - a. `current->link == temp`
  - b. `temp->link->link->info == 50`
  - c. `trail->link->link == 0`
  - d. `last->link == NULL`
  - e. `list == current`
- 8. What are the effects, if any, of each of the following C++ statements?
  - a.
    ```cpp
    trail->link = NULL;
    delete last;
    ```
  - b. `temp->link = trail;`
  - c. `list->info = 19;`
  - d.
    ```cpp
    current = current->link;
    current->link = temp->link;
    ```
- 9. Write C++ statements to do the following:
  - a. Set the info of the second node to 52.
  - b. Make current point to the node with info 10.
  - c. Make trail point to the node before temp.
  - d. Make temp point to an empty list.
  - e. Set the value of the node before trail to 36.
  - f. Write a while loop to make current point to the node with info 10.
- 10. Mark each of the following statements as valid or invalid. If a statement is invalid, explain why.
  - a. `current = list;`
  - b. `temp->link->link = NULL;`
  - c. `trail->link = 0;`
  - d. `*temp = last;`
  - e. `list = 75;`
  - f. `temp->link->info = 75;`
  - g. `current->info = trail->link;`
  - h. `*list = *last;`
  - i. `current = last;`
  - j. `cout << trail->link->link->info;`
- 11. Write C++ statements to do the following:
  - a. Write a C++ code so that current traverses the entire list.
  - b. Create the node with info 68 and insert between trail and last.
  - c. Delete the last node of the list and also deallocate the memory occupied by this node. After deleting the node, make last point to the last node of the list and the link of the last node must be NULL.
  - d. Delete the node with info 10. Also, deallocate the memory occupied by this node.
- 12. What is the output of the following C++ code?
  - a.
    ```cpp
    while (current != NULL)
        cout << current->info << " ";
        current = current->link;
        cout << endl;
    ```
  - b.
    ```cpp
    while (current != last)
        current = current->link;
        cout << current->info << " ";
        cout << endl;
    ```
- 13. If the following C++ code is valid, show the output. If it is invalid, explain why.

  ```cpp
  temp = current;               //Line 1
  current = current->link;      //Line 2
  current->link = last;         //Line 3
  trail = current->link;        //Line 4
  trail = trail->link;          //Line 5
  cout << current->info << " "
       << trail->info << endl;  //Line 6
  ```

```cpp
{
    cout << current->info << " ";
    current = current->link;
}
cout << endl;
```

- 17. Assume that the node of a linked list is in the usual info-link form with the info of type int. The following data, as described in parts (a) to (d), is to be inserted into an initially empty linked list: 72, 43, 8, 12. Suppose that head is a pointer of type nodeType. After the linked list is created, head should point to the first node of the list. Declare additional variables as you need them. Write the C++ code to create the linked list. After the linked list is created, write a code to print the list. What is the output of your code?
  - a. Insert 72 into an empty linked list.
  - b. Insert 43 before 72.
  - c. Insert 8 at the end of the list.
  - d. Insert 12 after 43.
- 18. Assume that the node of a linked list is in the usual info-link form with the info of type int. (list and ptr are pointers of type nodeType.) The following code creates a linked list:

  ```cpp
  ptr = new nodeType;
  ptr->info = 16;
  list = new nodeType;
  list->info = 25;
  list->link = ptr;
  ptr = new nodeType;
  ptr->info = 12;
  ptr->link = NULL;
  list->link->link = ptr;
  ```

  Use the linked list created by this code to answer the following questions. (These questions are independent of each other.) Declare additional pointers if you need them.

  - a. Which pointer points to the first node of the linked list?
  - b. Determine the order of the nodes of the linked list.
  - c. Write a C++ code that creates and inserts a node with info 45 after the node with info 16.
  - d. Write a C++ code that creates and inserts a node with info 58 before the node with info 25. Does this require you to change the value of the pointer that was pointing to the first node of the linked list?
  - e. Write a C++ code that deletes the node with info 25. Does this require you to change the value of the pointer that was pointing to the first node of the linked list?
- 19. Consider the following C++ statements. (The class unorderedLinkedList is as defined in this chapter.)

  ```cpp
  unorderedLinkedList<int> list;

  list.insertFirst(38);
  list.insertFirst(42);
  list.insertLast(55);
  list.insertFirst(60);
  list.insertLast(18);
  list.insertLast(35);
  list.insertFirst(66);
  list.deleteNode(60);
  list.insertFirst(93);
  list.deleteNode(42);
  list.deleteNode(12);
  list.print();
  cout << endl;
  ```

  What is the output of this program segment?
- 20. Suppose the input is:

  ```text
  45 35 12 83 40 23 11 98 64 120 16 -999
  ```

  What is the output of the following C++ code? (The class unorderedLinkedList is as defined in this chapter.)

  ```cpp
  unorderedLinkedList<int> list;
  unorderedLinkedList<int> copyList;
  int num;

  cin >> num;
  while (num != -999)
  {
      if (num % 4 == 0 || num % 3 == 0)
          list.insertFirst(num);
      else
          list.insertLast(num);
      cin >> num;
  }

  cout << "list = ";
  list.print();
  cout << endl;

  copyList = list;

  copyList.deleteNode(33);
  copyList.deleteNode(58);

  cout << "copyList = ";
  copyList.print();
  cout << endl;
  ```

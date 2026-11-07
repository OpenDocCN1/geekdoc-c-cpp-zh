What is the output of the following C++ code? (The class `unorderedLinkedList` is as defined in this chapter.) (8)

```
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
```

+   23. Draw the UML diagram of the class `doublyLinkedList` as discussed in this chapter. (10)

+   24. Draw the UML diagram of the class `dvdType` of the DVD Store programming example.

+   25. Draw the UML diagram of the class `dvdListType` of the DVD Store programming example.

# PROGRAMMING EXERCISES

+   1. **(Online Address Book revisited)** Programming Exercise 5 in Chapter 11 could handle a maximum of only 500 entries. Using linked lists, redo the program to handle as many entries as required. Add the following operations to your program:
+      a. Add or delete a new entry to the address book.
+      b. Allow the user to save the data in the address book.

+   2. Extend the class `linkedListType` by adding the following operations:
+      a. Find and delete the node with the smallest info in the list. (Delete only the first occurrence and traverse the list only once.)
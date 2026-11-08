
- 21. Draw the UML diagram of the class `doublyLinkedList` as discussed in this chapter.
- 22. Draw the UML diagram of the class `dvdType` of the DVD Store programming example.
- 23. Draw the UML diagram of the class `dvdListType` of the DVD Store programming example.

## PROGRAMMING EXERCISES

- 1. **(Online Address Book revisited)** Programming Exercise 5 in Chapter 11 could handle a maximum of only 500 entries. Using linked lists, redo the program to handle as many entries as required. Add the following operations to your program:
  - a. Add or delete a new entry to the address book.
  - b. Allow the user to save the data in the address book.

- 2. Extend the class `linkedListType` by adding the following operations:
  - a. Find and delete the node with the smallest `info` in the list. (Delete only the first occurrence and traverse the list only once.)
  - b. Find and delete all occurrences of a given `info` from the list. (Traverse the list only once.)

  Add these as abstract functions in the class `linkedListType` and provide the definitions of these functions in the class `unorderedLinkedList`. Also, write a program to test these functions.

- 3. Extend the class `linkedListType` by adding the following operations:
  - a. Write a function that returns the `info` of the k<sup>th</sup> element of the linked list. If no such element exists, terminate the program.
  - b. Write a function that returns the k<sup>th</sup> element of the linked list. If no such element exists, terminate the program.

  Provide the definitions of these functions in the class `linkedListType`. Also, write a program to test these functions. (Use either the class `unorderedLinkedList` or the class `orderedLinkedList` to test your function.)

- 4. **(Printing a single linked list backward)** Include the functions `reversePrint` and `recursiveReversePrint`, as discussed in this chapter, in the class `linkedListType`. Also, write a program function to print a (single) linked list backward. (Use either the class `unorderedLinkedList` or the class `orderedLinkedList` to test your function.)

- 5. **(Dividing a linked list into two sublists of almost equal sizes)**
  - a. Add the operation `divideMid` to the class `linkedListType` as follows:

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

```
unorderedLinkedList<int> myList;
unorderedLinkedList<int> subList;
```

Suppose `myList` points to the list with elements 34 65 27 89 12 (in this order). The statement:

```
myList.divideMid(subList);
```

divides myList into two sublists: myList points to the list with the elements 34 65 27, and subList points to the sublist with the elements 89 12.

  - b. Write the definition of the function template to implement the operation `divideMid`. Also, write a program to test your function.

- 6. **(Splitting a linked list, at a given node, into two sublists)**
  - a. Add the following operation to the class `linkedListType`:

```
void divideAt(linkedListType<Type> &secondList,
              const Type& item);
//Divide the list at the node with the info item into two
//sublists.
//Postcondition: first and last point to the first and
//              last nodes of the first sublist.
//              secondList.first and secondList.last
//              point to the first and last nodes of the
//              second sublist.
```

Consider the following statements:

```
unorderedLinkedList<int> myList;
unorderedLinkedList<int> otherList;
```

Suppose `myList` points to the list with the elements 34 65 18 39 27 89 12 (in this order). The statement:

```cpp
myList.divideAt(otherList, 18);
```

divides `myList` into two sublists: `myList` points to the list with the elements 34 65, and `otherList` points to the sublist with the elements 18 39 27 89 12.

  - b. Write the definition of the function template to implement the operation `divideAt`. Also, write a program to test your function.

- 7.
  - a. Add the following operation to the class `orderedLinkedList`:

```
void mergeLists(orderedLinkedList<Type>& list1,
                orderedLinkedList<Type>& list2);
//This function creates a new list by merging the
//elements of list1 and list2.
//Postcondition: first points to the merged list
//              list1 and list2 are empty
```

Consider the following statements:

```
orderedLinkedList<int> newList;
orderedLinkedList<int> list1;
orderedLinkedList<int> list2;
```

Suppose `list1` points to the list with the elements 2 6 7, and `list2` points to the list with the elements 3 5 8. The statement:

```
newList.mergeLists(list1, list2);
```

creates a new linked list with the elements in the order 2 3 5 6 7 8, and the object `newList` points to this list. Also, after the preceding statement executes, `list1` and `list2` are empty.

  - b. Write the definition of the function template `mergeLists` to implement the operation `mergeLists`.

- 8. The function `insert` of the class `orderedLinkedList` does not check if the item to be inserted is already in the list; that is, it does not check for duplicates. Rewrite the definition of the function `insert` so that before inserting the item, it checks whether the item to be inserted is already in the list. If the item to be inserted is already in the list, the function outputs an appropriate error message. Also, write a program to test your function.

- 9. In this chapter, the class to implement the nodes of a linked list is defined as a `struct`. The following rewrites the definition of the `struct nodeType` so that it is declared as a class and the member variables are private:

```
template <class Type>
class nodeType
{
```

the member functions of the class nodeType to access the info and link fields of a node. Also, write programs to test various operations of the classes unorderedLinkedList and orderedLinkedList.

- 11. Write the definitions of the function copyList, the copy constructor, and the function to overload the assignment operator for the class doublyLinkedList.

- 12. Write a program to test various operations of the class doublyLinkedList.

- 13. **(Circular linked lists)** This chapter defined and identified various operations on a circular linked list.
  - a. Write the definitions of the class circularLinkedList and its member functions. (You may assume that the elements of the circular linked list are in ascending order.)
  - b. Write a program to test various operations of the class defined in (a).

- 14. **(DVD Store programming example)**
  - a. Complete the design and implementation of the class customerType defined in the DVD Store programming example.
  - b. Design and implement the class customerListType to create and maintain a list of customers for the DVD store.

- 15. **(DVD Store programming example)** Complete the design and implementation of the DVD store program. In other words, write a program that uses the classes designed in the DVD Store programming example and in Programming Exercise 14 to make a DVD store operational.

- 16. Extend the class linkedListType by adding the following function:

```
void rotate();
//Function to remove the first node of a linked list and put it
//at the end of the linked list.
```

Also write a program to test your function. Use the class unorderedLinkedList to create a linked list.

- 17. Write a program that prompts the user to input a string and then outputs the string in the pig Latin form. The rules for converting a string into pig Latin form are described in Programming Example: Pig Latin Strings of Chapter 7. Your program must store the characters of a string into a linked list and use the function rotate, as described in Programming Exercise 16, to rotate the string.

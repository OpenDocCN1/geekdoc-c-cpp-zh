
The following program tests various operations on an ordered linked list:

```cpp
//Program to test the various operations on an ordered linked list
#include <iostream>
#include "OrderedLinkedList.h"

using namespace std;

int main()
{
    orderedLinkedList<int> list1, list2;        //Line 1
    int num;                                     //Line 2

    cout << "Line 3: Enter numbers ending "
         << "with -999." << endl;              //Line 3
    cin >> num;                                  //Line 4
    while (num != -999)                          //Line 5
    {
        list1.insert(num);                       //Line 6
        cin >> num;                              //Line 7
    }

    cout << endl;                                //Line 8

    cout << "Line 9: list1: ";                  //Line 9
    list1.print();                               //Line 10
    cout << endl;                                //Line 11

    list2 = list1; //test the assignment operator  //Line 12

    cout << "Line 13: list2: ";                 //Line 13
    list2.print();                               //Line 14
    cout << endl;                                //Line 15

    cout << "Line 16: Enter the number to be "
         << "deleted: ";                        //Line 16
    cin >> num;                                  //Line 17
    cout << endl;                                //Line 18

    list2.deleteNode(num);                       //Line 19

    cout << "Line 20: After deleting "
         << num << ", list2: " << endl;         //Line 20
    list2.print();                               //Line 21
    cout << endl;                                //Line 22

    return 0;
}
```

Sample Run: In this sample run, the user input is shaded.

```text
Line 3: Enter numbers ending with -999.
23 65 34 72 12 82 36 55 29 -999
Line 9: list1: 12 23 29 34 36 55 65 72 82
Line 13: list2: 12 23 29 34 36 55 65 72 82
Line 16: Enter the number to be deleted: 34
Line 20: After deleting 34, list2:
12 23 29 36 55 65 72 82
```

The preceding output is self-explanatory. The details are left as an exercise for you.

> **NOTE**
>
> Notice that the function `insert` does not check whether the item to be inserted is already in the list, that is, it does not check for duplicates. Programming Exercise 8 at the end of this chapter asks you to revise the definition of the function `insert` so that before inserting the item, it checks whether it is already in the list. If the item to be inserted is already in the list, the function outputs an appropriate error message. In other words, duplicates are not allowed.

## Print a Linked List in Reverse Order (Recursion Revisited)

The nodes of an ordered list (as constructed previously) are in ascending order. Certain applications, however, might require the data to be printed in descending order, which means that we must print the list backward. We now discuss the function `reversePrint`. Given a pointer to a list, this function prints the elements of the list in reverse order.

Consider the linked list shown in Figure 16-37.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1167_0.png)

**FIGURE 16-37** Linked list

For the list in Figure 16-37, the output should be in the following form:

```text
20 15 10 5
```

Because the links are in only one direction, we cannot traverse the list backward starting from the last node. Let us see how we can effectively use recursion to print the list in reverse order.

Let us think in terms of recursion. We cannot print the info of the first node until we have printed the remainder of the list (that is, the tail of the first node). Similarly, we cannot print the info of the second node until we have printed the tail of the second node, and so on. Every time we consider the tail of a node, we reduce the size of the list by 1. Eventually, the size of the list will be reduced to zero, in which case the recursion will stop. Let us first write the algorithm in pseudocode. (Suppose that current is a pointer to a linked list.)

```cpp
if (current != nullptr)
{
    reversePrint(current->link);    //print the tail
    cout << current->info << endl;  //print the node
}
```

Here, we do not see the base case; it is hidden. The list is printed only if the pointer to the list is not nullptr. Also, in the body of the if statement, the recursive call is on the tail of the list. Because eventually the tail of the list will be empty, the if statement in the next call will fail, and the recursion will stop. Also, note that statements (for example, printing the info of the node) appear after the recursive call; thus, when the transfer comes back to the calling function, we must execute the remaining statements. Recall that the function exits only after the last statement executes. (By the “last statement,” we do not mean the physical last statement, but rather the logical last statement.)

Let us write the previous function in C++ and then apply it to a list.

```cpp
template <class Type>
void linkedListType<Type>::reversePrint
                (nodeType<Type> *current) const
{
    if (current != nullptr)
    {
        reversePrint(current->link);    //print the tail
        cout << current->info << " ";   //print the node
    }
}
```

Consider the statement:

```cpp
reversePrint(first);
```

in which `first` is a pointer of type `nodeType<Type>`.

Let us trace the execution of this statement, which is a function call, for the list shown in Figure 16-37. Because the formal parameter is a value parameter, the value of the actual parameter is passed to the formal parameter. See Figure 16-38.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1169_0.png)

**FIGURE 16-38** Execution of the statement `reversePrint(first);`

### printListReverse

Now that we have written the function `reversePrint`, we can write the definition of the function `printListReverse`. Its definition is:

```cpp
template <class Type>
void linkedListType<Type>::printListReverse() const
{
    reversePrint(first);
    cout << endl;
}
```

## Doubly Linked Lists

A doubly linked list is a linked list in which every node has a next pointer and a back pointer. In other words, every node contains the address of the next node (except the last node), and every node contains the address of the previous node (except the first node) (see Figure 16-39).

![](img/d0be7fc6d804b63484835c6c8bc67a07_1170_0.png)

**FIGURE 16-39** Doubly linked list

A doubly linked list can be traversed in either direction. That is, we can traverse the list starting at the first node or, if a pointer to the last node is given, we can traverse the list starting at the last node.

As before, the typical operations on a doubly linked list are:

- 1. Initialize the list.
- 2. Destroy the list.
- 3. Determine whether the list is empty.
- 4. Search the list for a given item.
- 5. Retrieve the first element of the list.
- 6. Retrieve the last element of the list.
- 7. Insert an item in the list.
- 8. Delete an item from the list.
- 9. Find the length of the list.
- 10. Print the list.
- 11. Make a copy of the doubly linked list.

Next, we describe these operations for an ordered doubly linked list. The following class defines a doubly linked list as an ADT:

```cpp
//Definition of the node
template <class Type>
struct nodeType
{
    Type info;
    nodeType<Type> *next;
    nodeType<Type> *back;
};
```

```cpp
template <class Type>
class doublyLinkedList
{
public:
    const doublyLinkedList<Type>& operator=
                              (const doublyLinkedList<Type>&);
    //Overload the assignment operator.

    void initializeList();
       //Function to initialize the list to an empty state.
       //Postcondition: first = nullptr; last = nullptr; count = 0;

    bool isEmptyList() const;
       //Function to determine whether the list is empty.
       //Postcondition: Returns true if the list is empty,
       //               otherwise returns false.

    void destroy();
       //Function to delete all the nodes from the list.
       //Postcondition: first = nullptr; last = nullptr; count = 0;

    void print() const;
       //Function to output the info contained in each node.

    void reversePrint() const;
       //Function to output the info contained in each node
       //in reverse order.

    int length() const;
       //Function to return the number of nodes in the list.
       //Postcondition: The value of count is returned.

    Type front() const;
       //Function to return the first element of the list.
       //Precondition: The list must exist and must not be empty.
       //Postcondition: If the list is empty, the program
       //               terminates; otherwise, the first
       //               element of the list is returned.

    Type back() const;
       //Function to return the last element of the list.
       //Precondition: The list must exist and must not be empty.
       //Postcondition: If the list is empty, the program
       //               terminates; otherwise, the last
       //               element of the list is returned.

    bool search(const Type& searchItem) const;
       //Function to determine whether searchItem is in the list.
       //Postcondition: Returns true if searchItem is found in
       //               the list, otherwise returns false.
};
```

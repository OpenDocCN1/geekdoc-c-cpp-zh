
From Cases 2, 3, and 4, it follows that the deletion of a node requires us to traverse the list. Because a linked list is not a random-access data structure, we must sequentially search the list. We handle Case 1 separately, because it does not require us to traverse the list. We sequentially search the list, starting at the second node. If the node to be deleted is in the middle of the list, we need to adjust the link field of the node just before the node to be deleted. Thus, we need a pointer to the previous node. When we search the list for the given info, we use two pointers: one to keep the info of the current node and one to keep track of the node just before the current node. If the node to be deleted is the last node, we must adjust the pointer last.

The definition of the function deleteNode is:

```cpp
template <class Type>
void unorderedLinkedList<Type>::deleteNode(const Type& deleteItem)
{
    nodeType<Type> *current;  //pointer to traverse the list
    nodeType<Type> *trailCurrent;  //pointer just before current
    bool found;

    if (first == NULL)    //Case 1: the list is empty
        cout << "Cannot delete from an empty list."
             << endl;
    else
    {
        if (first->info == deleteItem)  //Case 2
        {
            current = first;
            first = first->link;
            count--;

            if (first == NULL)    //the list has only one node
                last = NULL;

            delete current;
        }
        else //search the list for the node with the given info
        {
            found = false;
            trailCurrent = first;  //set trailCurrent to point
                                   //to the first node
            current = first->link;  //set current to point to
                                    //the second node

            while (current != NULL && !found)
            {
                if (current->info != deleteItem)
                {
                    trailCurrent = current;
                    current = current->link;
                }
                else
                    found = true;
            }//end while

            if (found) //Case 3: if found, delete the node
            {
                trailCurrent->link = current->link;
                count--;

                if (last == current)    //node to be deleted
                                         //was the last node
                    last = trailCurrent; //update the value
                                         //of last
                delete current;         //delete the node from the list
            }
            else
                cout << "The item to be deleted is not in "
                     << "the list." << endl;
        }//end else
    }//end else
}//end deleteNode
```

## Header File of the Unordered Linked List

For the sake of completeness, we will show how to create the header file that defines the class unorderedListType and the operations on such lists. (We assume that the definition of the class unorderedLinkedListType and the definitions of the functions to implement the operations are in the header file linkedlist.h.)

```cpp
#ifndef H_UnorderedLinkedList
#define H_UnorderedLinkedList

#include "linkedList.h"

using namespace std;

template <class Type>
class unorderedLinkedList: public linkedListType<Type>
{
public:
    bool search(const Type& searchItem) const;
        //Function to determine whether searchItem is in the list.
        //Postcondition: Returns true if searchItem is in the
        //              list, otherwise the value false is
        //              returned.

    void insertFirst(const Type& newItem);
        //Function to insert newItem at the beginning of the list.
        //Postcondition: first points to the new list, newItem is
        //              inserted at the beginning of the list,
        //              last points to the last node in the
        //              list, and count is incremented by 1.

    void insertLast(const Type& newItem);
        //Function to insert newItem at the end of the list.
        //Postcondition: first points to the new list, newItem
        //              is inserted at the end of the list,
        //              last points to the last node in the
        //              list, and count is incremented by 1.
```

## Insert a Node

To insert an item in an ordered linked list, we first find the place where the new item is supposed to go, and then we insert the item in the list. To find the place for the new item, as before, we search the list. Here, we use two pointers, current and trailCurrent, to search the list. The pointer current points to the node whose info is being compared with the item to be inserted, and trailCurrent points to the node just before current. Because the list is in order, the search algorithm is the same as before. The following cases arise.

**Case 1:** The list is initially empty. The node containing the new item is the only node and thus the first node in the list.

**Case 2:** The new item is smaller than the smallest item in the list. The new item goes at the beginning of the list. In this case, we need to adjust the list’s head pointer—that is, `first`. Also, `count` is incremented by 1.

**Case 3:** The item is to be inserted somewhere in the list.

**3a:** The new item is larger than all of the items in the list. In this case, the new item is inserted at the end of the list. Thus, the value of `current` is NULL, and the new item is inserted after `trailCurrent`. Also, `count` is incremented by 1.

**3b:** The new item is to be inserted somewhere in the middle of the list. In this case, the new item is inserted between `trailCurrent` and `current`. Also, `count` is incremented by 1.

The following statements can accomplish both Cases 3a and 3b. Assume `newNode` points to the new node.

```cpp
trailCurrent->link = newNode;
newNode->link = current;
```

Let us next illustrate these cases.

### Case 1: The list is empty.

Consider the list shown in Figure 16-30(a).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1112_0.png)

**FIGURE 16-30** List

Suppose that we want to insert 27 in the list. To accomplish this task, we create a node, copy 27 into the node, set the link of the node to NULL, and make `first` point to the node. Figure 16-30(b) shows the resulting list. Notice that, after inserting 27, the values of both `first` and `count` change.

### Case 2: The list is not empty, and the item to be inserted is smaller than the smallest item in the list.

Consider the list shown in Figure 16-31.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1112_1.png)

**FIGURE 16-31** Nonempty list before inserting 10

Suppose that 10 is to be inserted. After inserting 10 in the list, the node with info 10 becomes the first node of list. This requires us to change the value of first. Also, count is incremented by 1. Figure 16-32 shows the resulting list.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1113_0.png)

**FIGURE 16-32** List after inserting 10

### Case 3:

The list is not empty, and the item to be inserted is larger than the first item in the list. As indicated previously, this case has two scenarios.

### Case 3a:

The item to be inserted is larger than the largest item in the list; that is, it goes at the end of the list. Consider the list shown in Figure 16-33.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1113_1.png)

**FIGURE 16-33** List before inserting 65

Suppose that we want to insert 65 in the list. After inserting 65, the resulting list is as shown in Figure 16-34.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1113_2.png)

**FIGURE 16-34** List after inserting 65

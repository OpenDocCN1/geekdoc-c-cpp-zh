```
```cpp
if (found) //Case 3; if found, delete the node
{
    trailCurrent->link = current->link;
    count--;

    if (last == current)      //node to be deleted
                               //was the last node
        last = trailCurrent;   //update the value
                               //of last
    delete current;            //delete the node from the list
}
else
    cout << "The item to be deleted is not in "
         << "the list." << endl;
}//end else
}//end deleteNode
```
```

# Header File of the Unordered Linked List

For the sake of completeness, we will show how to create the header file that defines the class unorderedListType and the operations on such lists. (We assume that the definition of the class linkedListType and the definitions of the functions to implement the operations are in the header file linkedlist.h)

```
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
        //              list, otherwise false value is
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
```
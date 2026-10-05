```
/*
while(head != NULL)
{
/*
  ... keep calling the delEnd() function to keep
  deleting the last node.
*/
delEnd();
}

```

Don't do anything if list is empty (no else).

The destructor will be called whenever an object of the linked list goes out of scope. It has been designed to return the memory occupied by the nodes of the linked list back to the operating system. The function itself is simple. If the list is empty, it does not do anything. Otherwise, it simply keeps calling the delEnd() function as long as the list does not become empty.

When the delEnd() function is called repeatedly, it keeps deleting the nodes from the end of the list. However, remember that the delEnd() function makes the head pointer NULL when it is called to delete a list that has only one node. Therefore, when the delEnd() function is called when the list has only one node left, it will make the list empty and also make the head pointer NULL. At this point, the test expression of the while loop will return false, and the loop will break.

Also, remember that one function of a class (in this case, the destructor) can call another function of the same class (in this case, the delEnd() function).

One point about the significance of the destructor— suppose an object of the linked list class has been created in the main() function. When the main() function ends, the program also terminates. The memory occupied by the nodes in the linked list will always get returned to the operating system. You may think that the destructor is superfluous. However, objects of the linked list may not always get created in the main() function. Consider Listing 9.22.

# Listing 9.22 Illustrating the importance of the destructor

```
/*
Beginning of Destructor.cpp
*/
#include "SingleLinkedList.h"

void f1() {
/*
  Create a list object
*/
SingleLinkedList list1;
/*
  Call the prependNode() function on the list1 object.
*/
list1.prependNode(5287);
/*
  Call the prependNode() function on the list1 object.
*/
```
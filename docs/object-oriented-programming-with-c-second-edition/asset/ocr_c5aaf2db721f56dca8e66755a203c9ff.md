# 332 Object-Oriented Programming with C++

Listing 9.21 Executing the delEnd() function

```
/*
  Beginning of DelEnd02.cpp
*/
#include "SingleLinkedList.h"

void main() {
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
  list1.prependNode(325);
  /*
    Delete the last node
  */
  list1.delEnd();
  /*
    Display the values in the list.
  */
  list1.display();
}
// End of DelEnd02.cpp
```

Output

325

We expect the structure of the linked list after the call to the delEnd() function to be like Figure 9.52.

![](bbox=[0.265, 0.698, 0.815, 0.875])

Figure 9.52 Expected effect of the delEnd() function

Let us see whether this happens or not. We know that the structure of the linked list after the second call to the prependNode() function will look like Figure 9.53.
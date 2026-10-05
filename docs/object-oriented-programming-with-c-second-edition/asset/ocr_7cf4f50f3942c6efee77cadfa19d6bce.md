# Listing 9.31 Testing the BSTNode class

```
/*
  Beginning of BSTNodeTest01.cpp
 */
#include "BSTNode.h"
void main()
{
    BSTNode node1;
    node1.setVal(20);
    BSTNode * & temp = node1.getLeft();
    temp = new BSTNode();
    temp -> setVal(10);
    cout << node1.getLeft()->getVal() << endl;
}
/*
  End of BSTNodeTest01.cpp
 */
```

Output
10

The first statement of the above program declares an object of the BSTNode class and the second statement sets the value of the node to 20. Let us analyse Listing 9.31 from the third statement onwards.

BSTNode * & temp = node1.getLeft();

Since the call to the getLeft() function returns a reference to the left pointer of the node1 object and because the temp pointer is a reference variable, therefore the temp pointer ends up being a reference for the left pointer of the node1 object, as shown in Figure 9.66.

| 2172 | |
|---|---|
| 20 | val |
| NULL | left |
| NULL | right |
| 2176 | node1 |
| NULL |

> Figure 9.66 A temporary pointer pointing at a BST node

Since temp is a reference to the left pointer, its address will be the same as that of the left pointer, which is 2176. And, from our knowledge of reference, we know that any change to the value of temp will cause the same change to the value of the left pointer (because they are essentially two names for the same memory block). Thus, if the following statement executes now, it will change the value of the left pointer.
The next statement in the program is:

```
temp = new BSTNode();
```
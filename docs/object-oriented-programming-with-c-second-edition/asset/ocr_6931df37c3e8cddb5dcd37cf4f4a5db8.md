```
/*
* This function sets the value of the data part.
 */
void SingleLinkedListNode::setVal(int pVal)
{
    /*
     Set the value of the data part to the value of the
    passed parameter.
    */
    val = pVal;
}
```

This is a very simple function. It assigns the value of the parameter that is passed to it the val data member. Continuing with our previous example, it may be called as follows (Listing 9.4).

# Listing 9.4 Executing the setVal() function of the single linked node class

```
/*
 Beginning of SetVal.cpp
 */
#include <iostream>
#include "SingleLinkedListNode.h"
void main()
{
    SingleLinkedListNode * temp = new SingleLinkedListNode();
    temp -> setVal(10);
}
/*
End of SetVal.cpp
*/
```

A diagrammatic representation of the effects of the above statement is shown in Figure 9.7.

| 245 | 10 | val |
|---|---|---|
| temp | NULL | next |

Figure 9.7 Effect of setVal() function

The next function we need to look at is the getVal() function (Listing 9.5).

```
/*
 This function returns the data part.
 */
int SingleLinkedListNode::getVal()
{
    /*
 Return the value of the data part.
    */
    return val;
}
```

Again, this is a simple function. It simply returns the value of the val data member. Still continuing with our previous example, suppose we call it as follows.
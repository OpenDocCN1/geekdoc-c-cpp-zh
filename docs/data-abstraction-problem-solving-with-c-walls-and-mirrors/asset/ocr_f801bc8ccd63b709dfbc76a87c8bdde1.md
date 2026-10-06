# 7.1 An Array-Based Implementation

![](bbox=[0.138, 0.093, 0.203, 0.173])

Figure-7Ia shows a sketch of an array that contains the entries in a stack. Where in the array should the top entry be? Since entries are added or removed from the top of the stack, we can avoid shifting current entries if we use the bottom of the stack at index 0 and track the location of the stack's top using an index. If items is the array and items[top] is the top entry, items and top can be the private data members of our class of stacks. Figure-7Ib illustrates these details. Note that the top of the stack in this figure is at index 2. We can add a new entry at index[3] and increment or remove the top entry in index[2] by decrementing top to 1.

Our class has a default constructor to initialize the private data members in statically allocated memory, the compiler-generated destructor and copy constructor will be sufficient. However, if we plan to store a stack's entries in dynamically allocated memory, on the other hand, were to use a dynamically allocated array, we would have to define a constructor and a copy constructor.

Listing 7-1 shows the header file for an array-based implementation of the ADT stack. Comments describing the methods are in Listing 6-1 of Chapter 6.

FIGURE 7-1 Using an array to store a stack's entries: (a) a preliminary sketch; (b) implementation details

| | | items |
|---|---|---|---|---||
| 4 | | 10 | 20 | 30 | |
| 3 | | | | | |
| 2 | | 0 | 1 | 2 | MAX_STACK - 1 |
| 1 | | | | | |
| 0 | | | | | |
| Array | | | | | |

# LISTING 7-1 stack: The header file for an array-based stack

```
/* ADT stack: array-based implementation.
@file ArrayStack.h */

#ifndef _ARRAY_STACK
#define _ARRAY_STACK

#include "StackInterface.h"
const int MAX_STACK = maximum-size-of-stack;

template<<class ItemType>
class ArrayStack : public StackInterface<ItemType>{
private:
    ItemType items[MAX_STACK]; // Array of stack items
    int top; // Index to top of stack
```
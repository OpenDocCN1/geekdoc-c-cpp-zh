stack in the reverse of the order in which it enters the stack, the output shows the line written backward. We have #included the implementation of the Stack class in our application program, as we normally do with template classes. That means we cannot run or even compile our application program until we do the implementation of our Stack class template.

The definitions of the member functions of the template class Stack are given in the implementation file shown in Display 17.15. Our Stack class implemented as a linked list in which the head of the list serves as the top of the stack. The member variable top is a pointer that points to the head of the linked list. The pointer top serves the same purpose as the pointer head did in our previous discussions of linked lists.

# PUSH AND POP

Adding a data item to a stack data structure is referred to as pushing the data item onto the stack. Removing a data item from a stack is referred to as popping the item off the stack.

# Display 17.15  Implementation of the Stack Template Class (part 1 of 2)

```
1  //This is the implementation file stack.cpp.
2  //This is the implementation of the template class Stack.
3  //The interface for the template class Stack is in the header file stack.h.

4  #include <iostream>
5  #include <cstdlib>
6  #include <cstddef>
7  #include "stack.h"
8  using std::cout;

9  namespace StackSwitchit
10 {

11     //Uses cstddef
12     template<class T>
13     Stack<T>::Stack() : top(NULL)
14     {
15         //Intentionally empty
16     }

17     template<class T>
18     Stack<T>::Stack(const Stack<T>& aStack)
19     <The definition of the copy constructor is Self-Test Exercise 2.>
```
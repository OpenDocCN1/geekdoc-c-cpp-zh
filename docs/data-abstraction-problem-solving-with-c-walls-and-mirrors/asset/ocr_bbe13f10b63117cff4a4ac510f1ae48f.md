# 250 CHAPTER 7 Implementations of the ADT Stack

| LISTING 7-6 The implementation file for the class PrecondViolatedExcep |
| | /** @file PrecondViolatedExcep.cpp */
| #include "PrecondViolatedExcep.h"
| PrecondViolatedExcep::PrecondViolatedExcep(const string& message):
|     logic_error("Precondition Violated Exception: " + message);
| {
 // end constructor |

We revise the declarations of peek in the header files Array.h and LinkedStack.h by adding a throw clause as follows:

```
Item peek() const throw(PrecondViolatedExcep);
```

In the implementation, we add the same throw clause to the header of peek and then replace the assert statement in both definitions of peek with the following statement:

```
if (isEmpty())
    throw PrecondViolatedExcep("peek() called with empty stack");
```

Thus, the definition of peek in LinkedStack, for example is:

```
template<class ItemType>
ItemType LinkedStack<ItemType>::peek() const throw(PrecondViolatedExcep)
{
    Enforce precondition
    if (isEmpty())
        throw PrecondViolatedExcep("peek() called with empty stack");
    Stack is not empty; return top
    return topPtr->getItem();
} endTop
```

The previous revisions to peek are the same for the array-based and link-based implementation of the stack.

> Note: In the link-based implementation of the stack, both the method push and the copy constructor allocate new nodes. This allocation could fail if the system has no memory available. In such a case, the standard bad_alloc is thrown. In our simple examples, such an occurrence is unlikely to occur unless your system has a severely restricted memory size. For simplicity, we will not worry about this situation.

![](bbox=[0.218, 0.686, 0.273, 0.733])

Question 4 Define the exception class MemoryAllocationException and then revise the definition of the method push in the class LinkedStack so that it throws this exception if it cannot allocate a new node.

![](bbox=[0.218, 0.856, 0.263, 0.903])
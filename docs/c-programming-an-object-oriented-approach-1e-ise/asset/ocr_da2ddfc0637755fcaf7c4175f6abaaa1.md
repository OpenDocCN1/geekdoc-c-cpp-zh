![](bbox=[0.28, 0.08, 0.89, 0.29])

Note:
The push operation inserts an item in the stack.
The pop operation erases the item at the top of the stack.
We have simulated the stack as an upside-down array in the heap.

# **Figure 15.4** Operations on a stack

In this program we have defined the stack as an array (line 14), but the operations defined for the array allow only pushing and popping of the top element. Accessing or changing other elements is not allowed.

# **Program 15.12** File stack.h

```
```cpp
/**********************************************************
 * The interface file for the class template stack
 **********************************************************/
#ifndef STACK_H
#define STACK_H
#include <iostream>
#include <cassert>
using namespace std;

template <typename T>
class Stack
{
private:
    T* ptr;
    int capacity;
    int size;
public:
    Stack (int capacity);
    ~Stack ();
    void push (const T& element);
    T pop ();
};
#endif
```
```
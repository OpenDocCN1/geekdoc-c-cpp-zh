# 416 10 Generic Programming and the Standard Template Library

# 10.2.2 Adapters of Containers

Adapters of containers do not implement the mechanism of storing the data and other functionalities like iterators. They just implement different interfaces based on the containers provided by STL.

# 1. Stacks

A stack is a linear collection with restricted access. Elements can only be added or removed from one end of a stack. Such operations are called push and pop respectively. In theory, there is no limit on the number of elements in a stack. In practice, a stack will overflow if it exceeds the memory limit of the computer, and it will underflow if one tries to pop an empty stack. STL catches these exceptions to keep the program from crashing.

Stacks are based on the implementation of a certain container, which is specified at the declaration. Here is an example of declaration of a stack using deque as its underlying implementation of storage:

```
stack<int, deque<int>> myStack;
```

Stacks only implement the primitives of the stack data structure. Methods push()/pop() add or remove an element at the top of stack; the method pop() returns the reference of the element at the top of the stack. The method empty() checks whether a stack is empty. The method size() returns the number of elements in the stack. The underlying storage can be a vector, list, or deque, and the deque is the default implementation. Please refer to related documents like MSDN for detailed information. Here is a simple example of a stack.

# Example 10_4.cpp: Initialize a stack holding integers.

```
//include <iostream>
#include <stack> //include stack adapter header file
using namespace std;

template< class T>
void popElements( T &s );

int main(){
    stack< int > dequeStack; //use deque as the default container
    for ( int i = 0; i < 10; ++i ) {
        dequeStack.push( i ); //push the integer in deque as the
        //top of the stack
    }
}
```
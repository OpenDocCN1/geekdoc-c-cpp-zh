# Display 17.18 Program Using the Stack Template Class (part 2 of 2)

```
Enter a line of text:
I love C++
Written backward that is:
++C evol I
Again? (y/n): n
```

# Display 17.19 Implementation of the Stack Template Class (part 1 of 2)

```
1 //This is the implementation file stack.cpp.
2 //This is the implementation of the template class Stack.
3 //The interface for the template class Stack is in the header file
//stack.h

4 #include <iostream>
5 #include <cstdlib>
6 #include "stack.h"
7 using std::cout;

8 namespace StackSavitch
9 {

10    //Uses cstddef:
11    template<class T>
12    Stack<T>::Stack() : top(nullptr)
13    {
14       //Intentionally empty
15    }

16    template<class T>
17    Stack<T>::Stack(const Stack<T>& aStack)
18    <The definition of the copy constructor is Self-Test Exercise 14.>
19    template<class T>
20    Stack<T>& Stack<T>::operator =(const Stack<T>& rightSide)
21    <The definition of the overloaded assignment operator is Self-Test Exercise 15.>

22    template<class T>
23    Stack<T>::~Stack()
```
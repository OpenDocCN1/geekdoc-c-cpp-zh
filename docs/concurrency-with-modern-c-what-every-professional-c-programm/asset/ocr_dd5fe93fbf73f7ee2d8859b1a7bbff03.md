# ## 13.0.1 A Stack

![](bbox=[0.18, 0.16, 0.66, 0.28])

A `std::stack`¹ follows the LIFO principle (Last In First Out). A stack `sta`, which needs the header `<stack>`, has three member functions.

With `sta.push(e)` you can insert a new element `e` at the top of the stack, remove it from the top with `sta.pop()` and reference it with `sta.top()`. The stack supports the comparison operators and knows its size. The operations of the stack have constant complexity.

```
```cpp
#include <stack>
...
std::stack<int> myStack;

std::cout << myStack.empty() << '\n';   // true
std::cout << myStack.size() << '\n';    // 0

myStack.push(1);
myStack.push(2);
myStack.push(3);
std::cout << myStack.top() << '\n';     // 3

while (!myStack.empty()){
    std::cout << myStack.top() << " ";
    myStack.pop();
}
std::cout << '\n';                      // 3 2 1

std::cout << myStack.empty() << '\n';   // true
std::cout << myStack.size() << '\n';    // 0
```
```

Let me implement the concurrent stack successively.

# ### 13.0.1.1 A Simplified Implementation

My first implementation only supports the `push` member function. The class `ConcurrentStackPush` is a thin wrapper around a `std::stack`.

¹http://en.cppreference.com/w/cpp/container/stack
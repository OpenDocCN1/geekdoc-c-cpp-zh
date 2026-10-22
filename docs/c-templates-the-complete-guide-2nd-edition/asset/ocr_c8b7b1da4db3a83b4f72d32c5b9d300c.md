```
// stack for ints using a vector as an internal container
Stack<int,std::vector<int>> vStack;
...
vStack.push(42);
vStack.push(7);
std::cout << vStack.top() << '\n';
```
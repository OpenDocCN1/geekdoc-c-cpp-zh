In the above given sample program, funcPtr is a pointer to a function that takes no parameters and returns nothing It is assigned the address of the greet function and then used to call

# Functors (Function Objects)

Functors are objects that can be called as if they were ordinary functions based on the operator overloading of the function call operator This makes them more flexible than function pointers since they can also hold state.

Given below is how you can define and use a functor:

```
```cpp
#include

class GreetFunctor {

public:

void operator()() const {

std::cout << "Hello from GreetFunctor." << std::endl;

}
```
```
+   3. *(Code)* Write a statement that you'd place in a catch handler to return the current exception to the next enclosing try block.

Answer: `throw;`

# ## 12.5 Stack Unwinding and Uncaught Exceptions

When you do not catch an exception in a particular scope, the function-call stack “unwinds” in an attempt to catch the exception in an enclosing scope—that is, a catch block of the next outer try block. You can nest try blocks, in which case the next outer try block could be in the same function. When try blocks are not nested, stack unwinding occurs. The function in which the exception was not caught terminates, and its existing local variables go out of scope. During stack unwinding, control returns to the statement that invoked the function. If that statement is in a try block, that block terminates, and an attempt is made to catch the exception. If the statement is not in a try block or the exception is not caught, stack unwinding continues. In fact, this mechanism is one reason you should not wrap a try...catch around every function call that might throw an exception.^21 Sometimes it’s more appropriate to let an earlier function in the call chain deal with the problem. Figure 12.4 demonstrates stack unwinding.

```
```cpp
// fig12_04.cpp
// Demonstrating stack unwinding.
#include <iostream>
#include <stdexcept>

// function3 throws runtime error
void function3() {
    std::cout << "In function 3\n";

    // no try block, stack unwinding occurs, return control to function2
    throw std::runtime_error{"runtime_error in function3"};
}

// function2 invokes function3
void function2() {
    std::cout << "function3 is called inside function2\n";
    function3(); // stack unwinding occurs, return control to function1
}

// function1 invokes function2
void function1() {
    std::cout << "function2 is called inside function1\n";
    function2(); // stack unwinding occurs, return control to main
}
```
```

**Fig. 12.4** | Demonstrating stack unwinding. (Part 1 of 2.)

21. C++ Core Guidelines, “E.17: Don’t Try to Catch Every Exception in Every Function.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Re-not-al-ways.
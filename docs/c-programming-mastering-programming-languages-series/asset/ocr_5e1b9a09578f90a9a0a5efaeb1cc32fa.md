```
```cpp
return 0;
}
```
```

In this example, the processInput function may throw either a std::out_of_range exception for negative input or a std::invalid_argument exception for even numbers. The corresponding catch blocks handle these exceptions individually, allowing for tailored error messages and responses.

# **Catch-All Blocks: Handling Unknown Exceptions**

To provide a catch-all mechanism for handling unknown or unexpected exceptions, developers can use a catch block without specifying an exception type. This catch-all block ensures that any exception not caught by preceding blocks is handled, preventing the program from abruptly terminating.

```
```cpp
#include <iostream>
#include <stdexcept>

void processInput(int value) {
    try {
        if (value < 0) {
            throw std::out_of_range("Input must be non-negative");
        } else if (value % 2 == 0) {
            throw std::invalid_argument("Even numbers not allowed");
        }
        // Process the input if it is valid
    } catch (const std::out_of_range& e) {
        std::cerr << "Out of Range Exception: " << e.what() << std::endl;
    } catch (const std::invalid_argument& e) {
        std::cerr << "Invalid Argument Exception: " << e.what() << std::endl;
    } catch (...) {
        std::cerr << "Unknown Exception Caught" << std::endl;
    }
}

int main() {
    try {
        processInput(-5);
    } catch (const std::exception& e) {
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }

    return 0;
}
```
```
constructs provide a structured and systematic approach to manage errors, making code more resilient and facilitating the development of robust software. Developers should use these features judiciously to ensure a balance between robust error handling and maintaining code clarity.

# ## Handling Multiple Exceptions

Effective exception handling in C++ extends beyond managing a single type of exception. This section delves into the techniques and best practices for handling multiple exceptions, allowing developers to create more resilient and adaptable code in the face of diverse error scenarios.

# ### Catching Multiple Exception Types

C++ allows catch blocks to handle multiple exception types, providing flexibility in addressing different error conditions. By specifying multiple catch blocks, each associated with a distinct exception type, developers can tailor their error-handling logic based on the specific nature of the exception thrown.

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
    }
}

int main() {
    try {
        processInput(-5);
    } catch (const std::exception& e) {
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }
}
```
```
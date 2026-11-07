```
```cpp
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }
    return 0;
}
```
```

In this instance, a custom exception class, CustomException, is defined to provide a specific error message when thrown and caught.

Exception handling is crucial for creating resilient and maintainable C++ programs. By employing try-catch blocks, throwing meaningful exceptions, and utilizing custom exception classes, developers can enhance the reliability of their code and facilitate effective error management.

# ## try-catch Blocks and Throwing Exceptions

Exception handling is a key mechanism in C++ for gracefully managing unexpected situations during program execution. This section focuses on the utilization of try-catch blocks and the throwing of exceptions, providing a comprehensive understanding of how these constructs work together to enhance the robustness of C++ code.

# ## try-catch Blocks: Structuring Exception Handling

The try-catch construct is fundamental to C++ exception handling. Code that may potentially throw an exception is enclosed within a try block. If an exception occurs within the try block, the control is transferred to the appropriate catch block, where error-handling logic is implemented. This structure allows developers to separate normal code execution from error-handling code, promoting cleaner and more maintainable code.

```
```cpp
#include <iostream>

int main() {
    try {
        // Code that may throw an exception
        throw std::runtime_error("An exception occurred!");
    } catch (const std::exception& e) {
        // Catch block handling the exception
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }
}
```
```
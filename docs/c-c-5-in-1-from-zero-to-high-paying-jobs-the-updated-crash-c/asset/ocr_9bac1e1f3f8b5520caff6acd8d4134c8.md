```
```cpp
#include <iostream>

void greet(std::string name) {
    std::cout << "Hello, " << name << "!" << std::endl;
}

int main() {
    greet("Alice");
    greet("Bob");
    return 0;
}
```
```

In this example, the function `greet` takes a parameter named `name`, which represents the name of the person being greeted. If the function is called, we see that the argument `"Alice"` is then passed to the `name` parameter the first time, and `"Bob"` the second time.

# **Passing Arguments to Functions:**

When you call a function that has parameters, you provide values (arguments) that match the types of the parameters. These arguments are passed to the function and can be used within its code block.

# **Syntax of Function Call with Arguments:**
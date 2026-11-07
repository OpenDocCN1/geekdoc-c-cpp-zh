```
```cpp
JANUARY = 1,
FEBRUARY = 2,
MARCH = 3,
APRIL = 4,
// ... (remaining months)
};

int main() {
    // Using the Month enum to declare a variable
    Month currentMonth = MARCH;

    // Displaying the current month
    std::cout << "Current Month: " << static_cast<int>(currentMonth) << std::endl;

    return 0;
}
```
```

Here, the Month enum assigns explicit values to each constant, ensuring a direct mapping to calendar months.

# Scoped Enums for Enhanced Encapsulation

To enhance encapsulation and prevent naming collisions, C++ introduces scoped enums (enum class). Unlike traditional enums, scoped enums encapsulate their constants within a distinct scope. Consider the following example:

```
```cpp
#include <iostream>

// Scoped enum named State
enum class State {
    INIT,
    PROCESSING,
    COMPLETE
};

int main() {
    // Using the State enum to declare a variable
    State currentState = State::PROCESSING;

    // Displaying the current state
    std::cout << "Current State: " << static_cast<int>(currentState) << std::endl;

    return 0;
}
```
```

In this case, the State enum class provides a more robust mechanism for defining constants, reducing the risk of naming conflicts.
```
std::endl;
}
return 0;
}
```

# 77. Write a program that prompts the user for a list of numbers, until the user types the number zero, and displays the largest and smallest numbers in the list.

```
#include <iostream>
#include <limits> // For std::numeric_limits
int main() {
    double largest = std::numeric_limits<double>::lowest();
    double smallest = std::numeric_limits<double>::max();
    double num;
    std::cout << "Enter numbers (enter 0 to stop): ";
```
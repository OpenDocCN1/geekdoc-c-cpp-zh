# Figure 5.5 Flowchart with multiple optional execution pathways

![](bbox=[0.115, 0.185, 0.805, 0.395])

# 5.8 Multi-way if/else Statements

A simple if/else statement can select from between two execution paths. Suppose we wish to choose one execution path from among several possible paths, as shown in Figure 5.5?

Listing 5.9 (enhancedcheckrange.cpp) showed how to select from among three options. What if exactly one of many actions should be taken? Nested if/else statements are required, and the form of these nested if/else statements is shown in Listing 5.15 (digittoword.cpp).

```
Listing 5.15: digittoword.cpp
#include <iostream>

int main() {
    int value;
    std::cout << "Please enter an integer in the range 0...5: ";
    std::cin >> value;
    if (value < 0)
        std::cout << "Too small";
    else
        if (value == 0)
            std::cout << "zero";
        else
            if (value == 1)
                std::cout << "one";
            else
                if (value == 2)
                    std::cout << "two";
                else
                    if (value == 3)
                        std::cout << "three";
                    else
```
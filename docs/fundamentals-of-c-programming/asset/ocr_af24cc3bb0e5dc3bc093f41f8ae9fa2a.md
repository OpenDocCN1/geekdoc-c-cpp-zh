```
if (value == 4)
    std::cout << "four";
else
    if (value == 5)
        std::cout << "five";
    else
        std::cout << "Too large";
std::cout << '\n';
}
```

Observe the following about Listing 5.15 (digitword.cpp):

+   - It prints exactly one of eight messages depending on the user's input.
+   - Notice that each `if` body contains a single printing statement and each `else` body, except the last one, contains an `if` statement. The control logic forces the program execution to check each condition in turn. The first condition that matches wins, and its corresponding `if` body will be executed. If none of the conditions are true, the last `else`'s `Too large` message will be printed.
+   - No curly braces are necessary to delimit the `if` or `else` bodies since each body contains only a single statement (although a single deeply nested `if`/`else` statement is a mighty big statement).

Listing 5.15 (digitword.cpp) is formatted according to the conventions used in earlier examples. As a consequence, the mass of text drifts to the right as more conditions are checked. A commonly used alternative style, shown in Listing 5.16 (restyleddigitword.cpp), avoids this rightward drift.

# Listing 5.16: restyleddigitword.cpp

```
#include <iostream>

int main() {
    int value;
    std::cout << "Please enter an integer in the range 0...5: ";
    std::cin >> value;
    if (value < 0)
        std::cout << "Too small";
    else if (value == 0)
        std::cout << "zero";
    else if (value == 1)
        std::cout << "one";
    else if (value == 2)
        std::cout << "two";
    else if (value == 3)
        std::cout << "three";
    else if (value == 4)
        std::cout << "four";
    else if (value == 5)
        std::cout << "five";
    else
        std::cout << "Too large";
    std::cout << '\n';
}
```

Based on our experience so far, the formatting of Listing 5.16 (restyleddigitword.cpp) somewhat hides the true structure of the program's logic, but this style of formatting multi-way `if`/`else` statements is
```
#include <iostream>
int main() {
    unsigned int five = 5;
    int negative_five = -5;
    if (negative_five < five) // signed/unsigned mismatch
        std::cout << "true";
    else
        std::cout << "false";
    return 0;
}
```
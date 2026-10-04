# 118. Implement a method to perform basic string compression using the counts of repeated characters. For instance, the string aabcccccaaa would become a2b1c5a3.

```
#include <iostream>
#include <string>
#include <sstream>

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::cin >> input;

    if (input.empty()) {
        std::cout << "Compressed string: " << input << std::endl;
        return 0;
    }
```
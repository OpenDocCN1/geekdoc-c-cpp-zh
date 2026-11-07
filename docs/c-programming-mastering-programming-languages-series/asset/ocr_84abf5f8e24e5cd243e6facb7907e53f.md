```
```cpp
std::cout << "Enter your name: ";
std::getline(std::cin, userInput);

// Displaying the input
std::cout << "Hello, " << userInput << "!" << std::endl;

return 0;
}
```
```

In this example, the std::getline function is employed to read a line of text from the user, demonstrating the flexibility of C++ strings in handling user input.

# String Manipulation and Operations

C++ provides a rich set of string manipulation functions and operators. The ability to easily manipulate strings is showcased through operations such as substring extraction, finding substrings, and replacing portions of the string.

```
```cpp
#include <iostream>
#include <string>

int main() {
    // String manipulation
    std::string sentence = "C++ programming is powerful.";

    // Extracting a substring
    std::string fragment = sentence.substr(4, 11);

    // Finding a substring
    size_t position = sentence.find("programming");

    // Replacing a substring
    sentence.replace(position, 11, "development");

    // Displaying the result
    std::cout << sentence << std::endl;

    return 0;
}
```
```

This snippet showcases operations such as substring extraction, finding a substring's position, and replacing a portion of the string. The flexibility of these operations demonstrates the convenience and power of C++ strings in handling textual data.
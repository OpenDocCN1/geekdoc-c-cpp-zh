# Regular Expressions

146. Write a regex to validate
mail addresses, ensuring it
contains @ and . symbols.

```
#include <iostream>
#include <regex>
#include <string>
```

```
int main() {
    std::string email;
    std::cout << "Enter email address: ";
    std::cin >> email;

    // Regex pattern to check if email contains @
    // and . symbols
    std::regex pattern(R"([^@]+@[^@]+\.[^@]+$\)");

    if (std::regex_match(email, pattern)) {
        std::cout << "Valid email address!" << std::endl;
```
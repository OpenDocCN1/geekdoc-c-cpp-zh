# 8. Make a program that reads the names of three people in sequence, followed by their respective ages, and prints each name with their respective ages on the screen.

```
#include <iostream>
#include <string>

int main() {
    std::string name1, name2, name3;
    int age1, age2, age3;

    // Read details for the first person
    std::cout << "Enter the name of the first person: ";
    std::getline(std::cin, name1);
    std::cout << "Enter the age of " << name1 << ":";
    std::cin >> age1;
    std::cin.ignore(); // To Clear the newline left by the previous input
```
**3** *(Code)* Write a string member function call that finds the last vowel in the string `s`.
Answer: `s.find_last_of("aeiou")`.

# 8.8 Replacing and Erasing Characters in a string

Figure 8.7 demonstrates string member functions for replacing and erasing characters. We broke this example into parts for discussion. Lines 9–13 declare and initialize string1. When string literals are separated only by whitespace, the compiler concatenates them into a single string literal. Breaking apart lengthy strings in this manner can make your code more readable.

```
```cpp
// fig08_07.cpp
// Demonstrating string member functions erase and replace.
#include <format>
#include <iostream>
#include <string>

int main() {
    // compiler concatenates all parts into one string
    std::string string1{"The values in any left subtree"
        "\nare less than the value in the"
        "\nparent node and the values in"
        "\nany right subtree are greater"
        "\nthan the value in the parent node"};

    std::cout << std::format("Original string:\n{}\n\n", string1);
```

```

![](bbox=[0.166, 0.551, 0.833, 0.657])

**Fig. 8.7** | Demonstrating string member functions erase and replace.

Line 17 uses string member function erase to erase everything from (and including) the character in position 62 to the end of string1. Each newline character occupies one character in the string.

```
```cpp
string1.erase(62); // remove from index 62 through end of string1
std::cout << std::format("string1 after erase:\n{}\n\n", string1);
```

```

![](bbox=[0.166, 0.81, 0.833, 0.877])
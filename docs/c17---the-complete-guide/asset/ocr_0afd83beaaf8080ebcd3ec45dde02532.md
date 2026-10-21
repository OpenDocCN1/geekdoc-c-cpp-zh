# Chapter 18

# std::byte

With std::byte, C++17 introduces a type which represents the “natural” type of the elements of memory: bytes. std::byte essentially represents all the values a byte can hold but places no numeric or character interpretation on them, other than their bit-wise representation. For cases where numeric computing or character sequence are not the goal, this results in more type safety.

However, note that std::byte is implemented with the size of an unsigned char, meaning that it is not guaranteed to have 8 bits. It may be more.

# 18.1 Using std::byte

The following example demonstrates the core abilities of std::byte:

```
#include <cstddef> // for std::byte

std::byte b1{0x3F};
std::byte b2{0b1111'0000};

std::byte b3[4] {b1, b2, std::byte{1}};  // 4 bytes (last is 0)

if (b1 == b3[0]) {
    b1 <<= 1;
}

std::cout << std::to_integer<int>(b1) << '\n';  // outputs: 126
```

Here, we define two bytes with two different initial values. b2 is initialized using two features available since C++14:

+   - The prefix 0b enables the definition of binary literals.
+   - The digit separator ’ allows you to make numeric literals more readable in source code (it can be placed between any two digits of numeric literals).
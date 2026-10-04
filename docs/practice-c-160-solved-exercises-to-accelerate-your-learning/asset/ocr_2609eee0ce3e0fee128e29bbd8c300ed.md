# 63. Write a program that displays even numbers 1 to 50 and odd numbers 51 to 100 using a repeating loop.

```
#include <iostream>
```

```
int main() {
    // Display even numbers from 1 to 50
    for (int i = 2; i <= 50; i += 2) {
        std::cout << i << "";
    }

    std::cout << std::endl; // For better separation

    // Display odd numbers from 51 to 100
    for (int i = 51; i <= 100; i += 2) {
        std::cout << i << "";
    }

    return 0;
}
```
```
}
```

# 75. Write a program that prompts the user for a number and displays the Fibonacci sequence up to the given number using a repeating loop.

```
#include <iostream>

int main() {
    int n, t1 = 0, t2 = 1, nextTerm = 0;

    std::cout << "Enter the number of terms: ";
    std::cin >> n;

    std::cout << "Fibonacci Series: ";

    for (int i = 1; i <= n; ++i) {
        if (i == 1) {
            std::cout << t1 << "";
            continue;
        }
        if (i == 2) {
```
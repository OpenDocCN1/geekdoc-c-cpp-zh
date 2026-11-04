# 2. `do-while` Loop:

The `do-while` loop is just like the `while` loop, but it guarantees that the block of code is executed at least once, regardless of whether the condition is initially true or false.

# Syntax:

```
do {
    // Code to repeat
} while (condition);
```

# Example: Using a `do-while` Loop:

```
#include <iostream>

int main() {
    int count = 0;

    do {
        std::cout << "Count: " << count << std::endl;
        count++;
    } while (count < 5);

    return 0;
}
```

# 3. `for` Loop:

The `for` loop is designed for iterating a specific number of times. It consists of an initialization step, a condition, and an update statement.

# Syntax:
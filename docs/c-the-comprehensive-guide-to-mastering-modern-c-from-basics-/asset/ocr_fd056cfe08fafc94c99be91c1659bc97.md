```
std::cout << sum << std::endl;
}
```

# Listing 8.14 Sum with a “for” loop.

Here is the initialization int number=1. Before the statements in the loop are executed, the condition number <= 100 is checked. Then follows the execution of the loop, here sum += number;. At the end of the block, the update is executed with number += 1.

Then the condition is checked again. If it is met, the next loop iteration follows; if not, the loop ends.

Even with for, number ends up at 101. As I have written it, I cannot output it because the number variable only exists within the loop. However, you can declare it before the loop and leave the initialization part empty.

```
// https://godbolt.org/z/185ha3q3f
#include <iostream>
int main() {
    /* Sum from 1 to 100 */
    int sum = 0; // Initialization before
    int number = 1;
    for(; number <= 100; number=number+1) { // empty initialization
        sum = sum + number;
    }
    std::cout << number << std::endl; // number now also exists
}

```

# Listing 8.15 “for” loop with empty initialization part.

Here you can also access number outside the loop and thus see how 101 is printed.
As with the for statement, a; at the end of the while statement declares an empty loop body. For example, putting a; after the parentheses:

```
int a = 1;
while (a != 10) {
    a++;
```

makes the loop infinite, and the statement a++; will never be executed. A last example before we go to the exercises. What does the following program output?

```
#include <iostream> // Example 6.10
int main() {
    int i = 6, sum = 0;
    while (i >= 0) {
        sum += 20;
        i -= 2;
    }
    std::cout << "Sum: " << sum << '\\n';
    return 0;
}
```

Trace the iterations and be careful with the calculations, before you see the answer in the next page; should be easy for you.
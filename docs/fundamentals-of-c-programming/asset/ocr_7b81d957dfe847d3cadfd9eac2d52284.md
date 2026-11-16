If during the program’s execution the condition of the if is ever false (for example, when n is 3 and factor is 2), the inner loop cannot change the state of the program. This means factor does not change, and factor controls the progression of the inner loop. This effectively creates an infinite loop for the inner while loop. We must move the statement that modifies the factor variable outside of the if statement’s body.

```
while (factor < n) {
    if (n % factor == 0)
        std::cout << factor << " ";
    factor++;
}
```

Note that the curly braces are necessary for the statement incrementing factor to be part of the body of the while. Now the inner while statement contains two statements: the if statement and the statement incrementing factor. This new version runs correctly because factor changes during each iteration of the inner while loop regardless of the truth value of the condition in the if statement.

Programmers can use a debugger to step through a program to see where and why an infinite loop arises. Another common technique is to put print statements in strategic places to examine the values of the variables involved in the loop’s control. The original inner loop can be so augmented:

```
while (factor <= n) {
    std::cout << " factor = " << factor
              << " n = " << n << '\n';
    if (n % factor == 0) {
        std::cout << factor << " ";
        factor++;
    }
}
```

It produces the following output:

| Output |
| :--- |
| 1: factor = 1 n = 1 |
| 1 |
| 2: factor = 1 n = 2 |
| 1 factor = 2 n = 2 |
| 2 |
| factor = 1 n = 3 |
| 1: factor = 2 n = 3 |
| factor = 2 n = 3 |
| factor = 2 n = 3 |
| factor = 2 n = 3 |
| factor = 2 n = 3 |
| factor = 2 n = 3 |
| . |
| . |
| . |

The program continues to print the same line until the user interrupts its execution. The output demonstrates that once factor becomes equal to 2 and n becomes equal to 3 the program’s execution becomes trapped in the inner loop. Under these conditions:

+   1. 2 < 3 is true, so the loop continues and
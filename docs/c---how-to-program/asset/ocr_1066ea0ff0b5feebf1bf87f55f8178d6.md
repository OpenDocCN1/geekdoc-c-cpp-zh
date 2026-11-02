The Fibonacci series may be defined recursively as follows:

\[
\begin{aligned}
fibonacci(0) &= 0 \\
fibonacci(1) &= 1 \\
fibonacci(n) &= fibonacci(n - 1) + fibonacci(n - 2)
\end{aligned}
\]

Figure 5.19 calculates the \(n^{th}\) Fibonacci number recursively using function `fibonacci`. Notice that Fibonacci numbers tend to become large quickly. Therefore, we've chosen the data type `unsigned int` for the parameter type and the data type `unsigned long long int` for the return type in function `fibonacci`. In Fig. 5.19, each pair of output lines shows a separate run of the program.

```
```c
// Fig. 5.19: fig05_19.c
// Recursive fibonacci function
#include <stdio.h>

unsigned long long int fibonacci(unsigned int n); // function prototype

int main(void)
{
    unsigned int number; // number input by user

    // obtain integer from user
    printf("%s", "Enter an integer: ");
    scanf("%u", &number);

    // calculate fibonacci value for number input by user
    unsigned long long int result = fibonacci(number);

    // display result
    printf("Fibonacci(%u) = %llu\n", number, result);
}

// Recursive definition of function fibonacci
unsigned long long int fibonacci(unsigned int n)
{
    // base case
    if (0 == n || 1 == n) {
        return n;
    }
    else { // recursive step
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```
```

```
```text
Enter an integer: 0
Fibonacci(0) = 0
```
```

```
```text
Enter an integer: 1
Fibonacci(1) = 1
```
```

**Fig. 5.19**  Recursive fibonacci function. (Part 1 of 2.)
# 336 Introduction to C++

What I'm asking you is not to prove the “Colatz conjecture” and contest for the next Fields prize, but just that, to verify it with a simple program. Write a recursive function that takes as parameter a positive integer and displays the produced sequence of numbers.

```
#include <iostream>

int collatz(int n);

int main()
{
    int a;
    do {
        std::cout << "Enter a positive integer: ";
        std::cin >> a;
    } while (a <= 0);

    std::cout << "The result is " << collatz(a) << " indeed!!!\n";
    return 0;
}

int collatz(int n)
{
    std::cout << n << '\n';
    if(n == 1)
        return 1;
    else if (n & 1) // If n is odd.
        return collatz(3*n+1);
    else // If n is even.
        return collatz(n/2);
}
```

**Comments:** Run the program for various positive integers. The result is really impressive. You'll always end up with 1.

# UNSOLVED EXERCISES

**U.11.1** Write a function that takes as parameters three integers and checks if the sum of the first two numbers is equal to the third. If it is, the function should return the larger of the first two numbers, otherwise the smaller of the second and the third one. Write a program that reads three, calls the function, and displays the return value.

**U.11.2** Write a function that takes as parameters two pointers to floats and returns the pointer to the variable with the larger value. Write a program that reads two floats and uses the function to display the larger of them.

**U.11.3** Write the functions $f()$ and $g()$, as follows:

![](bbox=[0.31, 0.838, 0.74, 0.898])

Write a program that reads an integer (e.g., $x$) and uses $f()$ and $g()$ to display the result of $f(g(x))$, with the restriction that $g()$ must be called from inside $f()$.
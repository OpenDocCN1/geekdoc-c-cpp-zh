```
unsigned long num int fact(int num)
{
    if (num == 0) || (num == 1)
        return 1;
    else
        return num * fact(num-1);
}
```

**Comments:** Notice that for large values of num calls to fact() increase; therefore, the time to calculate its factorial also increases. In that case, the alternative solution with the for loop in C.6.3 calculates the factorial's number faster.

# **C.11.32** Write a recursive function that takes as parameter integer (e.g., N) and returns the Nth term of the Fibonacci sequence, using the formula F(N) = F(N-1) + F(N-2), where F(0) = 0 and F(1) = 1. Write a program that reads an integer N between 2 and 40 and uses the function to display the Nth term.

```
#include <iostream>

unsigned int fib(int num)

int main()
{
    int num;
    do
    {
        std::cout << "Enter a number between 2 and 40: ";
        std::cin >> num;
    } while (num < 2 || num > 40);

    std::cout << "Fib" << num << " = " << fib(num) << "\n";
    return 0;
}

unsigned int fib(int num)
{
    if (num == 0)
        return 0;
    else if (num == 1)
        return 1;
    else
        return fib(num-1) + fib(num-2);
}
```

**Comments:** This recursive solution for calculating Fibonacci numbers is not so efficient, because the calculation of the lower terms is repeated. For example, fib(5) = fib(4) + fib(3). To calculate fib(4), fib(3) and fib(2) are calculated. However, the second term fib(3) is repeated. As a result, the execution time of fib(), especially for large values, increases significantly. Comparing the solutions, the code presented earlier in exercise C.11.15 is executed faster.
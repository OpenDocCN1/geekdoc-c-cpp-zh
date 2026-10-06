3.7 Write a function that contains two unsigned short int parameters. When the second parameter is nonzero, it returns the result of the first parameter dividing by the second parameter, and the result is of the short int type; otherwise, it returns -1. Realize input and output in the main function.

3.8 Write a function to convert Fahrenheit degrees to Celsius degrees. The formula is: C = (F - 32) * 5/9. In the main function, prompt users to input a Celsius degree, convert it into the corresponding Fahrenheit degree, and output the result.

3.9 Write a function to judge whether a number is prime or not. Realize input and output in the main function.

3.10 Write a function to get the greatest common divisor and the least common multiple of two integers.

3.11 What is a nested call? What is a recursive call?

3.12 Input an integer n in the main function, and write a function to calculate 1 + 2 + ... + n in a recursive way.

3.13 Write a recursive function Power(int x, int y) to calculate the y-th power of x. Realize input and output in the main function.

3.14 Write a function to calculate Fibonacci numbers in a recursive way.

fib(n) = fib(n-1) + fib(n-2), n > 2 ; fib(1) = fib(2) = 1

Observe the procedure of making a recursive call.

3.15 Write a function to calculate the n-th Legendre Polynomial in a recursive way. Realize input and output in the main function. The recursion formula of the n-th Legendre Polynomial is:

```
p_n(x) = \begin{cases} 1 & (n = 0) \ x & (n = 1) \ ((2n-1) \times x \times p_{n-1}(x) - (n-1) \times p_{n-2}(x))/n & (n > 1) \end{cases}
```
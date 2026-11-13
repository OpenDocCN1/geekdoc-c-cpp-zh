Let us consider an example of computing the factorial of a number. Factorial is a mathematical term. The factorial of a number, say n, is equal to the product of all the integers from 1 to n. The factorial of n is denoted as

n! = 1 x 2 x 3 x ... x n or n! = n x n - 1 x ... x 1 (4.1)

For example, 10! = 1 x 2 x 3 x 4 x 5 x 6 x 7 x 8 x 9 x 10. The simplest program to calculate the factorial of a number is by using a loop with a product variable.

Algorithm 4.1 states the iterative process of computing the factorial of n as 10! = 10 x 9 x 8 x ... x 1.

```
ALGORITHM 4.1
An iterative version of an algorithm to compute the factorial of a number
1. start
2. Let n be the number whose factorial is to be computed and let Factorial = 1
3. while(n > 1) do
   begin
   Factorial = Factorial * n
   n = n - 1
   end
4. stop
```

The iterative process of computing the factorial of n in Algorithm 4.1 can also be written as in Algorithm 4.2.

```
ALGORITHM 4.2
An iterative version of the algorithm to compute the factorial of a number
1. start
2. Let n be the number whose factorial is to be computed and let Factorial = 1
3. for I = 1 to n do // I can also be initialized to 2
   begin
   Factorial = Factorial * I
   end
4. stop
```
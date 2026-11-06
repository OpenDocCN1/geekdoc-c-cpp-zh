The Fibonacci series can be defined recursively as follows:

```
```text
fibonacci(0) = 0
fibonacci(1) = 1
fibonacci(n) = fibonacci(n − 1) + fibonacci(n − 2)
```
```

The program of **Fig. 6.26** calculates the *n*th Fibonacci number recursively by using function `fibonacci`. Fibonacci numbers tend to become large quickly, although slower than factorials do. Therefore, we chose the data type `unsigned long` for the parameter type and the return type in function `fibonacci`. **Figure 6.26** shows the execution of the program, which displays the Fibonacci values for several numbers.
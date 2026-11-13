```
```c
int Fact(n)
{
    return Fact1(n, 1);
}
int Fact1(int n, int res)
{
    if (n == 1)
        return res;
    else
        return Fact1(n-1, n*res);
}
```
```

Whenever there is a pending operation to be performed, the function becomes non-tail recursive. In such a non-tail recursive function, information about each pending operation must be stored, so the amount of information directly depends on the number of calls.

However, the same factorial function can be written in a tail-recursive manner as shown Fig. 7.31. In the code, Fact1 function preserves the syntax of Fact(n). Here the recursion occurs in the Fact1 function and not in Fact function. Carefully observe that Fact1 has no pending operation to be performed on return from recursive calls. The value computed by the recursive call is simply returned without any modification.

# Figure 7.31 Tail recursion

in this case, the amount of information to be stored on the system stack is constant (only the values of n and res need to be stored) and is independent of the number of recursive calls.

# Converting Recursive Functions to Tail Recursive

A non-tail recursive function can be converted into a tail-recursive function by using an auxiliary parameter as we did in case of the Factorial function. The auxiliary parameter is used to form the result. When we use such a parameter, the pending operation is incorporated into the auxiliary parameter so that the recursive call no longer has a pending operation. We generally use an auxiliary function while using the auxiliary parameter. This is done to keep the syntax clean and to hide the fact that auxiliary parameters are needed.

# Linear and Tree Recursion

```
```c
int Fibonacci(int num)
{
    if(num == 0)
        return 0;
    else if (num == 1)
        return 1;
    else
        return (Fibonacci(num - 1) + Fibonacci(num - 2));
}
```
```

Observe the series of function calls. When the function returns, the pending operations in turn calls the function

+   - Fibonacci(7) = Fibonacci(6) + Fibonacci(5)
+   - Fibonacci(6) = Fibonacci(5) + Fibonacci(4)
+   - Fibonacci(5) = Fibonacci(4) + Fibonacci(3)
+   - Fibonacci(4) = Fibonacci(3) + Fibonacci(2)
+   - Fibonacci(3) = Fibonacci(2) + Fibonacci(1)
+   - Fibonacci(2) = Fibonacci(1) + Fibonacci(0)

Now we have, Fibonacci(2) = 1 + 0 = 1
Fibonacci(3) = 1 + 1 = 2
Fibonacci(4) = 2 + 1 = 3
Fibonacci(5) = 3 + 2 = 5
Fibonacci(6) = 3 + 5 = 8
Fibonacci(7) = 5 + 8 = 13

# Figure 7.32 Tree recursion

Recursive functions can also be characterized depending on the way in which the recursion grows in a linear fashion or forming a tree structure (Fig. 7.32). In simple words, a recursive function is said to be linearly recursive when the pending operation (if any) does not make another recursive call to the function. For example, observe the last line of recursive factorial function. The factorial function is linear recursive as the pending operation involves only multiplication to be performed and does not involve another recursive call to fact. On the contrary, a recursive function is said to be tree recursive (or non-linear recursive) if the pending operation makes another recursive call to the function. For example, the Fibonacci function in which the pending operations recursively call the Fibonacci function.

# Tower of Hanoi

The tower of Hanoi is one of the main applications of recursion. It says, 'if you can solve n-1 cases, then you can easily solve the nth case'.
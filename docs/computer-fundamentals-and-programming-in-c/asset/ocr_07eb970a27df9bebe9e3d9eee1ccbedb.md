The recursive step adds the results from the two smaller problems fib(n-2) and fib(n-1) to obtain the solution to the current fib(n) problem. This function uses what is known as 'non-linear' recursion.

In this context, brief definitions of linear, non-linear, and mutual recursions are given as follows.

**Linear recursion**  This term is used to describe a recursive function where at most one recursive call is carried out as part of the execution of a single recursive process.

**Non-linear recursion**  This term is used to describe a recursive function where more than one recursion can be carried out as part of the execution of a single recursive process.

**Mutual recursion**  In order to check and compile a function call, a compiler must know the type of the function, the number of parameters, and so on. In direct recursion the function header, which contains this information, is seen before any call within the function body or later. In mutual recursion, the functions must be defined in some order. This means that a call of at least one function must be compiled before its definition is seen. Different programming languages approach this problem in various ways. Some use separate *forward* definitions of function headers to give sufficient information to compile a call and *body* definitions to contain those calls.

Coming back to the Fibonacci sequence problem, any number in the sequence can be determined by the following definition.

Fibo(n) = { 1, if n <= 2; Fibo(n-1) + Fibo(n-2), otherwise }

Considering the definition, the following code may be used in a recursive function to generate the numbers in the Fibonacci sequence.

```
    int fib(int val)
    {
        if(val <= 2)
            return 1;
        else
            return(fib(val - 1) + fib(val - 2));
    }
```

The following example illustrates the use of the preceding recursive function for generating the Fibonacci numbers.

# EXAMPLE

```
    23. /****************************************/
    /* Program for computing the Fibonacci number sequence using recursion. */
    /****************************************/
    #include <stdio.h>
    #include <stdlib.h>
    int fib(int); /* function prototype */
```

```
    int main()
    {
        int i,j;
        printf("\n Enter the number of terms: ");
        scanf("%d",&i);
        if(i < 0)
        {
            printf("\n Error - Number of terms cannot be negative\n");
            exit(1);
        }
        printf("\n Fibonacci sequence for %d terms is:",i);
        for(j=1; j<=i; ++j)
            printf(" %d",fib(j)); /* function call to return jth Fibonacci term*/
        return 0;
    }
    /****************************************/
    /* Recursive function fib() */
    /****************************************/
    int fib(int val)
    {
        if(val <= 2)
            return 1;
        else
            return(fib(val - 1) + fib(val - 2));
    }
```

```
    Output
    (a) Enter the number of terms: 6
        Fibonacci sequence for 6 terms is: 1 1 2 3 5 8
    (b) Enter the number of terms: 4
        Fibonacci sequence for 4 terms is: 1 1 2 3
```

The non-recursive version of the Fibonacci function discussed above is as follows.

```
    int fib(int val)
    {
        int current = 1;
        int old = 1;
        int older = 1;
        val -= 2;
        while(val > 0)
        {
            current = old + older;
            older = old;
            old = current;
            --val;
        }
        return current;
    }
```

# Greatest common divisor

The greatest common divisor of two integers is the largest integer that divides them both. The problem is to calculate the GCD of two non-negative integers m and n recursively.
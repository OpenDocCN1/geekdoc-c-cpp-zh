```
repeat{
  do any code in here
}
```

Notice that a repeat statement doesn't include any kind of loopindex or loopcondition. To stop repeating the code inside the braces, you must use a break declaration inside the braced area (usually within an if statement); without it, the braced code will repeat without end, creating an infinite loop. To avoid this, you must make sure the operations will repeat at some point the loop to reach a break.

To see repeat in action, you will use it to calculate the famous Fibonacci sequence. The Fibonacci sequence is an infinite series of integers beginning with 1, 1, 2, 3, 5, 8, 13... where each term in the series is determined by the sum of the two previous terms. Formally, if $F_n$ represents the nth Fibonacci number, then:

```
$F_{n+1} = F_n + F_{n-1}; \quad n = 2, 3, 4, 5, \dots$
```

where

```
$F_1 = F_2 = 1$.
```

The following repeat statement computes and prints the Fibonacci sequence, ending when it reaches a term greater than 150:

```
R fib.a <- 1
R fib.b <- 1
R repeat{\n+ temp <- fib.a+fib.b
+ fib.a <- fib.b
+ fib.b <- temp
+ cat(fib.b,",",sep="=")
+ if(fib.b>150) {
+ cat("BREAK NOW...\n")
+ break
+ }
}
2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, BREAK NOW...
```

First, the sequence is initialized by the first two terms, both 1, as fib.a and fib.b. Then, the repeat statement is entered, and it uses fib.a and fib.b to compute the next term in the sequence, stored as temp. Next, fib.a is overwritten by fib.b, and fib.b is overwritten to so that the two variables move forward through the series. In is, fib.b becomes the newly calculated Fibonacci number, and fib.a becomes the second-to-last number in the series so far. Use of cat prints the new value of fib.b to the console. Finally, a check is made to see whether the latest term is greater than 150, and if it is, break is declared.
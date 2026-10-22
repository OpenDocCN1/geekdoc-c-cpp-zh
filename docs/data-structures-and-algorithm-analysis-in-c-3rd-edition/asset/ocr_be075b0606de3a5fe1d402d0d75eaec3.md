algorithm match the lower bound for the problem with certainty, it is nearly as good. Once we realize that a problem is NP-complete, then we know that our next step must either be to redefine the problem to make it easier, or else use one of the “coping” strategies discussed in this section.

# 17.3 Impossible Problems

Even the best programmer sometimes writes a program that goes into an infinite loop. Of course, when you run a program that has not stopped, you do not know for sure if it is just a slow program or a program in an infinite loop. After “enough time,” you shut it down. Wouldn’t it be great if your compiler could look at your program and tell you before you run it that it will get into an infinite loop? To be more specific, given a program and a particular input, it would be useful to know if executing the program on that input will result in an infinite loop without actually running the program.

Unfortunately, the Halting Problem, as this is called, cannot be solved. There will never be a computer program that can positively determine, for an arbitrary program P, if P will halt for all input. Nor will there even be a computer program that can positively determine if arbitrary program P will halt for a specified input I. How can this be? Programmers look at programs regularly to determine if they will halt. Surely this can be automated. As a warning to those who believe any program can be analyzed in this way, carefully examine the following code fragment before reading on.

```
while (n > 1)
    if (ODD(n))
        n = 3 * n + 1;
    else
        n = n / 2;
```

This is a famous piece of code. The sequence of values that is assigned to n by this code is sometimes called the Collatz sequence for input value n. Does this code fragment halt for all values of n? Nobody knows the answer. Every input that has been tried halts. But does it always halt? Note that for this code fragment, because we do not know if it halts, we also do not know an upper bound for its running time. As for the lower bound, we can easily show Ω(log n) (see Exercise 3.14).
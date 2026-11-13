induction method requires a programmer to demonstrate the following facts about the function's behavior:

# Induction Method
## to Show That a Recursive Function is Correct

To show that a recursive function meets its precondition/postcondition contract, first show that there is no infinite recursion (by showing the previous Conditions 1 and 2); and then show that the following two conditions are also valid:

3. Whenever the function makes no recursive calls, then it meets its precondition/postcondition contract. (This is called the base step.)

4. Whenever the function is called and all the recursive calls it makes meet their precondition/postcondition contracts, then the original call will also meet its precondition/postcondition contract. (This is called the induction step.)

The conditions are numbered 3 and 4 to emphasize that they ensure correctness only if you know that there is no infinite recursion. You must also ensure that Conditions 1 and 2 hold for an appropriate variant expression and threshold.

Let's return to the function pow defined in Figure 9.11 on page 465. To complete our demonstration so that it performs as desired, we must show that Conditions 3 and 4 hold.

It is easy to see that Condition 3 holds. The only way that the function can terminate without a recursive call is if the value of x is zero or n is zero. If x is zero the function returns 0, which is the correct answer; if n is zero (and x is not zero) the function returns 1, which is also correct.

To see that Condition 4 holds we need only recall the algebraic identities:

```
x^n = x(x^{n-1}) and x^n = 1/x^{-n}
```

To summarize how to reason about recursion: First check that the function always terminates (no infinite recursion); next make sure that the stopping cases work correctly; finally, for each recursive case, pretend that you know the recursive calls will work correctly, and use this to show that each recursive case works correctly.

# Self-Test Exercises for Section 9.3

+   13. What is a variant expression?

+   14. Write a recursive function that finds the sum of the first n odd positive integers. Find a variant expression and a threshold for this function.
A recursive definition of the factorial function is arrived at by observing the following algebraic relationship:

$n! = n \cdot (n - 1)!$

For example, 5! is clearly equal to 5 · 4! as is shown by the following:

```
5! = 5 · 4 · 3 · 2 · 1
5! = 5 · (4 · 3 · 2 · 1)
5! = 5 · (4!)
```

The evaluation of 5! would proceed as shown in Fig. 6.27. Figure 6.27(a) shows how the succession of recursive calls proceeds until 1! is evaluated to be 1, which terminates the recursion. Figure 6.27(b) shows the values returned from each recursive call to its caller until the final value is calculated and returned.

The program of Fig. 6.28 uses recursion to calculate and print the factorials of the integers 0–10. (The choice of the data type unsigned long is explained momentarily.) The recursive function factorial (lines 23–29) first determines whether the terminating condition number <= 1 (line 25) is true. If number is less than or equal to 1, the factorial function returns 1 (line 26), no further recursion is necessary and the function terminates. If number is greater than 1, line 28 expresses the problem as the product of number and a recursive call to factorial evaluating the factorial of number − 1. Note that factorial(number − 1) is a slightly simpler problem than the original calculation factorial(number).

Function factorial has been declared to receive a parameter of type unsigned long and return a result of type unsigned long. This is shorthand notation for unsigned long

![](bbox=[0.164, 0.561, 0.837, 0.918])

**Fig. 6.27** | Recursive evaluation of 5!.
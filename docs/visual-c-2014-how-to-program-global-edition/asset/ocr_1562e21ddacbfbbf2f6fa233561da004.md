The factorial of an integer, greater than or equal to 0 can be calculated iteratively (nonrecursively) using the for statement as follows:

```
long factorial = 1;
for (long counter = number; counter >= 1; --counter)
{
    factorial *= counter;
}
```

A recursive declaration of the factorial method is arrived at by observing the following relationship:

n! = n · (n - 1)!

For example, 5! is clearly equal to 5 · 4!, as is shown by the following equations:

+   - 5! = 5 · 4 · 3 · 2 · 1
- 5! = 5 · (4 · 3 · 2 · 1)
- 5! = 5 · (4!)

The evaluation of 5! would proceed as shown in Fig. 7.16. Figure 7.16(a) shows how the succession of recursive calls proceeds until 1! is evaluated to 1, which terminates the recursion. Figure 7.16(b) shows the values returned from each recursive call to its caller until the value is calculated and returned.

![](bbox=[0.146, 0.507, 0.857, 0.797])

Fig. 7.16 | Recursive evaluation of 5!

# 7.16.3 Implementing Factorial Recursively

Figure 7.17 uses recursion to calculate and display the factorials of the integers from 0 to 10. The recursive method Factorial (lines 17–28) first tests to determine whether a terminating condition (line 20) is true. If number is less than or equal to 1 (the base case), Factorial returns 1 and no further recursion is necessary. If number is greater than 1, line
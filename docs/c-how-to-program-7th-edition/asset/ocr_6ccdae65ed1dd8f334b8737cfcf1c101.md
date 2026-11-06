is also called the recursion step. The recursion step often includes the keyword return, because its result will be combined with the portion of the problem the function knew how to solve to form the result passed back to the original caller, possibly main.

The recursion step executes while the original call to the function is still “open,” i.e., it has not yet finished executing. The recursion step can result in many more such recursive calls, as the function keeps dividing each new subproblem with which the function is called into two conceptual pieces. In order for the recursion to eventually terminate, each time the function calculates a slightly simpler version of the original problem, this sequence of smaller and smaller problems must eventually converge to the base case. At that point, the function recognizes the base case and returns a result to the previous copy of the function, and a sequence of returns ensues up the line until the original call eventually returns the final result to main. This sounds quite exotic compared to the kind of problem solving we’ve been using to this point. As an example of these concepts at work, let’s write a recursive program to perform a popular mathematical calculation.

The factorial of a nonnegative integer n, written n! (and pronounced “n factorial”), is the product

$$n \cdot (n - 1) \cdot (n - 2) \cdot \ldots \cdot 1$$

with 1! equal to 1, and 0! defined to be 1. For example, 5! is the product 5 · 4 · 3 · 2 · 1, which is equal to 120.

The factorial of an integer, number, greater than or equal to 0, can be calculated iteratively (nonrecursively) by using a for statement as follows:

```
factorial = 1;
for ( int counter = number; counter >= 1; counter-- )
    factorial *= counter;
```

A recursive definition of the factorial function is arrived at by observing the following algebraic relationship:

$$n! = n \cdot (n - 1)!.$$

For example, 5! is clearly equal to 5 * 4! as is shown by the following:

```
5! = 5 · 4 · 3 · 2 · 1
5! = 5 · (4 · 3 · 2 · 1)
5! = 5 · (4!)
```

The evaluation of 5! would proceed as shown in Fig. 6.28. Figure 6.28(a) shows how the succession of recursive calls proceeds until 1! is evaluated to be 1, which terminates the recursion. Figure 6.28(b) shows the values returned from each recursive call to its caller until the final value is calculated and returned.

Figure 6.29 uses recursion to calculate and print the factorials of the integers 0---10. (The choice of the data type unsigned long is explained momentarily.) The recursive function factorial (lines 18---24) first determines whether the terminating condition number <= 1 (line 20) is true. If number is less than or equal to 1, the factorial function returns 1 (line 21), no further recursion is necessary and the function terminates. If number is greater than 1, line 23 expresses the problem as the product of number and a recursive call to factorial evaluating the factorial of number - 1, which is a slightly simpler problem than the original calculation factorial(number).
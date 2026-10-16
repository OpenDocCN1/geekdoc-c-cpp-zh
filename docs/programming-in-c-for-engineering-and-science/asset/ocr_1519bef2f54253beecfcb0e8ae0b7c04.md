problems whose solutions require *selection*. In this section we introduce the third control structure, *repetition.*

# 5.5.1 Example: Computing Factorials

The **factorial** of a nonnegative integer *n*, denoted by *n!*, is defined by

*n!* = { 1 if *n* = 0
1 × 2 × ⋯ × *n* if *n* > 0 }

To calculate *n!* by hand, we would probably begin with 1, multiply it by 2, multiply that product by 3, and so on, until we multiply by *n*. For example, to find 5!, we might do the following computation in which we keep a running product and increment a count from one step to the next:

| | |
|---|---|---|
| 1 | ← initial running product |
| × 2 | ← initial count |
| 2 | ← new running product |
| × 3 | ← new count |
| 6 | ← new running product |
| × 4 | ← new count |
| 24 | ← new running product |
| × 5 | ← new count |
| 120 | ← new running product |

If we analyze this computation of 5!, we see three parts in this repetition mechanism (also called a **loop**):

+   1. *Initialization:* Assign starting values to the running product and count.
+   2. *Repeated execution:* Repeatedly multiply the product by the count and increment the count.
+   3. *Termination:* Stop when the count reaches our final value 5.

We can describe the computation in general as follows:

# Algorithm for Factorial Computation

+   1. Initialize *product* to 1.
+   2. Repeat the following for each value of *count* in the range 2 to *n*
+      Multiply *product* by *count.*
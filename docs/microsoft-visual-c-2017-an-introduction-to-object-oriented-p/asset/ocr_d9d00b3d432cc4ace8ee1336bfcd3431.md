# CHAPTER 4 Making Decisions

A partial solution to this problem is to add an else clause to the statement:

```
if(saleAmount >= 1000)
    commissionRate = 0.08;
else if(saleAmount >= 500)
    commissionRate = 0.06;
else if(saleAmount <= 499)
    commissionRate = 0.05;
```

> Don't Do It
The logic reaches this point, the
expression must be true, so it is
waste of time to test this condition.

168

The last two logical tests in this code are sometimes called else-if statements because each
it subsequent if are placed on the same line. When the else-if format is used to test multiple cases,
programmers frequently forgo the traditional indentation and align each-if with the others.

With this code, saleAmount is $5000, the expression (saleAmount >= 1000) is true
and commissionRate becomes 0.08; then the entire structure ends. When saleAmount is
not greater than equal to $1000 (for example, $800), the first if is false and the
else statement executes and correctly sets commissionRate to 0.06.

This version of the code works, which is somewhat inefficient because it executes as follows:

+   - When saleAmount is at least $1000, the first Boolean test is true, so commissionRate is
assigned .08 and the reach ends.
- When saleAmount is less than $1000 but at least $500, the first Boolean test is false, but
the second one is true, so commissionRate is assigned .06 and if else structure ends.
- The only saleAmount that reaches the third Boolean test is less than $500, so the only
Boolean test, if(saleAmount <= 499), is always true. When an expression is true,
is there no need to evaluate it. In other words, if saleAmount is not at least $1000 and is also
not least $500, it must be default by least to reach or $499.

The improved code is as follows:

```
if(saleAmount >= 1000)
    commissionRate = 0.08;
else if(saleAmount >= 500)
    commissionRate = 0.06;
else
    commissionRate = 0.05;
```

In other words, this example uses three commission rates, two boundaries should be
checked. If there were three rates, there would be three boundaries to check, and so on.

With a nested if-else, processing is most efficient when the first question asked is the one
t is most likely to be true. In other words, if you know that a large number of saleAmount
values are greater than $1000, compare saleAmount to that value. That way, the logic
bypasses the rest of the decisions. If, however, you know that most saleAmounts are small,
processing is most efficient when the first decision is if(saleAmount < 500).
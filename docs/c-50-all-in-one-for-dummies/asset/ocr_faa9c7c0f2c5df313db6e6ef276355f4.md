# Performing Logical Comparisons — Is That Logical?

Remember that every expression has a type and a value. In the following code, both ++n and n++ are of type int:

```
int n;
n = 1;
int p = ++n;
n = 1;
int m = n++;
```

But what are the resulting values of m and p? (Hint: The choices are 1 and 2.) The value of p is 2, and the value of m is 1. That is, the value of the expression ++n is the value of n after being incremented, and the value of the expression n++ is the value of n before it's incremented. Either way, the resulting value of n itself is 2.

C# has equivalent decrement operators — n-- and --n. They work in exactly the same way as the increment operators.

C# provides a set of logical comparison operators, as shown in Table 4-2. These operators are logical comparisons because they return either a true or a false value of type bool.

| Table 4-2 | Logical Comparison Operators |
|---|---|
| Operator | Operator Is True If |
| a == b | a has the same value as b |
| a > b | a is greater than b |
| a >= b | a is greater than or equal to b |
| a < b | a is less than b |
| a <= b | a is less than or equal to b |
| a != b | a is not equal to b |

Here’s an example that involves a logical comparison:

```
int m = 5;
int n = 6;
bool b = m > n;
```

This example assigns the value false to the variable b because 5 is not greater than 6.
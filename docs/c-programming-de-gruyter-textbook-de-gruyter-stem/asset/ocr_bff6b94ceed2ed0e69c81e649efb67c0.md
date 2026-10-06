![](bbox=[0.176, 0.068, 0.823, 0.305])

# 2.4.1 Achieving Case Structure Using if Statement

if statements are designed to achieve case structure. Their syntax form is:

```
if (expression) statement 1
else statement 2
```

The execution order is: firstly evaluate the expression; if the expression is true, execute statement 1; otherwise execute statement 2. The flow chart of an if statement is shown in Figure 2.5.

> Here Statement 1 and 2 can also be several statements enclosed in brackets (known as a compound statement).
For example:

```
if (x>y) cout<<x;
else cout<<y;
```

The above statements output the larger number between x and y.
Statement 2 can be empty. When statement 2 is empty, we can ignore else, and the syntax form becomes the following:

```
if (expression) statement
```

For example:
if (x>y) cout<<x;

Example 2.2: Input a certain year and determine whether it is a leap year.
Analysis: a year is divisible by 4 but not by 100, or is divisible by 400. Therefore, we can first store the value of the input into the variable, and then evaluate the expression ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)). If the expression is true, then the input is a leap year; otherwise it is not.
# Two-Way Selection

There are many programming situations in which you must choose between two alternatives. For example, if a part-time employee works overtime, the paycheck is calculated using the overtime payment formula; otherwise, the paycheck is calculated using the regular formula. This is an example of two-way selection. To choose between two alternatives—that is, to implement two-way selections—C++ provides the if...else statement. Two-way selection uses the following syntax:

```
```cpp
if (expression)
    statement1
else
    statement2
```
```

Take a moment to examine this syntax. It begins with the reserved word if, followed by a logical expression contained within parentheses, followed by a statement, followed by the reserved word else, followed by a second statement. Statements 1 and 2 are any valid C++ statements. In a two-way selection, if the value of the expression is true, statement1 executes. If the value of the expression is false, statement2 executes. Figure 4-3 shows the flow of execution of the if...else statement (two-way selection).

![](bbox=[0.171, 0.495, 0.982, 0.735])

**FIGURE 4-3** Two-way selection

# EXAMPLE 4-1

Consider the following statements:

```
```cpp
if (hours > 40.0)                         //Line 1
    wages = 40.0 * rate +
            1.5 * rate * (hours - 40.0); //Line 2
else                                      //Line 3
    wages = hours * rate;                 //Line 4
```
```
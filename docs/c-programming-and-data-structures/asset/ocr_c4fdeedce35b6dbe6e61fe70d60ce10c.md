# UNIT 2
Selection and Decision Making

# 2.1 INTRODUCTION

We have seen that a C program is a set of statements which are normally executed sequentially in the order in which they appear. This happens when no options or no repetitions of certain calculations are necessary. However, in practice, we have a number of situations where we may have to change the order of execution of statements based on certain conditions, or repeat a group of statements until certain specified conditions are met. This involves a kind of decision making to see whether a particular condition has occurred or not and then direct the computer to execute certain statements accordingly.

C language possesses such decision-making capabilities by supporting the following statements:

+   1. if statement
+   2. switch statement
+   3. Conditional operator statement
+   4. goto statement

These statements are popularly known as decision-making statements. Since these statements ‘control’ the flow of execution, they are also known as control statements.

We have already used some of these statements in the earlier examples. Here, we shall discuss their features, capabilities and applications in more detail.

# 2.2 DECISION MAKING WITH IF STATEMENT

The if statement is a powerful decision-making statement and is used to control the flow of execution of statements. It is basically a two-way decision statement and is used in conjunction with an expression. It takes the following form:

```
if (test expression)
```

It allows the computer to evaluate the expression first and then, depending on whether the value of the expression (relation or condition) is ‘true’ (or non-zero) or ‘false’ (zero), it transfers the control to a particular statement. This point of program has two paths to follow, one for the true condition and the other for the false condition as shown in Fig. 2.1.

![](bbox=[0.65, 0.6, 0.95, 0.9])

Some examples of decision making, using if statements are:

+   1. if (bank balance is zero)
+      borrow money
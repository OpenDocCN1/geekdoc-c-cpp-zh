# **Program 4.5**  Find the relationship between two numbers (Continued)

```
Run
Enter the first number: 12
Enter the second number: 12
12 == 12

Run
Enter the first number: 12
Enter the second number: 28
12 < 28
```

# **A Serious Pitfall: Dangling Else Problem**

Nested *if-else* statements may create a classic problem known as the **dangling else**. If in a nested *if-else* statement we can have more *if* branches than *else* branches, we need to know which *if* branch should be paired with which *else* branch. The answer is that the compiler matches an *else* with the most recent unpaired *if*. This is done regardless of how we have intended our code.

> **An else is always paired with the most recent unpaired if.**

Figure 4.5 shows one flow diagram and two coded solutions. The first code does not correspond with the diagram because the *if* and the *else* sections are wrongly paired. In cases like this, we must use a compound statement as shown in the second code to be sure that the *else* statement is paired with the first *if* statement, not the second. We will see later that there is another solution to this problem: using logical expressions.

> **Always use compound statements to avoid a dangling else problem.**

# ### 4.1.4 Multiway Selection

Sometimes we need to solve a problem with several conditions, as shown below. Note that each statement could be a compound statement:

![](bbox=[0.295, 0.689, 0.868, 0.908])

**Figure 4.5**  Dangling else problem
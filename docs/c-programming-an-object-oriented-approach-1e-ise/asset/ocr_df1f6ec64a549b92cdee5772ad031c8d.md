# **Program 5.17** Finding if a number is a prime (Continued)

```
```
Run:
Enter a positive integer: 23
23 is a prime.

Run:
Enter a positive integer: 97
97 is a prime.
```
```

# ### 5.6.2 The *break* Statement

The **break statement** in C++ can be used in the body of a loop or a *switch* statement. We saw the use of the *break* statement in a *switch* statement in Chapter 4. We can also use a *break* statement to come out of a loop prematurely when we need to. All three loop statements can be terminated by the *break* statement. The *break* statement transfers control to the end of the loop. Most computer science professionals consider the use of the *break* in a loop non structural. They believe the Boolean expression in the loop should be redesigned to avoid using a *break* statement. The following code shows two different loops, with and without a *break* statement; both code segments do the same thing. (Statement1 and Statement2 are symbolic and can be any statement, including a compound statement.)

```
```
while (expression)
{
    Statement1
    if (condition)
        break;
    Statement2
}

while (expression && !condition)
{
    Statement1
    if (!condition)
        Statement2
}
```
```

# ### 5.6.3 The *continue* Statement

The next statement related to looping is the **continue statement**. As we saw before, a *break* statement terminates a loop if a condition occurs. But sometimes we do not want to terminate the loop; we just want to terminate one iteration and continue with the remaining iterations. In this case, we can use a *continue* statement, but we need to be careful because in the *while* and *do-while* loops, control is transferred to the Boolean expression. Therefore, any required updating must be included in the statements before the *continue* statement. In a *for* loop, however, the control is transferred to the updating statement in the header of the loop because the updating is explicitly there. Figure 5.15 shows the transfer point in each loop.

# ### 5.6.4 The *goto* Statement

Another statement in C++ that can be used with a loop statement is the **goto statement**. The following shows the format of this statement.

```
```
goto label
```
```
# **Program 5.11**  Printing a calendar for a month (Continued)

```
```text
Run:
Enter the number of days in the month (28, 29, 30, or 31): 31
Enter start day (0 to 6): 3

Sun Mon Tue Wed Thr Fri Sat
--- --- --- --- --- --- ---
                  1   2   3   4
  5   6   7   8   9  10  11
 12  13  14  15  16  17  18
 19  20  21  22  23  24  25
 26  27  28  29  30  31
```
```

# ### 5.4 THE *do-while* STATEMENT

The last repetition statement we discuss is the *do-while statement*, in which the logical expression is tested at the end of each iteration instead of at the beginning. For this reason, the *do-while* loop is a *post-test loop*. Since the logical expression in each iteration is tested after the body of the loop is executed, the body of the loop in a *do-while* statement is always executed at least once (Figure 5.12).

The *do-while* statement consists of five parts: the reserved word *do*, the statement that is the body of the loop (usually a compound statement enclosed in braces), the reserved word *while*, a logical expression in parentheses, and a semicolon. Note that the semicolon is required at the end of the *do-while* statement.

> **A semicolon is required at the end of the *do-while* statement.**

# #### 5.4.1 Event-Controlled Loop

The *do-while* statement is designed to be used as an event-controlled loop. However, the post-test feature of the *do-while* loop requires a different provision to control the loop.

# **At Least One Iteration**

The *do-while* loop is the recommended solution when a problem requires that the body of the loop be executed at least once.

![](bbox=[0.294, 0.719, 0.736, 0.906])

**Figure 5.12**  Flow diagram and syntax for a do-while statement
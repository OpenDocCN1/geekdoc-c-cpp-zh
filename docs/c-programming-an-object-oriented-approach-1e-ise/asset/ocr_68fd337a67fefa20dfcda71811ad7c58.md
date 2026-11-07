![](bbox=[0.394, 0.086, 0.781, 0.207])

```
~~~cpp
// Using x as count-up counter                         // Using y as count-down counter
int x = 3;                                              int y = 8;
++x;                                                    y--;
++x;                                                    y--;
++x;                                                    y--;
cout << x;  // 6 is printed                             cout << y;  // 5 is printed
~~~
```

# ### Comparison between Postfix and Prefix Expressions

When we compare the postfix and prefix expressions, we see that they behave the same if we are only interested in their side effects (contents of the variable). The difference is in the return values. The return value of the postfix expression is the original value of the variable; the return value of the prefix expression is the value of the variable after the side effect. In other words, if we are using any of these expressions as a counter, there is no difference. Traditionally programmers use the postfix expressions.

# ### 5.1.2 Repetition Statements

Three repetition statements are used in C++: the *while* statement, the *for* statement, and the *do-while* statement, as shown in Figure 5.5. We discuss all three in this chapter.

# ## 5.2 | THE *while* STATEMENT

The first repetition statement we discuss is the **while statement** (or *while* loop). *Figure 5.6* shows the flow diagram and the syntax of this statement. The *while* statement is made of the reserved word *while*, followed by a Boolean expression (called the condition) in parentheses, followed by a single statement, which is the body of the *while* statement.

![](bbox=[0.338, 0.729, 0.916, 0.925])
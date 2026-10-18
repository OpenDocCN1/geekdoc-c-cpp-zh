# DISPLAY 2.13 Syntax of the while Statement

# A Loop Body with Several Statements:

```
1   while ( Boolean_Expression )
2   {
3       Statement_1
4       Statement_2
5       ...
6       Statement_Last
7   }
```

Do NOT put a semicolon here.

body

# A Loop Body with a Single Statement:

```
8   while ( Boolean_Expression )
9       Statement
```

body

are no longer satisfied. So, this while statement ends after repeating the loop body three times.

The syntax for a while statement is given in Display 2.13. The Boolean_Expressions allowed are exactly the same as the Boolean expressions allowed in an if-else statement. Just as in if-else statements, the Boolean expression in a while statement must be enclosed in parentheses. In Display 2.13 we have given the syntax templates for two cases: the case when there is more than one statement in the loop body and the case when there is just a single statement in the loop body. Note that when there is only a single statement in the loop body, you need not include the braces { and }.

Let’s go over the actions performed by a while statement in greater detail. When the while statement is executed, the first thing that happens is that the Boolean expression following the word while is checked. It is either true or false. For example, the comparison

```
countDown > 0
```

is true if the value of countDown is positive. If it is false, then no action is taken and the program proceeds to the next statement after the while statement. If the comparison is true, then the entire body of the loop is executed. At least one of the expressions being compared typically contains something that might be changed by the loop body, such as the value of countDown in the while statement in Display 2.12. After the body of the loop is executed, the comparison is again checked. This process is repeated again and again as long as the comparison continues to be true. After each iteration of the loop body, the comparison is again checked and if it is true, then the entire loop body is executed again. When the comparison is no longer true, the while statement ends.
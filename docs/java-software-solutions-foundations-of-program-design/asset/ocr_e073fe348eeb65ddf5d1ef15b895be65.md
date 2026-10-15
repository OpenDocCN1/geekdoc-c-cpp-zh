| done | count > MAX | !done | !done && (count > MAX) |
|---|---|---|---|
| false | false | true | false |
| false | true | true | true |
| true | false | false | false |
| true | true | false | false |

# FIGURE 5.5 A truth table for a specific condition

different reasons. If the left operand of the && operator is false, then the result of the operation will be false no matter what the value of the right operand is. Likewise, if the left operand of the || is true, then the result of the operation is true no matter what the value of the right operand is.

Sometimes you can capitalize on the fact that the operation is short-circuited. For example, the condition in the following if statement will not attempt to divide by zero if the left operand is false. If count has the value zero, the left side of the && operation is false; therefore. the whole expression is false and the right side is not evaluated.

```
if (count != 0 && total/count > MAX)
    System.out.println ("Testing.");
```

You should consider carefully whether or not to rely on these kinds of subtle programming language characteristics. Not all programming languages work the same way. As we have stressed before, you should favor readability over clever programming tricks. Always strive to make it clear to any reader of the code how the logic of your program works.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   SR 5.1 What is meant by the flow of control through a program?
+   SR 5.2 What type of conditions are conditionals and loops based on?
+   SR 5.3 What are the equality operators? The relational operators? The logical operators?
+   SR 5.4 Given the following declarations, what is the value of each of the listed boolean expressions?

```
int value1 = 5, value2 = 10;
boolean done = true;
```
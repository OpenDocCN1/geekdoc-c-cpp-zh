Let’s look at a couple more examples. Consider the following declaration:

```
int larger = (num1 > num2) ? num1 : num2;
```

If num1 is greater than num2, the value of num1 is returned and used to initialize the variable larger. If not, the value of num2 is returned and used to initialize larger. Similarly, the following statement prints the smaller of the two values:

```
System.out.println ("Smaller: " + ((num1 < num2) ? num1 : num2));
```

The conditional operator is occasionally helpful to evaluate a short condition and return a result. It is not a replacement for an if-else statement, however, because the operands to the ?: operator are expressions, not necessarily full statements. Even when the conditional operator is a viable alternative, you should use it carefully because it may be less readable than an if-else statement.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   SR 6.5 What is the difference between a conditional operator and a conditional statement?

+   SR 6.6 Write a declaration that initializes a char variable named id to 'A' if the boolean variable first is true and to 'B' otherwise.

+   SR 6.7 Express the following logic in a succinct manner using the conditional operator.
+   if (val <= 10)
+       System.out.println ("The value is not greater than 10.");
+   else
+       System.out.println ("The value is greater than 10.");

# 6.3 The do Statement

Remember from Chapter 5 that the while statement first examines its condition, then executes its body if that condition is true. The do statement is similar to the while statement except that its termination condition is at the end of the loop body. Like the while loop, the do loop executes the statement in the loop body until the condition becomes false. The condition is written at the end of the loop to indicate that it is not evaluated until the loop body is executed. Note that the body of a do loop is always executed at least once. Figure 6.1 shows this processing.
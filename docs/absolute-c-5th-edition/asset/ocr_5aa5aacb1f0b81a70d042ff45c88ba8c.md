# Omitting the else

Sometimes you want one of the two alternatives in an if-else statement to do nothing at all. In C++ this can be accomplished by omitting the else part. These sorts of statements are referred to as if statements to distinguish them from if-else statements. For example, the first of the following two statements is an if statement:

```
if (sales >= minimum)
    salary = salary + bonus;
cout << "$" << salary;
```

If the value of sales is greater than or equal to the value of minimum, the assignment statement is executed and then the count statement is executed. On the other hand, if the value of sales is less than minimum, the embedded assignment statement is not executed. Thus, if the statement causes no change (that is, no bonus is added to the base salary), the program proceeds to the count statement.

# Nested Statements

As you have seen, if-else statements and if statements contain smaller statements within them. Thus far we have used compound statements and simple statements such as assignment statements as smaller substates, but there are other possibilities. In fact, any statement at all can be a subst of an if-else statement or of other statements that have one or more statements within them.

When nesting statements, you normally indent each level of nested statements, although there are special situations (as a multiway if-else branch) where this rule is not followed.

# Multiway if-else Statement

The multiway if-else statement is not really different kind of C++ statement. It is simply an ordinary if-else statement nested inside of if-else statements, but it is thought of as a kind of statement and indented differently from other statements so as to reflect this thinking.

The syntax for a multiway if-else statement and a simple example are given in the accompanying box. Note that the Boolean expressions are aligned with one other. This makes it easy to see the correspondence between Boolean expressions and actions. The Boolean expressions are evaluated in order until a true Boolean expression is found. At that point the evaluation of Boolean expressions stops, and the action corresponding to the first true Boolean expression is executed. The final else is optional. If there is a final else and all the Boolean expressions are false, the final action is executed. If there is no final else and all the Boolean expressions are false, then no action is taken.
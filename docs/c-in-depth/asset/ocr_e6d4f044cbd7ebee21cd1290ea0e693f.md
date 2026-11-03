```
for(expression1;expression2;expression3)
    statement;
for(expression1;expression2;expression3)
{
    statement;
    statement;
    ........
}
```

The loop body can be a single statement or block of statements.

expression1 is an initialization expression, expression2 is a test expression or condition and expression3 is an update expression. expression1 is executed only once when the loop starts and is used to initialize the loop variables. This expression is generally an assignment expression. expression2 is a condition and is tested before each iteration of the loop. This condition generally uses relational and logical operators. expression3 is an update expression and is executed each time after the body of the loop is executed.

Now let us see how this loop works. Firstly the initialization expression is executed and the loop variables are initialized, and then the condition is checked, if the condition is true then the body of loop is executed. After executing the loop body, control transfers to expression3(update expression) and it modifies the loop variables and then again the condition is checked , and if it is true, the body of loop is executed. This process continues till the condition is true and when the condition becomes false the loop is terminated and control is transferred to the statement following the loop.

The work done by the for loop can be performed by writing a while loop as-

![](bbox=[0.3, 0.78, 0.9, 0.95])

# Flow chart of for loop
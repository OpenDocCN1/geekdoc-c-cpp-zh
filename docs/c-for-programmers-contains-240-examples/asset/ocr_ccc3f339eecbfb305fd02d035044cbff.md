# for Statement Header Components

Figure 5.3 takes a closer look at the for statement header (line 11) of Fig. 5.2. Notice that the for statement header “does it all”—it specifies each of the items needed for counter-controlled repetition with a control variable. If there is more than one statement in the body of the for, braces are required to enclose the body of the loop.

Notice that Fig. 5.2 uses the loop-continuation condition counter <= 10. If you incorrectly wrote counter < 10, then the loop would execute only 9 times. This is a common off-by-one error.

> **Common Programming Error 5.2**
> 
> *Using an incorrect relational operator or using an incorrect final value of a loop counter in the condition of a while or for statement can cause off-by-one errors.*

The general form of the for statement is

```
for ( initialization; loopContinuationCondition; increment )
    statement
```

where the initialization expression initializes the loop’s control variable, loopContinuationCondition determines whether the loop should continue executing (this condition typically contains the final value of the control variable for which the condition is true) and increment increments the control variable. In most cases, the for statement can be represented by an equivalent while statement, as follows:

```
initialization;

while ( loopContinuationCondition )
{
    statement
    increment;
}
```

There is an exception to this rule, which we’ll discuss in Section 5.7.

If the initialization expression in the for statement header declares the control variable (i.e., the control variable’s type is specified before the variable name), the control variable can be used only in the body of the for statement—the control variable will be unknown outside the for statement. This restricted use of the control variable name is

![](bbox=[0.164, 0.735, 0.837, 0.918])

**Fig. 5.3** | for statement header components.
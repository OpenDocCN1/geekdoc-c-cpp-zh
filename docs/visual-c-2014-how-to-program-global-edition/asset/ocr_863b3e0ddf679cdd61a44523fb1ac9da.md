# Chapter 6 Control Statements: Part 2

Combining these results illustrates that any form of control ever needed in a C# app can be expressed in terms of

+   - sequence structure
- if statement (selection)
- while statement (iteration)

and these can be combined in only two ways—stacking and nesting.

# 6.13 Wrap-Up

Chapter 5 discussed the if, if...else and while control statements. In Chapter 6, we discuss the for, do...while and switch control statements. (We'll discuss the foreach statement in Chapter 8.) You learned that any algorithm can be developed using combinations of sequence (i.e., statements in the order in which they execute), the three selection statements—if, if...else and switch—and the four iteration statements—while, do...while, for and for. You saw that the for and do...while statements are simply more convenient ways to express types of iteration. Similarly, we showed that the switch statement is a convenient notion for multiple selection, rather than using if...else statements. We discussed how you can combine control statements by stacking and nesting them. We showed how to use the break and continue statements to alter the flow of control in iteration statements. You learned about the logical operators, which enable you to use more complex conditional expressions in control statements. In Chapter 7, we examine methods in greater depth.

# Summary

# Section 6.2 Essentials of Counter-Controlled Iteration

+   - Counter-controlled iteration requires a control variable, the initial value of the control variable, the increment (or decrement) by which the control variable is modified each time through the loop and the loop-continuation condition that determines whether looping should continue.

# Section 6.3 For Iteration Statement

+   - Typically, for statements are used for counter-controlled iteration, and while statements for sentinel-controlled iteration.

# Section 6.3.1 A Closer Look at the for's Header

+   - The header "does it all"—it specifies each of the items needed for counter-controlled iteration with a control variable.

# Section 6.3.2 General Format of a for Statement

+   - The general format of the for statement is

```
for (initialization; loopContinuationCondition; increment)
{
    statement
}
```

where the initialization expression names the loop's control variable and provides its initial value, the loopContinuationCondition is the condition that determines whether looping should continue
```
For 5 times
{
  Get the number from the user.
  Calculate the requested triangular number.
  Display the results.
}
```

The portion of the loop referred to in the preceding Calculate actually consists of setting the value of the variable triangularNumber to 0 plus the for loop that calculates the triangular number. Thus, a for statement is actually contained within another for statement. This is perfectly valid in Objective-C, and nesting can continue further to any desired level.

The proper use of indentation becomes even more critical when dealing with more sophisticated program constructs, such as nested for statements. At a quick glance, you can easily determine which statements are contained within each for statement.

# for Loop Variants

Before leaving this discussion of the for loop, we should mention some of the syntactic variations that are permitted in forming this loop. When writing a for loop, you might discover that you want to initialize more than one variable before the loop begins, or perhaps you want to evaluate more than one expression each time through the loop. You can include multiple expressions in any of the fields of the for loop, as long as you separate expressions by commas. For example, in the for statement begins

```
for ( i = 0, j = 0; i < 10; ++i )
...
```
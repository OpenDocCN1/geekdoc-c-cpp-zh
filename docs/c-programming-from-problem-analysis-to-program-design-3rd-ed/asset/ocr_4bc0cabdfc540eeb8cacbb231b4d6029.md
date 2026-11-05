As shown in Example 5-15, the else in Line 12 matches the if in Line 1; Line 10 matches Line 5. What value would be stored in amount if aValue, bValue, cValue, dValue, and eValue were all equal to 0? Did you get 25 when you traced the logic? Look at Example 5-15. By properly lining up the else clauses with their corresponding if clauses, the answer can be determined much more quickly.

# Example 5-15

```
if (aValue > 10)
    if (bValue == 0)
        amount = 5;
    else
        if (cValue > 100)
            if (dValue > 100)
                amount = 10;
            else
                amount = 15;
        else
            amount = 20;
else
    if (eValue == 0)
        amount = 25;
```

The rule indicates that an else matches up with the closest previous if that does not already have an else attached to it. However, you can use braces to attach an else to an outer if, as shown in Example 5-16.

# Example 5-16

```
if (average > 59)
{
    if (average < 71)
        grade = 'D';
}
else
    grade = 'F';
```

The braces enclose the true statement associated with the expression of (average > 59). The inner if statement is ended as a statement when the closing curly brace is encountered. Consider the statements in Example 5-17 that determine a grade based on testing the value in average.
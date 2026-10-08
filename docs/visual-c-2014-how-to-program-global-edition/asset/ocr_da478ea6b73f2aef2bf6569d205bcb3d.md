sage indicating the value of the control variable when the loop terminated. The loop fully
executes its body only four times instead of 10 because of the break.

```
// Fig. 6.13: BreakTest.cs
// break statement exiting a for statement.
using System;
class BreakTest
{
 static void Main()\{
    int count; // control variable also used after loop terminates
    for (count = 1; count <= 10; ++count) // loop 10 times
    {
        if (count == 5) // if count is 5,
            break; // terminate loop
    }
    Console.Write($"{count}");
}
Console.WriteLine($"\nbroke out of loop at count = {count}");
```

Broke out of loop at count = 5

**Fig. 6.13** | break statement exiting a for statement.

# 6.10.2 continue Statement

The continue statement, when executed in a while, for, do...while or for each, skips
the remaining statements in the loop body and proceeds with the next iteration of
loop. In while and do...while statements, the app evaluates the loop-continuation test
immediately after the continue statement executes. In a statement, the increment ex-
ormally executes next, then the app evaluates the loop-continuation test.

Figure 14 uses the continue statement in a for to skip the statement at line 16
when the nested if (line 11) determines that the value of count is 5. When the continue
statement executes, program control continues with the increment of the control variable
in the statement (line 9).

> Software Engineering Observation 6.I
Some programmers feel that break and continue statements violate structured
programming. Since the same effects are achievable with structured-programming
techniques, these programmers prefer not to use break or continue statements.
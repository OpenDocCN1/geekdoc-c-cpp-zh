# 5.5 do...while Repetition Statement

gram evaluates the loop-continuation test at the bottom of the loop (line 14). If the condition is true, the loop continues from the first body statement (line 12). If the condition is false, the loop terminates and the program continues with the next statement after the loop.

Figure 5.8 contains the UML activity diagram for the do...while statement. This diagram makes it clear that the loop-continuation condition is not evaluated until after the loop performs the action state at least once. Compare this activity diagram with that of the while statement (Fig. 4.4).

![](bbox=[0.1, 0.35, 0.9, 0.62])

It isn’t necessary to use braces in the do...while repetition statement if there’s only one statement in the body. However, many programmers include the braces, to avoid confusion between the while and do...while statements. For example,

```
while ( condition )
```

is normally the first line of a while statement. A do...while statement with no braces around a single-statement body appears as:

```
do
while ( condition );
```

which can be confusing. A reader may misinterpret the last line—while( condition );— as a while statement containing an empty statement (the semicolon by itself). Thus, the do...while statement with one body statement is usually written as follows:

```
do
{
statement
} while ( condition );
```
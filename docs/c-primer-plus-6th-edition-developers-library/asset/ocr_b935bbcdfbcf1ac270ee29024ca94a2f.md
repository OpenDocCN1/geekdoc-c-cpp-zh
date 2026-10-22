There is a use of goto tolerated by many C practitioners—getting out of a nested set of loops if trouble shows up (a single break gets you out of the innermost loop only):

```
while (funct > 0)
{
    for (i = 1, i <= 100; i++)
    {
        for (j = 1; j <= 50; j++)
        {
            statements galore;
            if (bit trouble)
                goto help;
            statements;
        }
        more statements;
    }
    yet more statements;
}
and more statements;
help : bail out;
```

As you can see from the other examples, the alternative forms are clearer than the goto forms. This difference grows even greater when you mix several of these situations. Which gotos are helping ifs, which are simulating if elses, which are controlling loops, which are just there because you have programmed yourself into a corner? By using gotos excessively, you create a labyrinth of program flow. If you aren’t familiar with gotos, keep it that way. If you are used to using them, try to train yourself not to. Ironically, C, which doesn’t need a goto, has a better goto than most languages because it enables you to use descriptive words for labels instead of numbers.

# Summary: Program Jumps

Keywords:
break, continue, goto
General Comments:
These three instructions cause program flow to jump from one location of a program to another location.
The break Command:
The break command can be used with any of the three loop forms and with the switch statement. It causes program control to skip the rest of the loop or the switch containing it and to resume with the next command following the loop or switch.
Example:

```
switch (number)
{
    case 4: printf("That's a good choice.\n");
```
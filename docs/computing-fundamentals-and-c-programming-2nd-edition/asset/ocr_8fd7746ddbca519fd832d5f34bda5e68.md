# ### 7.5.1 Dangling Else Problem

One of the classic problems encountered when we start using nested if....else statements is the dangling else. This occurs when a matching else is not available for an if. The answer to this problem is very simple. Always match an else to the most recent unmatched if in the current block. In some cases, it is possible that the false condition is not required. In such situations, else statement may be omitted

> > “else is always paired with the most recent unpaired if”

# ## 7.6 THE ELSE IF LADDER

LO 7.2

There is another way of putting ifs together when multipath decisions are involved. A multipath decision is a chain of ifs in which the statement associated with each else is an if. It takes the following general form:

```
~~~
if ( condition 1)
    statement-1;

    else if ( condition 2)
        statement-2;

        else if ( condition 3)
            statement-3;

            else if ( condition n)
                statement-n;
                else
                    default-statement;

statement-x;
~~~
```

This construct is known as the else if ladder. The conditions are evaluated from the top (of the ladder), downwards. As soon as a true condition is found, the statement associated with it is executed and the control is transferred to the statement-x (skipping the rest of the ladder). When all the n conditions become false, then the final else containing the default-statement will be executed. Figure 7.9 shows the logic of execution of else if ladder statements.

Let us consider an example of grading the students in an academic institution. The grading is done according to the following rules:

| Average marks | Grade |
| --- | --- |
| 80 to 100 | Honours |
| 60 to 79 | First Division |
| 50 to 59 | Second Division |
| 40 to 49 | Third Division |
| 0 to 39 | Fail |
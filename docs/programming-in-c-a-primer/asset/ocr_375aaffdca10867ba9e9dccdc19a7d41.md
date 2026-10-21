# 6.6 THE ELSE IF LADDER

Output of Program 6.4:
Largest value is : 712

There is another way of putting ifs together when multipath decisions are involved. A multipath decision is a chain of ifs in which the statement associated with each else is an if. It takes the following general form:
This construct is known as the else if ladder. The conditions are evaluated from the top (of the ladder), downwards. As soon as the true condition is found, the statement associated with it is executed and the control is transferred to the statement-x (skipping the rest of the ladder). When all the n conditions become false, then the final else containing the default-statement will be executed. Figure 6.5 shows pictorially the logic of execution of else if ladder statements.

Let us consider an example of grading the students in an academic institution. The grading is done according to the following rules:

```
if (condition 1)
    statement-1;
else if (condition 2)
    statement-2;
else if (condition 3)
    statement-3;
else if (condition n)
    statement-n;
else
    default-statement;
statement-x;
```

| AVERAGE MARKS | GRADE |
|---|---|
| 80 to 100 | Honours |
| 60 to 79 | First Division |
| 50 to 59 | Second Division |
| 40 to 49 | Third Division |
| 0 to 39 | Fail |

This grading can be done using the else if ladder as follows:

```
if(marks > 79)
    grade = "Honours";
else if(marks > 59)
    grade = "First Division";
else if(marks > 49)
    grade = "Second Division";
else if(marks > 39)
    grade = "Third Division";
else
    grade = "Fail";
Console.WriteLine("Grade: " + grade);
```

Consider another example given below:

```
if (code == 1)
    colour = "RED";
else if (code == 2)
```
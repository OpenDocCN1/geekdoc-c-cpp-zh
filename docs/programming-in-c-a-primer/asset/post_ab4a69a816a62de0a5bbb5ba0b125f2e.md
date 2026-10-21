
```
if(sex is female)
{
    if (balance > 5000)
        bonus = 0.05 * balance;
}
else
    bonus = 0.02 * balance;
    balance = balance + bonus;
```

In this case, else is associated with the outer if and therefore bonus is calculated for the male account holders. However, bonus for the female account holders, whose balance is equal to or less than 5000 is not calculated because of the missing else option for the inner if.

Program 6.4 employs nested if....else statements to determine the largest of three given numbers.

## Program 6.4    NESTING IF....ELSE STATEMENTS

```
using System;
class IfElseNesting
{
    public static void Main()
    {
        int a = 325, b = 712, c = 478;

        Console.Write("Largest value is : ");
        if (a > b)
        {
            if (a > c)
            {
                Console.WriteLine(a);
            }
            else
            {
                Console.WriteLine(c);
            }
        }
        else
        {
            if (c > b)
            {
                Console.WriteLine(c);
            }
            else
            {
                Console.WriteLine(b);
            }
        }
    }
}
```

## 6.6 THE ELSE IF LADDER

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

```
colour = "GREEN";
else if (code == 3)
code = "WHITE";
else
colour = "YELLOW";
........
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_106_0.png)

Code numbers other than 1, 2 or 3 are considered to represent YELLOW. The same results can be obtained by using nested if...else statements.

```
if(code != 1)
if (code != 2)
if (code != 3)
colour = "YELLOW";
else
colour = "WHITE";
else
colour = "GREEN";
else
colour = "RED";
```

In such situations, the choice of the method is left to the programmer. However, in order to choose an if structure that is both effective and efficient, it is important that the programmer is fully aware of the various forms of an if statement and the rules governing their nesting. Program 6.5 demonstrates the use of if....else ladder in analysing a marks list.

## Program 6.5 DEMONSTRATION OF ELSE IF LADDER

```
using System;
class ElselfLadder
{
    public static void Main()
    {
        int[] rollNumber = { 111, 222, 333, 444 };
        int[] marks = { 81, 75, 43, 58 };

        for (int i = 0; i < rollNumber.Length; i++)
        {
            if (marks[i] > 79)
                Console.WriteLine(rollNumber[i] + " Honours");
            else if (marks[i] > 59)
                Console.WriteLine(rollNumber[i] + " I Division");
            else if (marks[i] > 49)
                Console.WriteLine(rollNumber[i] + " II Division");
            else
                Console.WriteLine(rollNumber[i] + " FAIL");
        }
    }
}
```

Program 6.5 produces the following output:

111 Honours
222 I Division
333 FAIL
444 II Division

## 6.7 THE SWITCH STATEMENT

We have seen that when one of many alternatives has to be selected, we can design a program using if statements to control the selection. However, the complexity of such a program increases dramatically when the alternatives increase. The program becomes difficult to read and follow. At times, it may confuse even the designer of the program. Fortunately, C# has a built-in multiway decision statement known as a switch. The switch statement tests the value of a given variable (or expression) against a list of case values and when a match is found, a block of statements associated with that case is executed. The general form of the switch statement is as shown below:

```
switch(expression)
{
    case value-1:
        block-1
        break;
}
```

```
case value-2:
    block-2
    break;
    .....
    .....
default:
    default-block
    break;
}
statement-x;
```

The expression must be an integer type or char or string type. value-1, value-2 .... are constants or constant expressions and are known as case labels. Each of these values should be unique within a switch statement. block-1, block-2 .... are statement lists and may contain zero or more statements. There is no need to put braces around these blocks but it is important to note that case labels end with a colon (:).

The switch statement is executed in the following order:

+   1. The expression is evaluated first.
+   2. The value of the expression is successively compared against the values, value-1, value-2, .... If a case is found whose value matches the value of the expression, then the block of statements that follows the case are executed.
+   3. The break statement at the end of each block signals the end of a particular case and causes an exit from the switch statement, transferring the control to the statement-x following the switch.
+   4. The default is an optional case. When present, it will be executed if the value of the expression does not match any of the case values. If not present, no action takes place when all matches fail and the control goes to the statement-x.

The selection process of switch statement is illustrated in the flowchart shown in Fig. 6.6.

The switch statement can be used to grade the students as discussed in the last section. This is illustrated below:

```
........
........
index = marks/10;
switch(index)
{
    case 10:
    case 9:
    case 8:
        grade = "Honours";
        break;
    case 7:
    case 6:
        grade = "First Division";
        break;
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_108_0.png)

# Fig. 6.6 Selection process of the switch statement

```
case 5:
    grade = "Second Division";
    break;
case 4:
    grade = "Third Division";
    break;
default:
    grade = "Fail";
    break;
}
Console.WriteLine(grade);
```

Note that we have used a conversion statement index = marks/10; where, index is defined as an integer. The variable index takes the following integer values.

| MARKS | INDEX |
|-------|-------|
| 100 | 10 |
| 90 – 99 | 9 |
| 80 – 89 | 8 |
| 70 – 79 | 7 |
| 60 – 69 | 6 |
| 50 – 59 | 5 |
| 40 – 49 | 4 |
| 30 – 39 | 3 |
| 20 – 29 | 2 |
| 10 – 19 | 1 |
| 0 – 9 | 0 |

This segment of the program illustrates two important features First, it uses empty cases. The first three cases will execute the same statements grade = "Honours"; break;

Same is the case with case 7 and case 6. Second, the default condition is used for all other cases where marks are less than 40.

Program 6.6 illustrates the use of switch for a menu-driven interactive program.

## Program 6.6 TESTING THE SWITCH STATEMENT

```
using System;
class CityGuide
{
    public static void Main()
    {
        Console.WriteLine("Select your choice");
```


# Flowcharting a Pretest Loop

from the user. This instruction is referred to as the update read, because it allows the user to update the value of the input item (in this case, the sales amount) that controls the looping condition. The update read is often an exact copy of the priming read. Keep in mind if you do not include the update read in the loop body, there will be no way to enter the sentinel value after the loop body instructions are processed the first time. This is because the priming read is processed once and gets only the first amount from the user. You will learn more about this in the section titled "The while Statement" later in the chapter.

# Flowcharting a Pretest Loop

Figure 7-6 shows the Miller Incorporated algorithm in flowchart form. Recall that all of a flowchart use the start/stop symbol, the rectangle is the process symbol, the parallelogram is the input/output symbol, and the diamond is the decision symbol. The diamond in Figure 7-6 indicates the beginning of a repetition structure. Like the diamond in a selection structure, the parallelogram structure contains a condition that evaluates to true or false. The condition determines whether the instructions within the loop body are processed. Like the diamond in a selection structure, the diamond has one flowline entering it and two flowlines leaving it. The two flowlines leading out of the diamond are marked with a "T" (for true) and an "F" (for false). The inline marked with a "T" leads to the loop body, which contains the instructions to be processed when the loop's condition evaluates to true. Notice that the flowline marked with an "F", on the other hand, leads to the instructions to be processed when the loop's condition evaluates to false. The flowline entering the diamond, along with the diamond and the symbols and flowlines within the true path, form a circle or loop. It is this loop (circle) that distinguishes the repetition structure from the selection structure in flowchart.

![](img/d64a28a68f49d61137bf2f3170ac40ad_239_0.png)

Figure 7-6 Miller Incorporated algorithm shown in flowchart form

# CHAPTER 7 The Repetition Structure

To illustrate how a loop operates in a program, you will desk-check the algorithm in Figure 7-6 using the following sales data: 10000, 25000, and -1. The bonus amounts should be $500 and $1,250. First, you will record the input and output items in a desk-check table, as shown in Figure 7-7.

| bonus rate | sales | bonus |
| --- | --- | --- |
| .05 | | |

**Figure 7-7** Input and output items entered in the desk-check table

Next, follow each of the symbols in the flowchart, from top to bottom, recording in the desk-check table any changes made to values of the input and output items. The first symbol is the start oval, which merely marks the beginning of the flowchart. The next symbol is a parallelogram that gets the first sales amount from the user. This symbol represents the priming read. Figure 7-8 shows the first sales amount recorded in the desk-check table.

| bonus rate | sales | bonus |
| --- | --- | --- |
| .05 | 10000 | |

**Figure 7-8** First sales amount recorded in the desk-check table

The next symbol in the flowchart is a diamond that represents the condition in a pretest loop. You can tell that the loop is a pretest loop (rather than a posttest loop), because the diamond appears before the true and false path. The loop's condition tells the computer to compare the sales amount entered by the user with the sentinel value, which is the number -1. In this case, the condition evaluates to true, because 10000 is not equal to -1. When the condition evaluates to true, the computer processes the instructions in the loop body to calculate and display the bonus amount. Figure 7-9 shows the first salesperson's bonus information recorded in the desk-check table. The bonus agrees with your manually calculated results.

| bonus rate | sales | bonus |
| --- | --- | --- |
| .05 | 10000 | 500 |

**Figure 7-9** First salesperson's bonus information recorded in the desk-check table

The last instruction in the loop body in Figure 7-6 is contained in a parallelogram. The instruction gets the next salesperson's sales—in this case, 25000—from the user. Recall that this instruction is read. After the user enters the sales amount, the condition is reevaluated to determine whether the loop should be processed again (a true condition) or end (a false condition). Recall that the condition is contained in the diamond located at the top of the loop. In this case, the condition evaluates to true because 25000 is not equal to -1. As a result, the bonus amount is calculated and then displayed on the screen. Figure 7-10 shows the second salesperson's information recorded in the desk-check table.

220

# The while Statement

| bonus rate | sales | bonus |
| --- | --- | --- |
| .05 | 25000 | 1250 |

Figure 7-10 Second salesperson's information recorded in the desk-check table

The last parallelogram in the loop body gets the salesperson's sales among the user. In this case, the user enters the sentinel value (-1) as the sales. The loop's condition is reevaluated to determine whether the loop should be processed again (a true condition) or end (a false condition). In this case, the condition evaluates to false, because the amount entered by the user is -1. When the loop's condition evaluates to false, the computer skips over the loop body instructions and processes the instruction immediately following the end of the loop. In Figure 7-6's flowchart, the stop follows the loop and marks the end of the flowchart. The completed desk-check table is shown in Figure 7-11.

![](img/d64a28a68f49d61137bf2f3170ac40ad_241_0.png)

| bonus rate | sales | bonus |
| --- | --- | --- |
| .05 | 25000 | 1250 |

Figure 7-11 Completed desk-check table

You can code a potest in C++ using either the while statement or the for statement. First, you will learn how to use the while statement. The for statement is covered later in the chapter.

# The while Statement

Figure 7-12 shows the syntax of the while statement, which you can use to code a potest loop in a C++ program. The boldfaced text indicates that the parentheses surround the condition are essential components of the statement. The keyword while and the italicized items in the syntax indicate that the programmer must supply information. In this case, the programmer must supply the loop condition. The condition must be a Boolean expression, which is an expression that evaluates to true or false. The expression can contain variables, constants, functions, arithmetic operators, comparison operators, and logical operators. Besides the condition, the programmer must also provide the loop body statements, which are executed. If more than one statement needs to be processed, the statements must be entered as a block enclosing them in a set of braces {}. You can also enter the braces when a loop body contains only one statement. By doing this, you won't need to remember to enter the braces when statements are added subsequently to the loop body. Forgetting to enter the braces is a common error when making the while statement in a program. Although not a requirement, it is a good programming practice to use a comment such as //end while to mark the end of the while statement. The comment will make your program easier to read and understand. Also included in Figure 7-12 are examples of using the while statement. In Example 1, the while (age > 0) tells the computer to repeat

# CHAPTER 7 The Repetition Structure

loop body instructions as long as (or while) the value in the age variable is greater than zero. The loop will stop when the user enters the number 0 or a negative number. In Example 2, the while (makeEntry == 'Y' || makeEntry == 'y') indicates that the loop body instructions should be repeated as long as the value in the makeEntry variable is either upper-case Y or the lowercase y. In this case, the loop will stop when the user enters anything other than the Y or y. You could also write the while clause as either while (toupper(makeEntry) == 'Y') or while (tolower(makeEntry) == 'y').

HOW TO Use the while Statement

Syntax
while (condition)

either one statement or a block to be processed as long as the condition is true
//end while

Example 1

```int age = 0;
cout << "Enter age: ";
cin >> age;
while (age > 0)
```

```
cout << "You entered " << age << endl;
cout << "Enter age: ";
cin >> age;
//end while
```

Example 2

```
char makeEntry = ' ';
double sales = 0.0;
```

```
cout << "Enter a sales amount? (Y/N)";
cin >> makeEntry;
while (makeEntry == 'Y' || makeEntry == 'y')
```

```

cout << "Enter the sales: ";
cin >> sales;
cout << "You entered " << sales << endl;
cout << "Enter a sales amount? (Y/N)";
cin >> makeEntry;
//end while
```

Figure 7-12 How to use the while statement

Figure 7-13 shows the IPO chart and corresponding C++ instructions for the Miller Incorporated program. The first three statements in Figure 7-13 declare and initialize the RATE named and the sales and bonus variables. The cout <<First sales amount (-1 to stop):" prompts the user to enter the first sales, and the cin >> sales; stores the user's response in the

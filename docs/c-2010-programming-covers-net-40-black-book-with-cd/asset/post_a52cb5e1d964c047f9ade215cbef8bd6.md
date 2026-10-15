
- **condition** – Specifies an expression that is checked before starting any new iteration of the loop. It must evaluate to true for another iteration to be executed.
- **loop expression** – Specifies an expression that is evaluated after ending each iteration of the loop. You can use it for either incrementing or decrementing the loop counter.

The following code snippet shows the use of the `for` loop:

```
for (int Number = 1; Number <= 50; Number++) {
    Console.WriteLine("I will be executed 50 times");
}
```

In the preceding code snippet, the Number variable is initialized to 1. The loop iterates as long as the value of the Number variable is less than or equal to 50. After each iteration, the value of the Number variable increments by 1 and the statement inside the for loop executes as long as the specified condition inside the for loop is true.

## The foreach Loop

The foreach loop iterates through all the items in a list. The list may be an array or a collection of objects. The foreach loop works same as the for loop. The syntax of the foreach loop is as follows:

```
foreach(<data_type> <variable_name> in <array_name>) {
    ...       //statements
}
```

The description of the terms used in the syntax is as follows:

- **data_type** – Specifies data type of a variable. The data type of the variable and array must be same.
- **variable_name** – Represents the variable name that act as a representative for each value of item in the array_name array.
- **in** – Denotes a keyword that is applied after the variable_name variable.
- **array_name** – Represents the name of an array or a collection of objects, which you are accessing.

The following code snippet shows the use of the foreach loop:

```
string[] bookTitles = new string[] { "Alice in Wonderland",
"Pelican Brief",
"Ignited Minds" };
foreach (string i in bookTitles)
{
    ...       //statements
}
```

In the preceding code snippet, an array of string type with the name bookTitles is defined and the foreach loop is used to iterate the items of the bookTitles array.

In case, there exist one or more loops inside a loop then it is known as nested loops. For example, if a for loop is inside another for loop or do...while loop, the it is known as nested loops. You can also create an infinite loop if you do not want to terminate the loop. In an infinite loop, an unrealistic terminating condition is given, which is never met.

## Jump Statements

Jump statements are the statements that allow you to move the program control from one point to another, at any particular instance during execution of the program. In C#, there are five types of jump statements, which are as follows:

- **goto statement** – Transfers the program control directly to a labeled statement. The statement or block of statements that have been given some name or label is known as labeled statement.
- **break statement** – Terminates the loop in which it appears. Therefore, the program control is transferred to the statement that follows the break statement.
- **continue statement** – Transfers the program control to the next iteration of in which the continue keyword appears.
- **return statement** — Terminates the execution of the method in which it appears and returns control to the calling method.
- **throw statement** — Specifies the occurrence of an exception during a program execution.

Let’s discuss the important jump statements in detail.

## The goto Statement

The goto statement is used to transfer the program control to a statement that has the same label as that of the goto statement. The statement having the same label is known as the labeled statement. More than one goto statements can transfer the program control to the same labeled statement. The goto statement can transfer the program control outside a control statement; however, it cannot transfer the program control inside the control statement, such as the while loop, the do...while loop, and the for loop. Generally, the use of goto statements is not recommended as it increases the complexity of the program execution. However, they can be used in switch statements or when you want to transfer the program control outside a nested loop. The following code snippet shows an example of the goto statement:

```
if(Number1>Number2)
{
    if(Number1>Number3)
    {
        goto MyLabel; // label
    }
}
MyLabel: //labeled statement
{
    Console.WriteLine("Number1 is greater than Number2");
    ...//Statements
}
```

In the preceding code snippet, you can see that the goto statement (goto MyLabel;) inside the nested if statements transfers the program control to a labeled statement (MyLabel:).

## The break Statement

The break statement terminates the loop in which it exists. It can also alter the flow of a loop. After exiting the loop, the program control is transferred to the next block of statements following the loop. You can use the break statement to exit from a case in a switch statement or control statements, such as for, foreach, while, or do...while loop. The following code snippet shows the use of the break statement:

```
{
    int number;
    for (number = 1; number <= 10; number++)
    {
        Console.WriteLine(number);
        if (number>=5)
            break; //break statement
    }
    Console.WriteLine("Press ENTER to quit...");
    Console.ReadLine();
}
```

In the preceding code snippet, you can see that value of the number variable is required to be printed till the condition, number<=10, specified in the for loop is true. However, in the for loop, we have used the if statement in which we have specified the condition that when the value of the number variable becomes equal to or greater than 5, then the loop should be terminated. This is done by using the break statement inside the if statement.

The output of the preceding code snippet is shown as follows:

![](img/e073a4882197be4ab61103cbe0bcb394_156_0.png)

Figure 3.1: Showing the Output of the break Statement

## The continue Statement

The continue statement starts a new iteration of the enclosing loop in which it exists. This statement can exist in different kinds of loop statements, such as while, do..while, for, or foreach loop. The continue statement executes the statements following it when a certain condition is not fulfilled. This statement must be enclosed within a loop; otherwise, a compile time error occurs. The following code snippet shows how to use the continue statement:

```
{
    int number;
    for (number = 1; number <= 10; number++)
    {
        if (number<=5)
            continue;
        Console.WriteLine(number);
    }
    Console.WriteLine("Press ENTER to quit...");
    Console.ReadLine();
}
```

In the preceding code snippet, the continue statement inside the if statement transfers the program control at the beginning of the for loop and does not execute the next statement as long as the value of number variable is less than or equal to 5. Whenever the value of number variable becomes greater than 5, the next statement following the continue statement is executed.

The output of the preceding code snippet is as follows:

![](img/e073a4882197be4ab61103cbe0bcb394_157_0.png)

After learning about the control flow statements, let’s learn about exception handling.

## Exception Handling

Exception is a runtime error that arises because of some abnormal conditions, such as division of a number by zero, passing a string to a variable that holds an integer value. Capturing and handling of runtime errors is one of the important and crucial tasks for any programmer; but before we discuss runtime errors, let’s take a look at compile time errors. Compile time errors are those errors that occur during compilation of a program. It can happen due to bad coding or incorrect syntax. You can correct these compile time errors after looking at the error message that the compiler generates. On the other hand, runtime errors are those errors that occur during the execution of a program and thus at that time they cannot be corrected. So, necessary actions need to be taken beforehand to prevent such types of errors. To do so, you should first identify the following two aspects:

- Find out those parts of a program which can cause runtime errors
- How to handle those errors, when they occur

Table 3.1 describes some common exception classes:

| Exception Class | Description |
|---|---|
| SystemException | Represents a base class for other exception classes |
| AccessException | Occurs when a type member, such as a variable, cannot be accessed |

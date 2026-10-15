# The continue Statement

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

![](bbox=[0.32, 0.56, 0.72, 0.68])

After learning about the control flow statements, let’s learn about exception handling.

# Exception Handling

Exception is a runtime error that arises because of some abnormal conditions, such as division of a number by zero, passing a string to a variable that holds an integer value. Capturing and handling of runtime errors is one of the important and crucial tasks for any programmer; but before we discuss runtime errors, let’s take a look at compile time errors. Compile time errors are those errors that occur during compilation of a program. It can happen due to bad coding or incorrect syntax. You can correct these compile time errors after looking at the error message that the compiler generates. On the other hand, runtime errors are those errors that occur during the execution of a program and thus at that time they cannot be corrected. So, necessary actions need to be taken beforehand to prevent such types of errors. To do so, you should first identify the following two aspects:

+   - Find out those parts of a program which can cause runtime errors
+   - How to handle those errors, when they occur

Table 3.1 describes some common exception classes:

| Table 3.1: Noteworthy Exception Classes |
| Exception Class | Description |
| SystemException | Represents a base class for other exception classes |
| AccessException | Occurs when a type member, such as a variable, cannot be accessed |
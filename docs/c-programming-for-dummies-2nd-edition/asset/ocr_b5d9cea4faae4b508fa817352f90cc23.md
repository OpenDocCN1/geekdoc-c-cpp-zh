Exercise 9-1: Create a new program using the source code from Listing 9-1. Type everything carefully, especially Line 7. Build and run.

As output, the program coughs up the tongue-twister Sore shoulder surgery ten times, in ten lines of text. The key, of course, is in Line 7, the for statement. That statement directs the program to repeat the statement(s) in curly brackets a total of ten times.

Exercise 9-2: Using the source code from Listing 9-1 again, replace the value 10 in Line 7 with the value 20. Build and run.

# Introducing the for loop

The for loop is usually the first type of loop you encounter when you learn to program. It looks complex, but that's because it's doing everything required of a loop in a single statement:

```
for(initialization; exit_condition; repeat_each)
```

Here's how it works:

initialization is a C language expression that's evaluated at the start of the loop. Most often, it's where the variable that counts the loop's iterations is initialized.

exit_condition is the test upon which the loop stops. In a for loop, the statements continue to repeat until the exit condition is true. The expression used for the exit_condition is most often a comparison, like something you'd find in an if statement.

repeat_each is an expression that's executed once every iteration. It's normally an operation affecting the initialization variable at the first part of the for statement.

The for statement is followed by a block of one or more statements held in curly brackets:

```
for(x=0; x<10; x=x+1)
{
    puts("Sore shoulder surgery");
}
```
# B.6.1 Debugging Functions and Methods

You should examine the values of the arguments passed to a function or method as at its beginning and end by using either watches or cout statements. Ideally, you should debug each major function or method separately before using it in your program.

# B.6.2 Debugging Loops

You should examine the values of key variables at the beginnings and ends of loops, as the comments in this example indicate:

```
// Check values of start and stop before entering loop
for (index = start; index <= stop; index++)
{
    // Check values of index and key variables
    // at the beginning of iteration
    ...
    // Check values of index and key variables
    // at the end of iteration
}
// End for
// Check values of start and stop after exiting loop
```

# B.6.3 Debugging if Statements

Just before an if statement, you should examine the values of the variables within its expression. You can use either breakpoints or cout statements to determine which branch the if statement takes, as this example indicates:

```
// Check variables within expression before executing if
if (expression)
{
    cout << "Condition is true (value of expression is 1).";
    ...
}
else
{
    cout << "Condition is false (value of expression is 0).";
    ...
}
// end if
```

# B.6.4 Using cout Statements

Sometimes cout statements can be more convenient than watches. Such cout statements should report both the values of key variables and the location in the program at which the variables have those values. You can use a comment to label the location, as follows:

```
// This is point A
cout << "At point A in the method computeResults:\n"
     << "x = " << x << ", y = " << y << endl;
```

Remember to either disable or remove these statements when your program finally works.

# B.6.5 Using Special Dump Functions

Often the variables whose values you wish to examine are arrays or other, more complex data structures. If so, you should write dump functions to display the data structures in a highly readable manner. You can easily move the single statement that calls each dump function from one point in the
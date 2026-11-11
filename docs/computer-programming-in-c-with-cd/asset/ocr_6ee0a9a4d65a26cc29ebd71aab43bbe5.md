```
    void main()
    {
    int amt;
    cout<<"Enter amount: ";
    cin>>amt;
    cout<<"You have entered "<<dollar<<amt;
    }

    Output:

    Enter amount: 1000
    You have entered $ 1000
```

> > Write short note on Manipulators (Mumbai University, December 2008)

Now, let's see how conditional statements are used to check conditions in a program.

# ## 2.2 Working with Conditional Statements

A conditional statement is a control statement that allows you to choose between two or more execution paths in a program. Conditional statements cause a program to execute a block of code after evaluating a given conditional expression. If the conditional expression comes out to be true, the accompanying block of code is executed; otherwise, the block of code is bypassed. The following is the list of the conditional statements supported by C++:

+   - if statement
+   - if-else statement
+   - Nested if statements
+   - if-else ladders
+   - switch statement
+   - Nested switch statement

Let’s now discuss these statements in detail.

# ### Using the if Statement

The `if` statement executes code depending on whether or not an expression is true or false. The code following the conditional expression is executed only if the expression in the `if` statement is evaluated to be true; otherwise, the program control passes to the next statement.

The following is the syntax of the `if` statement:
Typical output from this program is:

```
Enter an integer less than 2 billion: 123456
Your number is even,
```

# How It Works

After reading the input value into number, the value is tested by taking the remainder after division by two (using the remainder operator % that you saw in the last chapter) and using that as the condition for the if. In this case, the condition of the if statement returns an integer, not a Boolean. The if statement interprets a non-zero value returned by the condition as true, and interprets zero as false. In other words, the condition expression for the if statement:

```
(number % 2L)
```

is equivalent to

```
(number % 2L != 0)
```

If the remainder is 1, the condition is true, and the statement immediately following the if is executed. If the remainder is 0, the condition is false, and the statement following the else keyword is executed.

> In an if statement, the condition can be an expression that results in a value of any of the fundamental data types that you saw in Chapter 2. When the condition expression evaluates to a numerical value rather than the bool value required by the if statement, the compiler inserts an automatic cast of the result of the expression to type bool. A non-zero value that is cast to type bool results in true, and a zero value results in false.

Because the remainder from the division of an integer by two can only be one or zero, I have commented the code to indicate this fact. After either outcome, the return statement is executed to end the program.

> The else keyword is written without a semicolon, similar to the if part of the statement. Again, indentation is used as a visible indicator of the relationship between various statements. You can clearly see which statement is executed for a true or non-zero result, and which for a false or zero result. You should always indent the statements in your programs to show their logical structure.

The if-else combination provides a choice between two options. The general logic of the if-else is shown in Figure 3-2.
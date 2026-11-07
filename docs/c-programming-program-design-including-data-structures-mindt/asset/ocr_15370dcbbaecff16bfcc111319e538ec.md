```
Your guess is lower than the number.
Guess again!
Enter an integer greater than or equal to 0 and less than 100: 35

Your guess is higher than the number.
Guess again!
Enter an integer greater than or equal to 0 and less than 100: 28

Your guess is lower than the number.
Guess again!
Enter an integer greater than or equal to 0 and less than 100: 32

You guessed the correct number.
```

The preceding program works as follows: The statement in Line 12 creates an integer greater than or equal to 0 and less than 100 and stores this number in the variable `num`. The statement in Line 13 sets the bool variable `isGuessed` to `false`. The expression in the `while` loop at Line 14 evaluates the expression `!isGuessed`. If `isGuessed` is `false`, then `!isGuessed` is `true` and the body of the `while` loop executes; if `isGuessed` is `true`, then `!isGuessed` is `false`, so the `while` loop terminates. We could also have used `isGuessed == false` as the test expression, but `!isGuessed` does the same thing and is shorter.

The statement in Line 16 prompts the user to enter an integer greater than or equal to 0 and less than 100. The statement in Line 17 stores the number entered by the user in the variable `guess`. The expression in the `if` statement in Line 19 determines whether the value of `guess` is the same as `num`, that is, if the user guessed the number correctly. If the value of `guess` is the same as `num`, the statement in Line 21 outputs the message:

```
You guessed the correct number.
```

The statement in Line 22 sets the variable `isGuessed` to `true`. The control then goes back to Line 13. If the expression in Line 19 evaluates to `false`, then the `else` statement in Line 24 determines whether the value of `guess` is less than or greater than `num` and outputs the appropriate message.

# Case 4: EOF-Controlled while Loops

If the data file is frequently altered (for example, if data is frequently added or deleted), it’s best not to read the data with a sentinel value. Someone might accidentally erase the sentinel value or add data past the sentinel, especially if the programmer and the data entry person are different people. Also, it can be difficult at times to select a good sentinel value. In such situations, you can use an end-of-file (EOF)-controlled `while` loop.

Until now, we have used an input stream variable, such as `cin`, and the extraction operator, `>>`, to read and store data into variables. However, the input stream variable can also return a value after reading data, as follows:
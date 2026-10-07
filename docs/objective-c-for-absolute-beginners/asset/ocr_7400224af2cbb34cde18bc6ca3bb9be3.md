# CHAPTER 4: Making Decisions About...and Planning Flow

randomNumber = (arc4random() % 101);

This line will produce a random number between 0 and 100; arc4random() is a function that returns a random number. Although this will not generate a truly random number, it will work for this example.

The modulus operator is called %. In this case, it's the remainder of its two operands; in this case, arc4random() divided by 101.

The next line of code is scanc("%i", &userGuess);

The function scanf reads the value from the keyboard and stores it in userGuess.

> NOTE: The source code for this Objective-C project is available for download at forum.xcel.com. Additionally, there is a short video explaining the source code and the project.

# Nested If Statements and Else-If Statements

Sometimes, it is necessary to nest statements. This means that you need to have statements nested inside an existing statement. Additionally, it is sometimes necessary to have a comparison as the first step in the section of the if statement. This is called else-if statement (recall line 38 in Line 4–9).

```
else if (userGuess > randomNumber)
```

# Removing Extra Characters

Line 31 is another new line of code. fgetc(stdin); //remove CR/LF extra character

The function scanf can be difficult to work with. In this case, scanf leaves a remnant in your input buffer that needs to be flushed, so you can read a Y or N from the keyboard to determine if the user wants to play again.

# Improving the Code Through Refactoring

Often, after you get your code to work, you examine the code and find more efficient ways to write it. The process of rewriting your code to make it more efficient, maintainable, and readable is code refactoring.

As you were reviewing your code in Objective-C, you noticed that you could eliminate unnecessary code. Your code had the following line repeated in the if-else statement:
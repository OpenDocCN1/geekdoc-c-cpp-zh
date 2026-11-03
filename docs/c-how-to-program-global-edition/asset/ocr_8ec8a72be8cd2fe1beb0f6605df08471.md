g) Print the message "This is a C program." with each word on a separate line.
h) Print the message "This is a C program." with the words separated by tabs.

# 2.4 Write a statement (or comment) to accomplish each of the following:

+   a) State that a program will calculate the product of three integers.
+   b) Prompt the user to enter three integers.
+   c) Define the variables x, y and z to be of type int.
+   d) Read three integers from the keyboard and store them in the variables x, y and z.
+   e) Define the variable result, compute the product of the integers in the variables x, y and z, and use that product to initialize the variable result.
+   f) Print "The product is" followed by the value of the integer variable result.

2.5 Using the statements you wrote in Exercise 2.4, write a complete program that calculates the product of three integers.

# 2.6 Identify and correct the errors in each of the following statements:

```
a) printf( "The value is %d\n", &number );
b) scanf( "%d%d", &number1, number2 );
c) if ( c < 7 ) {
    printf( "c is less than 7\n" );
}
d) if ( c >= 7 ) {
    printf( "c is greater than or equal to 7\n" );
}
```

# Answers to Self-Review Exercises

2.1 a) main. b) left brace ({), right brace (}). c) semicolon. d) printf. e) newline. f) scanf. g) %d. h) destructive. i) nondestructive. j) if.

2.2 a) False. Function printf always begins printing where the cursor is positioned, and this may be anywhere on a line of the screen.
b) False. Comments do not cause any action to be performed when the program is executed. They're used to document programs and improve their readability.
c) True.
d) True.
e) True.
f) False. C is case sensitive, so these variables are unique.
g) True.
h) False. Arguments in a printf function ordinarily should not be preceded by an ampersand. Arguments following the format control string in a scanf function ordinarily should be preceded by an ampersand. We'll discuss exceptions to these rules in Chapter 6 and Chapter 7.
i) True.
j) False. The operators *, / and % are on the same level of precedence, and the operators + and - are on a lower level of precedence.
k) False. A printf statement with multiple \n escape sequences can print several lines.

2.3 a) int c, thisVariable, q76354, number;
b) printf( "Enter an integer: " );
c) scanf( "%d", &a );
d) if ( number != 7 ) {
    printf( "The variable number is not equal to 7.\n" );
}
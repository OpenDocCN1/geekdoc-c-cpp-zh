(which can appear anywhere in the program) sets intptr pointing to an array of 100 integers, whose 3 elements are initialized as specified.

If the size of the array is not specified, the initializer list determines it.

# The goto Statement

Executing a goto statement causes a direct branch to be made to a specified point in the program. To identify where in the program the branch is to be made, a label is named with the same rules as variable names; it must be immediately followed by a colon. The label is placed directly before the statement to which the branch is to be made and must appear in the same function or method as the goto.

For example, the statement

```
goto out_of_data;
```

causes the program to branch immediately to the statement that is preceded by the label out_of_data. This label can be located anywhere in the function or method, or after the goto, and may be used as here:

```
out_of_data: NSLog ("Unexpected end of data.");
```

...

Lazy programmers frequently abuse the goto statement to branch to other portions of their code. The goto statement interrupts the normal sequential flow of a program. As a result, programs are harder to follow. Using many gotos in a program can make it impossible to decipher. For this reason, goto statements are not considered part of good programming style.

# The null Statement

Objective-C permits you to place a solitary semicolon wherever a normal program statement can appear. The effect of such a statement, called the null statement, is that nothing is done. This might seem useless, but programmers do this in while, for, and do statements. For example, the purpose of the following statement is to store all the characters read from standard input (your terminal, by default) in the character array until a null character is encountered. This statement uses the library getchar, which reads and returns a single character at a time from standard input:

```
while (text++ != getchar()) {
```

All the operations are performed inside the looping conditions part of the while statement. The null statement is needed because the compiler takes the statement that follows the looping expression as the body of the loop. Without the null statement, the compiler would treat whatever statement follows in the program as the body of the program loop.
# Loop with Test at the Beginning

For a loop that tests at the beginning, you can use a while loop in C++, C#, Java, Visual Basic, and most other languages. You can emulate a while loop in other languages.

# Loop with Test at the End

You might occasionally have a situation in which you want a flexible loop, but the loop needs to execute at least one time. In such a case, you can use a while loop that is tested at its end. You can use do-while in C++, C#, and Java, Do-Loop-While in Visual Basic, or you can emulate end-tested loops in other languages.

# When to Use a Loop-With-Exit Loop

A loop-with-exit loop is a loop in which the exit condition appears in the middle of the loop rather than at the beginning or at the end. The loop-with-exit loop is available explicitly in Visual Basic, and you can emulate it with the structured constructs while and break in C++, C, and Java or with gotos in other languages.

# Normal Loop-With-Exit Loops

A loop-with-exit loop usually consists of the loop beginning, the loop body (including an exit condition), and the loop end, as in this Visual Basic example:

```
Visual Basic Example of a Generic Loop-With-Exit Loop
Do
    ...
    If ( some exit condition ) Then Exit Do
    ...
Loop
Statements.
More statements.
```

The typical use of a loop-with-exit loop is for the case in which testing at the beginning or at the end of the loop requires coding a loop-and-a-half. Here’s a C++ example of a case that warrants a loop-with-exit loop but doesn’t use one:

```
C++ Example of Duplicated Code That Will Break Down Under Maintenance
// Compute scores and ratings.
score = 0;
GetNextRating( &ratingIncrement );
rating = rating + ratingIncrement;
while ( ( score < targetScore ) && ( ratingIncrement != 0 ) ) {
    GetNextScore( &scoreIncrement );
    score = score + scoreIncrement;
    GetNextRating( &ratingIncrement );
    rating = rating + ratingIncrement;
}
These lines appear here...
...and are repeated here.
```
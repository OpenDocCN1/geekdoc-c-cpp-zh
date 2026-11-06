braces leads to errors. To avoid errors, as a rule, always enclose an `if` statement’s body statement(s) in braces.

![](bbox=[0.119, 0.241, 0.191, 0.297])

# Common Programming Error 2.5

Placing a semicolon immediately after the right parenthesis after the condition in an `if` statement is often a logic error (although not a syntax error). The semicolon causes the body of the `if` statement to be empty, so the `if` statement performs no action, regardless of whether or not its condition is true. Worse yet, the original body statement of the `if` statement now becomes a statement in sequence with the `if` statement and always executes, often causing the program to produce incorrect results.

# White Space

Note our use of blank lines in Fig. 2.13. We inserted these for readability. Recall that white-space characters, such as tabs, newlines and spaces, are normally ignored by the compiler. So, statements may be split over several lines and may be spaced according to your preferences. It’s a syntax error to split identifiers, strings (such as `"hello"`) and constants (such as the number `1000`) over several lines.
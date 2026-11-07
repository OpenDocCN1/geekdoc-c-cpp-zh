# Indentation in the if Statement

The indentation in the if statement's second line is optional but highly recommended. It emphasizes the inherent structure of structured programs. The compiler ignores white-space characters such as blanks, tabs and newlines used for indentation and vertical spacing.

# if Statement Flowchart

The following flowchart segment illustrates the single-selection if statement:

![](bbox=[0.282, 0.247, 0.667, 0.428])

It contains perhaps the most important flowchart symbol—the diamond (or decision) symbol, which indicates a decision is to be made. The decision symbol's expression typically is a condition that can be *true* or *false*. The two flowlines emerging from it indicate the paths to take when the expression is *true* or *false*. Decisions can be based on any expression's value—zero is *false*, and nonzero is *true*.

The if statement is a single-entry/single-exit statement. We'll soon learn that the flowchart segment for the remaining control structures also can contain rectangle symbols to indicate the actions to be performed and diamond symbols to indicate decisions to be made. This is the action/decision model of programming we've been emphasizing.

# ✓ Self Check

+   1. *(Multiple Choice)* Which of the following statements is false?

+   a) The pseudocode statement

```
~~~
If student's grade is greater than or equal to 60
    Print "Passed"
~~~
```

can be written in C as

```
~~~c
if (grade >= 60) {
    puts("Passed");
} // end if
~~~
```

+   b) The two flowlines emerging from the decision flowchart symbol indicate the directions to take when the expression in the symbol is *true* or *false*.

+   c) Decisions can be based on any expression—if the expression evaluates to nonzero, it's treated as *false*, and if it evaluates to zero, it's treated as *true*.

+   d) The if statement is a single-entry/single-exit statement.

Answer: c) is false. Actually, decisions can be based on any expression—if the expression evaluates to zero, it's treated as *false*, and if it evaluates to nonzero, it's treated as *true*.
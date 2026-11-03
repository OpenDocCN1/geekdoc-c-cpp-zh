would be outside the body of the else part of the if and would execute regardless of whether the grade was less than 60, so even a passing student would have to take the course again!

> **Error-Prevention Tip 3.2**
> Always include your control statements' bodies in braces ({ and }), even if those bodies contain only a single statement. This solves the "dangling-else" problem, which we discuss in Exercises 3.30–3.31.

A syntax error is caught by the compiler. A logic error has its effect at execution time. A fatal logic error causes a program to fail and terminate prematurely. A nonfatal logic error allows a program to continue executing but to produce incorrect results.

Just as a compound statement can be placed anywhere a single statement can be placed, it's also possible to have no statement at all, i.e., the empty statement. The empty statement is represented by placing a semicolon (;) where a statement would normally be.

> **Common Programming Error 3.1**
> Placing a semicolon after the condition in an if statement as in if ( grade >= 60 ); leads to a logic error in single-selection if statements and a syntax error in double-selection if statements.

> **Error-Prevention Tip 3.3**
> Typing the beginning and ending braces of compound statements before typing the individual statements within the braces helps avoid omitting one or both of the braces, preventing syntax errors and logic errors (where both braces are indeed required).

# 3.7 The while Iteration Statement

An iteration statement (also called an repetition statement or loop) allows you to specify that an action is to be repeated while some condition remains true. The pseudocode statement

*While there are more items on my shopping list*
*Purchase next item and cross it off my list*

describes the iteration that occurs during a shopping trip. The condition, "there are more items on my shopping list" may be true or false. If it's true, then the action, "Purchase next item and cross it off my list" is performed. This action will be performed repeatedly while the condition remains true. The statement(s) contained in the while iteration statement constitute the body of the while. The while statement body may be a single statement or a compound statement. Eventually, the condition will become false (when the last item on the shopping list has been purchased and crossed off the list). At this point, the iteration terminates, and the first pseudocode statement after the iteration structure is executed.

> **Common Programming Error 3.2**
> Not providing in the body of a while statement an action that eventually causes the condition in the while to become false. Normally, such an iteration structure will never terminate—an error called an "infinite loop."
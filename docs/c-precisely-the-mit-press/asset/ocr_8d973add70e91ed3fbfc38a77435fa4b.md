# 13.7 Returns, Labeled Statements, Exits, and Jumps

# 13.7.1 The return Statement

The simplest form of a return statement, without an expression argument, is this:

return;

This form of return statement may occur in the body of a method or anonymous delegate whose re-type is void, in the body of a constructor, or in a set-accessor of a property or indexer, but not in an operator or in the get-accessor of a property or indexer. Execution of the return statement exits the method and continues execution at the place from which it was called.

Alternatively, a return statement may have an expression argument:

return expression;

This form of return statement may occur inside the body of a method or anonymous delegate whose type is non-void, in the get-accessor of a property or indexer, or in an operator, but not in the set-accessor of a property or indexer. The type of the expression must be implicitly convertible to the return type of the enclosing function. The return statement is executed as follows. First the expression is evaluated to some value v. Then it exits and continues execution at the method call expression that the method; the value of that expression will be v.

See 13.8.2 for execution of a return statement inside a try statement with an associated finally block.

# 13.7.2 The break Statement

A break statement is legal only inside a switch or loop; it has the form

break;

Executing break exits the innermost enclosing loop and continues execution after that switch or loop. A break statement is not allowed to exit a finally block.

See 13.8.2 for execution of a break statement inside a try statement with an associated finally block.

# 13.7.3 The continue Statement

A continue statement is legal only inside a loop; it has the form

continue;

Executing continue terminates the current iteration of the innermost enclosing loop, and continues the execution at the step (in for loops; see section 13.6.1) or with the next element (in foreach loops; see section 13.6.2) or the condition (in while and do-while loops; see sections 13.6.3 and 13.6.4).

A continue statement is not allowed to exit a finally block.

See 13.8.2 for execution of a continue statement inside a try statement with an associated finally block.
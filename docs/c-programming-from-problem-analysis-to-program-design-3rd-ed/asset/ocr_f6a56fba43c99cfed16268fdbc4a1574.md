+   11. With short-circuit evaluation, as soon as the value of the entire expression is known, the common language runtime (CLR) stops evaluating the expression. For complex expressions using &&, when the first part of the expression evaluates to false, there is no need to evaluate the second.
+   12. In C#, there is no conversion between the bool type and other types; thus, when x is defined as int, you cannot type if (x).
+   13. Do not place a semicolon at the end of the if statement’s parenthesized expression being evaluated. This makes a null (empty) statement, but does not create a syntax error.
+   14. With a two-way if statement, either the true statement(s) is executed or the false statement(s), but not both. After the execution of the statement(s) is (are) finished, control always transfers to the statements following the if block.
+   15. Any statement, including another if statement, can be included within the statements to be executed when the expression evaluates to true. The same holds for the false statements.
+   16. When determining which else matches which if, follow this rule: The else matches up with the closest previous if that does not already have an attached else.
+   17. Use a series of else...if for a long, nested, multiway statement.
+   18. The switch statement is considered a multiple selection structure that allows a large number of alternatives to be executed. The switch is used for equality comparisons only.
+   19. The case value with a switch statement must be a constant literal of the same type as the expression. It cannot be a variable.
+   20. With a switch statement, the occurrence of the first case value that matches the expression causes that case’s statement(s) to be executed. If no match is made with any of the case values, the statements associated with default are executed.
+   21. Having a default is not required, but it is a good idea always to include one.
+   22. There is no way to program a switch statement in C# to fall through to the code for the next case. After code is associated with a case, there must be a break. If used, the default statements must also end with a break.
+   23. Multiple cases in a switch statement can be associated with the same statements. This works like having a logical OR operator between each of the cases.
+   24. The switch statement cannot be used to test for a range of values, or to perform a relational test.
+   25. Also called the conditional operator, the ternary operator ? : provides a shorthand way to express a simple if...else selection statement.
+   26. When an expression contains multiple operators, the precedence of the operators controls the order in which the individual operators are evaluated.
+   27. Equality operators have a lower precedence than relational operators; && has a higher precedence than ||, but both && and || have lower precedence than the relational or equality operators. The very lowest precedence is the assignment operators.
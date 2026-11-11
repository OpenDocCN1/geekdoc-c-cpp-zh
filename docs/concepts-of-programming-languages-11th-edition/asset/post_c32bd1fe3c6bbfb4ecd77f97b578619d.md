
which is an easily made mistake, it is not detectable as an error by the compiler. Rather than testing a relational expression, the value that is assigned to *x* is tested (in this case, it is the value of *y* that reaches this statement). This is actually a result of two design decisions: allowing assignment to behave like an ordinary binary operator and using two very similar operators, `==` and `=`, to have completely different meanings. This is another example of the safety deficiencies of C and C++ programs. Note that Java and C# allow only boolean expressions in their `if` statements, disallowing this problem.

## history note

The PDP-11 computer, on which C was first implemented, has autoincrement and autodecrement addressing modes, which are hardware versions of the increment and decrement operators of C when they are used as array indices. One might guess from this that the design of these C operators was based on the design of the PDP-11 architecture. That guess would be wrong, however, because the C operators were inherited from the B language, which was designed before the first PDP-11.

### 7.7.6 Multiple Assignments

Several recent programming languages, including Perl, Ruby, and Lua, provide multiple-target, multiple-source assignment statements. For example, in Perl one can write

```
($first, $second, $third) = (20, 40, 60);
```

The semantics are that 20 is assigned to `$first`, 40 is assigned to `$second`, and 60 is assigned to `$third`. If the values of two variables must be interchanged, this can be done with a single assignment, as with

```
($first, $second) = ($second, $first);
```

This correctly interchanges the values of `$first` and `$second`, without the use of a temporary variable (at least one created and managed by the programmer).

The syntax of the simplest of Ruby’s multiple assignment is similar to that of Perl, except the left and right sides are not parenthesized. Also, Ruby includes a few more elaborate versions of multiple assignments, which are not discussed here.

### 7.7.7 Assignment in Functional Programming Languages

All of the identifiers used in pure functional languages and some of them used in other functional languages are just names of values. As such, their values never change. For example, in ML, names are bound to values with the `val` declaration, whose form is exemplified in the following:

```
val cost = quantity * price;
```

If cost appears on the left side of a subsequent `val` declaration, that declaration creates a new version of the name cost, which has no relationship with the previous version, which is then hidden.

F# has a somewhat similar declaration that uses the `let` reserved word. The difference between F#’s `let` and ML’s `val` is that `let` creates a new scope, whereas `val` does not. In fact, `val` declarations are often nested in `let` constructs in ML. `let` and `val` are further discussed in Chapter 15.

### 7.8 Mixed-Mode Assignment

Mixed-mode expressions were discussed in Section 7.4.1. Frequently, assignment statements also are mixed mode. The design question is: Does the type of the expression have to be the same as the type of the variable being assigned, or can coercion be used in some cases of type mismatch?

C, C++, and Perl use coercion rules for mixed-mode assignment that are similar to those they use for mixed-mode expressions; that is, many of the possible type mixes are legal, with coercion freely applied.⁷

In a clear departure from C++, Java and C# allow mixed-mode assignment only if the required coercion is widening.⁸ So, an `int` value can be assigned to a `float` variable, but not vice versa. Disallowing half of the possible mixed-mode assignments is a simple but effective way to increase the reliability of Java and C#, relative to C and C++.

Of course, in functional languages, where assignments are just used to name values, there is no such thing as a mixed-mode assignment.

## SUMMARY

Expressions consist of constants, variables, parentheses, function calls, and operators. Assignment statements include target variables, assignment operators, and expressions.

The semantics of an expression is determined in large part by the order of evaluation of operators. The associativity and precedence rules for operators in the expressions of a language determine the order of operator evaluation in those expressions. Operand evaluation order is important if functional side effects are possible. Type conversions can be widening or narrowing. Some narrowing conversions produce erroneous values. Implicit type conversions, or coercions, in expressions are common, although they eliminate the error-detection benefit of type checking, thus lowering reliability.

Assignment statements have appeared in a wide variety of forms, including conditional targets, assigning operators, and list assignments.

7. Note that in Python and Ruby, types are associated with objects, not variables, so there is no such thing as mixed-mode assignment in those languages.

8. Not quite true: If an integer literal, which the compiler by default assigns the type `int`, is assigned to a `char`, `byte`, or `short` variable and the literal is in the range of the type of the variable, the `int` value is coerced to the type of the variable in a narrowing conversion. This narrowing conversion cannot result in an error.

## REVIEW QUESTIONS

-   1. Define operator precedence and operator associativity.
-   2. What is a ternary operator?
-   3. What is a prefix operator?
-   4. What operator usually has right associativity?
-   5. What is a nonassociative operator?
-   6. What associativity rules are used by APL?
-   7. What is the difference between the way operators are implemented in C++ and Ruby?
-   8. Define functional side effect.
-   9. What is a coercion?
-   10. What is a conditional expression?
-   11. What is an overloaded operator?
-   12. Define narrowing and widening conversions.
-   13. In JavaScript, what is the difference between == and ===?
-   14. What is a mixed-mode expression?
-   15. What is referential transparency?
-   16. What are the advantages of referential transparency?
-   17. How does operand evaluation order interact with functional side effects?
-   18. What is short-circuit evaluation?
-   19. Name a language that always does short-circuit evaluation of Boolean expressions. Name one that never does it.
-   20. How does C support relational and Boolean expressions?
-   21. What is the purpose of a compound assignment operator?
-   22. What is the associativity of C's unary arithmetic operators?
-   23. What is one possible disadvantage of treating the assignment operator as if it were an arithmetic operator?
-   24. What two languages include multiple assignments?
-   25. What mixed-mode assignments are allowed in Java?
-   26. What mixed-mode assignments are allowed in ML?
-   27. What is a cast?

## PROBLEM SET

-   1. When might you want the compiler to ignore type differences in an expression?
-   2. State your own arguments for and against allowing mixed-mode arithmetic expressions.
-   3. Do you think the elimination of overloaded operators in your favorite language would be beneficial? Why or why not?
-   4. Would it be a good idea to eliminate all operator precedence rules and require parentheses to show the desired precedence in expressions? Why or why not?
-   5. Should C's assigning operations (for example, +=) be included in other languages (that do not already have them)? Why or why not?
-   6. Should C's single-operand assignment forms (for example, ++count) be included in other languages (that do not already have them)? Why or why not?
-   7. Describe a situation in which the add operator in a programming language would not be commutative.
-   8. Describe a situation in which the add operator in a programming language would not be associative.
-   9. Assume the following rules of associativity and precedence for expressions:

| Precedence | Operators |
| --- | --- |
| Highest | *, /, not |
|  | +, -, &, mod |
|  | - (unary) |
|  | =, /=, <, <=, >=, > |
|  | and |
| Lowest | or, xor |

Associativity: Left to right

Show the order of evaluation of the following expressions by parenthesizing all subexpressions and placing a superscript on the right parenthesis to indicate order. For example, for the expression

a + b * c + d

the order of evaluation would be represented as

((a + (b * c)^1)^2 + d)^3

-   a. a * b - 1 + c
-   b. a * (b - 1) / c mod d
-   c. (a - b) / c & (d * e / a - 3)
-   d. -a or c = d and e
-   e. a > b xor c or d <= 17
-   f. -a + b

-   10. Show the order of evaluation of the expressions of Problem 9, assuming that there are no precedence rules and all operators associate right to left.

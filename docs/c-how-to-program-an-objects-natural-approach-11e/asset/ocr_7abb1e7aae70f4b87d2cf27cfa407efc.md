original value (5) is output, then c’s value is incremented (to 6). Thus, line 10 outputs c’s initial value (5) again. Line 11 outputs c’s new value (6) to prove that the variable’s value was incremented in line 10. Line 16 resets c’s value to 5, and line 17 outputs c’s value. Line 18 outputs the value of the expression ++c. This expression preincrements c, so its value is incremented. Then the new value (6) is output. Line 19 outputs c’s value again to show that c is still 6 after line 18 executes.

# Simplifying Statements with the Arithmetic Compound Assignment, Increment and Decrement Operators

The arithmetic compound assignment operators and the increment and decrement operators can be used to simplify program statements. For example, the three assignment statements in Fig. 3.3 (lines 21, 24 and 28)

```
passes = passes + 1;
failures = failures + 1;
studentCounter = studentCounter + 1;
```

can be written more concisely with compound assignment operators as

```
passes += 1;
failures += 1;
studentCounter += 1;
```

with prefix increment operators as

```
++passes;
++failures;
++studentCounter;
```

or with postfix increment operators as

```
passes++;
failures++;
studentCounter++;
```

When incrementing or decrementing a variable in a statement by itself, the prefix increment and postfix increment forms have the same effect, and the prefix decrement and postfix decrement forms have the same effect. Only when a variable appears in the context of a larger expression does preincrement or postincrement the variable have a different effect (and similarly for predecrement or postdecrement).

Attempting to use the increment or decrement operator on an expression other than one to which a value can be assigned is a compilation error. For example, writing ++(x + 1) is a syntax error, because (x + 1) is not a variable.

# Operator Precedence and Grouping

The following table shows the precedence and grouping of the operators introduced to this point. The operators are shown top-to-bottom in decreasing order of precedence. The second column indicates the grouping of the operators at each level of precedence. Notice that the conditional operator (?:), the unary operators preincrement (++), predecrement (--), plus (+) and minus (-), and the assignment operators +=, -=, *=, /= and %= group right-to-left. All other operators in this table group left-to-right.
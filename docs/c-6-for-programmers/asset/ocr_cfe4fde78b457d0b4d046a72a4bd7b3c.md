Line 18 resets c's value to 5, and line 19 outputs c's value. Line 20 outputs the value of the expression ++c. This expression preincrements c, so its value is incremented; then the new value (6) is output. Line 21 outputs c's value again to show that the value of c is still 6 after line 20 executes.

# 5.1.12 Simplifying Increment Statements

The arithmetic compound assignment operators and the increment and decrement operators can be used to simplify statements. For example, the three assignment statements in Fig. 5.9 (lines 24, 28 and 32)

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

and even more concisely with prefix-increment operators as

```
++passes;
++failures;
++studentCounter;
```

or with postfix-increment operators as

```
passes++;
failures++;
studentCounter++;
```

When incrementing or decrementing a variable in a statement by itself, the prefix increment and postfix increment forms have the same effect, and the prefix decrement and postfix decrement forms have the same effect. It's only when a variable appears in the context of a larger expression that the prefix increment and postfix increment have different results (and similarly for the prefix decrement and postfix decrement).

> **Common Programming Error 5.4**
> 
> Attempting to use the increment or decrement operator on an expression other than one to which a value can be assigned is a syntax error. For example, writing ++(x + 1) is a syntax error, because (x + 1) is not an expression to which a value can be assigned.

# 5.1.13 Operator Precedence and Associativity

Figure 5.13 shows the precedence and associativity of the operators introduced to this point shown from top to bottom in decreasing order of precedence. The second column describes the associativity of the operators at each level of precedence. The conditional operator (? :); the unary operators prefix increment (++), prefix decrement (--), plus (+) and minus (-); the cast operators; and the assignment operators =, +=, -=, *=, /= and %=
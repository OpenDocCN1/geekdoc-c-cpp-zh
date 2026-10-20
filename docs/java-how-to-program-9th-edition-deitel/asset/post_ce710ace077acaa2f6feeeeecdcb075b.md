
```
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed: 6
Failed: 4
```

Fig. 4.12 | Analysis of examination results using nested control statements. (Part 3 of 3.)

Figure 4.12 shows the input and output from two sample executions of the program. During the first, the condition at line 39 of method main is true—more than eight students passed the exam, so the program outputs a message to bonus the instructor.

This example contains only one class, with method main performing all the class’s work. In this chapter and in Chapter 3, you’ve seen examples consisting of two classes—one containing methods that perform useful tasks and one containing method main, which creates an object of the other class and calls its methods. Occasionally, when it does not make sense to try to create a reusable class to demonstrate a concept, we’ll place the program’s statements entirely within the main method of a single class.

## 4.11 Compound Assignment Operators

The compound assignment operators abbreviate assignment expressions. Statements like

```
variable = variable operator expression;
```

where operator is one of the binary operators +, -, *, / or % (or others we discuss later in the text) can be written in the form

```
variable operator= expression;
```

For example, you can abbreviate the statement

```
c = c + 3;
```

with the addition compound assignment operator, +=, as

```
c += 3;
```

The += operator adds the value of the expression on its right to the value of the variable on its left and stores the result in the variable on the left of the operator. Thus, the assignment expression c += 3 adds 3 to c. Figure 4.13 shows the arithmetic compound assignment operators, sample expressions using the operators and explanations of what the operators do.

*Assume: int c = 3, d = 5, e = 4, f = 6, g = 12;*

| Assignment operator | Sample expression | Explanation | Assigns |
|---|---|---|---|
| += | c += 7 | c = c + 7 | 10 to c |
| -= | d -= 4 | d = d - 4 | 1 to d |
| *= | e *= 5 | e = e * 5 | 20 to e |
| /= | f /= 3 | f = f / 3 | 2 to f |
| %= | g %= 9 | g = g % 9 | 3 to g |

Fig. 4.13 | Arithmetic compound assignment operators.

## 4.12 Increment and Decrement Operators

Java provides two unary operators (summarized in Fig. 4.14) for adding 1 to or subtracting 1 from the value of a numeric variable. These are the unary increment operator, ++, and the unary decrement operator, --. A program can increment by 1 the value of a variable called c using the increment operator, ++, rather than the expression c = c + 1 or c += 1. An increment or decrement operator that's prefixed to (placed before) a variable is referred to as the prefix increment or prefix decrement operator, respectively. An increment or decrement operator that's postfixed to (placed after) a variable is referred to as the postfix increment or postfix decrement operator, respectively.

| Operator | Operator name | Sample expression | Explanation |
|---|---|---|---|
| ++ | prefix increment | ++a | Increment a by 1, then use the new value of a in the expression in which a resides. |
| ++ | postfix increment | a++ | Use the current value of a in the expression in which a resides, then increment a by 1. |
| -- | prefix decrement | --b | Decrement b by 1, then use the new value of b in the expression in which b resides. |
| -- | postfix decrement | b-- | Use the current value of b in the expression in which b resides, then decrement b by 1. |

Fig. 4.14 | Increment and decrement operators.

Using the prefix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable is known as preincrementing (or predecrementing). This causes the variable to be incremented (decremented) by 1; then the new value of the variable is used in the expression in which it appears. Using the postfix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable is known as postincrementing (or postdecrementing). This causes the current value of the variable to be used in the expression in which it appears; then the variable's value is incremented (decremented) by 1.

> Good Programming Practice 4.4
> Unlike binary operators, the unary increment and decrement operators should be placed next to their operands, with no intervening spaces.

Figure 4.15 demonstrates the difference between the prefix increment and postfix increment versions of the ++ increment operator. The decrement operator (-- ) works similarly.

```
// Fig. 4.15: Increment.java
// Prefix increment and postfix increment operators.

public class Increment
{
    public static void main( String[] args )
    {
        int c;

        // demonstrate postfix increment operator
        c = 5; // assign 5 to c
        System.out.println( c );  // prints 5
        System.out.println( c++ ); // prints 5 then postincrements
        System.out.println( c );  // prints 6

        System.out.println(); // skip a line

        // demonstrate prefix increment operator
        c = 5; // assign 5 to c
        System.out.println( c );  // prints 5
        System.out.println( ++c ); // preincrements then prints 6
        System.out.println( c );  // prints 6
    } // end main
} // end class Increment
```

![](img/009e962758dcc71dbc43a493362e6dc0_169_0.png)

Fig. 4.15 | Preincrementing and postincrementing.

Line 11 initializes the variable c to 5, and line 12 outputs c’s initial value. Line 13 outputs the value of the expression c++. This expression postincrements the variable c, so c’s original value (5) is output, then c’s value is incremented (to 6). Thus, line 13 outputs c’s initial value (5) again. Line 14 outputs c’s new value (6) to prove that the variable’s value was indeed incremented in line 13.

Line 19 resets c’s value to 5, and line 20 outputs c’s value. Line 21 outputs the value of the expression ++c. This expression preincrements c, so its value is incremented; then the new value (6) is output. Line 22 outputs c’s value again to show that the value of c is still 6 after line 21 executes.

The arithmetic compound assignment operators and the increment and decrement operators can be used to simplify program statements. For example, the three assignment statements in Fig. 4.12 (lines 27, 29 and 32)

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

When incrementing or decrementing a variable in a statement by itself, the prefix increment and postfix increment forms have the same effect, and the prefix decrement and postfix decrement forms have the same effect. It’s only when a variable appears in the context of a larger expression that preincrementing and postincrementing the variable have different effects (and similarly for predecrementing and postdecrementing).

> Common Programming Error 4.7
> Attempting to use the increment or decrement operator on an expression other than one to which a value can be assigned is a syntax error. For example, writing ++(x + 1) is a syntax error, because (x + 1) is not a variable.

Figure 4.16 shows the precedence and associativity of the operators we’ve introduced. They’re shown from top to bottom in decreasing order of precedence. The second column describes the associativity of the operators at each level of precedence. The conditional operator (?:); the unary operators increment (++), decrement (--), plus (+) and minus (-); the cast operators and the assignment operators =, +=, -=, *=, /= and %= associate from right to left. All the other operators in the operator precedence chart in Fig. 4.16 associate from left to right. The third column lists the type of each group of operators.

| Operators | Associativity | Type |
|---|---|---|
| ++ -- | right to left | unary postfix |
| ++ -- + - ( type ) | right to left | unary prefix |
| * / % | left to right | multiplicative |
| + - | left to right | additive |
| < <= > >= | left to right | relational |
| == != | left to right | equality |
| ?: | right to left | conditional |
| = += -= *= /= %= | right to left | assignment |

Fig. 4.16 | Precedence and associativity of the operators discussed so far.

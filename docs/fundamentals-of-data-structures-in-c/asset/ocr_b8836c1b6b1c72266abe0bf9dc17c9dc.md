The value of the expression is either one or zero. If the expression is true then the result will be one, if the expression is false then the result will be zero. If the values of x and y are 1 and 2 respectively, then the various expressions and their results are

| Expression | Result | Value |
|---|---|---|
| y != 2 | False | 0 |
| x == 2 | False | 0 |
| x == 1 | True | 1 |
| y != 3 | True | 1 |

# 1.7.5 Logical Operators

Operators, which are used to combine two or more relational expressions, are called as logical operators. These operators are used to test more than one condition at a time.

Table 1.9, shows various logical operators and their meaning.

| Operator | Meaning |
|---|---|
| && | Logical AND |
| || | Logical OR |
| ! | Logical NOT |

# 1.7.6 Bit wise Operators

C has certain operators known as bit wise operators that are used in applications, which require manipulation of individual bits within a word of memory. These operators permit the programmer to access and manipulate individual bits within a piece of data. Bit wise operators can operate only on integers and characters but not on floats and doubles.

Table 1.10, shows the various bit wise operators and their meaning.

| Operator | Meaning |
|---|---|
| ~ | One's complement |
| << | Left shift |
| >> | Right shift |
| & | Bit wise AND |
| | | Bit wise OR |
| ^ | Bit wise X-OR |

# Masking

Masking is a process in which a given pattern is transformed into another bit pattern by means of bit wise operator. The original bit pattern is one of the operands in the bitwise operation. The second operand called as the mask is a specially selected bit pattern that brings the desired transformation. Usually logical bitwise AND operator (&) is used for masking.
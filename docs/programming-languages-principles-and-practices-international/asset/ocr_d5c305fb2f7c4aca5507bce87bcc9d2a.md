6.12 Add the integer remainder and power operations to (a) the arithmetic BNF or (b) EBNF of Figures 6.9 or 6.10. Use % for the remainder operation and ^ for the power operation. Recall that the remainder operation is left-associative and has the same precedence as multiplication, but that power is right-associative (and has greater precedence than multiplication, so 2 ^ 2 ^ 3 = 256, not 64).

6.13 Unary minuses can be added in several ways to the arithmetic expression grammar of Figure 6.17 or Figure 6.18. Revise the BNF and EBNF for each of the cases that follow so that it satisfies the stated rule:
(a) At most, one unary minus is allowed in each expression, and it must come at the beginning of an expression, so -2 + 3 is legal (and equals 1) and -2 + (-3) is legal, but -2 + -3 is not.
(b) At most, one unary minus is allowed before a number or left parenthesis, so -2 + -3 and -2 * -3 are legal, but --2 and -2 + --3 are not.
(c) Arbitrarily many unary minuses are allowed before numbers and left parentheses, so everything above is legal.

6.14 Using the grammar of Figure 6.17, draw parse trees and abstract syntax trees for the arithmetic expressions:
(a) ((2))
(b) 3 + 4 * 5 + 6 * 7
(c) 3 * 4 + 5 * 6 + 7
(d) 3 * (4 + 5) * (6 + 7)
(e) (2 + (3 + (4 + 5)))

6.15 Finish writing the pseudocode for a recursive-descent recognizer for the English grammar of Section 6.2 that was begun in Section 6.6.

6.16 Translate the pseudocode of the previous exercise into a working recognizer program in C or another programming language of your choice. (Hint: This will require a scanner to separate the text into token strings.)

6.17 Revise the program of the previous exercise so that it randomly generates legal sentences in the grammar. (This will require the use of a random number generator.)

6.18 Modify the recursive-descent calculator program of Figure 6.24 to use the grammar of Figure 6.26 and the scanner of Figure 6.1 (so that the calculator also skips blanks appropriately).

6.19 Add subtraction and division to either (a) the calculator program of Figure 6.24, or (b) your answer to the previous exercise.

6.20 Add the remainder and power operations as described in Exercise 6.12 to (a) the program of Figure 6.24, (b) your answer to Exercise 6.18, or (c) your answer to Exercise 6.19.

6.21 Rewrite the program of Figure 6.24 or your answer to any of the previous three exercises (except for the remainder operation) to produce floating-point answers, as well as accept floating-point constants using the following revised grammar rules (in EBNF):
... (rules for expr and term as before)
factor → ( expr ) | decimal-number
decimal-number → number [ . number ]
... (rules for number and digit as before)
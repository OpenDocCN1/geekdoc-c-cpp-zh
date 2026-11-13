4. If the element is left parenthesis "(" then push it onto the stack.
5. If the element is an operator then:
   a) Repeatedly pop from stack (until the element on top of the stack has higher or same precedence than the operator currently scanned) and add it to P.
   b) Add the operator to stack.
6. If the element is a right parenthesis ")" then:
   a) Repeatedly pop from stack and add to P each operator until a left parenthesis "(" is found
   b) Pop the left parenthesis from the stack.
[End of Loop]
7. Return

# Example:

Find the postfix expression of the following infix expression:

Q = A + (B * C – (D / E ↑ F) * G) * H

| Serial Number | Symbol Scanned | Stack | Postfix Expression (P) |
| :--- | :--- | :--- | :--- |
| Initial | | ( | |
| 1 | A | ( | A |
| 2 | + | (+ | A |
| 3 | ( | (+( | A |
| 4 | B | (+( | AB |
| 5 | * | (+(* | AB |
| 6 | C | (+(* | ABC |
| 7 | - | (+(- | ABC * |
| 8 | ( | (+(-( | ABC * |
| 9 | D | (+(-( | ABC *D |
| 10 | / | (+(-(/ | ABC *D |
| 11 | E | (+(-(/ | ABC *DE |
| 12 | ↑ | (+(-(/↑ | ABC *DE |
| 13 | F | (+(-(/↑ | ABC *DEF |
| 14 | ) | (+- | ABC *DEF↑/ |
| 15 | * | (+-* | ABC *DEF↑/ |
| 16 | G | (+-* | ABC *DEF↑/G |
| 17 | ) | (+ | ABC *DEF↑/G*- |
| 18 | * | (+* | ABC *DEF↑/G*- |
| 19 | H | (+* | ABC *DEF↑/G*-H |
| 20 | ) | STACK EMPTY | ABC *DEF↑/G*-H*+ |

Postfix expression A B C * D E F ↑ / G * - H * +
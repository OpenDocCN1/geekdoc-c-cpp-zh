
## Truth table

| A | B | C | Y |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 0 |

The function Y in SOP form is given as follows:

`Y = A̅B̅C + A̅BC̅ + AB̅C̅ + ABC̅ = C̅ + A̅C`  ...(i)

The function Y in POS form is given as follows:

`Y = (A̅ + B + C)(A + B̅ + C)(A + B + C̅)(A̅ + B̅ + C̅) = (A̅ + C)(A + C)`  ...(ii)

Complement of (ii) is given by

`Y = (A + B + C̅) · (A̅ + B̅ + C) · (A̅ + B + C̅) · (A̅ + B̅ + C̅)`

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_73_0.png)

`Y = (A + C) · (A̅ + C̅) = A̅C + AC̅`

The expression for Y is found to be the same in both SOP and POS forms.

## 7. How is a Boolean function realized using logic gates?

**Answer:**

A Boolean function can be realized or implemented with the help of logic gates. This is best demonstrated by an example given below.

Consider the function `Y = A · C̅ + A̅ · C`. Here the first product term has to be implemented by NOT-ing C and then AND-ing this with A. The second term is implemented by NOT-ing A and then AND-ing this with C. These two terms are then OR-ed to yield the function Y. The circuit, using the gates AND, OR and NOT that realizes this function Y from the inputs A and C is shown below.

## 8. Why is it necessary to simplify a Boolean function?

**Answer:**

The expression representing a Boolean function has to be simplified or reduced for the simple reason of decreasing the number of terms in the expression. This in turn reduces the requirement of the number of logic gates for realizing the function. Hence the complexity, hardware and cost of the logic circuit for implementing a function can be reduced.

## 9. How is the compact form used to represent a Boolean function?

**Answer:**

A Boolean function, with the canonical sum of product terms, can be expressed in a compact form by listing the decimal value corresponding to the minterm for which the function value is 1. For example, the following Boolean function expressed in SOP form can be expressed in compact form as shown below:

`Y = A̅B̅C + A̅BC̅ + AB̅C̅ + ABC̅`

`Y = Σm (1, 3, 4, 6, 7) = m₁ + m₃ + m₄ + m₆ + m₇`

Similarly, a Boolean function can be expressed in compact form by listing the decimal value corresponding to the maxterms for which the function value is 0. Hence the following Boolean function represented in POS form can be expressed in compact form as shown below:

`Y = (A + B + C) · (A + B̅ + C) · (A̅ + B + C̅)`

`Y = ΠM (0, 2, 5) = M₀M₂M₅`

## 10. What is the difference in representing a Boolean function in SOP form and POS form?

**Answer:**

The difference lies in the way the expression representing the Boolean function is formed. In the SOP form the expression is formed with OR-ing minterms, while in the POS form the expression is formed by AND-ing the maxterms. This is very well illustrated in the example given with the answer for the previous question.

## EXERCISES

- 1. Solve the following.
  - (i) `A + 1 = ______`
  - (ii) `A + 0 = ______`
  - (iii) `A · 1 = ______`
  - (iv) `A + A̅ = ______`
  - (v) `A + A̅ = ______`
  - (vi) `A · 0 = ______`
  - (vii) `A · A̅ = ______`
  - (viii) `A · A = ______`

- 2. State De Morgan’s theorem.

- 3. Construct truth tables for the following Boolean functions.
  - (i) Q = AB + \bar{A}B
  - (ii) Q = A · B
  - (iii) Q = A + B
  - (iv) Q = A
  - (v) Q = \bar{A} + B
  - (vi) Q = \bar{A} · B
  - (vii) Q = A + \bar{B} · C
  - (viii) Q = (A + B) · C
  - (ix) Q = A · \bar{B} + C · \bar{D}
  - (x) Q = X(\bar{X} + Y)(\bar{X} + Z)
  - (xi) f = ABC + \bar{A}BC + AB\bar{C}
  - (xii) f = (\bar{A} + B + C)(A + B + \bar{C})(A + B + C)

- 4. Simplify the following Boolean expressions.
  - (i) AA + AB + AC + BC
  - (ii) (A + B + C)(D + E) + (A + B + C)(D + E)
  - (iii) XZ + Z(\bar{X} + XY)
  - (iv) (A + B)(C + D + E) + (A + B)
  - (v) AB + ABC + ABCD + ABCDE + ABCDEF
  - (vi) (A + B + C)(D + E) + (A + B + C)(D + E)
  - (vii) A · (\bar{A} + C) + C
  - (viii) (A + B) · (B + \bar{A})
  - (ix) \bar{a}\bar{b}c + \bar{a}b\bar{c} + ab\bar{c} + abc
  - (x) (a + \bar{a})(ab + abc)
  - (xi) (a + b)(\bar{c} + d)
  - (xii) ab + \overline{ac}(b + \bar{c})
  - (xiii) ab + \bar{a}c + bc
  - (xiv) \overline{(a + b + c)}(\bar{a} + b + \bar{c})

- 5. Find the dual of:
  - (i) A + 1 = 1
  - (ii) X + \bar{X}Y = X + Y
  - (iii) A · B = B · A
  - (iv) A(A + B) = A
  - (v) A · (B + C) = AB + AC
  - (vi) \overline{AB} = \bar{A} + \bar{B}
  - (vii) A + (C + B) = (A + B) + C
  - (viii) A + B = AB + \bar{A}B + A\bar{B}
  - (ix) A + B · (C + DE) = A + BCDE
  - (x) A + BC(\bar{A} + \bar{B}C) = A + BC

- 6. Prove the following.
  - (i) (X + Y) · (\bar{X} + Z) = X · Z + \bar{X} · Y + YZ
  - (ii) (A + D)(A + C)(B + C + D) = AB + CD
  - (iii) ABC(AB + \bar{C})(BC + AC) = ABC
  - (iv) \bar{A}BC + BC + AC = C
  - (v) AB + ABC + B\bar{C} = AC + BC
  - (vi) \overline{AB} + \bar{A} + AB = 0
  - (vii) (A + \bar{A})(AB + ABC) = AB
  - (viii) \overline{ABC}(A + B + C) = ABC
  - (ix) (ABC + \overline{AB}) + BC = \overline{AB}
  - (x) If XY + \bar{X}Y = Z then XZ + \bar{X}\bar{Z} = Y

- 7.
  - (i) Convert Q = ABCD + ABC into a sum of minterms by algebraic method.
  - (ii) Convert Q = ABC + \bar{B}CD into a product of maxterms by algebraic method.

- 8.
  - (i) To get into a physics program in University, Jagan needs to have Physics and either algebra or calculus. Assign Boolean variables to the conditions and write a Boolean expression for the program requirements.
  - (ii) Aman wants to go go-karting at Kart World. They have conditions on who can drive their go-karts. You must be either over sixteen or be over twelve years of age and have parental permission. Using Boolean variables create an expression for the karting requirements.

- 9. Find the output Y in each of the following when (a) A = 1 and (b) A = 0.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_74_0.png)

- 10. Construct the truth tables for each of the following. Find the Boolean expressions of output Y in each of the circuits. What conclusions can be drawn?

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_74_1.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_0.png)

- 11. Construct the truth table for the given circuits and derive the output Boolean expressions for each.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_1.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_2.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_3.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_4.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_5.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_6.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_7.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_8.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_9.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_10.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_11.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_75_12.png)

- 12. (a) Construct the circuits for the following Boolean expressions using AND, OR, and NOT gates without simplifying the expressions.
  - (i) Q = A\overline{B} + \overline{A}B
  - (ii) Q = AA + AB + AC + BC
  - (iii) Q = AC + ABC
  - (iv) Q = (B + \overline{B})(B + \overline{A})
  - (v) Q = A(\overline{A} + C) + C
  - (vi) Q = (\overline{A} + B) \cdot (C + D)
  - (vii) Q = (A + B + C)(\overline{A} + \overline{B} + \overline{C}) + A \cdot \overline{B} \cdot C
  - (viii) Q = A \cdot B \cdot \overline{C}(\overline{A} + B + C)

  (b) For each of these, create a circuit using AND, OR, and NOT gates for the Boolean expression after simplification.

- 13. For each of the questions, 12a (i) to (viii), create a circuit using NAND or NOR gates for the Boolean expression after simplification.

- 14. With respect to questions 4 and 5, explain why simplifying Boolean expressions is useful when designing circuits.

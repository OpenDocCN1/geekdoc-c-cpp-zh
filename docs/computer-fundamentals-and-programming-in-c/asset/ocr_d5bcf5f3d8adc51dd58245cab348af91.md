# Truth table

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

![](bbox=[0.511, 0.051, 0.963, 0.241])

`Y = (A + C) · (A̅ + C̅) = A̅C + AC̅`

The expression for Y is found to be the same in both SOP and POS forms.

# 7. How is a Boolean function realized using logic gates?

**Answer:**

A Boolean function can be realized or implemented with the help of logic gates. This is best demonstrated by an example given below.

Consider the function `Y = A · C̅ + A̅ · C`. Here the first product term has to be implemented by NOT-ing C and then AND-ing this with A. The second term is implemented by NOT-ing A and then AND-ing this with C. These two terms are then OR-ed to yield the function Y. The circuit, using the gates AND, OR and NOT that realizes this function Y from the inputs A and C is shown below.

# 8. Why is it necessary to simplify a Boolean function?

**Answer:**

The expression representing a Boolean function has to be simplified or reduced for the simple reason of decreasing the number of terms in the expression. This in turn reduces the requirement of the number of logic gates for realizing the function. Hence the complexity, hardware and cost of the logic circuit for implementing a function can be reduced.

# 9. How is the compact form used to represent a Boolean function?

**Answer:**

A Boolean function, with the canonical sum of product terms, can be expressed in a compact form by listing the decimal value corresponding to the minterm for which the function value is 1. For example, the following Boolean function expressed in SOP form can be expressed in compact form as shown below:

`Y = A̅B̅C + A̅BC̅ + AB̅C̅ + ABC̅`

`Y = Σm (1, 3, 4, 6, 7) = m₁ + m₃ + m₄ + m₆ + m₇`

Similarly, a Boolean function can be expressed in compact form by listing the decimal value corresponding to the maxterms for which the function value is 0. Hence the following Boolean function represented in POS form can be expressed in compact form as shown below:

`Y = (A + B + C) · (A + B̅ + C) · (A̅ + B + C̅)`

`Y = ΠM (0, 2, 5) = M₀M₂M₅`

# 10. What is the difference in representing a Boolean function in SOP form and POS form?

**Answer:**

The difference lies in the way the expression representing the Boolean function is formed. In the SOP form the expression is formed with OR-ing minterms, while in the POS form the expression is formed by AND-ing the maxterms. This is very well illustrated in the example given with the answer for the previous question.

# EXERCISES

+   1. Solve the following.
+      (i) `A + 1 = ______`
+      (ii) `A + 0 = ______`
+      (iii) `A · 1 = ______`
+      (iv) `A + A̅ = ______`
+      (v) `A + A̅ = ______`
+      (vi) `A · 0 = ______`
+      (vii) `A · A̅ = ______`
+      (viii) `A · A = ______`

+   2. State De Morgan’s theorem.
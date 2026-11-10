minterms. Minterms are designated as $m_0, m_1, \ldots, m_n$, etc., where the subscripts represent the decimal values obtained from the equivalent binary value of the combined variables.

The minterms are also called standard products. Similarly, ORing the variables form maxterms. For three variables, the minterms and maxterms are determined as shown in Table 3.3.

**Table 3.3** Summary of canonical and standard forms

| A | B | C | Minterm term | Minterm designation | Maxterm term | Maxterm designation |
|---|---|---|---|---|---|---|
| 0 | 0 | 0 | $\overline{A}\,\overline{B}\,\overline{C}$ | $m_0$ | $A+B+C$ | $M_0$ |
| 0 | 0 | 1 | $\overline{A}\,\overline{B}C$ | $m_1$ | $A+B+\overline{C}$ | $M_1$ |
| 0 | 1 | 0 | $\overline{A}B\,\overline{C}$ | $m_2$ | $A+\overline{B}+C$ | $M_2$ |
| 0 | 1 | 1 | $\overline{A}BC$ | $m_3$ | $A+\overline{B}+\overline{C}$ | $M_3$ |
| 1 | 0 | 0 | $A\overline{B}\,\overline{C}$ | $m_4$ | $\overline{A}+B+C$ | $M_4$ |
| 1 | 0 | 1 | $A\overline{B}C$ | $m_5$ | $\overline{A}+B+\overline{C}$ | $M_5$ |
| 1 | 1 | 0 | $AB\overline{C}$ | $m_6$ | $\overline{A}+\overline{B}+C$ | $M_6$ |
| 1 | 1 | 1 | $ABC$ | $m_7$ | $\overline{A}+\overline{B}+\overline{C}$ | $M_7$ |

Since each minterm or the maxterm is formed by the combination of all the n complemented or uncomplemented variables, each of these is called a canonical term. Each minterm is obtained by ANDing the variables, with each variable having an overbar if its corresponding binary value is 0 and not having an overbar if its binary value is 1. Similarly, each maxterm is obtained by ORing the variables, with each variable having an overbar if its corresponding binary value is 1 and not having an overbar if it is 0. It may be noted that each maxterm is the complement of its corresponding minterm and vice versa.

Any Boolean function may be expressed as an OR combination of the minterms for which the function is 1. This form of the function is a 'sum' of minterms or standard 'products'. A Boolean function may also be expressed as an AND combination of maxterms for which the function is 0. The function, thus, is the 'product' of maxterms. A Boolean function written as a sum of minterms or product of maxterms is said to be in **canonical form**. De Morgan's theorem allows conversion between the two canonical forms. The two canonical forms of Boolean algebra are basic forms.

Another method of expressing a Boolean function is the **standard form**. There are two types of standard forms: sum of products and product of sums.

**The sum of products** is a Boolean expression containing AND terms, called product terms, formed with one or more logic variables. The sum denotes the ORing of these terms. Example: $f_1(A,B,C) = \overline{B} + AB + A\overline{B}C$

**A product of sums** is a Boolean expression containing OR terms called sum terms, comprising one or more logic variables. The product denotes the ANDing of these terms. Example: $f_2 = A \cdot (B+C) \cdot (A+B+C+D)$

A Boolean function may be expressed in a non-standard form also. For example: $F_3 = (AB + CD)(\overline{A}\,\overline{B} + \overline{C}\,\overline{D})$ is neither in the form of sum of products nor in product of sums form. However, it can be transformed to a standard form using the distributive law, that is, $F_3 = AB\overline{C}\,\overline{D} + \overline{A}\,\overline{B}CD$.

# ### 3.8 NUMERICAL REPRESENTATION OF BOOLEAN FUNCTIONS IN CANONICAL FORM

A Boolean function, with the canonical sum of product terms, can be expressed in a compact form by listing the decimal value corresponding to the minterm for which the function value is 1.

As an example, the truth table of a three-variable function is shown below. Three variables, each of which can take the values 0 or 1, yield eight possible combinations of values for which the function may be true. These eight combinations are listed in ascending binary order and the equivalent decimal value is also shown in Table 3.4.

**Table 3.4** Equivalent decimal value for Boolean terms

| Decimal value | A | B | C | F |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 2 | 0 | 1 | 0 | 1 |
| 3 | 0 | 1 | 1 | 1 |
| 4 | 1 | 0 | 0 | 0 |
| 5 | 1 | 0 | 1 | 0 |
| 6 | 1 | 1 | 0 | 0 |
| 7 | 1 | 1 | 1 | 1 |
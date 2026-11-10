Boolean addition (+)
0 + 0 = 0
1 + 0 = 1
0 + 1 = 1
1 + 1 = 1

Boolean negation
0̄ = 1
1̄ = 0

Based on the axioms, the following laws have evolved:

AND law
A · 0 = 0 (Null law)
A · 1 = A (Identity law)
A · A = A (Idempotence law)
A · A̅ = 0 (Complement law)

OR law
A + 0 = A (Null law)
A + 1 = 1 (Identity law)
A + A = A (Idempotence law)
A + A̅ = 1 (Complement law)

Complementation law
If A = 0 then A̅ = 1
If A = 1 then A̅ = 0
A̅̅ = A (Double negation law)

Associative law
(A · B) · C = A · (B · C) = A · B · C
(A + B) + C = A + (B + C) = A + B + C

Distributive law
A · (B + C) = (A · B) + (A · C)
A + (B · C) = (A + B) · (A + C)

Commutative law
A · B = B · A
A + B = B + A

It should be evident from above that there are three basic logic operations in Boolean algebra, namely, AND, OR, and NOT. The common symbols used for each of these operations are given in Table 3.1.

Table 3.1 Boolean operations and their symbols

| Operation | Symbol |
|---|---|
| AND | · |
| OR | + |
| NOT | - or ' |

# 3.2 THEOREMS

From the axioms above, we can derive the following theorems.

| Theorem 1: Idempotent | Proof |
|---|---|
| (a) x + x = x | (a) x + x = (x + x) · 1 (Identity)<br>(x + x) · (x + x̅) (Complement)<br>x + x·x̅ (Distributive)<br>x + 0 (Complement)<br>x (Null) |
| (b) x · x = x [Dual of (a)] | (b) It is not necessary to provide a separate proof for (b) which is the dual of (a) because of the principle of duality. |

# Duality

Any algebraic equality derived from the axioms of Boolean algebra remains true when the operators OR and AND are interchanged and the identity elements 0 and 1 are interchanged. This property is called duality. For example,

x + 1 = 1
x · 0 = 0 (dual)

Because of the duality principle, for any given theorem its dual may be easily obtained.

| Theorem 2: Operations with 0 and 1 | Proof |
|---|---|
| (a) x + 1 = 1<br>(b) x · 0 = 0 [Dual of (a)] | (a) x + 1<br>x + x + x̅ (Complement)<br>x + x̅ (Idempotent theorem)<br>1 (Complement) |

| Theorem 3: Absorption | Proof |
|---|---|
| (a) y · x + x = x<br>(b) (y + x) · x = x [Dual of (a)] | (a) y·x + x<br>y·x + x·1 (Identity)<br>y·x + 1·x (Commutative)<br>(y + 1)·x (Distributive)<br>1·x (Operations with 0 and 1)<br>x (Identity) |

| Theorem 4: DeMorgan's Law | Proof |
|---|---|
| (a) (x + y)̄ = x̅ · y̅<br>(b) (x · y)̄ = x̅ + y̅<br>[Dual of (a)] | The proof for De Morgan's Law using the axioms of Boolean algebra is long. Another method (that also works for the other theorems just discussed) is to prove by the method of perfect induction, which uses the following truth tables: |

| x | y | x+y | (x+y)̄ | x̅ | y̅ | x̅·y̅ |
|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 1 | 1 | 1 | 1 |
| 0 | 1 | 1 | 0 | 1 | 0 | 0 |
| 1 | 0 | 1 | 0 | 0 | 1 | 0 |
| 1 | 1 | 1 | 0 | 0 | 0 | 0 |
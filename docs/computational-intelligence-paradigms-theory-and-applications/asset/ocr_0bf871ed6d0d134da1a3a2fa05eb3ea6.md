A defined on a finite universal set X, its fuzzy cardinality, |A~|, is a fuzzy number defined by the formula

|A~|( |aA| ) = a

for all a in Lambda(A).

# 6.10.1 Arithmetic Operations on Intervals

Fuzzy arithmetic is based on two properties of fuzzy numbers:

+   1. Each fuzzy set, and thus each fuzzy number, can fully and uniquely be represented by its alpha-cuts.
+   2. Alpha-cuts of each fuzzy number are closed intervals of real numbers for all alpha in [0,1]. Therefore, arithmetic operations on fuzzy numbers can be defined in terms of arithmetic operations on their alpha-cuts (i.e., arithmetic operations on closed intervals), which is treated in the field of “interval analysis”.

Let # denote any of the four arithmetic operations on closed intervals: “addition” +, “subtraction” −, “multiplication” *, and “division” /. Then,

[a,b] # [d,e] = {#fg | a ≤ f ≤ b, d ≤ g ≤ e}

is a general property of all arithmetic operations on closed intervals, except [a,b]/[d,e] is not defined when 0 is in the interval [d,e]. Therefore, the result of an arithmetic operation on closed intervals is again a closed interval.

The four arithmetic operations on closed intervals are defined as follows:

[a,b] + [d,e] = [a+d,b+e]
[a,b] − [d,e] = [a−e,b−d]
[a,b] * [d,e] = [min(ad,ae,bd,be), max(ad,ae,bd,be)]

and, provided that 0 is not in [d,e]

[a,b] / [d,e] = [a,b] * [1/e,1/d]
= [min(a/d,a/e,b/d,b/e), max(a/d,a/e,b/d,b/e)]

Note that a real number r may also be regarded as a special (degenerated) interval [r,r]. When one of the intervals in the above equations is degenerated, we obtain special operations; when both of them are degenerated, we obtain the standard arithmetic of real numbers.

+   Letting A=[a1,a2], B=[b1,b2], C=[c1,c2], 0=[0,0], 1=[1,1], useful properties of arithmetic operations are as follows:
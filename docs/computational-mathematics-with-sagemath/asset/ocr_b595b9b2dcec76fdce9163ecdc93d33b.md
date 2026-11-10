# ### 5.1.2 Objects and Polymorphism

Almost all Sage operations are *polymorphic*, i.e., they apply to several kinds of objects. For example, whatever the nature of the object `o` that we want to “factor”, we will use the same notation `o.factor()` (or its shortcut `factor(o)`). The computations to be performed however differ to factor an integer or a polynomial! They also differ if the polynomial has rational coefficients, or coefficients in a finite field. The object class determines the version of the factor code that will be called.

Similarly, like the usual mathematical notation, the product of two objects `a` and `b` can always be denoted `a*b`, even if the algorithm used differs in each case[^1]. Here is a product of two integers:

```
```
sage: 3 * 7
21
```
```

a product of two rational numbers, obtained by multiplying the numerators and denominators, then reducing the fraction:

```
```
sage: (2/3) * (6/5)
4/5
```
```

a product of two complex numbers, using the relation `i² = −1`:

```
```
sage: (1 + I) * (1 - I)
2
```
```

some commutative products of two formal expressions:

```
```
sage: (x + 2) * (x + 1)
(x + 2)*(x + 1)
sage: (x + 1) * (x + 2)
(x + 2)*(x + 1)
```
```

Apart from the notation simplicity, this form of polymorphism enables us to write *generic* programs which apply to any object having the involved operations (here multiplication):

```
```
sage: def fourth_power(a):
....:     a = a * a
....:     a = a * a
....:     return a
```
```

```
```
sage: fourth_power(2)
16
sage: fourth_power(3/2)
81/16
```
```

[^1]: For a binary operation like the product, the selection of the appropriate method is slightly more complex than what was described above. Indeed, with mixed operations like the sum 2 + 3/4 of an integer and of a rational number. In this case, 2 will be converted in the rational 2/1, and the addition of two rationals will be called. The rules that describe which operand must be converted, and how it should be converted, are part of the *coercion model*.
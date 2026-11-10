<table>
<tr><th colspan="2">Main monomial orders, with the example of Q[x, y, z]</th></tr>
<tr><td>lex</td><td>x^α ≺ x^β ⇔ α1 < β1 or (α1 = β1 and α2 < β2) or ...<br>or (α1 = β1,...,αn−1 = βn−1 and αn < βn)<br>x^3 > x^2 y > x^2 z > x^2 > xy^2 > xyz > xy > xz^2 > xz > x > y^3 > y^2 z > yz^2 > yz > y > z^3 > z^2 > z > 1</td></tr>
<tr><td>invlex</td><td>x^α ≺ x^β ⇔ αn < βn or (αn = βn and αn−1 < βn−1) or ...<br>or (αn = βn,...,α2 = β2 and α1 < β1)<br>z^3 > yz^2 > xz^2 > y^2 z > yz > xyz > z^2 > xz > z > y^3 > y^2 > xy^2 > y > x^2 y > x^2 > x > 1</td></tr>
<tr><td>deglex</td><td>x^α ≺ x^β ⇔ |α| < |β| or (|α| = |β| and x^α ≺_{lex} x^β)<br>x^3 > x^2 y > x^2 z > xy^2 > xyz > xz^2 > y^3 > y^2 z > yz^2 > z^3 > x^2 > xy > xz > y^2 > yz > z^2 > x > y > z > 1</td></tr>
<tr><td>degrevlex</td><td>x^α ≺ x^β ⇔ |α| < |β| or (|α| = |β| and x^α ≻_{invlex} x^β)<br>x^3 > x^2 y > xy^2 > y^3 > x^2 z > xyz > y^2 z > xz^2 > yz^2 > z^3 > x^2 > xy > y^2 > xz > yz > z^2 > x > y > z > 1</td></tr>
<tr><th colspan="2">Construction of monomial orders</th></tr>
<tr><td>object representing a predefined order on n variables</td><td>TermOrder('nom', n)</td></tr>
<tr><td>matrix order: x^α &lt;_M x^β ⇔ Mα &lt;_{lex} Mβ</td><td>TermOrder(M)</td></tr>
<tr><td>blocks: x^a y^b ≺ x^{a'} y^{b'} ⇔ a &lt;_1 a' or (a = a', b &lt;_2 b')</td><td>T1 + T2</td></tr>
</table>
<p>TABLE 9.5 · Monomial orders.</p>

# ### 9.3.1 Monomial Orders

A monomial order or admissible order is a total order on the monomials x^α of a polynomial ring, which satisfies

x^α ≺ x^β ⟹ x^{α+γ} ≺ x^{β+γ}      and      γ ≠ 0 ⟹ 1 ≺ x^γ      (9.9)

for all exponents α, β, γ. Equivalently, we can consider ≺ as an order on the exponents α ∈ ℕ^n or on the terms c x^α. The leading monomial, leading coefficient and leading term of a polynomial p (see §1.1.3) for the current monomial order are those of largest exponent; we denote them respectively by lm p, lc p and lt p.

The first condition in (9.9) states that the monomial order should be compatible with products: multiplying by a fixed monomial does not change the order. The second condition implies that ≺ is a well-order, i.e., an infinite sequence of decreasing monomials does not exist. Let us notice that the only monomial order on K[x] is the usual one x^n > x^{n−1} > ⋯ > 1.

We have seen in §9.1.1 that Sage allows an order to be chosen when defining a polynomial ring via constructions like

```
```
sage: R.<x,y,z,t> = PolynomialRing(QQ, order='lex')
```
```

Table 9.5 lists the main predefined monomial orders; lex is the lexicographic order of the exponents, invlex is the lexicographic order of exponents read^a

^a Sage also allows orders called “local”) where 1 is the largest monomial instead of the smallest one. For example, in the order neglex on Q[x,y,z], we have 1 > z > z^2 > z^3 > y > ⋯
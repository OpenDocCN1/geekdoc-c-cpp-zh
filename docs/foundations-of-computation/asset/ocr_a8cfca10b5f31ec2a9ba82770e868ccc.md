equation will be true when \(a = b + 52\). So every element \(b\) is the image of the number \(a = b + 52\), and \(f\) is therefore onto. Note that if \(f\) had been specified to have domain \(\mathbb{N}\), then \(f\) would _not_ be onto, as for some integer \(b \in \mathbb{Z}\) the number \(a = b + 52\) is not in the domain \(\mathbb{N}\) (for example, the integer \(-73\) is not in the image of \(f\), since \(-21\) is not in \(\mathbb{N}\).)

If \(f : A \rightarrow B\) and if \(a \in A\), then \(a\) is associated to only one element \(B\). This is part of the definition of a function. However, no such restriction holds for elements of \(B\). If \(b \in B\), it is possible for \(b\) to be associated to zero, one, two, three, ... or even to an infinite number of elements of \(A\). In the case where each element of the range is associated to at most one element of the domain, the function is said to be **one-to-one**. Sometimes, the term **injective** is used instead. The function \(f\) is one-to-one (or injective) if for any two distinct elements \(x\) and \(y\) in the domain of \(f\), \(f(x)\) and \(f(y)\) are also distinct. In terms of logic, \(f : A \rightarrow B\) is one-to-one if and only if

```
\(\forall x \in A \forall y \in A (x \neq y \rightarrow f(x) \neq f(y))\).
```

Since a proposition is equivalent to its contrapositive, we can write this condition equivalently as

```
\(\forall x \in A \forall y \in A (f(x) = f(y) \rightarrow x = y)\).
```

Sometimes, it is easier to work with the definition of one-to-one when it is expressed in this form. The function that associates every person to his or her mother is not one-to-one because it is possible for two different people to have the same mother. The function \(s : \mathbb{N} \rightarrow \mathbb{N}\) specified by \(s(n) = n^2\) is one-to-one. However, we can define a function \(r : \mathbb{Z} \rightarrow \mathbb{Z}\) by the same formula: \(r(n) = n^2\), for \(n \in \mathbb{Z}\). The function \(r\) is _not_ one-to-one since two different integers can have the same square. For example, \(r(-2) = r(2)\).

A function that is both one-to-one and onto is said to be **bijective**. The function that associates each point in a map of New York State to a point in the state itself is presumably bijective. For each point on the map, there is a corresponding point in the state, and _vice versa_. If we specify the function \(f\) from the set \(\{1, 2, 3\}\) to the set \(\{a, b, c\}\) as the set of ordered pairs \(\{(1, b), (2, a), (3, c)\}\), then \(f\) is a bijective function. Or consider the function from \(\mathbb{Z}\) to \(\mathbb{Z}\) given by \(f(n) = n - 52\). We have already shown that \(f\) is onto. We can show that it is also one-to-one: pick an arbitrary \(x\) and \(y\) in \(\mathbb{Z}\) and assume that \(f(x) = f(y)\). This means that \(x - 52 = y - 52\), and adding 52 to both sides of the equation yields \(x = y\). Since \(x\) and \(y\) were arbitrary, we have proved \(\forall x \in \mathbb{Z} \forall y \in \mathbb{Z} (f(x) = f(y) \rightarrow x = y)\), that is, that \(f\) is one-to-one. Altogether, then, \(f\) is a bijection.

One difficulty that people sometimes have with mathematics is its generality. A set is a collection of entities, but an “entity” can be anything at
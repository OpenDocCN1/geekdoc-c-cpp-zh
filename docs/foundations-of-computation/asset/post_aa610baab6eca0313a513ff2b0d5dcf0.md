
equation will be true when \(a = b + 52\). So every element \(b\) is the image of the number \(a = b + 52\), and \(f\) is therefore onto. Note that if \(f\) had been specified to have domain \(\mathbb{N}\), then \(f\) would _not_ be onto, as for some integer \(b \in \mathbb{Z}\) the number \(a = b + 52\) is not in the domain \(\mathbb{N}\) (for example, the integer \(-73\) is not in the image of \(f\), since \(-21\) is not in \(\mathbb{N}\).)

If \(f : A \rightarrow B\) and if \(a \in A\), then \(a\) is associated to only one element of \(B\). This is part of the definition of a function. However, no such restriction holds for elements of \(B\). If \(b \in B\), it is possible for \(b\) to be associated to zero, one, two, three, ... or even to an infinite number of elements of \(A\). In the case where each element of the range is associated to at most one element of the domain, the function is said to be **one-to-one**. Sometimes, the term **injective** is used instead. The function \(f\) is one-to-one (or injective) if for any two distinct elements \(x\) and \(y\) in the domain of \(f\), \(f(x)\) and \(f(y)\) are also distinct. In terms of logic, \(f : A \rightarrow B\) is one-to-one if and only if

```
\(\forall x \in A \forall y \in A (x \neq y \rightarrow f(x) \neq f(y))\).
```

Since a proposition is equivalent to its contrapositive, we can write this condition equivalently as

```
\(\forall x \in A \forall y \in A (f(x) = f(y) \rightarrow x = y)\).
```

Sometimes, it is easier to work with the definition of one-to-one when it is expressed in this form. The function that associates every person to his or her mother is not one-to-one because it is possible for two different people to have the same mother. The function \(s : \mathbb{N} \rightarrow \mathbb{N}\) specified by \(s(n) = n^2\) is one-to-one. However, we can define a function \(r : \mathbb{Z} \rightarrow \mathbb{Z}\) by the same formula: \(r(n) = n^2\), for \(n \in \mathbb{Z}\). The function \(r\) is _not_ one-to-one since two different integers can have the same square. For example, \(r(-2) = r(2)\).

A function that is both one-to-one and onto is said to be **bijective**. The function that associates each point in a map of New York State to a point in the state itself is presumably bijective. For each point on the map, there is a corresponding point in the state, and _vice versa_. If we specify the function \(f\) from the set \(\{1, 2, 3\}\) to the set \(\{a, b, c\}\) as the set of ordered pairs \(\{(1, b), (2, a), (3, c)\}\), then \(f\) is a bijective function. Or consider the function from \(\mathbb{Z}\) to \(\mathbb{Z}\) given by \(f(n) = n - 52\). We have already shown that \(f\) is onto. We can show that it is also one-to-one: pick an arbitrary \(x\) and \(y\) in \(\mathbb{Z}\) and assume that \(f(x) = f(y)\). This means that \(x - 52 = y - 52\), and adding 52 to both sides of the equation yields \(x = y\). Since \(x\) and \(y\) were arbitrary, we have proved \(\forall x \in \mathbb{Z} \forall y \in \mathbb{Z} (f(x) = f(y) \rightarrow x = y)\), that is, that \(f\) is one-to-one. Altogether, then, \(f\) is a bijection.

One difficulty that people sometimes have with mathematics is its generality. A set is a collection of entities, but an “entity” can be anything at all, including other sets. Once we have defined ordered pairs, we can use ordered pairs as elements of sets. We could also make ordered pairs of sets. Now that we have defined functions, every function is itself an entity. This means that we can have sets that contain functions. We can even have a function whose domain and range are sets of functions. Similarly, the domain or range of a function might be a set of sets, or a set of ordered pairs. Computer scientists have a good name for this. They would say that sets, ordered pairs, and functions are first-class objects. Once a set, ordered pair, or function has been defined, it can be used just like any other entity. If they were not first-class objects, there could be restrictions on the way they can be used. For example, it might not be possible to use functions as members of sets. (This would make them “second class.”)

For example, suppose that $A$, $B$, and $C$ are sets. Then since $A \times B$ is a set, we might have a function $f : A \times B \to C$. If $(a, b) \in A \times B$, then the value of $f$ at $(a, b)$ would be denoted $f((a, b))$. In practice, though, one set of parentheses is usually dropped, and the value of $f$ at $(a, b)$ is denoted $f(a, b)$. As a particular example, we might define a function $p : \mathbb{N} \times \mathbb{N} \to \mathbb{N}$ with the formula $p(n, m) = nm + 1$. Similarly, we might define a function $q : \mathbb{N} \times \mathbb{N} \to \mathbb{N} \times \mathbb{N}$ by $q(n, m) = (nm - nk, mk - nk)$.

Suppose that $A$ and $B$ are sets. There are, in general, many functions that map $A$ to $B$. We can gather all those functions into a set. This set, whose elements are all the functions from $A$ to $B$, is denoted $B^A$. (We’ll see later why this notation is reasonable.) Using this notation, saying $f : A \to B$ is exactly the same as saying $f \in B^A$. Both of these notations assert that $f$ is a function from $A$ to $B$. Of course, we can also form an unlimited number of other sets, such as the power set $\mathcal{P}(B^A)$, the cross product $B^A \times A$, or the set $A^{A \times A}$, which contains all the functions from the set $A \times A$ to the set $A$. And of course, any of these sets can be the domain or range of a function. An example of this is the function $\mathcal{E} : B^A \times A \to B$ defined by the formula $\mathcal{E}(f, a) = f(a)$. Let’s see if we can make sense of this notation. Since the domain of $\mathcal{E}$ is $B^A \times A$, an element in the domain is an ordered pair in which the first coordinate is a function from $A$ to $B$ and the second coordinate is an element of $A$. Thus, $\mathcal{E}(f, a)$ is defined for a function $f : A \to B$ and an element $a \in A$. Given such an $f$ and $a$, the notation $f(a)$ specifies an element of $B$, so the definition of $\mathcal{E}(f, a)$ as $f(a)$ makes sense. The function $\mathcal{E}$ is called the “evaluation function” since it captures the idea of evaluating a function at an element of its domain.

## Exercises

- 1. Let $A = \{1, 2, 3, 4\}$ and let $B = \{a, b, c\}$. Find the sets $A \times B$ and $B \times A$.

- 2. Let A be the set {a,b,c,d}. Let f be the function from A to A given by the set of ordered pairs {(a,b), (b,b), (c,a), (d,c)}, and let g be the function given by the set of ordered pairs {(a,b), (b,c), (c,d), (d,d)}. Find the set of ordered pairs for g ◦ f.

- 3. Let A = {a,b,c} and let B = {0,1}. Find all possible functions from A to B. Give each function as a set of ordered pairs. (Hint: Every such function corresponds to one of the subsets of A.)

- 4. Consider the functions from Z to Z which are defined by the following formulas. Decide whether each function is onto and whether it is one-to-one; prove your answers.
  - a) f(n) = 2n
  - b) g(n) = n + 1
  - c) h(n) = n^2 + n + 1
  - d) s(n) = { n/2 if n is even; (n+1)/2 if n is odd }

- 5. Prove that composition of functions is an associative operation. That is, prove that for functions f : A → B, g : B → C, and h : C → D, the compositions (h ◦ g) ◦ f and h ◦ (g ◦ f) are equal.

- 6. Suppose that f : A → B and g : B → C are functions and that g ◦ f is one-to-one.
  - a) Prove that f is one-to-one. (Hint: use a proof by contradiction.)
  - b) Find a specific example that shows that g is not necessarily one-to-one.

- 7. Suppose that f : A → B and g : B → C, and suppose that the composition g ◦ f is an onto function.
  - a) Prove that g is an onto function.
  - b) Find a specific example that shows that f is not necessarily onto.

## 2.5 Application: Programming with Functions

Functions are fundamental in computer programming, although not everything in programming that goes by the name of “function” is a function according to the mathematical definition.

In computer programming, a function is a routine that is given some data as input and that will calculate and return an answer based on that data. For example, in the C++ programming language, a function that calculates the square of an integer could be written

```
int square(int n) {
    return n*n;
}
```

In C++, int is a data type. From the mathematical point of view, a data type is a set. The data type int is the set of all integers that can be represented as 32-bit binary numbers. Mathematically, then, int ⊆ Z.


## Exercises

- 1. For each of the following C++ function prototypes, translate the prototype into a standard mathematical function specification, such as $func: float \rightarrow int$.
  - a) int strlen(string s)
  - b) float pythag(float x, float y)
  - c) int round(float x)
  - d) string substring(string s, int n, int m)
  - e) string unlikely() int (string)
  - f) int h(int f(int), int g(int))

- 2. Write a C++ function prototype for a function that belongs to each of the following sets.
  - a) string -> string
  - b) bool -> float
  - c) float^{int}

- 3. It is possible to define new types in C++. For example, the definition

```
struct point {
    float x;
    float y;
}
```

defines a new type named point. A value of type point contains two values of type float. What mathematical operation corresponds to the construction of this data type? Why?

- 4. Let square, sum, and monomial be the JavaScript functions described in this section. What is the value of each of the following?
  - a) sum(square, 2, 4)
  - b) sum(monomial(5,2), 1, 3)
  - c) monomial(square(2), 7)
  - d) sum(function(n) { return 2 * n; }, 1, 5)
  - e) square(sum(monomial(2,3), 1, 2))

- 5. Write a JavaScript function named compose that computes the composition of two functions. That is, compose(f, g) is f∘g, where f and g are functions of one parameter. Recall that f∘g is the function defined by (f∘g)(x) = f(g(x)).

### 2.6 Counting Past Infinity

As children, we all learned to answer the question “How many?” by counting with numbers: 1, 2, 3, 4, .... But the question of “How many?” was asked and answered long before the abstract concept of number was invented. The answer can be given in terms of “as many as.” How many cousins do you have? As many cousins as I have fingers on both hands. How many sheep do you own? As many sheep as there are notches on this stick. How many baskets of wheat must I pay in taxes? As many baskets as there are stones in this box. The question of how many things are in one collection of objects is answered by exhibiting another, more convenient, collection of objects that has just as many members.

In set theory, the idea of one set having just as many members as another set is expressed in terms of **one-to-one correspondence**. A one-to-one correspondence between two sets $A$ and $B$ pairs each element of $A$ with an element of $B$ in such a way that every element of $B$ is paired with one and only one element of $A$. The process of counting, as it is learned by children, establishes a one-to-one correspondence between a set of $n$ objects and the set of numbers from 1 to $n$. The rules of counting are the rules of one-to-one correspondence: Make sure you count every object, make sure you don't count the same object more than once. That is, make sure that each object corresponds to **one** and **only one** number. Earlier in this chapter, we used the fancy name "bijective function" to refer to this idea, but we can now see it as an old, intuitive way of answering the question "How many?"

In counting, as it is learned in childhood, the set $\{1, 2, 3, ..., n\}$ is used as a typical set that contains $n$ elements. In mathematics and computer science, it has become more common to start counting with zero instead of with one, so we define the following sets to use as our basis for counting:

- $N_0 = \emptyset$, a set with 0 elements
- $N_1 = \{0\}$, a set with 1 element
- $N_2 = \{0, 1\}$, a set with 2 elements
- $N_3 = \{0, 1, 2\}$, a set with 3 elements
- $N_4 = \{0, 1, 2, 3\}$, a set with 4 elements

and so on. In general, $N_n = \{0, 1, 2, ..., n-1\}$ for each $n \in \mathbb{N}$. For each natural number $n$, $N_n$ is a set with $n$ elements. Note that if $n \neq m$, then there is no one-to-one correspondence between $N_n$ and $N_m$. This is obvious, but like many obvious things is not all that easy to prove rigorously, and we omit the argument here.

**Theorem 2.6.** For each $n \in \mathbb{N}$, let $N_n$ be the set $N_n = \{0, 1, ..., n-1\}$. If $n \neq m$, then there is no bijective function from $N_m$ to $N_n$.

We can now make the following definitions:

**Definition 2.3.** A set $A$ is said to be **finite** if there is a one-to-one correspondence between $A$ and $N_n$ for some natural number $n$. We then say that $n$ is the **cardinality** of $A$. The notation $|A|$ is used to indicate the cardinality of $A$. That is, if $A$ is a finite set, then $|A|$ is the natural number $n$ such that there is a one-to-one correspondence between $A$ and $N_n$. A set that is not finite is said to be **infinite**. That is, a set $B$ is infinite if for every $n \in \mathbb{N}$, there is **no** one-to-one correspondence between $B$ and $N_n$.

Fortunately, we don't always have to count every element in a set individually to determine its cardinality. Consider, for example, the set $A \times B$, where $A$ and $B$ are finite sets. If we already know $|A|$ and $|B|$, then we can determine $|A \times B|$ by computation, without explicit counting of elements. In fact, $|A \times B| = |A| \cdot |B|$. The cardinality of the cross product $A \times B$ can be computed by multiplying the cardinality of $A$ by the cardinality of $B$. To see why this is true, think of how you might count the elements of $A \times B$. You could put the elements into piles, where all the ordered pairs in a pile have the same first coordinate. There are as many piles as there are elements of $A$, and each pile contains as many ordered pairs as there are elements of $B$. That is, there are $|A|$ piles, with $|B|$ items in each. By the definition of multiplication, the total number of items in all the piles is $|A| \cdot |B|$. A similar result holds for the cross product of more than two finite sets. For example, $|A \times B \times C| = |A| \cdot |B| \cdot |C|$.

It's also easy to compute $|A \cup B|$ in the case where $A$ and $B$ are disjoint finite sets. (Recall that two sets $A$ and $B$ are said to be disjoint if they have no members in common, that is, if $A \cap B = \emptyset$.) Suppose $|A| = n$ and $|B| = m$. If we wanted to count the elements of $A \cup B$, we could use the $n$ numbers from $0$ to $n - 1$ to count the elements of $A$ and then use the $m$ numbers from $n$ to $n + m - 1$ to count the elements of $B$. This amounts to a one-to-one correspondence between $A \cup B$ and the set $N_{n+m}$. We see that $|A \cup B| = n + m$. That is, for disjoint finite sets $A$ and $B$, $|A \cup B| = |A| + |B|$.

What about $A \cup B$, where $A$ and $B$ are not disjoint? We have to be careful not to count the elements of $A \cap B$ twice. After counting the elements of $A$, there are only $|B| - |A \cap B|$ new elements in $B$ that still need to be counted. So we see that for any two finite sets $A$ and $B$, $|A \cup B| = |A| + |B| - |A \cap B|$.

What about the number of subsets of a finite set $A$? What is the relationship between $|A|$ and $|P(A)|$? The answer is provided by the following theorem.

**Theorem 2.7.** A finite set with cardinality $n$ has $2^n$ subsets.

**Proof.** Let $P(n)$ be the statement “Any set with cardinality $n$ has $2^n$ subsets.” We will use induction to show that $P(n)$ is true for all $n \in \mathbb{N}$. Base case: For $n = 0$, $P(n)$ is the statement that a set with cardinality $0$ has $2^0$ subsets. The only set with $0$ elements is the empty set. The empty set has exactly $1$ subset, namely itself. Since $2^0 = 1$, $P(0)$ is true.

Inductive case: Let $k$ be an arbitrary element of $\mathbb{N}$, and assume that $P(k)$ is true. That is, assume that any set with cardinality $k$ has $2^k$ elements. (This is the induction hypothesis.) We must show that $P(k + 1)$ follows from this assumption. That is, using the assumption that any set with cardinality $k$ has $2^k$ subsets, we must show that any set with cardinality $k + 1$ has $2^{k+1}$ subsets.

Let $A$ be an arbitrary set with cardinality $k + 1$. We must show that $|P(A)| = 2^{k+1}$. Since $|A| > 0$, $A$ contains at least one element. Let $x$ be some element of $A$, and let $B = A \setminus \{x\}$. The cardinality of $B$ is $k$, so we have by the induction hypothesis that $|P(B)| = 2^k$. Now, we can divide the subsets of $A$ into two classes: subsets of $A$ that do not contain $x$ and subsets of $A$ that do contain $x$. Let $Y$ be the collection of subsets of $A$ that do not contain $x$, and let $X$ be the collection of subsets of $A$ that do contain $x$. $X$ and $Y$ are disjoint, since it is impossible for a given subset of $A$ both to contain $Y$ and to not contain $x$. It follows that $|P(A)| = |X \cup Y| = |X| + |Y|$.

Now, a member of $Y$ is a subset of $A$ that does not contain $x$. But that is exactly the same as saying that a member of $Y$ is a subset of $B$. So $Y = P(B)$, which we know contains $2^k$ members. As for $X$, there is a one-to-one correspondence between $P(B)$ and $X$. Namely, the function $f : P(B) \to X$ defined by $f(C) = C \cup \{x\}$ is a bijective function. (The proof of this is left as an exercise.) From this, it follows that $|X| = |P(B)| = 2^k$. Putting these facts together, we see that $|P(A)| = |X| + |Y| = 2^k + 2^k = 2 \cdot 2^k = 2^{k+1}$. This completes the proof that $|P(A)| = 2^{|A|}$.

We have seen that the notation $A^B$ represents the set of all functions from $B$ to $A$. Suppose $A$ and $B$ are finite, and that $|A| = n$ and $|B| = m$. Then $|A^B| = n^m = |A|^{|B|}$. (This fact is one of the reasons why the notation $A^B$ is reasonable.) One way to see this is to note that there is a one-to-one correspondence between $A^B$ and a cross product $A \times A \times \dots \times A$, where the number of terms in the cross product is $m$. (This will be shown in one of the exercises at the end of this section.) It follows that $|A^B| = |A| \cdot |A| \cdots |A| = n \cdot n \cdots n$, where the factor $n$ occurs $m$ times in the product. This product is, by definition, $n^m$.

This discussion about computing cardinalities is summarized in the following theorem:

### Theorem 2.8: Let $A$ and $B$ be finite sets. Then

- $|A \times B| = |A| \cdot |B|$.
- $|A \cup B| = |A| + |B| - |A \cap B|$.

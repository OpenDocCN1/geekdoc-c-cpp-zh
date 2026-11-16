~(a \in A).

It is possible for a set to be empty, that is, to contain no elements whatsoever. Since a set is completely determined by the elements that it contains, there is only one set that contains no elements. This set is called the **empty set**, and it is denoted by the symbol $\emptyset$. Note that for any element $a$, the statement $a \in \emptyset$ is false. The empty set, $\emptyset$, can also be denoted by an empty pair of braces, $\{ \}$.

If $A$ and $B$ are sets, then, by definition, $A$ is equal to $B$ if and only if they contain exactly the same elements. In this case, we write $A = B$. Using the notation of predicate logic, we can say that $A = B$ if and only if $\forall x(x \in A \leftrightarrow x \in B)$.

Suppose now that $A$ and $B$ are sets such that every element of $A$ is an element of $B$. In that case, we say that $A$ is a **subset** of $B$, i.e. $A$ is a subset of $B$ if and only if $\forall x(x \in A \rightarrow x \in B)$. The fact that $A$ is a subset of $B$ is denoted by $A \subseteq B$. Note that $\emptyset$ is a subset of every set $B$: $x \in \emptyset$ is false for any $x$, and so given any $x$, $(x \in \emptyset \rightarrow x \in B)$ is true for all $x$.

If $A = B$, then it is automatically true that $A \subseteq B$ and that $B \subseteq A$. The converse is also true: If $A \subseteq B$ and $B \subseteq A$, then $A = B$. This follows from the fact that for any $x$, the statement $(x \in A \leftrightarrow x \in B)$ is logically equivalent to the statement $(x \in A \rightarrow x \in B) \land (x \in B \rightarrow x \in A)$. This fact is important enough to state as a theorem.

**Theorem 2.1.** Let $A$ and $B$ be sets. Then $A = B$ if and only if both $A \subseteq B$ and $B \subseteq A$.

This theorem expresses the following advice: If you want to check that two sets, $A$ and $B$, are equal, you can do so in two steps. First check that every element of $A$ is also an element of $B$, and then check that every element of $B$ is also an element of $A$.

If $A \subseteq B$ but $A \neq B$, we say that $A$ is a **proper subset** of $B$. We use the notation $A \subsetneq B$ to mean that $A$ is a proper subset of $B$. That is, $A \subseteq B$ if and only if $A \subseteq B \neq A \neq B$. We will sometimes use $A \supseteq B$ as an equivalent notation for $B \subseteq A$ and $A \supsetneq B$ as an equivalent for $B \subsetneq A$.

A set can contain an infinite number of elements. In such a case, it is not possible to list all the elements in the set. Sometimes the ellipsis "..." is used to indicate a list that continues on infinitely. For example, $\mathbb{N}$, the set of natural numbers, can be specified as

$\mathbb{N} = \{0, 1, 2, 3, ...\}$

However, this is an informal notation, which is not really well-defined, and it should only be used in cases where it is clear what it means. It's not
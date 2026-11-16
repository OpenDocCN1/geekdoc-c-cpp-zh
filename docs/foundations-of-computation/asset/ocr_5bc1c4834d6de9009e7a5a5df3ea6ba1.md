# 2.1. BASIC CONCEPTS

Now that we have a way to express a wide variety of sets, we turn to operations that can be performed on sets. The most basic operations on sets are **union** and **intersection**. If A and B are sets, then we define the union of A and B to be the set that contains all the elements of A together with all the elements of B. The union of A and B is denoted by $A \cup B$.

$A \cup B = \{x \mid x \in A \lor x \in B\}$.

The intersection of A and B is defined to be the set that contains every entity that is both a member of A and a member of B. The intersection of A and B is denoted by $A \cap B$. Formally,

$A \cap B = \{x \mid x \in A \land x \in B\}$.

An entity gets into $A \cup B$ if it is in either A or B. It gets into $A \cap B$ if it is in both A and B. Note that the symbol for the logical “or” operator, $\lor$, is similar to the symbol for the union operator, $\cup$, while the logical “and” operator, $\land$, is similar to the intersection operator, $\cap$.

The **set difference** of two sets, A and B, is defined to be the set of all entities that are members of A but are not members of B. The set difference of A and B is denoted by $A \setminus B$. The idea is that $A \setminus B$ is formed by starting with A and then removing any element that is also found in B. Formally,

$A \setminus B = \{x \mid x \in A \land x \notin B\}$.

Union and intersection are clearly commutative operations. That is, $A \cup B = B \cup A$ and $A \cap B = B \cap A$ for any sets A and B. However, set difference is not commutative. In general, $A \setminus B \neq B \setminus A$.

Suppose that $A = \{a, b, c\}$, that $B = \{b, d\}$, and that $C = \{d, e, f\}$. Then we can apply the definitions of union, intersection, and set difference to compute, for example, that:

$A \cup B = \{a, b, c, d\}$
$A \cap B = \{b\}$
$A \setminus B = \{a, c\}$

$A \cup C = \{a, b, c, d, e, f\}$
$A \cap C = \emptyset$
$A \setminus C = \{a, b, c\}$

In this example, the sets A and C have no elements in common, so that $A \cap C = \emptyset$. There is a term for this: Two sets are said to be **disjoint** if they have no elements in common. That is, for any sets A and B, A and B are said to be disjoint if and only if $A \cap B = \emptyset$.

Of course, the set operations can also be applied to sets that are defined by predicates. For example, let L(x) be the predicate “x is lucky,” and let W(x) be the predicate “x is wise,” where the domain of discourse for each
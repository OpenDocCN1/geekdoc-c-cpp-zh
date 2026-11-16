
$N = |V| + 1$. Consider all possible parse trees for the grammar $G$ with height less than or equal to $N$. (Include parse trees with any non-terminal symbol as root, not just parse trees with root $S$.) There are only finitely many such parse trees, and therefore there are only finitely many distinct strings that are the yields of such parse trees. Let $K$ be an integer which is greater than the length of any such string.

Now suppose that $w$ is any string in $L$ whose length is greater than or equal to $K$. Then any parse tree for $w$ must have height greater than $N$. (This follows since $|w| \ge K$ and the yield of any parse tree of height $\le N$ has length less than $K$.) Consider a parse tree for $w$ of minimal size, that is one that contains the smallest possible number of nodes. Since the height of this parse tree is greater than $N$, there is at least one path from the root of the tree to tip of a branch of the tree that has length greater than $N$. Consider the longest such path. The symbol at the tip of this path is a terminal symbol, but all the other symbols on the path are non-terminal symbols. There are at least $N$ such non-terminal symbols on the path. Since the number of different non-terminal symbols is $|V|$ and since $N = |V| + 1$, some non-terminal symbol must occur twice on the path. In fact, some non-terminal symbol must occur twice among the bottommost $N$ non-terminal symbols on the path. Call this symbol $A$. Then we see that the parse tree for $w$ has the form here:

![](img/e1667d904eba93816cbfc3a4b0128062_217_0.png)

The structure of this tree breaks the string $w$ into five substrings, as shown in the above diagram. We then have $w = uxyzv$. It only remains to show that $x, y,$ and $z$ satisfy the three requirements stated in the theorem.

Let $T$ refer to the entire parse tree, let $T_1$ refer to the parse tree whose root is the upper $A$ in the diagram, and let $T_2$ be the parse tree whose root is the lower $A$ in the diagram. Note that the height of $T_1$ is less than or equal to N. (This follows from two facts: The path shown in T1 from its root to its base has length less than or equal to N, because we chose the two occurrences of A to be among the N bottommost non-terminal symbols along the path in T from its root to its base. We know that there is no longer path from the root of T1 to its base, since we chose the path in T to be the longest possible path from the root of T to its base.) Since any parse tree with height less than or equal to N has yield of length less than K, we see that |xyz| < K.

If we remove T1 from T and replace it with a copy of T2, the result is a parse tree with yield uvy, so we see that the string uvy is in the language L. Now, suppose that both x and z are equal to the empty string. In that case, w = uvy, so the tree we have created would be another parse tree for w. But this tree is smaller than T, so this would contradict the fact that T is the smallest parse tree for w. We see that x and z cannot both be the empty string.

If we remove T2 from T and replace it with a copy of T1, the result is a parse tree with yield ux^2 y z^2 v, so we see that ux^2 y z^2 v ∈ L. The two parse trees that we have created look like this:

![](img/e1667d904eba93816cbfc3a4b0128062_218_0.png)

Furthermore, we can apply the process of replacing T2 with a copy of T1 to the tree on the right above to create a parse tree with yield ux^3 y z^3 v. Continuing in this way, we see that ux^n y z^n v ∈ L for all n ∈ N. This completes the proof of the theorem.

Since this theorem guarantees that all context-free languages have a certain property, it can be used to show that specific languages are not context-free. The method is to show that the language in question does not have the property that is guaranteed by the theorem. We give two examples.

## Corollary 4.8. Let \( L \) be the language \(\{a^n b^n c^n \mid n \in \mathbb{N}\}\). Then \( L \) is not a context-free language.

### Proof. We give a proof by contradiction. Suppose that \( L \) is context-free. Then, by the Pumping Lemma for Context-free Languages, there is an integer \( K \) such that every string \( w \in L \) with \( |w| \ge K \) can be written in the form \( w = uxyzv \) where \( x \) and \( z \) are not both empty; \( |xyz| < K \), and \( ux^i y z^i v \in L \) for every \( n \in \mathbb{N} \).

Consider the string \( w = a^K b^K c^K \), which is in \( L \), and write \( w = uxyzv \), where \( u, x, y, z, \) and \( v \) satisfy the stated conditions. Since \( |xyz| < K \), we see that if \( xyz \) contains an \( a \), then it cannot contain a \( c \). And if it contains a \( c \), then it cannot contain an \( a \). It is also possible that \( xyz \) is made up entirely of \( b \)’s. In any of these cases, the string \( ux^2 y z^2 v \) cannot be in \( L \), since it does not contain equal numbers of \( a \)’s, \( b \)’s, and \( c \)’s. But this contradicts the fact that \( ux^i y z^i v \in L \) for all \( n \in \mathbb{N} \). This contradiction shows that the assumption that \( L \) is context-free is incorrect.

## Corollary 4.9. Let \( \Sigma \) be any alphabet that contains at least two symbols. Let \( L \) be the language over \( \Sigma \) defined by \( L = \{ss \mid s \in \Sigma^*\} \). Then \( L \) is not context-free.

### Proof. Suppose, for the sake of contradiction, that \( L \) is context-free. Then, by the Pumping Lemma for Context-free Languages, there is an integer \( K \) such that every string \( w \in L \) with \( |w| \ge K \) can be written in the form \( w = uxyzv \) where \( x \) and \( z \) are not both empty; \( |xyz| < K \), and \( ux^i y z^i v \in L \) for every \( n \in \mathbb{N} \).

Let \( a \) and \( b \) represent distinct symbols in \( \Sigma \). Let \( s = a^K b^K b a^K \) and let \( w = ss = a^K b^K b a^K b a^K b^K b a^K \), which is in \( L \). Write \( w = uxyzv \), where \( u, x, y, z, \) and \( v \) satisfy the stated conditions.

Since \( |xyz| < K \), \( x \) and \( z \) can, together, contain no more than one \( b \). If either \( x \) or \( z \) contains a \( b \), then \( ux^2 y z^2 v \) contains exactly five \( b \)’s. But any string in \( L \) is of the form \( rr \) for some string \( r \) and so contains an even number of \( b \)’s. The fact that \( ux^2 y z^2 v \) contains five \( b \)’s contradicts the fact that \( ux^i y z^i v \in L \). So, we get a contradiction in the case where \( x \) or \( z \) contains a \( b \).

Now, consider the case where \( x \) and \( z \) consist entirely of \( a \)’s. Again since \( |xyz| < K \), we must have either that \( x \) and \( z \) are both contained in the same group of \( a \)’s in the string \( a^K b^K b a^K b a^K b^K b a^K \), or that \( x \) is contained in one group of \( a \)’s and \( z \) is contained in the next. In either case, it is easy to check that the string $ux^2 y z^2 v$ is no longer of the form $rr$ for any string $r$, which contradicts the fact that $ux^2 y z^2 v \in L$.

Since we are led to a contradiction in every case, we see that the assumption that $L$ is context-free must be incorrect.

Now that we have some examples of languages that are not context-free, we can settle some other questions about context-free languages. In particular, we can show that the intersection of two context-free languages is not necessarily context-free and that the complement of a context-free language is not necessarily context-free.

## **Theorem 4.10.** The intersection of two context-free languages is not necessarily a context-free language.

### Proof. To prove this, it is only necessary to produce an example of two context-free languages $L$ and $M$ such that $L \cap M$ is not a context-free languages. Consider the following languages, defined over the alphabet $\Sigma = \{a, b, c\}$:

```
$L = \{a^n b^n c^m \mid n \in \mathbb{N} \text{ and } m \in \mathbb{N}\}$
$M = \{a^m b^m c^n \mid n \in \mathbb{N} \text{ and } m \in \mathbb{N}\}$
```

Note that strings in $L$ have equal numbers of $a$'s and $b$'s while strings in $M$ have equal numbers of $b$'s and $c$'s. It follows that strings in $L \cap M$ have equal numbers of $a$'s, $b$'s, and $c$'s. That is,

```
$L \cap M = \{a^n b^n c^n \mid n \in \mathbb{N}\}$
```

We know from the above theorem that $L \cap M$ is not context-free. However, both $L$ and $M$ are context-free. The language $L$ is generated by the context-free grammar

```
$S \longrightarrow TC$
$C \longrightarrow cC$
$C \longrightarrow \varepsilon$
$T \longrightarrow aTb$
$T \longrightarrow \varepsilon$
```

and $M$ is generated by a similar context-free grammar.

## **Corollary 4.11.** The complement of a context-free language is not necessarily context-free.

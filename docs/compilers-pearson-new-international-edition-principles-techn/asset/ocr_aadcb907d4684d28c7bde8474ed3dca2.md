# 5.5. IMPLEMENTING L-ATTRIBUTED SDD’S

+   1. Start with the SDT constructed as in Section 5.4.5, which places embedded actions before each nonterminal to compute its inherited attributes and an action at the end of the production to compute synthesized attributes.

+   2. Introduce into the grammar a marker nonterminal in place of each embedded action. Each such place gets a distinct marker, and there is one production for any marker $M$, namely $M \to \epsilon$.

+   3. Modify the action $a$ if marker nonterminal $M$ replaces it in some production $A \to \alpha\{a\}\beta$, and associate with $M \to \epsilon$ an action $a'$ that

+   (a) Copies, as inherited attributes of $M$, any attributes of $A$ or symbols of $\alpha$ that action $a$ needs.

+   (b) Computes attributes in the same way as $a$, but makes those attributes be synthesized attributes of $M$.

This change appears illegal, since typically the action associated with production $M \to \epsilon$ will have to access attributes belonging to grammar symbols that do not appear in this production. However, we shall implement the actions on the LR parsing stack, so the necessary attributes will always be available a known number of positions down the stack.

**Example 5.25:** Suppose that there is a production $A \to BC$ in an LL grammar, and the inherited attribute $B.i$ is computed from inherited attribute $A.i$ by some formula $B.i = f(A.i)$. That is, the fragment of an SDT we care about is

$$A \to \{B.i = f(A.i);\}\ B\ C$$

We introduce marker $M$ with inherited attribute $M.i$ and synthesized attribute $M.s$. The former will be a copy of $A.i$ and the latter will be $B.i$. The SDT will be written

$$A \to M\ B\ C$$
$$M \to \{M.i = A.i;\ M.s = f(M.i);\}$$

Notice that the rule for $M$ does not have $A.i$ available to it, but in fact we shall arrange that every inherited attribute for a nonterminal such as $A$ appears on the stack immediately below where the reduction to $A$ will later take place. Thus, when we reduce to $M$, we shall find $A.i$ immediately below it, from where it may be read. Also, the value of $M.s$, which is left on the stack along with $M$, is really $B.i$ and properly is found right below where the reduction to $B$ will later occur. □

**Example 5.26:** Let us turn the SDT of Fig. 5.28 into an SDT that can operate with an LR parser of the revised grammar. We introduce a marker $M$ before $C$ and a marker $N$ before $S_1$, so the underlying grammar becomes
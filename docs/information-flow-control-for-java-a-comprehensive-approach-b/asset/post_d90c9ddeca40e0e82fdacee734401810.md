
# CHAPTER 4. INFORMATION FLOW CONTROL

between all nodes in $dom(P)$ and all nodes in $dom(R)$ is satisfied and thus equivalent.

Computing a minimal fixpoint for $S(x)$ from constraints involving $S$ and subsequent checking constraints involving $P$ (backward propagation) is therefore equivalent to computing $S$'s fixpoint from $S$ and $P$ with subsequent checking of $R$-constraints (forward propagation).

## 4.7 Declassification

IFC as described is far too simplistic because in some situations one might accept that information with a higher security level to a "lower" channel. For instance, information may be published after statistical anonymization, secret data may be transferred over the Internet using encryption, and in electronic commerce needs to release secret data after its purchase. Declassification allows to lower the security level of incoming information as a means to relax the security policy. The password checking method presented earlier is another example: as passwords are encrypted, it does not matter information from the password table to the visible result, and hence a declassification to public at node 14 (where the illegal flow was discovered, section 4.5) is appropriate – a password-based authentication mechanism necessarily reveals something about the secret password.$^{17}$

When allowing such exceptions to the basic security policy, one major concern is that exceptions might introduce unforeseen information release. Several approaches for a semantics of declassification were proposed, each focusing on certain aspects of "secure" declassification. The current state of the art describes four dimensions of declassification according to where, who, when and what can be declassified [SS05] from that, some basic principles are presented that can serve as "sanity checks" for semantic security policies allowing declassifications. These principles are 1. semantic consistency, which is basically invariance without semantics-preserving transformations; 2. conservatism, i.e. without declassification, security reduces to noninterference; 3. monotonicity of release, which states that adding declassification should not render a secure program insecure; 4. non-occlusion which requires that declassification operations cannot mask other information release.

### 4.7.1 Declassification in SDGs

We model declassification by specifying certain SDG nodes to be declassification nodes. Let $D \subseteq N$ be the set of declassification nodes. A declassification node $x \in D$ must have a required and a provided security level:

```
$x \in D \Rightarrow (x \in dom(P) \cap dom(R)) \wedge (R(x) \geq P(x)) \quad (4.18)$
```

Information revealing $x$ with a maximal security level $R(x)$ is lower (de-classified) to $P(x)$ (note that $R(x) \not\geq P(x)$ does not make any sense,

> $^{17}$We all know that password crackers can exploit this approach in case weak passwords are used, hence just adding a declassification seems naive. Additional techniques to protect the table are needed.

as declassification should lower a level, not heighten it). Now a path from node $y$ to $a$ with $P(y) > R(a)$ is not a violation, if there is a declassification node $x \in D$ on the path with $P(y) \leq R(x)$ and $P(x) \leq R(a)$ (assuming there is no other declassification node on path). The actual security level $S(x)$ will be between $P(x)$ and $R(x)$. In the password example, $D=\{14\}, R(14)=secret, P(14)=public$; and the illegal flow described earlier disappears.

According to Sabelfeld and Sands [SS05], for expressing information release is describing which information is released: the set D of declassification nodes correspond to code locations—moreover, in the implemented system we have to specify the code locations, which are mapped to declassification nodes by the system.

In terms of propagation, a declassification simply changes the computation of Equation (4.11) must be extended as follows:

```
$S(x) \geq \begin{cases} P(x) & \text{if } x \in D \ P(x) \sqcup S(y) & \text{otherwise} \end{cases} \quad (4.19)$
```

Thus the inclusive security levels are ignored and replaced by the declassification security level.

Of course, (4.8) is valid for non-declassification nodes, but for $x \in D$ it must be modified by $S(x)$ as declassified:

```
$\forall x \in dom(R) \setminus D : R(x) \geq S(x) \\forall x \in D : R(x) \geq \bigcup_{y \in pred(x)} S(y) \quad (4.20)$
```

which expresses that normal flow of $S$ is interrupted at $x \in D$.

**Definition 4.3.** Let a program's SDG be given. The program monitors confidentiality, if for all $a \in dom(R)$ equations (4.19) and (4.20) are satisfied.

**Theorem 4.6.** For any $a \notin D$, Algorithm 7 generates a set of constraints which are correct and complete, and thus enforce confidentiality according to Definition 4.3.

**Proof.** We have already argued (proof for Theorem 4.4) for non-declassification nodes the generated constraints correspond exactly to equations (4.8) and (4.7), and to the non-declassification cases in equations (4.19) and (4.20). For declassification nodes $d \in D$, Algorithm 7 no longer generates constraints $S(w) \leq S(d)$, which is indeed required by (4.19), case $x \in D$. Instead it generates $R(d) \geq S(w)$ for $w \in pred(d)$, which is equivalent to the constraints in (4.20), case $x \in D$. Furthermore, it generates $S(d) \geq P(d)$ which is exactly required by (4.19), case $x \in D$.

Thus Algorithm 7 generates exactly the constraints required by (4.19) and (4.20). Because they have the same fixpoint, fulfill the requirements of Definition 4.3.

In case $D = \varnothing$, Algorithm 7 by theorem 4.4 checks noninterference without declassification. Thus we obtain free for the

**Corollary 4.7** (Conservativity of Declassification). Algorithm 7 is conservative, that is, without declassification it reduces to standard noninterference.

Let us finally point out a few special situations. It is explicitly allowed to have two or more declassification on one specific path, e. g. $x 	o^* d_1 	o^* d_2 	o^* y$. But this only makes sense if $P(d_1) \leq R(d_2)$, otherwise no legal flow is possible on the path, and $P(d_2) \leq P(d_1)$, as the second declassification is redundant.

In case there are several declassifications on paths from $x$ to $y$, by example $x 	o^* d_1 	o^* y 	o^* d_2 	o^* y, x 	o^* d_3 	o^* y,\dots$, it is possible to approximate all these declassifications conservatively by introducing a new declassification $R(d) = \bigsqcup R(d)$ and $P(d)$. Any flow legal through $d$ is also legal through (one of) the $d_i$, hence the approximation will not introduce new (illegal) flows. This observation seems unmotivated, but will be the source for some more precise IFC, as described in section 4.8.

## 4.7 Monotonicity of Release

Another useful property is monotonicity of release, which states that introduction of an additional declassification should not make previously secure insecure (i.e. generate illegal flow). Formally, this can be defined as follows:

**Definition 4.4.** Let a program satisfy confidentiality according to Definition 4.3 and let $d \in N$ where $d \in Dom(R) \cup Dom(P)$. Replace $d$ by $d' \in D$ where $d'$ has the same connecting edges as $d$, but $d'$ is annotated with $R$ and $P$. Recompute the actual security levels according to (4.19), $S'(x)$ for $x \in N$. Declassification of $d'$ respects monotonicity of release, if equation (4.20) still holds for all $S'(x)$.

**Theorem 4.8.** If $R'(d') \geq \bigsqcup_{y \in pred(d)} S(y)$, and $P(d') \leq \bigsqcup_{y \in pred(d)} S(y)$, then for $x \in N, S'(x) \leq S(x)$.

The first premise avoids that prevents illegal flow (where $R'(d') = \mathcal{T}$ as $d \notin Dom(R)$ is blocked by a too low arbitrary $R(d)$). Note that $P(d) \leq R(d)$ is required anyway in equation (4.18). The above premise is more precise and avoids that a declassification generates new illegal flows as the outgoing declassification is too high, or the incoming limit too low. In practice, both requirements are equal and do not restrict declassification.

**Proof.** In the optimal SDG, $\bigsqcup_{y \in pred(d)} S(y) \leq S(d) \leq S'(d) = \bigsqcup_{y \in pred(d)} S(y)$, in the new SDG $P'(d) \leq P(d) \leq S'(d) = \bigsqcup_{y \in pred(d)} S(y)$ by assumption and equation 4.19. Furthermore, $S'(d) \leq S(d) \leq \bigsqcup_{y \in pred(d)} S(y) \geq S'(y) = S(y)$ for all $y \in succ(d)$. Here $S(y) \geq \bigsqcup_{y \in pred(y)} S(y) \geq S'(y)$ works for the successors of $y$. By induction $^{18}$ $S'(x) \leq S(x)$ for all $x$.

> $^{18}$technically, a well-known fixpoint induction

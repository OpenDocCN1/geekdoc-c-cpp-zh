# 2.6 RELATED WORK

The first precedential $p_i$ in $P$ is a return
As statements in Java can - again - only access a memory cell via a parameter or local variable that was returned, we know that there exists an access path $A=(v, f_1, \dots, f_d)$ by which $p_i$ has gained access to mem in execution $E$.

+   a) For regular field modification statement we know by equation (2.4) that there exists an access path $A' \in GMod(method(p_i))$ because $p_i$ is a definition.
b) For an actual-out-parameter of a method call $A=\{f_1, \dots, f_d\} \in CMod(method(p_i))$, at $p_i$ we have access to equation (2.10) access path $A'=\{f'_1, \dots, f'_d\}@A \in GMod(method(p_i))$ for $A$ to be visible after $method(p_i)$ returns.

+   c) For a formal-path $A=\{f_1, \dots, f_d\} \in GRef(method(p_i))$, at $p_i$ (which also constitutes $A$) is corresponding to the access path $A' \in CMod(method(p_i))$ (which exists as $p_i$ is synthetic, so $p_i$ is synthetic, and $p_i=correspondingCall(p_i)$) due to equation (2.9). Thus, with equation (2.7) we have an access path $C \in CMod(method(p_i)), correspondingCall(p_i)$ with $C=\{w', f'_1, \dots, f'_d\}$ which defines a parameter at $p_{i+1}$.
Thus we apply the induction hypothesis on path $P'=\{p_{i+1}, \dots, p_n\}$. Then $\exists$ path $S=\{s_1, \dots, s_m=p_n\}$ where $label(s_i, s_{i+1}) \in \{DD, PI\}$, and a data dependence $(p_i, A')$ we get the claim.

Corollary 2.4 (Safety of Unfolding Criterion in Definition 2.5). Using $IRef/$ and $IMod/$, instead of $IRef$ and $IMod$ is sound.

Proof. The proofs of Theorem 2.2 and Lemma 2.3 do not rely on the access path $A$ of the execution $E$, but on an abstraction $A'$ that has (at least) the same relying relation and ends with the same field name. Thus, using the shortest location with the same field and aliasing relation, which is $IRef$/$IMod/$, is sufficient.

# 2.6 Related Work

Danicic et al. [DHHO07] present a lazy semantics for Weiser-program slicing (i.e. without using intermediate representations like dependence graphs) of a *while* language. This semantics allows program slicing to introduce termination (if a program slice may terminate while the original program does not, see [Wei84], so it is non-termination insensitive in the sense of Ranganath et al. [RAB*07]). Their semantics are consistent with program slicing and substitutive, allowing program transformations and software tasks like component reuse.

A formalization of program slicing allows comparison of various variants of program slicing has been given in Binkley et al. [BDG*06]. This theory allows
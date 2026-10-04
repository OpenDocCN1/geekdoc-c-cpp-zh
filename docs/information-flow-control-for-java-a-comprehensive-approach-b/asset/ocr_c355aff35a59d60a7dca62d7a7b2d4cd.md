# CHAPTER 2 DEPENDENCE GRAPHS AND SLICING FOR
OBJECT-ORIENTED LANGUAGES

ment,$^9$ and $\forall p_i \in \{p_2, \dots, p_n\}$ we have that $p_i$ is not a regular field assignment to statement memory, then $\exists p$ in $G$ with $S=(p_1=s_1, \dots, s_m=p_n)$ where label$(s_i, s_{i+1}) \in [DD, PI, PO].

Proof. Proof is an induction over the number $q$ of interprocedural statements in the execution trace $P$

**Base case: $q=0$ (intra-procedural case)** We have that $P=(p_1,\dots,p_n)$ is a subsequence of $E$ where $p_1$ defines memory cell mem and $p_n$ reads mem, thus $p_1 \in Def(f)$ and $p_n \in Ref(f)$ for field $f$ and may-aliases($base(p_1), base(p_n)$). As name of $p_i \in \{p_2, \dots, p_n\}$ refines memory mem in the execution, of $p_1$ reaches $p_n$ in the CFG and points-to($p_1$) $\cap$ points-to($p_n$) $
eq \emptyset$. Therefore definition 2.18 applies, such that we get a

**Inductive step: $q ightarrow q+1$

The last interprocedural statement $p_i$ in $P$ is a call

```
$ \dots p_n$
```

$p_1 \rightarrow \dots, p_i$: call

+   a) A regular field access statement in Java can only access a memory cell via variable$^{10}$, so we know that there exists an access path $A=\langle f_1, \dots, f_d angle$ through which $p_n$ has gained access to mem in execution. By equation, (2.3) access path $A' \in IRef(method(p_n))$ such that length of both access paths $A'$ and $A$ is an alias for mem.
nb) For an actual parameter $A=\langle act, f_1, \dots, f_n angle$ of a call statement $p_n$, where $A \in Ref(method(p_n))$, there must be a parameter form such that access path $A'=\langle f_1, \dots, f_g angle @A$ is an alias for mem due to equation (2.9).
c) If, $p_i$ is a return statement, then the use $A=\langle f_1, \dots, f_d angle$ at $p_n$ must be in $GMod(method(p_n))$. With equation (2.9), we get $A' \in Ref(method(p_n))$ with $A'=A$.

In all cases, with (2.6) we have an access $C \in Ref(method(p_1), p_i)$ which corresponds to $A'$, i.e. $C=\langle act, f_1, \dots, f_d angle$ $(f_d^g=f_d)$ which constitutes a use in $method(p_1)$. Now we can apply the induction hypothesis on the path $P'=(p_1,\dots,p_i)$ which yields a path $S=\langle p_1=s_1, \dots, s_m=p_i angle$ where label$(s_i, s_{i+1})$

> ^9A regular field access assignment statement is a bytecode that effectively manipulates the heap, in contrast to static field assignments induced by parameter passing.
^10Or static (global) variables, which are modeled as extra parameters in SDGs

60
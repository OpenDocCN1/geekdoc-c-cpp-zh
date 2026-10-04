# CHAPTER 4. INFORMATION FLOW CONTROL

The program contains P-annotations for input variables, and an R-annotation for the result value. Thus the list of passwords is secret, i.e. $P(3) = secret\nP(4) = secret$. The list of names and the parameter password is confidential, because they should not be visible to a user. Thus, $P(1) = confidential \wedge P(5) = confidential \wedge P(6) = confidential$.

No confidential or secret information will flow out of check, unless we require $R(14) = public$. Remember that the PDG has added dependences for exceptions (see Figure 4.5). In order to prevent an implicit flow from check to the calling method via uncaught exception, $m$ is annotated with $R(m) = public$. Thus an implicit flow via an uncaught exception, where the exception is on a secret variable, will occur.

Starting with these specifications for R and P, the actual security levels $S(x)$, as computed according to 4.13, are depicted in Figure 4.8 (for white, light for gray, and for secret¹²). Let us now apply the PDG-based confidentiality check. It turns out that $3 \in BS(14)$ where $R(14) = public, P(3) = secret$. The criterion fails. Identify a security violation: violated: $S(14) = secret \neq R(14)$, which (Figure 4.8) is violated. The chop $CH(3,14)$ contains all nodes contributing to the illegal flow.

It is unavoidable that match has be computed from secret information. Declaration was invented to handle such situations, and will be discussed later.

# 4.6 Inter-procedural propagation of security levels

Let us discuss interprocedural IPC. To understand the problem of sensitivity, consider the program fragment and its SDG in Figure 4.9. In this fragment, $P(secret) = P(1) = High, P(public) = P(2) = Low$, and $R(P) = R(5) = Low$. Let us first backward slices are computed just as in the interprocedural case, that is, all nodes which have a path to the point of interest are in the slice. This approach reaches interprocedural SDG edges like control or control dependences, and as a result will include the calling context. In the example, $3 \in BS(5)$ due to the SDG path $3 \rightarrow 3i \rightarrow a \rightarrow b \rightarrow 4o \rightarrow 5$ (where $3i$ is the actual parameter of the first call, and $4o$ is the return value of the second call). By equation (4.13), $S(4o) = S(5)=S(p) = High$, and $R(p) \neq S(p)$. However, semantically secret cannot influence p.

# 4.6.1 Context-Sensitive Slicing

To avoid such alarms, an approach based on context-sensitive slicing (see 2.2.2) must be used: not every SDG path is allowed in a slice, but only reachable paths. Realistic paths require that the actual parameter nodes to/a function, which are on the path, belong to the same call statement.¹³

> ¹²node 14 is only half shaded for the moment.
¹³more precisely, in-/out nodes must form a "matched parenthesis" structure, since calls can be nested.
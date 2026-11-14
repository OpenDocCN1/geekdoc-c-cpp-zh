The receive construct is typechecked using the [rBRANCH] rule. It expects an (external) branching session type &{...}, where each branch in the session type must match with a corresponding branch in the receive construct, where both the labels (1i) and payload types (Ti) correspond. Each receive branch is checked w.r.t. the common type T and a common residual session type S'. The types within each receive branch are computed using the pattern typing judgement, \(\Gamma \vdash_{pat} P : T \triangleright \Gamma'\), which assigns types to variables present in patterns (explained later in Fig. 6).

To ensure that all possible patterns are exhausted, we use Simple Patterns to filter out pattern structures such as lists and basic values. As a result, if a receive construct (contains exclusively simple patterns) is well-typed against the branching session type, then we are certain that any valid incoming messages can be matched with one of the available branches. This is further discussed later in Proposition 3. Simple patterns do not limit the expressivity of our language: complex patterns can still be expressed using a combination of (simple) receives and inner case constructs, which allow us to use patterns that do not block receives while postponing more specific patterns to the subsequent case matching.

**Definition 3.2 (Simple Patterns).** The predicate simplepat(p, T) only accepts patterns that exclusively contain variables and top-level tuples, eliminating the possibility of patterns with structures such as lists or basic values. It is defined as follows: simplepat(p, T) def = ((p = (x1, ..., xn) and T = (T1, ..., Tn)) or p = x)

**Example 3.1.** Consider the following receive construct (following the ?incr(number)... session type) which does not satisfy simplepat:

```
receive do {;incr,5}->... end
```

This can only accept messages of the form {;incr,5}, so other messages that are valid for the ?incr(number)... session type, e.g. {;incr,9}, cannot be processed, since not all valid patterns are exhausted. In contrast, simplepat limits us to branches such as the one below where the variable (called value) can accept any value:

```
receive do {;incr,value}->... end
```

Another crucial typing rule is [rCHOICE], which typechecks the sending of messages.

```
[rCHOICE]
\mu \in I   \forall j \in 1..n. { \Gamma \vdash_{exp} e_j : T_j }
-------------------------------------------------------
\Delta . \Gamma \vdash^w @{1_i(\bar{T}_i).S_i}_{i \in I} \triangleright \text{send}(w, \{;1_\mu, e_1, ..., e_n\}) : \{atom, \bar{T}_\mu\} < S_\mu
```

This rule requires an internal choice session type @{...}, where the label tagging the message to be sent must match with one of the labels (1mu) offered by the session choice. The message payloads also must match with the corresponding types associated with the label (Tmu of 1mu) stated via the expression typing judgement Gamma |- exp e : T (see Fig. 5). The resulting expression type of the send construct is equivalent to the type of message being sent, i.e., {;mu, e} has type atom(Tmu). The typing rule also checks the pid of the addressee of the send statement which must match with the dual pid (w) in the judgement itself to ensure that messages are only sent to the correct addressee.

```
\Delta (f(h) = S   \forall i \in 2..n. { \Gamma \vdash_{exp} e_i : T_i }
-----------------------------------------------------------
\Omega \vdash ... \Omega . \text{return\_type} = \bar{T}
```

Since public functions are decorated with a session type explicitly using the @session (or @dual) annotation, they are listed in dom(Delta). Calls to public functions are typechecked using the [rKNOWN CALL] rule, which verifies that the expected initial session type is equivalent to the function's known session type (S) known from the session typing environment, i.e., Delta(fh) = S. Without typechecking the function's body, which is done in rule [rMODULE], this rule ensures that the expected session type S is fully consumed, thus the residual type becomes end. Rule [rKNOWN CALL] also ensures that the pid (w) is preserved during a function call, by requiring it to be passed as a parameter and comparing it to the expected dual pid (i.e., Delta |- Gamma |- W > S > f(W, ...) : T < end).

```
\Sigma (fh) = \Omega
\Omega . \text{param\_args} = \bar{x} ... \Omega . \text{body} = t ... \Omega . \text{return\_type} = T
\forall i \in 2..n. { \Gamma \vdash_{exp} e_i : T_i }
```

```
[rUNKNOWN CALL]
(A, fh : S) : (y : pid, \bar{x} : \bar{T}) \vdash S \triangleright T : C < S'
-----------------------------------------------------------
\Delta . \Gamma \vdash^w S > f(w, e_2, ..., e_n) : T < S'
```

![](img/21b2a144330b93d666562c91ebc20aff_11_0.png)

Fig. 8. Term transition semantic rules.

the latter may be denoted as a silent action. The decoration facilitates our technical development. We note that, function calls can only transition subject to a well-formed function information environment (\(\Sigma\)) which contains details about all the functions available in the module. Since \(\Sigma\) remains static during transitions, we leave it implicit in the transitions rules.

The transitions are defined by the term transition rules listed in Fig. 8. Rules [RLET], and [RLET$_s$] deal with the evaluation of a `let` statement, \(x = t_1\); \(t_2\) modelling a call-by-value semantic, where the first term \(t_1\) has to transition fully to a value before being substituted for \(x\) in \(t_2\) denoted as \([t_1/v] \cdot t_2\) or \([t_1^{v_1}/v_1 \cdot t_2]\) for multiple substitutions). The send statement, `send`(\(t\), \(\{t_1, v_1, ..., v_n\}\)), evaluates \(t\) in \(t_2\) denoted as each part of the message to a value from left to right. This is carried out via rule [RCHOICE$_s$] which produces no observable side-effects. When the whole message is reduced to a tuple of values \(\{v_1, v_2, ..., v_n\}\), rule [RCHOICE] performs the actual message sending operation. This transition produces an action \(\uparrow\{t_1, v_1, ..., v_n\}\), where the message \(\{t_1, v_1, ..., v_n\}\) is sent to location \(t_1\) through the channel \(t\). A receive statement, `receive` do \(\{t_1:x_1, ..., t_n:x_n\} \rightarrow t_2\) end, is defined by rule [RBRANCH]. When a message is received (i.e., \(\sigma = \{?1, \vec{v}\}\)), it is matched with a value pattern from the received content using the label ?1. Should one of the labels match (\(\vec{j} \in i\) such that \(i_j = 1\)), the payload of the message (\(\vec{v}\)) is compared to the corresponding patterns in the selected branch (\(\vec{p}_j\)) using `match`(\(\vec{p}_j, \vec{v}\)). If the values match with the pattern, the **match** function (Definition 4.1) produces the substitutions \(\sigma\), mapping the matched variables in the pattern \(\vec{p}_j\) to values from \(\vec{v}\). This substitution is then used to instantiate the free values in continuation branch \(t_j\).

### Definition 4.1 (Pattern Matching).

The **match** function pairs patterns with a corresponding value, resulting in a sequence of substitutions (called \(\sigma\)), e.g., **match**(\(p, v\)) = \([v_1/x_1][v_n/x_n]\). The match function builds a meta-level list of substitutions, which should not be confused with the lists defined by the Elixir syntax in Fig. 3.

```
\(\text{\textbf{match}}(\vec{p}, \vec{v}) \stackrel{\text{def}}{=} \text{\textbf{match}}(p_1, v_1), ..., \text{\textbf{match}}(p_n, v_n) \quad \text{where } \vec{p} = p_1, ..., p_n \text{ and } \vec{v} = v_1, ..., v_n\)

\(\text{\textbf{match}}(p, v) \stackrel{\text{def}}{=} \begin{cases} [] & p = b, v = b \\ [v/x] & p = x \\ \text{\textbf{match}}(w_1, v_1), \text{\textbf{match}}(w_2, v_2) & p = [w_1 | w_2], v = [v_1 | v_2] \\ \text{\textbf{match}}(w_1, v_1), ..., \text{\textbf{match}}(w_n, v_n) & p = \{w_1, ..., w_n\} \text{ and } v = \{v_1, ..., v_n\} \end{cases}\)
```

### Example 4.1.

For the pattern \(p_1 = (x, 2, y)\) and the value tuple \(v_1 = (8, 2, true)\), \(\text{\textbf{match}}(p_1, v_1) = \sigma\) where \(\sigma = [8/x][true/y]\) (written also as \(\sigma = [8^{true}/x, y]\)). However for pattern \(p_2 = (x, 2, false)\), the operation \(\text{\textbf{match}}(p_2, v_1)\) fails, since \(p_2\) expects a \(false\) value as the third element, but finds a \(true\) value instead.

Using rule [RCALL] from Fig. 8, a function call is evaluated by first reducing all of its parameters to a value, using the expression reduction rules in Fig. 9; again this models a call-by-value semantics. Once all arguments have been fully reduced, [RCALLs], the implicit environment S is queried for function f with arity n to fetch the function's parameter names and body. This results in a transition to the function body with its parameters instantiated accordingly, t[f/y1|...vn/xn...αn], decorated by the function name, i.e., α = f/n. Along the same lines a case construct first reduces the expression which is being matched using rule [cRcase]. Then, rule [cRCase] matches the value with the correct branch, using the match function, akin to [rBRANCH]. Whenever a term consists solely of an expression, it silently reduces using [rEXPRESSION] using the expression reduction rules e → e′ of Fig. 9. These are fairly standard.

## 5. Validation of the ElixirST type system

We validate the static properties imposed by the ElixirST type system, overviewed in Section 3, by establishing a relation with a runtime behaviour of a typechecked Elixir program, using the transition semantics defined in Section 4. Broadly, we establish a form of _type preservation_, which states that if a well-typed term transitions, the resulting term then remains well-typed [10]. However, our notion of type preservation, needs to be stronger to also take into account _(i)_ the side-effects produced by the execution; and _(ii)_ the progression of the execution with respect to protocol expressed as a session type. Following the long-standing typing tradition, these type properties, then, two aspects are captured by the refined properties of _session fidelity_ and _session liveness_ [15,16]. This proposition formalises _(i)_ the type preservation property as a result of the execution of the typed process is one of the actions allowed from the current stage of the protocol; and that _(ii)_ the resultant process following the transition is still well-typed w.r.t. the remaining part of the protocol that is still outstanding. We also establish a conditional form of progress, where well-typed processes are either a value, or else they can safely transition to a new term, producing an internal (or external) action.

Before embarking on the proofs for session fidelity and progress, we prove an auxiliary proposition that acts as a sanity check for our operational semantics of Section 4. We note that the operational semantics assume that only _closed_ programs are executed; an open program (i.e., a program containing free variables) is seen as an incomplete program that cannot execute correctly due to missing information. To this end, Proposition 1 ensures that a closed term _remains closed_ even after transitioning.

### Proposition 1 (Closed Term).

_If_ fv(t) = ∅ _and_ t →ᵅ t′_, then_ fv(t′) = ∅_._

**Proof.** By induction on the structure of t. Refer to Appendix B.1 for details. □

The statement of the session fidelity property relies on the definition of a partial function called **after** (Definition 5.1), which takes a session type and an action as arguments and returns another session type as a result. This function serves two purposes: (i) the function after(S, α) is only defined for actions α that are (immediately) permitted by the protocol S, which allows us to verify whether a term transition step violated a protocol or not; and (ii) since S describes the current stage of the protocol to be followed, we need a way to evolve this protocol to the next stage should α be a permitted action, and this is precisely S′, the continuation session type returned where after(S, α) = S′.

### Definition 5.1 (After Function).

The after function is partial function defined for the following cases:

```
after(S, t) def S
after(S, f/n) def S
after(⊕{j₁:⟨T̃i⟩Si}i∈I, ⊕{j:⟨T̃j⟩Sj} def Sj where j ∈ I
after(&{?j₁:⟨T̃i⟩Si}i∈I, &{?j:⟨T̃j⟩Sj} def Sj where j ∈ I
```

![](img/21b2a144330b93d666562c91ebc20aff_13_0.png)

This function is undefined for all other cases. The **after** function is overloaded to range over session typing environments (\(\Delta\)) in order to compute a new session typing environment given some action \(\alpha\) and session type \(S\):

```
after(\(\Delta\), f, hn, S) def= \(\Delta\), f hn : S
```

```
after(\(\Delta\), \(\alpha\), S) def= \(\Delta\) if \(\alpha \neq\) f hn
```

Intuitively, when the action produced by the transition is f hn, the session typing environment is extended by the new mapping f hn : S. For all other actions, the session typing environment remains unchanged. \(\blacksquare\)

Recall module typechecking usage rule \(\vdash\) TModule] entails typechecking the bodies of all the public functions w.r.t. their ascribed session type. \(\Delta \langle y : \text{pid}, \vec{X} : \vec{T} \rangle \vdash S : t : T <: S'\) (where \(S = \text{end}\) for this specific case). At runtime, a spawned client handler process in a session starts running the function body term \(t\) where the parameter variables \(y, \vec{X}\) are instantiated with the pid of the client, say \(t_1\), and the function parameter values, say \(\vec{V}\), respectively, i.e., \(\{t/y\}[\vec{V}/\vec{x}]\), as modelled in rule [KCall$_2$] from Fig. 8. The instantiated function body is thus closed and can be typed w.r.t. an empty variable binding environment. \(f = \epsilon\): Session Fidelity thus states that if a closed term \(t\) is well-typed, i.e.,

```
\(\Delta \vdash \theta \vdash W S : t : T <: S'\) (5)
```

(where \(S\) and \(S'\) are initial and residual session types, respectively, and \(T\) is the basic expression type) and this term \(t\) transitions to a new term \(t'\) with action \(\alpha\), i.e.,

```
\(t \xrightarrow{\alpha} t'\) (6)
```

the new term \(t'\) is expected to remain well-typed, i.e.,

```
\(\Delta' \vdash \theta \vdash W S' \vdash t' : T <: S'\) (7)
```

where the expanded \(A'\) is computed as \(\text{after}(\Delta, \alpha, S) = A'\) and the base type of the term is preserved, as described by the constant type \(T\) in eqs. (5) and (7). To understand how the evolved initial session type (\(S'\)) is computed or assumed (in eq. (7)), we have to consider the context of our analysis. Our type-checker analyses one side of an interaction that does not interleave with other sessions. We also assume that the interacting dual processes are well-behaved and thus follow a compatible protocol (e.g. the dual session type) during execution. Despite these restrictions, we obtain a certain degree of flexibility, where we can statically analyse processes interacting with external processes which we may not have access to their source.

To this end, we make a distinction between the transition actions in Equation (6). If the action \(\alpha\) depends on the context process left implicit (i.e., \(\alpha\) is an incoming message), we only require the guarantee stated in Equation (7) whenever \(\alpha\) is permitted by the protocol \(S\) i.e., \(S' = \text{after}(S, \alpha)\). More specifically, the condition \(S'' = \text{after}(S, \alpha)\) is part of the antecedent of the first clause in Session Fidelity Theorem and captures our conditional guarantees that apply only when the context process is well-behaved. On the other hand, if the action \(\alpha\) depends solely on the process being typechecked (i.e., \(\alpha\) is an outputted message or an internal action), then we *require* that \(\alpha\) is permitted by the protocol \(S\). Concretely, the second clause of Session Fidelity Theorem is stronger than the condition \(\text{after}(S, \alpha)\) forms part of the succedent.

### Theorem 2 (Session Fidelity).

If \(\Delta \vdash \theta \vdash W S \vdash t : T <: S'\) and \(t \xrightarrow{\alpha} t'\)

- for \(\alpha = ?\{i, \vec{v}\}\) and some session type \(S' = \text{after}(S, \alpha)\), then there exists some \(\Delta'\), such that \(\Delta' \vdash \theta \vdash W S' \vdash t' : T <: S'\) and \(\text{after}(\Delta, \alpha, S) = \Delta'\)

- for \(\alpha \in \{f \text{ hn}, t, t\{i, \vec{v}\}\}\), then there exists some \(S''\) and \(\Delta'\), such that \(\Delta' \vdash \theta \vdash W S' \vdash t' : T <: S'\) for \(\text{after}(S, \alpha) = S''\) and \(\text{after}(\Delta, \alpha, S) = \Delta'\)

**Proof.** By induction on the typing derivation \(\Delta \vdash \theta \vdash W S \vdash t : T <: S'\). Refer to Appendix B.2. \(\square\)

As shown in Fig. 10, by repeatedly applying Theorem 2, we can therefore conclude that all the (external) actions generated as a result of a typed computation (i.e., sequence of transition steps) must all be actions that follow the protocol

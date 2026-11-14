![](bbox=[0.15, 0.05, 0.85, 0.26])

reduced, [RCALLs], the implicit environment S is queried for function f with arity n to fetch the function's parameter names and body. This results in a transition to the function body with its parameters instantiated accordingly, t[f/y1|...vn/xn...αn], decorated by the function name, i.e., α = f/n. Along the same lines a case construct first reduces the expression which is being matched using rule [cRcase]. Then, rule [cRCase] matches the value with the correct branch, using the match function, akin to [rBRANCH]. Whenever a term consists solely of an expression, it silently reduces using [rEXPRESSION] using the expression reduction rules e → e′ of Fig. 9. These are fairly standard.

# 5. Validation of the ElixirST type system

We validate the static properties imposed by the ElixirST type system, overviewed in Section 3, by establishing a relation with a runtime behaviour of a typechecked Elixir program, using the transition semantics defined in Section 4. Broadly, we establish a form of _type preservation_, which states that if a well-typed term transitions, the resulting term then remains well-typed [10]. However, our notion of type preservation, needs to be stronger to also take into account _(i)_ the side- effects produced by the execution; and _(ii)_ the progression of the execution with respect to protocol expressed as a session type. Following the long-standing typing tradition, these type properties, then, two aspects are captured by the refined properties of _session fidelity_ and _session liveness_ [15,16]. This proposition formalises _(i)_ the type preservation property as a result of the execution of the typed process is one of the actions allowed from the current stage of the protocol; and that _(ii)_ the resultant process following the transition is still well-typed w.r.t. the remaining part of the protocol that is still outstanding. We also establish a conditional form of progress, where well-typed processes are either a value, or else they can safely transition to a new term, producing an internal (or external) action.

Before embarking on the proofs for session fidelity and progress, we prove an auxiliary proposition that acts as a sanity check for our operational semantics of Section 4. We note that the operational semantics assume that only _closed_ programs are executed; an open program (i.e., a program containing free variables) is seen as an incomplete program that cannot execute correctly due to missing information. To this end, Proposition 1 ensures that a closed term _remains closed_ even after transitioning.

> **Proposition 1** (_Closed Term_)**.** _If_ fv(t) = ∅ _and_ t →ᵅ t′_, then_ fv(t′) = ∅_._

**Proof.** By induction on the structure of t. Refer to Appendix B.1 for details. □

The statement of the session fidelity property relies on the definition of a partial function called **after** (Definition 5.1), which takes a session type and an action as arguments and returns another session type as a result. This function serves two purposes: (i) the function after(S, α) is only defined for actions α that are (immediately) permitted by the protocol S, which allows us to verify whether a term transition step violated a protocol or not; and (ii) since S describes the current stage of the protocol to be followed, we need a way to evolve this protocol to the next stage should α be a permitted action, and this is precisely S′, the continuation session type returned where after(S, α) = S′.

# **Definition 5.1** (_After Function_)**.** The after function is partial function defined for the following cases:

```
after(S, t) def S
after(S, f/n) def S
after(⊕{j₁:⟨T̃i⟩Si}i∈I, ⊕{j:⟨T̃j⟩Sj} def Sj where j ∈ I
after(&{?j₁:⟨T̃i⟩Si}i∈I, &{?j:⟨T̃j⟩Sj} def Sj where j ∈ I
```
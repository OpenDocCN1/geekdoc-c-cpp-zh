(continued)

```
S : Statement → Environment → Environment

S[[ I ':=' E ]](Env) = Env & { I = E[[E]](Env) }

E : Expression → Environment → Integer⊥

E[[E₁ '+' E₂]](Env) = E[[E₁]](Env) + E[[E₂]](Env)
E[[E₁ '−' E₂]](Env) = E[[E₁]](Env) − E[[E₂]](Env)
E[[E₁ '*' E₂]](Env) = E[[E₁]](Env) * E[[E₂]](Env)
E[[ '(' E ')' ]](Env) = E[[E]](Env)
E[[I]](Env) = Env(I)
E[[N]](Env) = N[[N]]

N: Number → Integer

N[[ND]] = 10*N[[N]] + N[[D]]
N[[D]] = D[[D]]

D : Digit → Integer

D[['0']] = 0, D[['1']] = 1, ..., D[['9']] = 9
```

Figure 12.5 A denotational definition for the sample language extended with assignment statements and environments

# 12.3.6 Denotational Semantics of Control Statements

To complete our discussion of denotational semantics, we need to extend the denotational definition of Figure 12.5 to if- and while statements, with the following abstract syntax:

```
S: Statement
S → I ':=' E
  | 'if' E 'then' L₁ 'else' L₂ 'fi'
  | 'while' E 'do' L 'od'
```

As before, the denotational semantics of these statements must be given by a function from environments to environments:

```
S : Statement → Environment → Environment
```

We define the semantic function of the if statement as follows:

```
S[['if' E 'then' L₁ 'else' L₂ 'fi']](Env) =
    if E[[E]](Env) > 0 then L[[L₁]](Env) else L[[L₂]](Env)
```
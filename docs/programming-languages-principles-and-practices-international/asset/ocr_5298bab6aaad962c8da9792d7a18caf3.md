# Syntactic Domains

```
P: Program
L: Statement-list
S: Statement
E: Expression
N: Number
D: Digit
I: Identifier
A: Letter
P → L
L → L₁ ';' L₂ | S
S → I ':=' E
E → E₁ '+' E₂ | E₁ '−' E₂ | E₁ '*' E₂ | '(' E ')' | I | N
N → ND | D
D → '0' | '1' | … | '9'
I → IA | A
A → 'a' | 'b' | … | 'z'
```

# Semantic Domains

Domain v: Integer = { …, −2, −1, 0, 1, 2, … }

Operations

```
+ : Integer × Integer → Integer
− : Integer × Integer → Integer
* : Integer × Integer → Integer
```

Domain Env: Environment = Identifier → Integer⊥

# Semantic Functions

```
P : Program → Environment

P[[L]] = L[[L]](Env₀)

L : Statement-list → Environment → Environment

L[[L₁ ';' L₂]] = L[[L₂]] ○ L[[L₁]]
L[[S]] = S[[S]]
```

**Figure 12.5** A denotational definition for the sample language extended with assignment statements and environments *(continues)*
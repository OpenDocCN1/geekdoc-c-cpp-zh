
# Church encoding

In mathematics the **Church numerals** are a representation of the natural numbers using lambda notation. The method is named for Alonzo Church, who first encoded data in the lambda calculus this way.

0 ≡ λf. λx. x
1 ≡ λf. λx. f(x)
2 ≡ λf. λx. f(f(x))

The type of those numerals is (_→_)→(_→_), which we can define as delegate for simplicity:

```
delegate Func<_, _> N (Func<_, _> f);
```

Then you can define things like the Successor function, addition etc.

```
Func<N, N> Succ = (N n) => (f) => x => f(n(f)(x)); // add an additional f in front
```

This is just a Hacky way to do arithmetic, imagined by the genius of Alonzo Church during the 30’s, which constitute the ancient history of computer science.

Now, in the untyped lambda calculus we could have a lambda application (M N) of any two Terms. This led to problems early on because it allowed Russel type paradoxes [Curry's paradox]. That is why **Types** were introduced to restrict the operations of Terms based on their type.

This idea of types is considered today common knowledge, in all strongly typed, languages like C#.

## Types

The only types in λ→ is the Set of some base types **B**, and anything whatever is produced by this simple grammar in BNF form:

τ ::= τ→ τ | T where T ∈ B

this means the only types that occur in λ→ are inductively defined and are either of the form τ→ τ where τ is some already created type, or some type belonging to the base types. If for example B = {σ, ρ} then the types generated look like this :

σ, ρ, σ→ σ, ρ→ ρ, ρ→ σ, (ρ→ σ) → ρ, ..., (ρ→ σ) →(ρ→ σ) ...

If we take the C# type system with the usual primitive build-in types then a simple λ→ restricted version of C# would have as base types B= {int, char, bool, ...} and everything that would be generated using the τ ::= τ→ τ | T grammar. This would result in syntax trees like the following:

(int→ int) → int

![](img/d73681d801b4b826e0b2a293897bbba4_19_0.png)

(int→ bool) → (int → char)

![](img/d73681d801b4b826e0b2a293897bbba4_19_1.png)

The (int→ int) → int in C# is the delegate Func<Func<int,int>, int> while the second one (int→ bool) → (int → char) would be Func<Func<int,bool>, Func<int,char>>

As one can see an embedded λ→ version within C# would only allow for things that look like this Func<Func<..., ...>, Func<..., ...>> with nested Func delegates.

## Introduction and Elimination Rules

### Introduction Rule

Now we have used an inductive definition to create a Set of Types and used an inductive definition to define a Set of Terms, the next step is to link them. We have to give an Inductive definition of how specific Terms belong to specific Types.

First there is the introduction rule which signifies the way we construct a lambda abstraction.

![](img/d73681d801b4b826e0b2a293897bbba4_19_2.png)

Here you see the mechanism to create a λx:A.M Term and why this Term is of type A → B and that is the only way to create τ→ τ types. The [x: A]¹ means that at some point we make an assumption of having a variable x of type A, or in another phrasing we have a context where we have a variable x of type A. In C# this is expressed by the declaration:

```
(A x) => ...
```

By starting a lambda, you might assume that you introduce a x:A out of thin air. Then in this setting we finally construct a term M:B we can discharge the assumption and introduce this implication sign ⇒ (equivalently the => in C#) and this gives us the

```
Func<A, B> Id = (A x) => ... ;
```

We note the introduction with an arrow ⇒ I₁

[Another notation for the Introduction using the entailment sign ⊢ is

Γ, x : A ⊢ M : B
------------------- ⇒ E
Γ ⊢ λx.M : A → B

This meant to express the same thing as the previous notation. That in a Typing context

Γ, x:A ⊢ .... (the context is comprised by the assumptions that are placed left of the ⊢ ) we produce a term M:B and thus we infer that in the Typing context without the x:A, we can infer a lambda Term λx:A.M : A →B]

### Elimination Rule

The elimination rule for the lambda is equivalent to the very famous modus ponens in logic

M : A → B   N : A
------------------- ⇒ E
(MN) : B

This says you can use the application (M N) only with two terms that have this specific kind of types A →B and A and this will yield a new term (M N) of type B .

Of course, this does not explain how exactly that would happen, and for this reason we need the last type of set of rules the Computation rules.

## Computation Rules

The computation rule for the Application is just what is called β-reduction

(λx:A. M)(a ) → M[a/x]

The M[a/x] is the representation of substitution in type theory and it means wherever we find the variable x inside M we should replace it with a.

This is the standard notion of executing a function if we have the following f

```
Func<int, int> f = (int x) => x + 2;
```

And we want to compute the f(2) we replace x with 2 inside f.

That was a presentation of the Simply typed lambda calculus system.

Now in order to use the integer types, formally one should declare how they behave by declaring the formation, introduction, elimination, and computation rules [we would have to introduce Gödel’s System T (which we briefly see in the Recursion section)]. But here we will just provide a mix of typing rules and operational semantics in order to make it work with the λ→

Assuming only addition for example we could have a rule that says we only can add integers

a: int   b: int
-------------------
(a + b): int

And another computation rule that will say that if you have an addition (a+b): int you can infer the addition result which is an int

(a + b): int
---------------
n: int      where n = a + b

Now we can do simple derivations like the following:

[x: int]¹   2: int
-------------------
x + 2: int
---------------------------- ⇒ I₁
λx: int. (x + 2): int → int
---------------------------- ⇒ E
(λx: int. (x + 2))(2): int

## optional

## Curry-Howard correspondence

In programming language theory and proof theory, the Curry-Howard correspondence is the direct relationship between computer programs and mathematical proofs. We are going to explore some of those connections as we go along. We are going to only scratch the surface of the Curry-Howard correspondence, in a simplistic presentation within the scope of this book.

The First clear connection is between the lambda abstraction ( ⇒ ) and logical implication ( → ):

Types | Logic
Introduction | [x:A]¹ ... M:B / λx.M: A → B ⇒ I₁ | [A]ˣ ... B / A → B ⇒ I₁
Elimination | λx.M: A → B   t:A / M(t): B ⇒ E | A → B   A / B → E

+   1. an introduction rule describing how elements of the type can be created, and
+   2. an elimination rule describing how elements of the type can be used.

The Correspondence is the following:

+   1. An implication **introduction** in Logic is like a Lambda **abstraction** in Lambda calculus.
+   2. An Implication **elimination** in Logic is like a Lambda **application** in Lambda calculus.

The easiest thing that we can prove is the identity, Func<A, A> Id = (A x) => x;

Logic

[A]^x
---
A → A  → I_x

Types

[x: A]
---
λx. x: A → A  ⇒ I_x

The natural deduction derivation is straightforward:

+   1. **[A]^x**: We make an **assumption [A]^x** that we have an **A**. In the code this means that we start the lambda (A x)=> in this way we are charged with an **A**, that we can use in our function implementation. The problem is that when we will need to use the **Id** we should have an **A** available. The notation of [...]^x is used within the context of deduction as a book-keeping mechanism to keep track of the assumptions.
+   2. And then immediately conclude **A** (A x) => x and **eliminate the assumption** (discharge the assumption) **[A]^x** by invoking the implication → introduction rule.

Another easy tautology is the proposition **A → (B → A)** [this is called **K combinator**] with the following straight forward implementation in C# using only lambdas:

```
Func<A, Func<B, A>> K = (A x) => ((B y) => x);
```

This corresponds to the lambda term:

**λx:A. λy:B. x: (A → (B → A))**

**K** just takes a variable **x:A** this returns a function which takes a **y:B** completely ignores it and returns the initial variable. Yes, as you might expect it is completely useless in real situations.

For a complete presentation of the combinators we are also going to briefly discuss the **S combinator**.

```
Func<Func<A, B>, Func<A, C>> S<A, B, C>(Func<A, Func<B, C>> f) =>
    (Func<A, B> g) => ((A a) => f(a)(g(a)));
```

The type of this function is :

**S: (A → (B → C)) → ((A → B) → (A → C))**

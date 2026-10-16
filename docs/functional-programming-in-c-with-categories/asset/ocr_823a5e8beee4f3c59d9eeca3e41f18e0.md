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
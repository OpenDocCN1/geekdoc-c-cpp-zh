# 3.2.1 Lambda Calculus with Product Types optional

The next useful extension of the simply typed lambda calculus λ→ is to add products _×_ λ→,×

# Types

The only types in λ→ is just a set of base types B and anything else that is produced by this simple grammar in BNF form:

τ ::= τ→τ | τ×τ | T where T ∈ B

(int × int) → int

![](bbox=[0.46, 0.3, 0.78, 0.4])

(int→ bool) → (int × char)

![](bbox=[0.43, 0.43, 0.78, 0.53])

The (int × int) → int in C# is the delegate:

```
Func<(int, int), int> f = ((int, int) a) => default(int);
```

Or in lambda notation now we can have lambdas where the variables are of product type

λx:(int× int).B: (int× int)→int

while the second one (int→ bool) → (int × char) would be:

```
Func<Func<int, bool>, (int a, char b)> g = (Func<int, bool> a) =>
    (a: default(int), b: default(char);
```

Also, we must treat Func<(int,int), int> and Func<int, int, int> as equivalent, because we can find two paths converting one to the other:

```
Func<A, B, C> Path1(Func<(A, B), C> f) => (A x, B y) => f((x, y));
```
# 3.5.1 Lambda Calculus Again- Gödel’s System T optional

Gödel’s System T is the simply typed λ-calculus with products λ→, ×, where a basic type ℕ for numbers and a Recursor for the Naturals have been added.

For the Naturals numbers the typing rules of introduction are simple we have a zero 0 which is in Naturals ℕ or if we have a term that is in naturals then its successor also is a Natural.

0 : ℕ
Zero — ℕ

n : ℕ
S(n) : ℕ
Succ — ℕ

While it has a single elimination rule, called Recursor Rec

n : ℕ   a : A   c : A → ℕ → A
Rec(n, a, c) : A
Rec — ℕ

The Recursor again here is the classic aggregate fold the a:A is the “seed” element (or the accumulator) and the c: A → ℕ → A is the aggregation function that takes the previous accumulation the current state of the counter n:ℕ and returns a new accumulation.

The Evaluation/β-reductions/computation rule for the Recursor is a case analysis on the current counter:

Rec(0, a, c):A →β a:A   β-ℕ

Rec(n, a, c):A →β c(Rec(n-1), n):A

And that is precisely the C# Recursive function:

```
public static A Rec<A>(int @num, A a, Func<A, int, A> c) =>
    num == 0 ?
        a :
        f(Rec(num - 1, acc, c), num - 1);
```

Let’s refactor this in order to take a familiar form. First we will add our Custom pattern matching (case analysis) on the definition of the Naturals:

```
public static T1 MatchWith<T1>(this int @this,
    (Func<T1> Zero, Func<int, T1> Succ) pattern) =>
        (@this == 0) ?
        pattern.Zero() :
        pattern.Succ(@this - 1);
```

this just hides the _?_:_ operation. Now we can rewrite the Recursion above using the custom pattern matching MatchWith function:

```
public static A Rec<A>(int @num, A a, Func<A, int, A> c) =>
    @num.MatchWith(pattern: (
        Zero: () => a,
```
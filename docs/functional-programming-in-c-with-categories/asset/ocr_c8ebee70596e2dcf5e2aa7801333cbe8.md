[SideNote: We have seen Recursive definitions before using MatchWith. For the first time we are creating a method that takes as an argument (Func<T1> Zero, Func<T1, T1> Succ) algebra which is of the same type as the the MatchWith argument. Inception. The Cata is a generalised MatchWith for composite Algebraic types. Or MatchWith is just the Cata for elementary Types]

This definition follows the structural induction and should be easy to follow by now. Now we can evaluate a numeral using our algebras above.

```
(Func<int> Zero, Func<int, int> Succ) algebraInt = (
    Zero: () => 0,
    Succ: (n) => n + 1
);

var four = fourNumeral.Cata<int>(algebraInt); //"4"
```

The Numeral functor has two parts the type of Zero is () → 1 this means that we can get an initial object ("",[],0 etc) depending on A, and the type of Succ is A → A since the Numeral is a union we should add them Numeral: A → 1+ A

You might already have seen the ToString() implementation for Numeral

```
public static string ToString(this Numeral @this) =>
    @this.MatchWith(pattern: (
        Zero: () => $"Zero( )",
        Succ: (Rest) => $"Succ({Rest.Show()})"
    ));
```

The Cata just generalize this by extracting the Recursion mechanics and allow Cata to be used with different algebras without defining any additional extension methods.

For example, We could provide a different ToString by providing custom patten matching algebras. For example, this is a different mapping from Numeral → string

```
(Func<string> Zero, Func<string, string> Succ) justExclamationmarks = (
    Zero: () => $"",
    Succ: (Rest) => $"!{Rest }"
);
```

# C# 8.0 pattern matching

We can instead use C#8.0 pattern matching instead we can unobtrusively attach Cata<T1> on the Numeral Type
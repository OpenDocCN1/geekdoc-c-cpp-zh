```
M = { "", "a", "b", ..., "z", "aa", "ab", ... } and • = <> ① ② ③
```

① e is "" the Empty String, which is the first element of Set M.

② M is the Set of Strings.

③ <> is the Concatenation (or Append) operator.

If we append the Empty String to any String, we get that same String back. Conversely, if we append any String to the Empty String, we still get that same String back.

This is why e is called the Identity since it simply returns back the exact same thing you started with. There is a function in Prelude called identity that has a similar effect:

```
identity :: ∀ a. a -> a
identity x = x
```

Here’s another example of a Monoid:

```
M = { 0, 1, 2, 3, ... } and • = +, e = 0
```

Remember that M is first a Magma:

```
1 + 3 = 4      (Closed)
```

and then a Semigroup:

```
1 + (2 + 3) = (1 + 2) + 3      (Associative)
```

and finally a Monoid:

```
0 + 1 = 1 + 0 = 1      (Identity)
```

Another example:

```
M = { true, false } and • = ||, e = false
```

M is first a Magma, then a Semigroup and finally a Monoid:
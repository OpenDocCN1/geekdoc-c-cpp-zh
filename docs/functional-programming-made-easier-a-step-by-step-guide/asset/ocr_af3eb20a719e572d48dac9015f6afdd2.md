```
Cons 1 (Cons 2 (Cons 3 Nil))
```

You can also use the Cons Binary Operator:

```
1 : 2 : 3 : Nil
```

Now add the following line to test:

```
log $ show $ singleton "xyz" ①
```

① Should print out ("xyz" : Nil).

Now, write the singleton Function without reading ahead.

# 5.11.1. Code for singleton

This Function is quite simple:

```
singleton :: ∀ a. a -> List a
singleton x = x : Nil ①
```

① Uses the Cons Operator.

It could also be written using Cons:

```
singleton :: ∀ a. a -> List a
singleton x = Cons x Nil ①
```

① This is merely the prefixed version, whereas the Operator version is the infixed version.

I prefer the Operator version due to its terseness.

# 5.12. Writing null

If you come from a language that has NULLs, I want you to realized that this is not the same thing. This Function checks to see if a List is empty.

Although, you can write this Function with an if or a case, it’s idiomatic to use Pattern Matching instead. So try to take that approach.

Also, test your code with the following lines added to test:
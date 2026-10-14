# 14.8. Invariant Functor

Polarity is a useful model for helping us determine if our a is in Positive or Negative Position. But what if a is in both?

```
newtype Both a = Both (a -> a)
```

We cannot write a Functor Instance because a is in Negative Position and we cannot write a Contravariant Instance since a is also in Positive Position. What we need is something that can handle both.

And that something is called an *Invariant Functor*. In PureScript, the Typeclass definition is as follows:

```
class Invariant f where
  imap :: ∀ a b. (a -> b) -> (b -> a) -> f a -> f b
```

The first mapping function, a -> b is the same as the one in Functor, which maps the OUTPUT value. The second mapping function b -> a is the same as Contravariant, which maps the INPUT.

We need both functions to map a -> a to b -> b:

![](bbox=[0.168, 0.504, 0.831, 0.663])

Notice how the 2 functions CAN form an Isomorphism (there's no requirement that the MUST):
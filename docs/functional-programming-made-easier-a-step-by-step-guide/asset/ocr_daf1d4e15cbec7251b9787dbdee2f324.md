requirements of a Monoid:

```
mempty <> mempty = mempty                 (Closed)      [Magma]
(mempty <> mempty) <> mempty = 
    mempty <> (mempty <> mempty)   (Associative) [Semigroup]
mempty <> mempty = mempty                (Idenity)     [Monoid]
```

We can also write a function that destroys that structure:

```
always123 :: String -> String
always123 _ = "123"
```

This function maps every String in our String Monoid to "123". The resulting Set, the Codomain, is NOT a Monoid. In fact, it’s not even a Magma:

```
"123" <> "123" = "123123"          (NOT CLOSED)
```

But so far, we’ve only seen contrived, simple examples. There is, however, a common function that we’ve all used many times that is a Monoid Homomorphism, length, the String length function. It maps Strings to Ints.

But before we verify that length is a Monoid Homomorphism, it might be good to give the formal definition for Monoid Homomorphism:

A function, h : M -> N, which maps elements from Monoid M to Monoid N, is a Homomorphism if:

```
h (m1 • m2) = h(m1) * h(m2)
```

In other words, first combining m1 and m2 in M and then mapping to N is equal to first mapping m1 and m2 to N and then combining in N.

Notice that combining in M uses M’s Binary Operator •, while combining in N uses N’s, *. These Binary Operators are different in the case of the length Homomorphism, but are the same when using idHom or constHom.

Here we can see that in action:
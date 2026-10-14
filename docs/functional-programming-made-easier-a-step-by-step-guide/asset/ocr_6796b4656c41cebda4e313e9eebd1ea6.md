```
ask :: ∀ r. Reader r r
asks :: ∀ a r. (r -> a) -> Reader r a
```

ask, which we saw in the example for how to use Readers, returns the full read-only Value.

In contrast, asks, takes a Function that will accept the full read-only Value and return at least some portion of it. Technically speaking, this Function could take any or all of the read-only Value and return some computation on it, but typically, it only returns a field from a Record.

Let’s start by examining the Type Signature for ask:

```
ask :: ∀ r. Reader r r
```

Notice that the second Type Parameter of Reader r r is an r, i.e. the Type of our read-only Value. The second Type Parameter is normally reserved for the computation Type. But for ask, the computation is the read-only Value. This is the only way we can get our hands on it.

Let me reiterate that because it’s important. Returning the read-only Value as the Pure Computation is how ask bridges the gap between the Parallel Computations in the Reader Monad.

And now, we’ll write the implementation starting with our familiar pattern:

```
ask :: ∀ r. Reader r r
ask = Reader \r -> ???
```

We know enough to write up to this point having seen this pattern over and over again, but now, we have to return something of Type r. The only thing we have that’s Type r is the Value r and so we’ll return that:

```
ask :: ∀ r. Reader r r
ask = Reader \r -> r
```

I hope you’re dying to change \r -> r to identity like I am:

```
ask :: ∀ r. Reader r r
ask = Reader identity
```

That’s all there is to ask. When the Reader returned by ask is run, it’ll return the read-only Value.

And now we’ll start with the Type Signature for asks:
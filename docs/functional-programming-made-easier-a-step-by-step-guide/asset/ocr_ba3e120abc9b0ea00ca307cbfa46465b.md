```
infiniteLoop :: AnyValidType -> AnyValidType
infiniteLoop x = infiniteLoop x ①
```

① By the way, if you Eta-reduce this the compiler will catch this infinitely recursion definition.

infiniteLoop’s return Type is met by calling itself. The compiler is happy with this because the Types match. But when we call this Function, we won’t be happy one bit. Not unless we want our program to sit and spin.

And the same is true about our use of join. To see why, let’s look at join and bind together:

```
join :: ∀ a m. Bind m => m (m a) -> m a
join x = x >>= identity

instance bindReader :: Bind (Reader r) where
  bind (Reader fx) f = join $ Reader \r -> f $ fx r
```

Can you see how this is like our infiniteLoop example?

Hopefully, you noticed how join is written in terms of bind, via >>=, and bind is written in terms of join.

This will cause an infinite loop when we run our program. bind will call join and join will call bind. They form an infinite recursion.

That means that we can’t use join as our solution to our Type problem. We’ll have to go back to where we started and try something else.

Here’s where we left off, i.e. before adding join:

```
instance bindReader :: Bind (Reader r) where
  bind (Reader fx) f = Reader \r -> f $ fx r -- COMPILER ERROR!!
```

And here’s the Types we came up with:

```
f :: a -> Reader r b
fx :: r -> a
fx r :: a
f $ fx r :: Reader r b
Reader \r -> f $ fx r :: Reader r (Reader r b)
whatWeWant :: Reader r b
```

The problem with what we wrote is that we have 2 Readers. The outer Reader, Reader \r -> f $ fx r,